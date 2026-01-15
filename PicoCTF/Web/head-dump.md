# Head-Dump
**Difficulty:** Easy  

---

## 🧠 Challenge Description

Welcome to the challenge! You are given access to a simple **blog web application** called *picoCTF News*. Among its articles is one about **API Documentation**.  
Your goal is to **explore the application**, find an **internal endpoint** that exposes a server-generated memory file, and extract the **hidden flag** inside it.

---

## 🔍 Initial Recon

After launching the challenge instance:

- A blog-style homepage is shown.
- There is a link titled **API Documentation** in one of the posts.
- No obvious flags are visible on the main UI.
---

## 📌 Find the API Docs

Click on the **API Documentation** link or directly visit:

/api-docs/
This opens a **Swagger UI** interface showing all the API endpoints the web app offers.

---

## 🔎 Alternative Discovery Method (Fuzzing)

Instead of relying on API documentation, the vulnerable endpoint can also be discovered using **directory and endpoint fuzzing**.

### 🔧 Using CLI Fuzzing Tools

Tools like `ffuf`, `gobuster`, or `dirsearch` can be used to brute‑force hidden endpoints:

```bash
ffuf -u https://target/FUZZ -w wordlist.txt


## 🧪 Discover the Flag Endpoint

Inside the Swagger API documentation you’ll find an endpoint named:

GET /heapdump


This endpoint digs into the **server’s memory** and returns a file that contains a **heap snapshot**.
A heap snapshot is a memory dump — it often contains all kinds of objects, variables, strings, and sometimes even sensitive information.

---

## ⚔️ Exploitation Steps

1. In Swagger UI, locate the `/heapdump` endpoint.
2. Click **Try it out**.
3. Click **Execute** to launch the request.
4. The server responds with a file download.
---

## 🛠 Extracting the Flag

The downloaded heap file is large and not human-friendly by default. To find the flag inside it:

1. Save the file locally (e.g., `heapdump.heapsnapshot`).
2. Use command-line tools to search for the picoCTF flag format:

```bash
strings heapdump.heapsnapshot | grep picoCTF

This extracts all text strings then filters for any line containing "picoCTF". 

🚩 Flag
find the flag inside the memory dump:
picoCTF{Pat!3nt_15_Th3_K3y_f1179e46}
