# wifi-ad-blocker
  * Pi-hole setup guide for Raspberry Pi 4 with Jellyfin

Introduction:
This guide explains how I installed and configured Pi-hole on a Raspberry Pi 4 (2GB) that already has Jellyfin running.

The goal was to set up a network-wide ad blocker while ensuring Jellyfin continued to work smoothly.

I document the challenges encountered, how they were solved, and tips for anyone attempting the same setup.

Operating System used: Raspberry Pi OS (32-bit)


# Disclaimer!
I'm going to assume you already have your pi up and running and it's connected to your wifi/lan cable and you have its IP and created a user and password using Raspberry Pi Imager.

# Step 1
On Windows using PowerShell/CMD/Putty do the following (fill in your details):
* ssh usernamepi@yourpi.ip.address
* enter your password

Now we need to update your pi:
* sudo apt update && sudo apt upgrade -y

# Step 2
Install Pi-hole:
* curl -sSL https://install.pi-hole.net | bash
* It will show popups; just keep pressing enter.
* If you haven’t set a static IP yet, the installer will ask you to do so – create one.
* Select your network interface (wlan or eth).
* Choose Cloudflare as your upstream DNS provider.
* Select yes to block ads and yes to hide domains and clients.

# Step 3
Set a password for the Pi-hole admin panel:
* sudo pihole setpassword

# Step 4
Change your Wi-Fi router’s DNS settings:
* Set the primary DNS to your Pi-hole’s IP (e.g., 192.168.1.96)
* Set the secondary DNS to 1.1.1.1 or 8.8.8.8
* Reboot your Wi-Fi router for the changes to take effect.

# Step 5
Verify it’s working:
* Open your Pi-hole admin panel: http://yourpi.ip.address/admin
* Check for traffic on the dashboard – if you see queries, Pi-hole is actively filtering your network.

# Notes / Tips
* Pi-hole will now block ads across your entire network.
* If you want to whitelist or blacklist specific domains, you can do it from the admin panel.
* Make sure Jellyfin’s port (default 8096) is not blocked by Pi-hole or any custom rules.
