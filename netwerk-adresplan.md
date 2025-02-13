# Subnets SEP 2024-25/sem2

Splitting 192.168.200.0/24

## Clients / VLAN 12

Up to 100 clients: 192.168.200.128/25 - rest nog uitwerken hieronder

```text
Network:        192.168.200.0/25
Netmask:        255.255.255.128 = 25
Broadcast:      192.168.200.127

Address space:  Private Use
HostMin:        192.168.200.1
HostMax:        192.168.200.126
Hosts/Net:      126
```

| Device  | Interface | IP            | Subnet                | Default gateway     |
| ------- | --------- | ------------- | --------------------- | ------------------- |
| R1      | g0/0.11   | 192.168.200.1 | 255.255.255.128       | /                   |
| Clients | Fa0       | DHCP: ?       | DHCP: 255.255.255.128 | DHCP: 192.168.200.1 |

DHCP range: 192.168.200.2 - 192.168.200.126

## Servers / VLAN 11

192.168.200.64/26 - rest nog uitwerken hieronder

```text
Network:        192.168.200.128/26
Netmask:        255.255.255.192 = 26
Broadcast:      192.168.200.191

Address space:  Private Use
HostMin:        192.168.200.129
HostMax:        192.168.200.190
Hosts/Net:      62
```

| Device    | Interface | IP              | Subnet          | Default gateway |
| --------- | --------- | --------------- | --------------- | --------------- |
| R1        | G0/0.42   | 192.168.200.129 | 255.255.255.192 | /               |
| DC + DNS  | Fa0       | 192.168.200.131 | 255.255.255.192 | 192.168.200.129 |
| DC2 + DNS | Fa0       | 192.168.200.132 | 255.255.255.192 | 192.168.200.129 |
| Web       | Fa0       | 192.168.200.141 | 255.255.255.192 | 192.168.200.129 |
| Database  | Fa0       | 192.168.200.142 | 255.255.255.192 | 192.168.200.129 |

- 192.168.200.32/27 free

## DMZ / VLAN 14

192.168.200.16/28 - rest nog uitwerken hieronder

```text
Network:        192.168.200.224/28
Netmask:        255.255.255.240 = 28
Broadcast:      192.168.200.239

Address space:  Private Use
HostMin:        192.168.200.225
HostMax:        192.168.200.238
Hosts/Net:      14
```

| Device        | Interface | IP              | Subnet          | Default gateway |
| ------------- | --------- | --------------- | --------------- | --------------- |
| R1            | g0/0.13   | 192.168.200.225 | 255.255.255.240 | /               |
| Reverse proxy | Fa0       | 192.168.200.226 | 255.255.255.240 | 192.168.200.225 |

## Management network / VLAN 1

Used for init switch/router: 192.168.200.8/29

```text
Network:        192.168.200.8/29
Netmask:        255.255.255.248 = 29
Broadcast:      192.168.200.15

Address space:  Private Use
HostMin:        192.168.200.9
HostMax:        192.168.200.14
Hosts/Net:      6
```

| Device      | Interface | IP             | Subnet          | Default gateway |
| ----------- | --------- | -------------- | --------------- | --------------- |
| R1          | Vlan 1    | 192.168.200.9  | 255.255.255.248 | /               |
| SW          | Vlan 1    | 192.168.200.10 | 255.255.255.248 | 192.168.200.9   |
| TFTP        | Fa0       | 192.168.200.11 | 255.255.255.248 | 192.168.200.9   |
| R-ISP [^1]  | ?         | 192.168.200.12 | 255.255.255.248 | 192.168.200.9   |
| SW-ISP [^1] | Vlan 1    | 192.168.200.13 | 255.255.255.248 | 192.168.200.9   |

[^1]: For ISP network (Andy/Jeroen) -> Sch00nmeers als ww voor R-ISP

- 192.168.200.4/30 free

## Uplink to ISP: determined in advance in assignment

192.168.200.0/30

```text
Network:        192.168.200.0/30
Netmask:        255.255.255.252 = 30
Broadcast:      192.168.200.3

Address space:  Private Use
HostMin:        192.168.200.1
HostMax:        192.168.200.2
Hosts/Net:      2
```

| Device | Interface | IP              | Subnet          | Default gateway |
| ------ | --------- | --------------- | --------------- | --------------- |
| R-ISP  | g0/0      | 192.168.200.254 | 255.255.255.252 | 192.168.200.1   |
| R1     | g0/1      | 192.168.200.253 | 255.255.255.252 | 192.168.200.2   |

## VLAN 999

Parking
