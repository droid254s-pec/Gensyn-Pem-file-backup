# Guide: Retrieving `swarm.pem` from VPS to Your Local Machine

This guide shows you how to copy the `swarm.pem` file from the root directory on your VPS into your user’s home directory there, fix its permissions, and then download it to your local Windows PC using PowerShell.

---

## Prerequisites

- You have **sudo** (root) access on your VPS.
- You have OpenSSH server running on your VPS (port 22 by default).
- You know your VPS username and IP address.
- You have PowerShell (run as Administrator) on your Windows PC.
- You know your Windows PC username.

---

## 1. On the VPS: Copy & Secure `swarm.pem`

1. **Create a directory** in your user’s home to store the key:
    ```bash
    sudo mkdir -p /home/"$SUDO_USER"/rl-swarm
    ```

2. **Copy** the `swarm.pem` file from root’s directory into that folder:
    ```bash
    sudo cp /root/rl-swarm/swarm.pem /home/"$SUDO_USER"/rl-swarm/swarm.pem
    ```

3. **Change ownership** so your non‑root user can read it:
    ```bash
    sudo chown "$SUDO_USER":"$SUDO_USER" /home/"$SUDO_USER"/rl-swarm/swarm.pem
    ```

4. **Restrict permissions** so only you can read/write:
    ```bash
    sudo chmod 600 /home/"$SUDO_USER"/rl-swarm/swarm.pem
    ```

At this point, `swarm.pem` lives in `/home/your_user/rl-swarm/swarm.pem` and is secured.

---

## 2. On Your Windows PC: Download via PowerShell

1. **Open PowerShell as Administrator**  
   - Press **Start**, type **PowerShell**, right‑click **Windows PowerShell**, and choose **Run as administrator**.

2. **Run the following command**, replacing:
   - `user` with your VPS username  
   - `vps.example.com` with your VPS IP or hostname  
   - `<YOUR_PC_USERNAME>` with your Windows login name  

   ```powershell
   ssh -p 22 user@vps.example.com "cat ~/rl-swarm/swarm.pem" `
     > "C:\Users\<YOUR_PC_USERNAME>\Downloads\swarm.pem"

If you use a different SSH port, replace 22 with your port number.

This will prompt you for your VPS password (or use your SSH key if set up).
3.Verify that swarm.pem landed in your Downloads folder:
```bash
Test-Path "C:\Users\<YOUR_PC_USERNAME>\Downloads\swarm.pem"
  ```
Tips & Security
Never leave swarm.pem in a world‑readable location.

Consider deleting the file on the VPS after you’ve securely transferred it.

Store swarm.pem safely on your PC (e.g., in an encrypted folder).

