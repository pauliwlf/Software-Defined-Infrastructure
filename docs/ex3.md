# Excercise 3: Improve your server's security!

## Step 1: Create a Firewall

1. If an old server is still running, delete it first: - Go to **Hetzner Cloud Dashboard → Select Server → Click Delete**.

2. Create a new firewall: - In the sidebar, click Firewalls. - At the bottom right, click the + (Add) button.

3. Under Rules (Inbound), configure:

   - Allow SSH access:
     - Direction: In
     - Protocol: TCP
     - Port: 22
   - Allow Ping (ICMP):
     - Direction: In
     - Protocol: ICMP

4. Save the new firewall and give it a name, e.g., `secure-firewall`.

## Step 2: Add an SSH Key

1. Go to **Security → SSH Keys → Add SSH Key**.

2. Paste your public key (not the private key!).
   - On Mac, you can display your public key with:
     ```tf
     cat ~/.ssh/id_ed25519.pub
     ```

## 3. Set the new SSH key as the default.

1. Create a new server (same process as before).

- Location: Falkenstein or Nuremberg
- Image: Debian 12
- Type: CX22 (Shared vCPU)
- Firewall: Select your created secure-firewall
- SSH Key: Select the public key you just added
- Name: For example, secure-server

2. Click Create & Pay Now.

## Step 4: Test the Server in the Terminal

1. Ping the server using its IPv4 address:

```tf
ping 162.55.178.186
```

- Find the IP under Servers → Select your server (secure-server).

2. Connect via SSH:

```tf
ssh root@162.55.178.186
```

### Fix Known Hosts Error

- If you get a host key mismatch error:

1. List your hidden `.ssh` directory:

```tf
ls -al ~/.ssh
```

2.Open the known_hosts file:

```tf
nano ~/.ssh/known_hosts
```

3. Remove all entries for this server (usually the last three).

- Tip for Mac: Install micro for easier file editing:

```tf
brew install micro
```

- Retry the SSH login after saving the file.

**Example root password (do not use in real setup):**

```tf
xTixqiReWkaLif3qhnN3
```

## Step 5: Update & Reboot

1. Update all packages:

```tf
apt update && apt upgrade -y
```

2. Reboot the server:

```tf
reboot
```

3. Log in again via SSH.

## Step 6: Install & Test Nginx

1. Install Nginx:

```tf
apt install nginx -y
```

2. Check status:

```tf
systemctl status nginx
```

- If you see active (running) → Nginx is working.

3. Test locally:

```tf
wget -O - http://162.55.178.186
```

- If you see HTML with “Welcome to nginx!”, it’s running.

## Step 7: Enable Browser Access

1. Open in your browser:

```tf
http://162.55.178.186
```

- If it doesn’t load, the firewall is blocking port 80.

2. Fix the firewall:

- Go to Firewalls → secure-firewall → Edit.
- Add a new inbound rule:
  - Direction: In
  - Protocol: TCP
  - Port: 80
- Save the changes.

3. Test again in your browser.

   - You should now see Welcome to nginx!.
