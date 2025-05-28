# wireguard
Wireguard Peer Andalas Cloud
$ sudo apt install wireguard

$ sudo nano /etc/wireguard/wg0.conf

------------------------------------------------------------

[Interface]

PrivateKey = UO1GE3vFDGa+yQhcTqejSQL8H+M2RlmB2csrsVaLZ2I=

Address = 11.1.1.9/32

DNS = 1.1.1.1



[Peer]

PublicKey = jISdD7vmr4/G0wcoDe9niFjHSzKNCizFhjbO+0FtRiw=

Endpoint = peer.hosts.web.id:51820

AllowedIPs = 0.0.0.0/0,::/0

PersistentKeepalive = 10


-----------------------------------------------------------
