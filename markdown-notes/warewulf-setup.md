# Warewulf Cluster Setup Guide - Rocky Linux 9

## System Configuration

### Hardware Setup

- **Master Node**: Rocky Linux 9
  - Built-in Ethernet: External/Internet connectivity
  - USB-C to Ethernet adapter (enp0s20f0u2): Cluster network
- **Worker Nodes**: PXE boot enabled

### Network Configuration

- **Cluster Network**: 10.0.0.0/22
- **Master Node IP**: 10.0.0.1
- **Cluster Interface**: enp0s20f0u2
- **DHCP Range**: 10.0.1.1 - 10.0.1.255
- **Worker IP Range**: 10.0.1.x
  
  ---

## Installation Steps

### 1. Install EPEL and Update System
  
  ```
  sudo dnf install -y epel-release
  sudo dnf update -y
  ```

### 2. Install OpenHPC Repository

```bash
sudo dnf install -y http://repos.openhpc.community/OpenHPC/3/EL_9/x86_64/ohpc-release-3-1.el9.x86_64.rpm

# Verify repository
dnf repolist | grep -i openhpc
```

### 3. Install Warewulf

```bash
sudo dnf install -y warewulf-ohpc
```

### 4. Configure Warewulf

Edit `/etc/warewulf/warewulf.conf`:

```bash
ipaddr: 10.0.0.1
netmask: 255.255.252.0
network: 10.0.0.0
device: enp0s20f0u2
warewulf:
port: 9873
secure: false
update interval: 60
autobuild overlays: true
host overlay: true
grubboot: false
systemd name: warewulfd
dhcp:
enabled: true
template: default
range start: 10.0.1.1
range end: 10.0.1.255
systemd name: dhcpd
tftp:
enabled: true
tftproot: /var/lib/tftpboot
systemd name: tftp
nfs:
enabled: true
export paths:
- path: /home
export options: rw,sync
- path: /opt
export options: ro,sync,no_root_squash
systemd name: nfs-server
```

### 5. Configure Firewall

```bash
sudo firewall-cmd --permanent --add-service=dhcp
sudo firewall-cmd --permanent --add-service=tftp
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=nfs
sudo firewall-cmd --permanent --add-port=9873/tcp
sudo firewall-cmd --reload

# Verify
sudo firewall-cmd --list-all
```

### 6. Initialize Warewulf
  
```bash
sudo wwctl configure --all
```

### 7. Start and Enable Services
  
```bash
sudo systemctl enable --now warewulfd
sudo systemctl enable --now tftp.socket

# Verify all services
sudo systemctl status warewulfd dhcpd tftp.socket nfs-server
```

### 8. Verify Installation
  
```bash
wwctl --version
wwctl server status
sudo wwctl container list
sudo wwctl vnfs list
```

## SSH Key Setup

### Generate SSH Keys (if not exists)

```bash
ssh-keygen -t ed25519
```

```bash
cat ~/.ssh/id_ed25519.pub | sudo tee -a /root/.ssh/authorized_keys
```

- ### Rebuild Overlays

```bash
sudo wwctl overlay build
```

## Node Management

### Managing Nodes via Config File

Edit `/etc/warewulf/nodes.conf`:

```bash
nodeprofiles:
default:
comment: This profile is automatically included for each node
image name: rockylinux-9
ipxe template: default
runtime overlay:
- hosts
- ssh.authorized_keys
system overlay:
- wwinit
- wwclient
- fstab
- hostname
- ssh.host_keys
- issue
- resolv
- udev.netname
- systemd.netname
- ifcfg
- NetworkManager
kernel:
args:
- quiet
- crashkernel=no
- net.ifnames=1
init: /sbin/init
root: initramfs
network devices:
default:
netmask: 255.255.252.0
gateway: 10.0.0.1
resources:
fstab:
- file: /home
mntops: defaults,nofail
spec: warewulf:/home
vfstype: nfs
- file: /opt
mntops: defaults,noauto,nofail,ro
spec: warewulf:/opt
vfstype: nfs

nodes:
easifem.worker01:
profiles:
- default
network devices:
default:
hwaddr: 38:F7:CD:D3:D1:26
ipaddr: 10.0.1.1

easifem.worker02:
profiles:
- default
network devices:
default:
ipaddr: 10.0.1.2
```

### Reload Node Configuration

After editing `nodes.conf`:

```bash
sudo wwctl configure nodes
```

### Auto-Discovery Setup

Create a discoverable node template (allows unknown nodes to auto-provision):

```bash
sudo wwctl node add worker-discover --discoverable --netname=default --ipaddr=10.0.1.0/22
```

## Common Commands

### Node Management

```bash
# List all nodes
sudo wwctl node list

# Show detailed node info
sudo wwctl node list -a <nodename>

# Check node status
sudo wwctl node status

# Add a node via command line
sudo wwctl node add <nodename> --ipaddr=10.0.1.X --netname=default

# Set node properties
sudo wwctl node set <nodename> --ipaddr=10.0.1.X

# Delete a node
sudo wwctl node delete <nodename>
```

### Container/Image Management

```bash
# List containers
sudo wwctl container list

# Build container image
sudo wwctl container build <container-name>

# List VNFS images
sudo wwctl vnfs list
```

### Overlay Management

```bash
# List overlays
sudo wwctl overlay list

# Build all overlays
sudo wwctl overlay build

# Show overlay for specific node
sudo wwctl overlay show <nodename>
```

