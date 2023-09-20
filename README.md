# frp Double-Tunnel

Step 1: START SERVER (@ Remote server)
```sh
sudo ./frps -c frps.ini
```

Step 2: START SERVER (@ Local server)
```sh
sudo ./frps -c frps.ini
```

Step 3: START CLIENT (@ Local server)
```sh
sudo ./frpc -c frpc.ini
```

Step 4: START CLIENT (@ Remote server)
```sh
sudo ./frpc -c frpc.ini
```

## FAQ

**1. How to allow the frp ports on the remote server?**

`[W] [service.go:128] login to server failed: dial tcp [$IP]:7000: i/o timeout`

I also encountered this situation, on Oracle Cloud VMs. Solution from [#2905](https://github.com/fatedier/frp/issues/2905)


Generally, this is due to the firewall settings on the server. I am using Tencent's lightweight server, and it can be successfully opened using the following command:

To check the firewall status:
`firewall-cmd --zone=public --list-ports`

To add the firewall rules to open ports for TCP protocol on ports 7000-7009:
`firewall-cmd --zone=public --add-port=7000-7009/tcp --permanent`

To update the firewall configuration:
`firewall-cmd --reload`