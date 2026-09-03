# AdGuard Home Smart TV & Mobile Setup Guide 🚀

A complete guide to configuring your network devices, Smart TVs, and smartphones to utilize our self-hosted **AdGuard Home** instance. This setup blocks tracking, telemetry, and annoying ads across all connected screens.

---

## 🔑 Infrastructure & Connection Details

Our AdGuard Home service is hosted on a remote cloud instance. If you need to access the server backend for maintenance or docker updates, use the dedicated secure SSH deployment key.

### Secure SSH Connection
The instance is configured to use strict cryptographic key authentication. The specific public key file `vultr-adguard.pub` is appended to the server's authorized list, meaning you **must** use the matching private key `vultr-adguard` to authenticate.

To establish a secure terminal session from your local machine, open your command prompt or terminal and execute:

```bash
ssh -i /path/to/keys/vultr-adguard root@YOUR_SERVER_IP_PLACEHOLDER
```

> [!WARNING]
> **Key Permissions:** If you receive a warning stating that permissions are too open, lock down your private key file layout permissions on Mac or Linux before trying again: `chmod 400 vultr-adguard`.

---

## 📺 How It Works for Smart TVs

Unlike desktop computers or smartphones, **Smart TVs (Samsung Tizen, LG webOS, Roku, Apple TV, Firestick)** do not support browser extensions or native ad-blocking applications. 

To bypass this restriction, our AdGuard Home system works at the network level using two methods:
1. **Plain DNS Resolution:** Directly handing the server's raw IP to the television settings.
2. **Encrypted DNS (DoH/DoT):** Routing queries through a secure web domain interface for modern devices that support it.

Whenever your Smart TV requests an advertising or tracking domain, AdGuard interceptively returns a `0.0.0.0` address, safely killing the ad before it even downloads to the screen.

---

## ⚙️ Network Configuration Methods

Choose **one** of the configuration methodologies below to start routing your Smart TV traffic through the ad blocker.

### Method 1: Network-Wide Protection (Highly Recommended)
Instead of configuring every single television manually, you can secure every device in the house simultaneously by modifying your primary router settings.

1. Access your home router admin interface via your web browser (typically `192.168.1.1` or `192.168.0.1`).
2. Navigate to the **LAN / DHCP Server Settings** section.
3. Locate the **DNS Server** fields (Primary/Secondary).
4. Update the fields to point directly to our server infrastructure:
   * **Primary DNS:** `YOUR_SERVER_IP_PLACEHOLDER`
5. Save the configuration and reboot your router. Your Smart TVs will automatically grab the new settings.

---

### Method 2: Manual Smart TV Configuration
If you only want specific smart televisions routed through the ad blocker, update their network layers directly using these platform blueprints:

#### 🇰🇷 Samsung Smart TVs (Tizen OS)
1. Press the **Home** button on your remote control and go to **Settings**.
2. Select **Network** ➡️ **Network Status**.
3. Choose **IP Settings**.
4. Scroll down to **DNS Setting** and toggle it to **Enter Manually**.
5. Select **DNS Server**, input `YOUR_SERVER_IP_PLACEHOLDER`, and press **OK**.

#### 🇰🇷 LG Smart TVs (webOS)
1. Press the **Settings** gear on your remote control and select **All Settings**.
2. Select **Network** and click on your active connection (**Wi-Fi Connection** or **Wired Connection**).
3. Click on **Edit**.
4. Uncheck **Set Automatically**.
5. Click on the **DNS Server** input field, erase the current entry, enter `YOUR_SERVER_IP_PLACEHOLDER`, and click **Connect**.

#### 🪵 Roku TV Streaming Devices
*Note: Roku OS does not allow manual DNS overrides directly inside its device menu.*
1. You **must** utilize **Method 1** (Router-Level Adjustment) to block advertisements on Roku devices.

---

## 📱 Mobile & Smartphone Configuration Info

Configuring your smartphones allows ad-blocking to work **even when you leave the house** on cellular 5G/LTE networks. 

### 🍏 Apple iPhones & iPads (iOS)
Apple devices natively support encrypted DNS, but they require a tiny file called a **Configuration Profile** (`.mobileconfig`) to activate it. You do not need to install any heavy apps or VPNs.

