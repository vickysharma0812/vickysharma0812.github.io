# Configuring the Network

To change the settings to use static IP address on a Linux system, you typically need to modify the network configuration files. The exact steps may vary depending on the Linux distribution you are using. Below are general instructions for some common distributions.

::: {.callout-note appearance="simple" }
Always prefer using the CLI tools instead of directly editing configuration files when possible.
:::

## For Debian/Ubuntu

1. Open the terminal.
2. Edit the network interfaces file using a text editor (e.g., `nano`):

```bash
sudo nano /etc/network/interfaces
```

1. Add or modify the configuration for your network interface (e.g., `eth0`) to use a static IP address. For example:

```
auto eth0
iface eth0 inet static
  address
  netmask
  gateway
  dns-nameservers
```

Replace , , , and  with your desired static IP address, subnet mask, gateway, and DNS servers respectively.

4. Save the file and exit the text editor.
5. Restart the networking service to apply the changes:

```bash
sudo systemctl restart networking
```

## For CentOS/RHEL

1. Open the terminal.
2. Edit the network configuration file for your interface (e.g., `ifcfg-eth0`):

```bash
sudo nano /etc/sysconfig/network-scripts/ifcfg-eth0
```

1. Modify the file to include the following lines:

```
BOOTPROTO=static
ONBOOT=yes
IPADDR=
NETMASK=
GATEWAY=
DNS1=
DNS2=
```

Replace , , , , and  with your desired static IP address, subnet mask, gateway, and DNS servers respectively.

4. Save the file and exit the text editor.
5. Restart the network service to apply the changes:

```bash
sudo systemctl restart network
```

## For Fedora

1. Open the terminal.
2. Use the `nmcli` command to set a static IP address. For example:

```bash
sudo nmcli con mod "Wired connection 1" ipv4.addresses /24 ipv4.gateway ipv4.dns " " ipv4.method manual
```

Replace , , , and  with your desired static IP address, subnet mask, gateway, and DNS servers respectively.

3. Restart the NetworkManager service to apply the changes:

```bash
sudo systemctl restart NetworkManager
```

## For Arch Linux

1. Open the terminal.
2. Edit the network configuration file for your interface (e.g., `eth0`):

```bash
sudo nano /etc/netctl/eth0
```

1. Modify the file to include the following lines:

```txt
Interface=eth0
Connection=ethernet
IP=static
Address=/24
Gateway=
DNS=(' ' ' ')
```

Replace , , , and  with your desired static IP address, subnet mask, gateway, and DNS servers respectively.

4. Save the file and exit the text editor.
5. Start the network profile to apply the changes:

```bash
sudo netctl start eth0
```

1. Enable the network profile to start on boot:

```bash
sudo netctl enable eth0
```

## Verify the Configuration

After configuring the static IP address, you can verify the settings by using the following command:

```bash
ip addr show
```

This command will display the network interfaces and their assigned IP addresses. Make sure the static IP address is correctly assigned to the desired interface.

