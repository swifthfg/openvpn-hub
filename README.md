# openvpn-hub

#### Requirements:
- Ubuntu 18.04 server (obtain it from any cloud provider i.e. DigitalOcean)

#### Usage:

```console
oof@server:~$ ./opensetup <optional-client-name>
oof@server:~$ ./create-client <other-client>
scp oof@server:$HOME/.opensetup/client/files/openclient.ovpn <your local directory>
```

#### How to use .ovpn file?
* For OSX: After fetching created .ovpn file from server via scp, you can install any vpn client (i.e. TunnelBrick) and show your .ovpn file to that client as vpn configuration.
* For Ubuntu: If you do not have openvpn installed first install and then run openvpn with .ovpn config.

```
oof@client:~$ sudo apt-get -y install openvpn
oof@client:~$ sudo openvpn --config /path/to/config.ovpn # <your local directory/clientname.ovpn>
```
