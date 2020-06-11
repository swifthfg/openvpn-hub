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
* For OSX: 
  - After fetching created .ovpn file from server via scp, you can install any vpn client (i.e. TunnelBrick) and show your .ovpn file to that client as vpn configuration.
  - If you go to https://ipleak.net and see that you still have DNS leak, then you should go to `System Preferences > Network > Advanced > DNS`. Then delete the existing DNS(ISP DNS) from the left frame and add `8.8.8.8` or any other DNS. 
* For Ubuntu:
  - If you do not have openvpn installed first install and then run openvpn with .ovpn config. `resolvconf` package is required to change dns properly while connecting. It prevents DNS leak problems.
  - In Ubuntu clients there will be DNS leak problem if you do not uncomment the lines below in your `.ovpn` config file.
```
script-security 2
up /etc/openvpn/update-resolv-conf
down /etc/openvpn/update-resolv-conf" > $CLIENT_BASE_CONFIG
```

#### How to test it?
To learn if your ip is leaked by any means or you have a dns leak go to https://ipleak.net and expect to see the Cloud Provider's ip address and DNS servers (not your own ISP's servers).

```
oof@client:~$ sudo apt-get -y install openvpn resolvconf
oof@client:~$ sudo openvpn --config /path/to/config.ovpn # <your local directory/clientname.ovpn>
```
