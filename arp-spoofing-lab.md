#Objective.

To perform an ARP spoofing attack to demonstrate Man-in-the-Middle (MitM) interception in a controlled lab environment.

ARP- Address Resolution Protocol.
It is a protocol that maps an IP address (logical address) to a MAC address (physical address) on a local network. 
When a computer wants to talk to another on the same network, it has to know the MAC address of that computer.
An ARP request is sent and is broadcasted to all devices on the network. It is something like- "who is 192.168.0.100, Tell me your MAC address"
The device with that IP replies with its MAC address. Something like - "I am 192.168.0.100 and my MAC address is AA:BB:CC:DD:EE:FF.
The sender then saves this information in its arp table so it can send packets directly now that it has the MAC address.

#Lab setup.

Attacker - Kali Linux VM - 192.168.0.102.

Victim- Windows machine - 192.168.0.100.

Gateway - Router IP - 192.168.0.1.

Wireshark.

#Procedure.

1. Open the kali linux VM and open the terminal. Run the command below to check the interface, IP address and MAC address associated with the Kali Linux VM.
   
       `ip a
3. Open command prompt on the windows victim machine and run the command to check the IP address and the default gateway IP address.

        `ipconfig
5. You can also run the command below to check all associated IP addresses of devices on your network with their MAC addresses.
   
       `arp -a
7. On the Kali VM, open wireshark, select the interface to capture the traffic on. Filter arp and start capture.
8. On the Kali terminal, type the commands below to perform the spoof.
   
        `arpspoof -i <interface> -t <victimIP> <gatewayIP>.
   
        `arpspoof -i <interface> -t <gatewayIP> <victim>.
   
  e.g   `arpspoof -i eth0 -t 192.168.0.1 192.168.0.100.
  
The commands above allow us to specify the interface we want to use using -i and the target we want to spoof using -t.

10. Observe spoofed ARP replies on Wireshark flagged as "duplicate use of 192.168.0.1 detected".
    
12. On the windows machine command prompt, run the `arp -a command again and note the changes on the MAC addresses.

#Packet analysis summary.

ARP requests showed 00:00:00:00:00:00 as the target MAC address when the sender did not know the real MAC address of the target.

ARP has no authentication therefore anyone can reply with a MAC address making ARP spoofing possible.

![image](https://github.com/user-attachments/assets/9179fadc-2283-408f-89f1-cf369e7d017e)

![image](https://github.com/user-attachments/assets/af827adf-b37c-4b5e-a0f2-e661d02b4ffa)

![image](https://github.com/user-attachments/assets/6c3d04db-1104-4897-97db-592fd6063e9d)

![image](https://github.com/user-attachments/assets/432b5c62-36ec-4300-8140-04c946faf41f)