### Profile Management

```bash
# List profiles
sudo wwctl profile list

# Show profile details
sudo wwctl profile list -a <profile-name>
```

### Service Management

```bash
# Restart Warewulf daemon
sudo systemctl restart warewulfd

# Check service status
sudo systemctl status warewulfd dhcpd tftp.socket nfs-server

# View logs
sudo journalctl -u warewulfd -f
sudo tail -f /var/log/messages
```

## Worker Node Operations

### SSH into Worker Nodes

```bash
# Using IP address
ssh root@10.0.1.1

# Using hostname (if DNS/hosts configured)
ssh root@easifem.worker01
```

### Power Off Worker Node

```bash
# From master node
ssh root@10.0.1.1 'shutdown -h now'

# Or login first, then shutdown
ssh root@10.0.1.1
shutdown -h now
```

### Reboot Worker Node

```bash
ssh root@10.0.1.1 'reboot'
```

## Troubleshooting

### SSH Issues

  If SSH fails with "Host key verification failed":

```bash
# Remove old host key
ssh-keygen -R 10.0.1.1
ssh-keygen -R easifem.worker01

# Connect again (will ask to accept new key)
ssh root@10.0.1.1
```

### Network Connectivity Issues

```bash
# Check if worker is reachable
ping 10.0.1.1

# Check ARP table
arp -a | grep 10.0.1

# Check cluster interface
ip addr show enp0s20f0u2

# Check node status
sudo wwctl node status
```

### DHCP Lease Check

```bash
# View DHCP leases
sudo cat /var/lib/dhcpd/dhcpd.leases

# Monitor DHCP requests
sudo tail -f /var/log/messages | grep -i dhcp
```

### TFTP Issues

```bash
# Check TFTP socket
sudo systemctl status tftp.socket

# Verify boot files
ls -la /var/lib/tftpboot/warewulf/
```

### Service Not Starting

```bash
# Check service status
sudo systemctl status <service-name>

# View detailed logs
sudo journalctl -u <service-name> -xe

# Restart services
sudo systemctl restart warewulfd dhcpd tftp.socket nfs-server
```

### Worker Not Booting

- Check physical connection to cluster network
- Verify PXE boot is enabled in BIOS/UEFI
- Check master node services are running
- Monitor logs: `sudo tail -f /var/log/messages`
- Check node status: `sudo wwctl node status`

## Important File Locations

```bash
/etc/warewulf/warewulf.conf  # Main Warewulf configuration
/etc/warewulf/nodes.conf     # Node definitions
/var/lib/warewulf/           # Warewulf data directory
/var/lib/warewulf/chroots/   # Container root filesystems
/var/lib/warewulf/overlays/  # System and runtime overlays
/var/lib/warewulf/provision/ # Provisioning data
/var/lib/tftpboot/warewulf/  # TFTP boot files
/var/lib/dhcpd/dhcpd.leases  # DHCP lease information
/root/.ssh/authorized_keys   # SSH keys for root access
```

## Best Practices

- **Always backup configuration files** before making changes:

```bash
sudo cp /etc/warewulf/warewulf.conf /etc/warewulf/warewulf.conf.backup
sudo cp /etc/warewulf/nodes.conf /etc/warewulf/nodes.conf.backup
```

- **Choose one method for node management**:
  - Either edit `nodes.conf` manually + `wwctl configure nodes`
  - Or use `wwctl node` commands exclusively
  - Don't mix both approaches to avoid losing changes
- **After editing nodes.conf manually**:

```bash
sudo wwctl configure nodes
```

- **Rebuild overlays after SSH key changes**:

```bash
sudo wwctl overlay build
```

- **Monitor node status regularly**:

```bash
sudo wwctl node status
```

- **Keep USB-C Ethernet adapter permanently connected** (cluster depends on it)

- **Worker nodes are diskless**: All data is lost on power-off. Use NFS mounts for persistent data

## Quick Reference Commands

```bash
# Check cluster status
sudo wwctl node status

# SSH to worker
ssh root@10.0.1.X

# Add node manually
sudo wwctl node add worker02 --ipaddr=10.0.1.2

# Reload node config after editing nodes.conf
sudo wwctl configure nodes

# Rebuild overlays
sudo wwctl overlay build

# Restart Warewulf
sudo systemctl restart warewulfd

# Monitor logs
sudo tail -f /var/log/messages

# Check all services
sudo systemctl status warewulfd dhcpd tftp.socket nfs-server
```

## Your Cluster Configuration Summary

- **Master Node**: easifem (10.0.0.1)
- **Cluster Network**: 10.0.0.0/22 via enp0s20f0u2
- **Worker Nodes**:
  - easifem.worker01: 10.0.1.1 (MAC: 38:F7:CD:D3:D1:26)
  - easifem.worker02: 10.0.1.2
  - easifem.worker03: 10.0.1.3
  - easifem.worker04: 10.0.1.4
- **Container Image**: rockylinux-9
- **NFS Exports**: /home (RW), /opt (RO)
- **Auto-discovery**: Enabled via worker-discover template

## Additional Resources

- Warewulf Documentation: <https://warewulf.lbl.gov/>
- OpenHPC Documentation: <https://openhpc.community/>
- Rocky Linux Documentation: <https://docs.rockylinux.org/>

