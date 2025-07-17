Welcome to Ubuntu 25.04 (GNU/Linux 6.14.0-15-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Thu May 22 01:35:37 PM UTC 2025

  System load:             0.03
  Usage of /:              50.4% of 26.17GB
  Memory usage:            10%
  Swap usage:              0%
  Temperature:             57.0 C
  Processes:               176
  Users logged in:         0
  IPv4 address for enp1s0: 192.168.1.3
  IPv6 address for enp1s0: 2001:448a:1105:19dd:7ed3:aff:fe11:56e0


0 updates can be applied immediately.


Last login: Thu May 22 13:27:31 2025 from 1x.x.x.1

Install Wireguard

$ sudo apt install wireguard


Buat file konfigurasi peer wireguard menggunakan editor

$ sudo nano /etc/wireguard/wg0.conf


[Interface]

PrivateKey = UO1GE3vFDGa+yQhcTqejSQL8H+M2RlmB2csrsVaLZ2I=

Address = 11.1.1.9/32

DNS = 1.1.1.1



[Peer]

PublicKey = jISdD7vmr4/G0wcoDe9niFjHSzKNCizFhjbO+0FtRiw=

Endpoint = peer.hosts.web.id:51820

AllowedIPs = 0.0.0.0/0,::/0

PersistentKeepalive = 10

Copy dan paste file konfigurasi ke editor

tekan control+o untuk menyimpan konfirmasi tekan y untuk keluar dari editor tekan control+x

Jalankan wireguard peer wg0 dan aktifkan service dengan cara 

$ sudo systemctl start wg-quick@wg0.service
$ sudo systemctl enable wg-quick@wg0.service
$ sudo systemctl status wg-quick@wg0.service
● wg-quick@wg0.service - WireGuard via wg-quick(8) for wg0
     Loaded: loaded (/usr/lib/systemd/system/wg-quick@.service; disabled; preset: enabled)
     Active: active (exited) since Wed 2024-06-12 04:47:53 UTC; 38s ago
       Docs: man:wg-quick(8)
             man:wg(8)
             https://www.wireguard.com/
             https://www.wireguard.com/quickstart/
             https://git.zx2c4.com/wireguard-tools/about/src/man/wg-quick.8
             https://git.zx2c4.com/wireguard-tools/about/src/man/wg.8
    Process: 2384 ExecStart=/usr/bin/wg-quick up wg0 (code=exited, status=0/SUCCESS)
   Main PID: 2384 (code=exited, status=0/SUCCESS)
        CPU: 125ms
Lihat status peer wireguard wg0

$ sudo wg
interface: wg0

  public key: XjRDFcZtmzmJpkQA7Xcr6nkmj87djhe7FhBA+JxeXyB0U=

  private key: (hidden)

  listening port: 47051

  fwmark: 0xca6c



peer: jISdD7vmr4/Gjdhbj8jniFjHSzKNCizFhjbO+0FtRiw=

  endpoint: 103.xxx.xxx.20:51820

  allowed ips: 0.0.0.0/0, ::/0

  latest handshake: 1 minute, 37 seconds ago

  transfer: 72.65 MiB received, 91.89 MiB sent

  persistent keepalive: every 10 seconds

Jika output seperti diatas berarti wireguard sudah terhubung dengan server.

$ ping 11.1.1.1
PING 10.0.0.1 (11.1.1.1) 56(84) bytes of data.
64 bytes from 11.1.1.1: icmp_seq=1 ttl=64 time=31.6 ms
64 bytes from 11.1.1.1: icmp_seq=2 ttl=64 time=31.7 ms
64 bytes from 11.1.1.1: icmp_seq=3 ttl=64 time=31.7 ms
64 bytes from 11.1.1.1: icmp_seq=4 ttl=64 time=31.7 ms
64 bytes from 11.1.1.1: icmp_seq=5 ttl=64 time=31.8 ms
64 bytes from 11.1.1.1: icmp_seq=6 ttl=64 time=31.2 ms
64 bytes from 11.1.1.1: icmp_seq=7 ttl=64 time=31.8 ms
64 bytes from 11.1.1.1: icmp_seq=8 ttl=64 time=31.4 ms
^C
--- 11.1.1.1 ping statistics ---
9 packets transmitted, 8 received, 11.1111% packet loss, time 8014ms
rtt min/avg/max/mdev = 31.161/31.613/31.843/0.222 ms
