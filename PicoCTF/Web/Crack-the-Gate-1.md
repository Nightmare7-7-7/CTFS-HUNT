# Crack the Gate 1


**Difficulty:** Easy  

---

## 🧠 Challenge Description

We are investigating a restricted web portal.  
A user named **ctf-player** is suspected of hiding sensitive data.

Known information:
- 📧 Email: `ctf-player@picoctf.org`
- 🔐 Password: Unknown
- ❌ Password guessing does not work

The challenge hints that:
> “it’s almost like the developer left a secret way in”

This suggests a **hidden backdoor or logic flaw**.

---

## 🔍 Recon / Analysis

After launching the challenge instance:

- A login page is presented
- Email and password fields exist
- Brute force attempts fail
- No rate-limiting or error clues appear

At this point, instead of attacking the login directly, we inspect the **page source**.

---

## 🧪 Source Code Inspection

Viewing the page source (`Ctrl + U`) reveals a suspicious HTML comment:
ABGR: Wnpx - grzcbenel olcnff: hfr urnqre "K-Qri-Npprff: lrf"


This text looks encoded.

---
## 🔐 Decoding the Hint

The string is encoded using **ROT13**.

Decoded result:
NOTE: Jack - temporary bypass: use header "X-Dev-Access: yes"



🚨 This clearly indicates:
- A **developer backdoor**
- Authentication can be bypassed by sending a special HTTP header

---

## ⚔️ Exploitation Steps

1. Open the login page
2. Enter the known email:



ctf-player@picoctf.org

3. Enter **any password**
4. Intercept the login request using **Burp Suite**
5. Add the following HTTP header: X-Dev-Access: yes
6. Forward the modified request

✅ The server accepts the request and bypasses authentication.

🚩 Collect The Flag
picoCTF{brut4_f0rc4_b3a957eb}