#### The Easy Route: Generate a Profile via Browser
1. On your iPhone, open **Safari** and go to an open-source profile generator tool like [AdGuard's Official Profile Generator](https://adguard-dns.io) or [://notjakob.com](https://://notjakob.com).
2. Choose **DNS-over-HTTPS** as the protocol.
3. Input our exact domain endpoint: `://chsnfam.com`
4. Click **Download**. Safari will pop up a message saying: *"This website is trying to download a configuration profile. Do you want to allow this?"* Tap **Allow**.
5. Open your iPhone **Settings** app. You will immediately see a new option near the top called **Profile Downloaded**. Tap it.
6. Tap **Install** in the top right corner, enter your passcode, and confirm the installation.

#### Switching or Turning It Off:
To verify it is active or to disable it later, navigate on your phone to:
**Settings** ➡️ **General** ➡️ **VPN & Device Management** ➡️ **DNS**. Make sure `://chsnfam.com` is selected.

---

### 🤖 Android Smartphones
Modern Android versions (Android 9+) support native system-wide encrypted DNS via a feature called **Private DNS**.

1. Open your phone's **Settings** app.
2. Navigate to **Network & Internet** ➡️ **Private DNS** (this might be under *More Connection Settings* depending on your phone brand).
3. Switch the setting from *Automatic* to **Private DNS provider hostname**.
4. Type in our exact secure domain hostname:
   ```text
   ://chsnfam.com
   ```
5. Tap **Save**. Your phone is now secured across both Wi-Fi and mobile data networks.

---

## 🔍 Verifying the Connection

To confirm your Smart TV or iPhone is actively running through our secure instance:
1. Open a browser on your smartphone or a streaming hub on your TV.
2. Check your AdGuard Home Web Interface by visiting `https://://chsnfam.com` in your personal browser.
3. Check the **Query Log** tab. You should visually see the telemetry logs and domain requests matching your device's brand getting flagged as **Blocked**.

---

### Method 2: Manual Smart TV Configuration
If you only want specific smart televisions routed through the ad blocker, update their network layers directly using these platform blueprints:

#### 🇰🇷 Samsung Smart TVs (Tizen OS)
1. Press the **Home** button on your remote control and go to **Settings**.
2. Select **Network** ➡️ **Network Status**.
3. Choose **IP Settings**.
4. Scroll down to **DNS Setting** and toggle it to **Enter Manually**.
5. Select **DNS Server**, input `YOUR_SERVER_IP_PLACEHOLDER`, and press **OK**.

#### 🇰🇷 LG Smart TVs (webOS)
1. Press the **Settings** gear on your remote control and select **All Settings**.
2. Select **Network** and click on your active connection (**Wi-Fi Connection** or **Wired Connection**).
3. Click on **Edit**.
4. Uncheck **Set Automatically**.
5. Click on the **DNS Server** input field, erase the current entry, enter `YOUR_SERVER_IP_PLACEHOLDER`, and click **Connect**.

#### 🪵 Roku TV Streaming Devices
*Note: Roku OS does not allow manual DNS overrides directly inside its device menu.*
1. You **must** utilize **Method 1** (Router-Level Adjustment) to block advertisements on Roku devices.

---

## 📱 Mobile & Smartphone Configuration Info

Configuring your smartphones allows ad-blocking to work **even when you leave the house** on cellular 5G/LTE networks. 

### 🍏 Apple iPhones & iPads (iOS)
Apple devices natively support encrypted DNS, but they require a tiny file called a **Configuration Profile** (`.mobileconfig`) to activate it. You do not need to install any heavy apps or VPNs.

#### The Easy Route: Generate a Profile via Browser
1. On your iPhone, open **Safari** and go to an open-source profile generator tool like [AdGuard's Official Profile Generator](https://adguard-dns.io) or [://notjakob.com](https://://notjakob.com).
2. Choose **DNS-over-HTTPS** as the protocol.
3. Input our exact domain endpoint: `://chsnfam.com`
4. Click **Download**. Safari will pop up a message saying: *"This website is trying to download a configuration profile. Do you want to allow this?"* Tap **Allow**.
5. Open your iPhone **Settings** app. You will immediately see a new option near the top called **Profile Downloaded**. Tap it.
6. Tap **Install** in the top right corner, enter your passcode, and confirm the installation.

#### Switching or Turning It Off:
To verify it is active or to disable it later, navigate on your phone to:
**Settings** ➡️ **General** ➡️ **VPN & Device Management** ➡️ **DNS**. Make sure `http://chsnfam.com` is selected.

---

### 🤖 Android Smartphones
Modern Android versions (Android 9+) support native system-wide encrypted DNS via a feature called **Private DNS**.

1. Open your phone's **Settings** app.
2. Navigate to **Network & Internet** ➡️ **Private DNS** (this might be under *More Connection Settings* depending on your phone brand).
3. Switch the setting from *Automatic* to **Private DNS provider hostname**.
4. Type in our exact secure domain hostname:
   ```text
   ://chsnfam.com
   ```
5. Tap **Save**. Your phone is now secured across both Wi-Fi and mobile data networks.

---

## 🔍 Verifying the Connection

To confirm your Smart TV or iPhone is actively running through our secure instance:
1. Open a browser on your smartphone or a streaming hub on your TV.
2. Check your AdGuard Home Web Interface by visiting `https://chsnfam.com` in your personal browser.
3. Check the **Query Log** tab. You should visually see the telemetry logs and domain requests matching your device's brand getting flagged as **Blocked**.
