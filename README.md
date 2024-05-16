# How-to-Enable-HotSpot-In-kali-Linux
How to Enable HotSpot In kali Linux

Creating a hotspot in Kali Linux can be done using various methods, but one of the simplest ways is by using the `hostapd` and `dnsmasq` utilities along with the built-in network manager `NetworkManager`. Here's a step-by-step guide to create a hotspot in Kali Linux:

### Step 1: Install Required Packages
Make sure you have `hostapd` and `dnsmasq` installed. You can install them using the following commands:
```bash
sudo apt update
sudo apt install hostapd dnsmasq
```

### Step 2: Configure `hostapd`
Create a configuration file for `hostapd`. You can name it anything, like `hostapd.conf`.
```bash
sudo nano /etc/hostapd/hostapd.conf
```
Add the following configuration to the file:
```plaintext
interface=wlan0
driver=nl80211
ssid=YourHotspotName
hw_mode=g
channel=7
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=3
wpa_passphrase=YourPassword
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
```
Replace `YourHotspotName` and `YourPassword` with your desired hotspot name and password.

### Step 3: Configure `dnsmasq`
Create a configuration file for `dnsmasq`.
```bash
sudo mv /etc/dnsmasq.conf /etc/dnsmasq.conf.orig
sudo nano /etc/dnsmasq.conf
```
Add the following configuration to the file:
```plaintext
interface=wlan0
dhcp-range=192.168.1.2,192.168.1.20,255.255.255.0,24h
```

### Step 4: Restart Services
Restart `hostapd` and `dnsmasq` services.
```bash
sudo systemctl start hostapd
sudo systemctl start dnsmasq
sudo systemctl enable hostapd
sudo systemctl enable dnsmasq
```

### Step 5: Configure `NetworkManager`
Now, configure `NetworkManager` to share your internet connection with the hotspot.
```bash
nmcli device wifi hotspot con-name MyHotspot ssid MyHotspot band bg password MyPassword
```
Replace `MyHotspot` and `MyPassword` with your desired hotspot name and password.

### Step 6: Start Hotspot
Activate the hotspot:
```bash
nmcli connection up MyHotspot
```

That's it! You've created a hotspot in Kali Linux. Other devices should be able to connect to your hotspot using the SSID and password you provided. Remember to adjust the configurations according to your specific network setup and requirements.


If the `hostapd` service is masked, it means that it has been intentionally prevented from starting. Masking a service in systemd prevents it from being started, either manually or automatically.

To unmask the `hostapd` service and start it, you can follow these steps:

### Step 1: Unmask the `hostapd` Service
```bash
sudo systemctl unmask hostapd
```

### Step 2: Start the `hostapd` Service
```bash
sudo systemctl start hostapd
```

### Step 3: Enable `hostapd` Service (Optional)
If you want `hostapd` to start automatically on boot, you can enable it:
```bash
sudo systemctl enable hostapd
```

After performing these steps, the `hostapd` service should be unmasked and started successfully. If there are any errors or issues, please feel free to ask for further assistance!
