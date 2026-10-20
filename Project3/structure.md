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

```
