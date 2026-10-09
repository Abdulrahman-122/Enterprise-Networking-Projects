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
