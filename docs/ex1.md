# Excersise 1

**Step-by-step guide to creating your first server**

## Step 1: Create a Server on Hetzner

1. Sign up or log in to Hetzner.
2. Under the dropdown menu, go to Cloud and select Projects.
3. Choose the Default project.
4. In the sidebar, click on Servers.
5. Next, click Add Server.
6. Under Create Server, choose the location (please select Nuremberg or Falkenstein).
7. Under Images, choose Debian 12.
8. For the type, select Shared vCPU x86 (Intel/AMD) CX22.
9. SSH Keys are optional, but we used them.
10. Create a unique name (for example: myFirstServer).
11. Click on Pay Now to confirm and create the server.

## Step 2: Set Root Password in Rescue Mode

1. Click on your newly created server.
2. At the top, go to the Rescue tab.
3. Click Reset Root Password and save the generated password.

Example password (don’t use this one in real setups):
`EnuA7rq3ks7MeuNLPn3H`

## Step 3: Access the Server Console

1. Click the Open Console icon on the right (>\_).
2. Log in as root with the new password.

- If you forget the password, you can find it again under the Rescue tab.
- Note: Copy-paste doesn’t work in the console, so you’ll need to type it manually.

## Step 4: (Optional) Fix Keyboard Configuration

If you need German keyboard settings:

1. Run:

```tf
dpkg-reconfigure keyboard-configuration
service keyboard-setup restart
```

2. Make the following selections:
1. **Keyboard Model:** Generic 105-key PC
1. **Keyboard Layout:** Other → German
1. **Country of Origin:** German
1. **AltGr Key:** Default (Right Alt)
1. **Compose Key:** Default (No compose key)

## 3. Restart the service:

```tf
service keyboard-setup restart
```

Note: You may need to reboot the server afterward.

## Step 5: Adjust Firewall to Allow ICMP (Ping)

To check if your server is online, we’ll enable ICMP in the firewall:

1. Log in to the Hetzner Cloud Dashboard.
2. In the sidebar, click **Firewalls** and create a new one.
3. Configure with the following rules:

- Any IPv4 / Any IPv6
- Protocol: TCP — Port 22
- Protocol: ICMP

4. Save and make sure the firewall is linked to your server:

- Under **Assigned Resources**, check if your server is listed.
- If not: click **Resources → Apply to → Server** and select your server.
- Warning: Sometimes it doesn’t display correctly — simply refresh or restart Hetzner.

## Step 6: Delete the Server (if needed)

1. n the Dashboard, go to **Servers**.
2. Select your server.
3. Click on **More (•••)** in the top right corner, or directly click **Delete**.
4. Confirm the action.
