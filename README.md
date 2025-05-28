# MITM ARP Spoofing Attack using Ettercap (Ethical Hacking Challenge)

This project documents an ethical hacking challenge in which I performed a Man-in-the-Middle (MITM) ARP spoofing attack using Ettercap on a Kali Linux system. The objective was to intercept traffic between a target host and its server in a controlled lab environment.

> ⚠️ **Disclaimer**  
> This project was conducted in a controlled lab as part of an ethical hacking course. All activities were authorized and performed for educational purposes only.

---

## 🛠 Tools Used

- Kali Linux
- Ettercap (GUI and CLI)
- Wireshark
- SSH
- ARP Protocol

---

## 🧪 Attack Process

### 1. Establish SSH Connection

Connected to the target host from Kali Linux:
```bash
ssh -l labuser 10.6.6.23
```

2. Check ARP Table on Target

```bash
ip neighbor
```
This displayed MAC addresses of devices on the local network.

3. Scan Network with Ettercap
Launched Ettercap GUI
Scanned the LAN subnet and discovered 6 hosts

4. Configure Targets in Ettercap
Target 1: Victim host 10.6.6.23
Target 2: Server 10.6.6.13
Ettercap was configured to forward all traffic between the two through my Kali machine.

5. Launch ARP Spoofing via Terminal
```bash
sudo ettercap -T -q -i br-internal --mitm arp /10.6.6.23// /10.6.6.13//
```

6. Trigger Traffic Between Targets
On the victim host:

```bash
ping -c 5 10.6.6.13
```
The ARP cache showed the server’s IP now mapped to my Kali MAC — spoofing confirmed.

7. Verify Precision
I pinged a third device (bystander host) to ensure it was not affected, confirming the spoof was targeted.

8. Capture and Analyze with Wireshark
Opened Wireshark to inspect the .pcap file
Verified MITM traffic and saw duplicate IP use (Kali impersonating server)


🖼 Screenshots

![SSH to target](https://github.com/user-attachments/assets/170911b1-1ecc-44f9-8160-bfb3006bd1fd)
SSH into Target Host

![Ettercap host scan](https://github.com/user-attachments/assets/b1314106-24f4-4eef-81b3-c190c2029e33)
Ettercap Host Scan

![Ettercap Terminal Attack](https://github.com/user-attachments/assets/ca5ce6cd-7032-4dfb-9788-a907616e8761)
Ettercap Target Configuration

![ARP Spoof Confirmation](https://github.com/user-attachments/assets/1216c018-8c63-4a9f-a682-fbacd9dfef69)
ARP Spoof Confirmation

![ARP Cache Manipulation](https://github.com/user-attachments/assets/b74cd8af-47b7-411b-9bf3-313c20cc3638)
ARP Cache Manipulation

![Wireshark Capture (Duplicate IP Detected)](https://github.com/user-attachments/assets/25761666-6814-4eb1-89d8-5bc73882efe7)
Wireshark MITM Traffic


✅ Learning Outcome

How ARP spoofing compromises LAN communications
Using Ettercap and Wireshark in real attack simulations
Ethical hacking skills in a lab-based environment
Importance of ARP table monitoring and spoof detection

📚 License

This project is licensed under the MIT License — for educational use only.
