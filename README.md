# frp Double-Tunnel

## Use Case

In this repository, we provide a simple solution to access a service running on a remote server. By following the steps outlined here, you will be able to access the service on your local server and local area network (LAN).

This solution is particularly useful when the local area network (LAN) is behind a strong firewall that blocks specific ports and protocols through deep packet inspection. By utilizing frp, you can bypass these restrictions and access a service running on a remote server within the LAN.

## Setup frp (on both remote and local servers)

1. Download and extract the latest release of frp from [here](https://github.com/fatedier/frp/releases).
2. Configure frp by editing the configuration (.ini) files on both servers based on the examples provided in this repository.

### Step 1: Start Server (Remote server)

```sh
sudo ./frps -c frps.ini
```

### Step 2: Start Server (Local server)

```sh
sudo ./frps -c frps.ini
```

### Step 3: Start Client (Local server)

```sh
./frpc -c frpc.ini
```

### Step 4: Start Client (Remote server)

```sh
./frpc -c frpc.ini
```

## Frequently Asked Questions

**Q: How can I allow frp ports on the remote server?**

**Solution from:** [#2905](https://github.com/fatedier/frp/issues/2905)

Sometimes, you may encounter the following error: `[W] [service.go:128] login to server failed: dial tcp [$IP]:7000: i/o timeout`. I also encountered this problem on Oracle Cloud VMs. If you face this issue, follow these steps to resolve it:

1. Check the firewall status on the server using the command: `firewall-cmd --zone=public --list-ports`.
2. Add the firewall rules to open ports for the TCP protocol on ports 7000-7009 using the command: `firewall-cmd --zone=public --add-port=7000-7009/tcp --permanent`.
3. Update the firewall configuration using the command: `firewall-cmd --reload`.

## Contributions

Contributions are welcome! If you have any suggestions, ideas, or enhancements for this project, please feel free to open an issue or submit a pull request.