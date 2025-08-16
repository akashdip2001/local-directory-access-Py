# **`Serving files from your PC` over LAN (Wi-Fi/Hotspot) using Python’s built-in `HTTP server`**.

![IMG20250817005946](https://github.com/user-attachments/assets/b3591e42-353d-4a69-be6b-7791313edf7f)

This lets your phone (or any device on the same Wi-Fi / LAN) access your computer’s directory via a browser using your **PC’s IP address** and a chosen **port**.

---

## 🔹 Step 1: Find Your Computer’s Local IP

Open **Command Prompt (cmd)** on Windows and type:

```bash
ipconfig
```

Look for:

```
Wireless LAN adapter Wi-Fi:
   IPv4 Address . . . . . . . . . . . : 192.168.x.x
```

That `192.168.x.x` is your **computer’s LAN IP**.

---

<img width="1920" height="1080" alt="Screenshot (671)" src="https://github.com/user-attachments/assets/8495538b-67a2-4c2c-bedf-f5ef359f6b50" />

## 🔹 Step 2: Run Python HTTP Server

Now go to the folder you want to share and open a terminal (cmd or PowerShell).
Run this command:

### For Python 3.x

```bash
python -m http.server 8000
```

or if you want to specify directory explicitly:

```bash
python -m http.server 8000 --directory "C:\Users\YourName\Videos"
```

This starts a server on **port 8000**.

---

## 🔹 Step 3: Access From Your Phone

* Make sure your **phone and laptop are on the same Wi-Fi network**.
* Open a browser on your phone and type:

```
http://<your_PC_IP>:8000
```

Example:

```
http://192.168.1.47:8000
```

Now you’ll see a **directory listing** like in your screenshot. You can click videos, images, or files — they’ll stream directly!

---

## 🔹 Step 4 (Optional): A Cleaner Web Server

If you want a nicer file browser, you can install **http.server with autoindex** (extra features):

```bash
pip install httpserver
httpserver
```

Or use **Flask** if you want a custom design:

```python
from flask import Flask, send_from_directory
import os

app = Flask(__name__)
SHARE_DIR = "C:/Users/YourName/Videos"

@app.route('/')
def list_files():
    files = os.listdir(SHARE_DIR)
    return '<br>'.join([f'<a href="/file/{f}">{f}</a>' for f in files])

@app.route('/file/<path:filename>')
def get_file(filename):
    return send_from_directory(SHARE_DIR, filename)

if __name__ == '__main__':
    app.run(host="0.0.0.0", port=8000, debug=True)
```

Run it:

```bash
python app.py
```

Then open:

```
http://<your_PC_IP>:8000
```

<p align="center">
  <img src="https://github.com/user-attachments/assets/a746ee40-a9f4-4b19-863d-a422fb683f66" width="69%" /> 
  <img src="https://github.com/user-attachments/assets/4810e025-bfaa-423f-ba46-b6cd54b490a2" width="24%" /> 
</p>

---
