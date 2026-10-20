- <img width="1266" height="899" alt="image" src="https://github.com/user-attachments/assets/43f3f587-abd4-45f6-a428-14d017740d8a" />
- <img width="1229" height="878" alt="image" src="https://github.com/user-attachments/assets/164df1d3-9bfe-42c6-b261-33be2f3497ca" />
- <img width="1472" height="662" alt="image" src="https://github.com/user-attachments/assets/9f480c63-985f-434f-87d8-16d627d6bdeb" />
# Test cases
- <img width="1451" height="759" alt="image" src="https://github.com/user-attachments/assets/6249a56c-4e26-4f36-b36b-803f098d5f85" />
- <img width="1388" height="710" alt="image" src="https://github.com/user-attachments/assets/860b989b-0c2b-4304-a49e-8b880aa3102a" />

#  How to build this project from a to z:

- step 1 (plan and connect your entire infrastructure)
  - - <img width="1472" height="662" alt="image" src="https://github.com/user-attachments/assets/9f480c63-985f-434f-87d8-16d627d6bdeb" />
- step 2(start build the protocols,configurations)
note: to make DCE connection on the router you need to do the following
- move that HWIC-2T and put it on one of the interfaces of the router
- <img width="662" height="609" alt="image" src="https://github.com/user-attachments/assets/28e0d702-48e6-4ff8-b93e-22a82cd3c5a2" />
- <img width="452" height="67" alt="image" src="https://github.com/user-attachments/assets/7decfc2d-08b6-4cf2-9607-520d32c2b7a1" />
-  and do the same with the other routers

-----

 - Configurations on router 
  
  ```
- for each router
  #en
  #conf t
  # int g0/0
  # no shutdown
  # int s0/1/0   (check the correct port)
  # no shutdown
  #int s0/2/0    (check the port)
  #no shutdown
  now if that router contain a clock symbol on one of its interfaces go into that interface and configure the clock rate of it
  #int s0/1/0   (for example)
  # clock rate 64000   (this will define the speed of the traffic that the router will redirect in or out of it
#do the same for each router
  ```
- Configurations on switches (Vlan,trunk port)
```
int fa0/1-3
switchport mode access
switchport access vlan 10
dp wr
# do this for each switch with all pairs of ports
```
- Add ip address for each interface of each router
```
for ex: router 1
has 3 interfaces (int Se0/2/1,Se0/2/0,g0/0)
  - set ip for each one;
    - int Se0/2/0
    - ip address 10.10.10.10.6 255.255.255.252      (as we have /30 as a subnet mask)
    - int Se0/2/1
    - ip address 10.10.10.10.9 255.255.255.252
    - for g0/0(divide the router int for each  vlan)
      - int g0/0.80
      - encapsulation dot1Q 80
        ip address 192.168.8.1 255.255.255.0
      - int g0/0.70
        encapsulation dot1Q 70
        ip address 192.168.7.1 255.255.255.0
      - int g0/0.60
        encapsulation dot1Q 60
        ip address 192.168.6.1 255.255.255.0
    - do the same for all routers
- then go to each switch on the link that connected them with the router and write:
    - int fa0/1
    - switchport mode trunk
```
- Configure the dhcp,dns on each router
```
#let's configure for Router1
#we have 3 vlans (Reception,store logistics)
write the following:
service dhcp
ip dhcp pool Reception
network 192.168.8.0 255.255.255.0
default router 192.168.8.1
dns-service 192.168.8.1

ip dhcp pool Store
network 192.168.7.0 255.255.255.0
default router 192.168.7.1
dns-service 192.168.7.1

ip dhcp pool Logictics
network 192.168.6.0 255.255.255.0
default router 192.168.6.1
dns-service 192.168.6.1

```
- Configure the OSPF on the routers
```
#for example router10
router ospf 10
network 10.10.10.8 255.255.255.252
network 10.10.10.4 255.255.255.252
network 192.168.8.0 255.255.255.0
network 192.168.7.0 255.255.255.0
network 192.168.6.0 255.255.255.0

```
- Configure ssh on the routers
```
Router(config)# hostname Myrouter
Myrouter(config)#ip domain-name Myrouter

Myrouter(config)# username Myrouter password myrouter

Myrouter(config)#crypto key generate rsa
#click: 2024 as a length for the rsa.
#line vty 0 15
#login local
#transport input ssh
Myrouter: secret enable Myrouter

# now go to any that is connected to that router and make him
#ssh -l Myrouter 10.10.10.6

```
- <img width="1350" height="709" alt="image" src="https://github.com/user-attachments/assets/9641624b-6c3f-44f8-926f-3090c2b5263b" />

- Now add port-security on IT pcs
1. **Enter global configuration mode:**
    
    text
    
    ```
    Switch> enable
    Switch# configure terminal
    ```
    
    Use code with caution.
    
2. **Navigate to the specific interface (Fa0/1):**
    
    text
    
    ```
    Switch(config)# interface fastEthernet 0/1
    ```
    
    Use code with caution.
    
3. **Set the interface port status to access mode:**  
    _(Port security can only be enabled on static access ports or trunk ports; it cannot be left on dynamic default settings)._
    
    text
    
    ```
    Switch(config-if)# switchport mode access
    ```
    
    Use code with caution.
    
4. **Enable port security on the interface:**
    
    text
    
    ```
    Switch(config-if)# switchport port-security
    ```
    
    Use code with caution.
    
5. **Configure the sticky method to dynamically learn the PC's MAC address:**  
    _(This tells the switch to learn the MAC address of the first PC that sends traffic through this port and save it into the running configuration)._
    
    text
    
    ```
    Switch(config-if)# switchport port-security mac-address sticky
    ```
    
    Use code with caution.
    
6. **Set the maximum number of allowed MAC addresses to 1:**
    
    text
    
    ```
    Switch(config-if)# switchport port-security maximum 1
    ```
    
    Use code with caution.
    
7. **Set the violation mode to shutdown:**  
    _(If an unauthorized device with a different MAC address is plugged into this port, the switch will immediately change the interface status to `err-disabled` / down)._
    
    text
    
    ```
    Switch(config-if)# switchport port-security violation shutdown
    ```
    
    Use code with caution.
    

---

How to Verify Your Work

To make sure the switch has successfully learned the PC's MAC address and locked down the port, go to the PC and ping something so it sends a packet. Then, run this command on the switch:

text

```
Switch# show port-security interface fastEthernet 0/1
```

Use code with caution.

Look for **Port Status: Secure-up**, **Violation Mode: Shutdown**, and **Sticky MAC Addresses: 1**.
