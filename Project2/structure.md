<img width="889" height="383" alt="image" src="https://github.com/user-attachments/assets/2a956094-3a25-4371-89a4-848158206d64" />

---
```
Network  -> 192.168.1.0
we need 3 subnets 
2^n =3 -> n=2 in order to get 3 we need 4 subnets as we use even power 
subnet mask= 11111111.11111111.11111111.11000000 = 255.255.255.192=/26
since 2^8 =256 
Block size=256-192 = 64 address per subnet
subnet 1
Network ID= 192.168.1.0
Broadcast ID= 192.168.1.63 (0+63)
Host range=192.168.1.1  -> 192.168.1.62
Default gateway = 192.168.1.1
subnet 2
Network ID= 192.168.1.64
Broadcast ID=192.168.1.127(63+64)
Host range=192.168.1.65 => 192.168.1.126
Default Gateway= 192.168.1.65
subnet 3
Network ID= 192.168.1.128
Broadcast ID=192.168.1.191  (127+64)
Host range=192.168.1.129 -> 192.168.1.190
Default Gateway= 192.168.1.129
```

---
#    How to build this project


<img width="1822" height="678" alt="image" src="https://github.com/user-attachments/assets/359195ee-5c7c-4b56-a690-004596590392" />

first go to the switch
```go
en
conf t
int range  fa0/1-4
switchport mode access
switch access vlan 10
int range fa0/5-8 
switchport mode access
switchport access vlan 20
int range fa0/9-12
switchport mode access
swithport access vlan 30
ex
do wr
int fa0/13
switchport mode trunk
ex
do wr
do show  interfaces trunk 

```

then now go to the router
```go
en
conf t
int g0/0.10
encapsulation dot1Q 10
ip address 192.168.1.1 255.255.255.192
exit
int g0/0.20
encapsulaation dot1Q 20
ip address 192.168.1.65 255.255.255.192
int g0/0.30
encapsulation dot1Q 30
ip address 192.168.1.129 255.255.255.192
#now configure the dhcp on the router for each department
service dhcp
ip dhcp pool Admin-Pool
network 192.168.1.0 255.255.255.192
default-router 192.168.1.1
dns-server 192.168.1.1
domain-name  admin.com

# for the second department
ip dhcp pool Finance-Pool
network 192.168.1.64 255.255.255.192
default-router 192.168.1.65
dns-server 192.168.1.65
domain-name  finance.com

#for the third department
ip dhcp pool Customer-Pool
network 192.168.1.128 255.255.255.192
default-router 192.168.1.129
dns-server 192.168.1.129
domain-name  customer.com

ex
do wr

```
now go with each device and enable dhcp on it
<img width="689" height="332" alt="image" src="https://github.com/user-attachments/assets/549de0ae-c662-4af4-82f3-48a85439a129" />

here : after you click : DHCP it will generate the default gateway for it+ it's IP by default
<img width="673" height="616" alt="image" src="https://github.com/user-attachments/assets/63d4b95a-7490-42cc-9b84-b27996d5b10b" />

do the same with all pcs and printers
<img width="689" height="747" alt="image" src="https://github.com/user-attachments/assets/82aaa87a-b9a9-4186-bc40-314912fa365a" />
<img width="728" height="836" alt="image" src="https://github.com/user-attachments/assets/8f0e1c59-db78-4149-ba7b-f2bcfcadcc64" />


Now for each access point :
- just give it new Name + password (in order to use them with the laptop,smartphone,laptop in order to sign in to the Network)
<img width="677" height="665" alt="image" src="https://github.com/user-attachments/assets/543ab73b-0af4-4396-9aeb-888764a1dfee" />

for any laptop you will need to move his card and put this card : 
<img width="704" height="683" alt="image" src="https://github.com/user-attachments/assets/02c50b92-3c42-4128-a50e-703e49a8bba2" />

 move it to the left and put instead this card after you power off the laptop 
 WPC300N
 <img width="701" height="733" alt="image" src="https://github.com/user-attachments/assets/f25cbb1c-0b40-4b3d-86be-be411f175b3c" />
<img width="719" height="721" alt="image" src="https://github.com/user-attachments/assets/ebb754ab-f1ac-413e-b4aa-ce34f667dfdb" />

then go to config bar and enable dhcp 
<img width="673" height="640" alt="image" src="https://github.com/user-attachments/assets/9a9c28e1-da67-4db5-a5b8-029748ba30c8" />

now you will notice that 
<img width="319" height="347" alt="image" src="https://github.com/user-attachments/assets/e49780d2-22e3-483a-90c5-68d6d7c6b4e1" />

it's  now connecting to the access point


with the tablet : just enable dhcp in the config bar + smartphonee also
<img width="683" height="740" alt="image" src="https://github.com/user-attachments/assets/ab9d8b7c-5b63-4374-91c9-041ec175e190" />
<img width="703" height="742" alt="image" src="https://github.com/user-attachments/assets/8b73b722-f3e8-47a0-a56a-128b9331933c" />

