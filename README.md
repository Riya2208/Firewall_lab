# 🧱 Host-Based Firewall Lab

## 🧭 Objective / Purpose
The purpose of this lab is to understand how a **host-based firewall** works and how to **configure, test, and verify** firewall rules in a controlled environment.  
This lab focuses on using **UFW (Uncomplicated Firewall)** in Kali Linux to manage inbound and outbound traffic and observe how firewalls protect systems from unauthorized access.

Through this project, I aimed to:
- Build hands-on experience with host-based firewalls.  
- Learn to configure and test firewall rules practically.  
- Understand how traffic is filtered between a host and a virtual machine.  
- Strengthen foundational security and networking skills.

---

## ⚙️ Tools & Technologies Used

| Component | Description |
|------------|-------------|
| **Operating System** | Kali Linux (Virtual Machine) |
| **Host OS** | Windows 10/11 |
| **Firewall Tool** | UFW (Uncomplicated Firewall) |
| **Web Server** | Python HTTP Server |
| **Text Editor** | Gedit |
| **Network Configuration** | Bridged Adapter |
| **Utilities** | `ip`, `ping`, `ufw`, `python3`, PowerShell |

---

## 🧩 Lab Setup

> 📁 **Recommended Repo Structure**

1. **Configure Network**  
- Set Kali Linux VM network mode to **Bridged Adapter** to allow communication between the VM and the host machine.  
   ![Network Settings](./screenshots/network-settings.png)

2. **Create Working Directory**
   ```bash
   mkdir firewall_lab
   cd firewall_lab
   sudo apt install gedit
   gedit index.html
 - Added the following content to the HTML file:
 ```bash
  I'm able to see this through Firewall!
 ```
3. **Start a Simple Web Server**
```bash
# From inside the firewall_lab directory
python3 -m http.server 8080
```
- Verified it by visiting http://localhost:8080/ in Firefox on the Kali VM.
4. **Check Firewall Status**
```bash
sudo ufw status
```
- Initially, the firewall should be inactive.
 5. **Check IP Address**
  ```bash
  ip a
  ```
  - Note the VM's IP (used for host ↔ VM testing).
6. **Verify Connectivity from Host**
   - On the host machine (PowerShell / Terminal):
```powershell
 ping 192.168.126.133
```
  - Successful replies confirm networking (bridged mode working).
  
7. **Access Web Server from Host**
    -On host browser:
```cpp
http://192.168.126.133:8080/
```
  - The page should load because UFW is not enabled yet.
    
## 🔐 Firewall Configuration and Testing

### 8. Enable the Firewall
```bash
sudo ufw enable
sudo ufw status
```
- Once enabled, UFW begins filtering incoming traffic based on default deny policies.
9. Test Connectivity After Enabling
  - On your host machine (PowerShell):
    ```bash
    ping 192.168.126.133
    ```
   - The ping should fail, confirming the firewall is actively blocking inbound ICMP requests.
10. Try Accessing Web Server Again
 -  On your host browser, enter:
   ```cpp
http://192.168.126.133:8080/
```
- The page should not load, since the firewall is blocking port 8080 by default.
11. Allow Incoming HTTP Traffic (Port 8080)
  ```bash
  sudo ufw allow 8080/tcp
  sudo ufw status
- Verify that UFW now shows an ALLOW rule for port 8080:
  ```pgsql
  To                         Action      From
  --                         ------      ----
  8080/tcp                   ALLOW       Anywhere
  8080/tcp (v6)              ALLOW       Anywhere (v6)
  ```
12. Verify and Re-Test
   - Go back to your host browser and reload:
      ```cpp
      http://192.168.126.133:8080/
  - The page should load successfully again, confirming that your new rule allows HTTP traffic.
13. Optional: Deny Rule Test
  ```bash
     sudo ufw deny 8080/tcp
     sudo ufw status
```
 - Now, when you refresh the page in your host browser, it should fail to load again — confirming that the deny rule is active and functioning.
   





