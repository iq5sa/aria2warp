# **aria2warp**

`aria2warp` is a high-performance, resumable downloader for macOS that uses **aria2c** with **Cloudflare WARP** proxy support. Optimized for bulk URL downloads and easy integration with `yt-dlp`.

---

## **Features**

* Multi-connection downloading (`16 connections`)
* Resumable downloads (`-c`)
* HTTP proxy via Cloudflare WARP
* Supports single URLs, text files, or stdin
* Customizable output folder
* Works anywhere on macOS after adding to PATH

---

## **Installation**

### **1. Install Dependencies**

```bash
# Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# aria2c
brew install aria2

# yt-dlp (optional)
brew install yt-dlp

# dos2unix (for cleaning Windows line endings)
brew install dos2unix
```

---

### **2. Install Cloudflare WARP (Optional)**

Download from [Cloudflare WARP](https://developers.cloudflare.com/warp-client/) and ensure it is running:

```bash
warp-cli status
```

Enable the built-in HTTP proxy (default port ``8080``):

```bash
warp-cli proxy port 8080
```
>The HTTP proxy will now listen on ``127.0.0.1:8080``.

---

### **3. Clone the aria2warp Repository**

Instead of manually creating the script, you can clone the repo:

```bash
# Choose a location for scripts
mkdir -p ~/bin
cd ~/bin

# Clone the aria2warp repository
git clone https://github.com/iq5sa/aria2warp.git
cd aria2warp

# Make script executable
chmod +x aria2warp
```
> The `aria2warp` script will now reside in `~/bin/aria2warp`.

Add it to your PATH if not already:

```bash
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

---

## **4. Prepare URL List**

Create a plain text file with one URL per line:

```
https://example.com/file1.mp4
https://example.com/file2.mp4
```

Clean it:

```bash
sed -i '' '/^$/d' urls.txt
dos2unix urls.txt
```

---

## **5. Usage**

### **Single URL**

```bash
aria2warp "https://example.com/file.zip"
```

### **URL File (Bulk Download)**

```bash
aria2warp ~/Downloads/urls.txt
```

### **URL File + Custom Output Folder**

```bash
aria2warp ~/Downloads/urls.txt ~/Downloads/Videos
```

### **Pipe URLs via stdin**

```bash
cat urls.txt | aria2warp ~/Downloads/Videos
```

---

## **6. Tips**

* **Integration with yt-dlp**:

```bash
yt-dlp -a ~/Downloads/urls.txt --external-downloader aria2warp
```

* **Change WARP proxy**

```bash
WARP_HOST=127.0.0.1 WARP_PORT=40001 aria2warp ~/Downloads/urls.txt
```

* **Organize downloads by date**:
  Modify `OUTPUT_DIR` in script to:

```bash
OUTPUT_DIR="${OUTPUT_DIR}/$(date +%F)"
mkdir -p "$OUTPUT_DIR"
```

---

## **Conclusion**

`aria2warp` provides fast, reliable, and reusable bulk downloads on macOS, with Cloudflare WARP routing and yt-dlp integration. Using a cloned repository makes installation and updates effortless.