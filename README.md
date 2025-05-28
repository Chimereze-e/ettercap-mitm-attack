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

3. Scan Network with Ettercap.
   
Launched Ettercap GUI

Scanned the LAN subnet and discovered 6 hosts

5. Configure Targets in Ettercap
6. 
Target 1: Victim host 10.6.6.23

Target 2: Server 10.6.6.13

Ettercap was configured to forward all traffic between the two through my Kali machine.

8. Launch ARP Spoofing via Terminal
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


![SSH into Target](https://github.com/user-attachments/assets/cff9d7f5-e3bf-453b-9dc3-74dc4e33377a)
SSH into Target Host

![Ettercap Host Scan](https://github.com/user-attachments/assets/73c70d05-c1fb-4739-9b5c-61db1704d235)
Ettercap Host Scan

![Ettercap Terminal Attack](https://github.com/user-attachments/assets/96fa34ab-8040-4fae-bf2c-98257ed10f86)
Ettercap Target Configuration

![ARP Spoof Confirmation](https://github.com/user-attachments/assets/ba27c771-e7b5-4604-a94e-4103ce928a89)
ARP Spoof Confirmation

![ARP Cache Manipulation](https://github.com/user-attachments/assets/82468204-1199-4119-a02b-d4772f2a3373)
ARP Cache Manipulation

![Wireshark Captur](https://github.com/user-attachments/assets/e4388214-58f3-4808-bddc-69e737c51100)
Wireshark MITM Traffic


✅ Learning Outcome

How ARP spoofing compromises LAN communications
Using Ettercap and Wireshark in real attack simulations
Ethical hacking skills in a lab-based environment
Importance of ARP table monitoring and spoof detection

📚 License

This project is licensed under the MIT License — for educational use only.
