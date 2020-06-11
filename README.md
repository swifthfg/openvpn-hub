# openvpn-hub

#### What is this about?
These bash scripts creates your own vpn server with openvpn. First it creates a full server setup in Ubuntu with firewall and proper openvpn configs. After the server setup, one can also create as many client config files as wanted for the server. In my own tests with Ubuntu 18.04 server and client there is no ip leak, dns leak, ip detection from webRTC. 

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
* For Ubuntu: If you do not have openvpn installed first install and then run openvpn with .ovpn config. `resolvconf` package is required to change dns properly while connecting. It prevents DNS leak problems.

#### How to test it?
To learn if your ip is leaked by any means or you have a dns leak go to https://ipleak.net and expect to see the Cloud Provider's ip address and DNS servers (not your own ISP's servers).

```
oof@client:~$ sudo apt-get -y install openvpn resolvconf
oof@client:~$ sudo openvpn --config /path/to/config.ovpn # <your local directory/clientname.ovpn>
```
