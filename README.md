# 🛡️ Cybersecurity Virtual Lab

A self-built, fully documented cybersecurity lab designed to simulate real-world enterprise network environments. This lab is built entirely on **Hyper-V**, **pfSense**, **Wazuh**, **Docker**, and **Portainer**, with layered VLAN segmentation, firewalling, monitoring, and vulnerable application testing — all configured step by step and tested manually.

> 🚀 Created and maintained by a cybersecurity student as a final capstone project — focused on hands-on learning, problem-solving, and real-world implementation.

---

## 📌 Project Goals

- Build a realistic, scalable cybersecurity lab for learning and experimentation
- Simulate segmented enterprise networks with real firewall rules and DHCP configurations
- Deploy Wazuh SIEM to collect logs and monitor alerts from multiple VLANs
- Run vulnerability testing using containers (DVWA, BWAPP, WebGoat)
- Practice attack simulation, network traffic control, and log analysis
- Use both **Hyper-V** and **VMware** with multiple adapters and inter-machine communication

---

## 🧠 What I Learned / Built Myself

✅ Hyper-V network configuration and VLAN design  
✅ pfSense installation, routing, DHCP, firewall rule tuning  
✅ Using Kali Linux and Metasploitable2 for attack simulation  
✅ Installing Wazuh on Ubuntu and integrating with the lab  
✅ Docker container networking and macvlan interface creation  
✅ Managing Portainer and testing vulnerable apps  
✅ Debugging physical-to-virtual Ethernet communication  
✅ Static IP planning and inter-VLAN security  
✅ Full lab documentation and snapshotting setup

---

## 🧱 Lab Architecture Overview

- **Host 1** (Windows PC): Hyper-V
  - pfSense firewall
  - VLAN 1 (LAN): Kali, Nessus, Wazuh Agent
  - VLAN 10: Metasploitable2
  - VLAN 20: Windows Server (Domain Controller), Windows 10 client
  - VLAN 30: Ubuntu with Docker (Portainer, DVWA, BWAPP, WebGoat)

- **Host 2** (Laptop): VMware Workstation
  - Ubuntu Server with Wazuh Manager (static IP)
  - Connected via Ethernet and bridged networks to interact with pfSense

---

## 🌐 Network Configuration

| VLAN | Name        | Subnet          | Gateway         | DHCP Range               | Purpose                          |
|------|-------------|------------------|------------------|--------------------------|----------------------------------|
| 1    | LAN         | 10.10.1.0/24     | 10.10.1.254      | 10.10.1.50 – 10.10.1.100 | Admin, Kali, Nessus, Wazuh Agent |
| 10   | Test-Net    | 10.10.10.0/24    | 10.10.10.254     | 10.10.10.50 – 10.10.10.100 | Metasploitable2 Target           |
| 20   | Windows-Net | 10.10.20.0/24    | 10.10.20.254     | 10.10.20.50 – 10.10.20.100 | AD + Windows 10                  |
| 30   | Docker-Net  | 10.10.30.0/24    | 10.10.30.254     | 10.10.30.50 – 10.10.30.100 | Docker containers via Portainer |


## 🔧 Lab Setup Highlights

### 🧩 pfSense Firewall
- Multi-VLAN setup with DHCP on each
- Strict inter-VLAN firewall rules
- Rule logging and ICMP/SSH/HTTP management
- VLAN assignment through Hyper-V workaround

### 🧩 Wazuh SIEM
- Installed on Ubuntu Server (static IP `10.10.1.75`)
- Uses bridged networking via VMware on a separate laptop
- Collects logs from Kali, Windows, and Docker containers
- Monitors and triggers alerts via agent logs and syslogs

### 🧩 Docker & Portainer
- Docker installed on Ubuntu VM in VLAN 30
- Portainer deployed to manage containers
- Vulnerable apps installed:
  - `DVWA` @ `10.10.30.129`
  - `BWAPP` @ `10.10.30.130`
  - `WebGoat` @ `10.10.30.128`
- Macvlan configured for external reachability

---

## 🧪 Next Steps

- [ ] Integrate Nessus scan reports into Wazuh dashboard
- [ ] Add reverse proxy for container access over DNS
- [ ] Simulate brute force and malware alerts via Wazuh
- [ ] Document incident response use case
- [ ] Package project as a guide for beginners

---

## 📸 Screenshots

> See `/Screenshots/` folder for:
- pfSense firewall rule GUI
- Wazuh alert interface
- Portainer container setup
- VLAN settings and IP maps

---

## 🗂️ Documentation

- [`Full_Lab_Setup.md`](Documentation/Full_Lab_Setup.md) — Everything, step by step
- [`Wazuh_Installation.md`](Documentation/Wazuh_Installation.md)
- [`Portainer_Config.md`](Documentation/Portainer_Config.md)

---

## 🙌 Credits & Reference

This project was inspired by self-learning and real-world infrastructure building. Main guide followed:  
📺 [This YouTube Lab Series](https://youtube.com/playlist?list=PL3ljjyal211AbTqlxSo6CGBiVqsXw8wrp&si=Bug8HsQNoIbcmKeD)  

And many hours of Googling, testing, and breaking things.

