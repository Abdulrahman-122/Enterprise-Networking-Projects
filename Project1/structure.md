# the aim of this project
 - how to connect two LAN with each other 
 - using 1 router,2 switches,
 - each LAN contain (2 pcs,1 printer)
 - the network that we will use:192.168.40.0
 - and configure the two Subnets on the router using auto duplex mode .
<img width="1710" height="647" alt="image" src="https://github.com/user-attachments/assets/7249c80b-02e8-4964-b32d-c9035df3db33" />
<img width="1378" height="696" alt="image" src="https://github.com/user-attachments/assets/1922c119-857c-4adc-8838-7741a7c78852" />
<img width="1292" height="377" alt="image" src="https://github.com/user-attachments/assets/b2390aa4-298c-41b7-ab15-fa5ff35ebb7c" />
<img width="711" height="607" alt="image" src="https://github.com/user-attachments/assets/5c2a0110-d1b8-4b82-9bc6-5f3d3ffbce12" />
<img width="1422" height="960" alt="image" src="https://github.com/user-attachments/assets/e26e3660-9b83-4f31-bfdc-6fd208e3170a" />



Network address=192.168.40.0
No.of subnets=2
2^n=2  => n=1  so we need to flip 0 to 1 in the  last octate
subnet mask = 11111111.11111111.11111111.10000000=/25
255.255.255.128 (subnet mask)



1st subnet:
subnet mask =255.255.255.128
Network ID=192.168.40.0
Range of valid addresses(host)=2^7=128 addresses in each subnet
192.168.40.1 -> 192.168.40.126
Broadcast ID=192.168.40.127
Default gateway: 192.168.40.1

2nd subnet
subnet mask =255.255.255.128
Network ID=192.168.40.128(always the first address in the Network)
Range of valid addresses(host bits)=128 addresses
192.168.40.129->192.168.40.254
Broadcast address=192.168.40.255 (always the last address)
default gateway: 192.168.40.129

note: enable show labels mode on the interfaces (in order to assign the correct ip range on the router)
- you can download the file of this project .pkt and import it on your cisco packet tracer
