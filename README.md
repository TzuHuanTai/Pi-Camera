<p align=center>
    <img src="img/icon.png" width="200" alt="Pi 4b latency demo">
</p>
<h1 align="center">
 Pi Camera
 <br>
</h1>

<p align=center>
<a href="https://play.google.com/store/apps/details?id=com.tzu.huan.tai.picamera"><img src="https://play.google.com/intl/en_us/badges/static/images/badges/en_badge_web_generic.png" width="168"></a>
</p>

Transform your Raspberry Pi into a powerful home security camera with the Pi Camera app. Using peer-to-peer (P2P) communication over WebRTC to make a decentralized monitor system, this app connects directly to your Raspberry Pi, allowing you to monitor live video with minimal delay and access historical footage. [[demo video](https://www.youtube.com/watch?v=JZ5bcSAsXog)]

<img src="./img/index_dark.png" width="30%"> <img src="./img/live_dark.jpg" width="30%"> <img src="./img/records_dark.jpg" width="30%">

## Key Features

👉 **Low-Latency Live Monitoring**: Achieve extremely low-latency video streaming through WebRTC technology, ensuring you don’t miss any important moments.

👉 **Playback of Historical Footage**: Easily view and manage recorded videos to meet your security needs.

👉 **Simple Setup**: Quickly configure your Raspberry Pi camera through a user-friendly interface.

👉 **Privacy Protection**: Direct P2P connection without relying on third-party servers ensures that your data is fully under your control.

👉 **Open-Source Support**: The camera source code is fully open-source, allowing you to customize and extend it as needed.

## Setting Up a New Raspberry Pi

### Step 0: Prerequisites

1. A Raspberry Pi with a camera module attached.
2. A MQTT server. (STUN and TURN servers are optional).

    <img src="./img/pi_zero_wi_shell.jpg" width=30%> <img src="./img/pi_zero_wo_shell.jpg" width=30%><br>

***Important Notice***
- *MQTT Server (necessary): This server exchanges initialized signals (ICE, SDP) to help p2p hole-punching. Please use the same setting on your raspberry pi camera program. You can setup own MQTT server, or choose some free plans including but not limited to [HiveMQ](https://www.hivemq.com), [EXMQ](https://www.emqx.com/en).*
- *STUN Server (optional): If it's empty, the Google STUN server `stun:stun.l.google.com:19302` will be used by default.*
- *TURN Server (optional): This is used for a few mobile networks or specific scenarios. If your NAT setup doesn't allow for p2p hole-punching, the TURN Server will help relay data transfers.*

### Step 1: Set Configurations on the App

1. Go to Setting Page.
2. Click 🌐 icon and paste your servers setting.
Here is an example mqtt setting shown on HiveMQ.
- **Notice!** Please use ***WebSocket Port*** here!

    <img src="./img/mqtt_cloud_sample.jpg" width=50%><br>
    <img src="./img/setting_1.jpg" width="30%"> <img src="./img/setting_2.jpg" width="30%">

### Step 2: Add a New Device in the Setting Page

1. Click ➕ icon
2. The app will generate a `UUID`, which will be used on your Raspberry Pi later.  
    *If you'd like to assign a specific ID to the device, you can edit the `UUID` at the beginning. Once confirmed, the `UUID` cannot be edited; you will need to delete the device and add a new one if changes are needed.*
3. Enter a name in the "Alias", which can be edited at any time in the future.
4. The new device will appear on the list after clicking the confirm button. You can change the order of devices on the selectors and home page by dragging the ☰ icon.

    <img src="./img/add_devices.jpg" width="30%">

### Step 3: Run Camera Software on Raspberry Pi

1. Download the `pi_webrtc` software from the [release page](https://github.com/TzuHuanTai/RaspberryPi_WebRTC/releases).

2. Run the `pi_webrtc` on your Raspberry Pi. Here’s an example where the device `uid` is set to `abcdefg-123-1qaz2wsx` in the app.

    ***Important:*** The MQTT port specified in the command is **NOT the WebSocket port** (8884), but the standard **MQTT protocol port** (8883).

    ```bash
    /path/to/pi_webrtc --device=/dev/video0 --fps=30 --width=1280 --height=960 --v4l2_format=h264 --hw_accel --mqtt_host=example.s1.eu.hivemq.cloud --mqtt_port=8883 --mqtt_username=hakunamatata --mqtt_password=WonderfulPhrase --uid=abcdefg-123-1qaz2wsx --record_path=/mnt/ext_disk/video/
    ```

For detailed setup instructions, please refer to the guide on the [RaspberryPi_WebRTC](https://github.com/TzuHuanTai/RaspberryPi_WebRTC) page.

### Step 4: Verify the Connection

- Please switch to the home page, the app will try to connect to Raspberry Pi.

- If everything is correct, the status light will turn green.

- The preview image is refreshed every 90 seconds, and it can be refreshed immediately by scrolling down the page.

    <img src="./img/connected_sample.jpg" width="30%">


### Step 5: Share to Other Phones

1. Click the share button on the phone that can connect to Raspberry Pi already. It'll show the QR code.
2. Pick up the second phone click the QR code button in the add device section, and scan the QR code will copy the device, including the network setting, to the second phone. **Notice! The network setting will be replaced in the second phone if set before.**

    <img src="./img/share_1.jpg" width="30%">
    <img src="./img/share_2.jpg" width="30%">



## Contact & Support

If you have any questions, need support, or just want to provide feedback, you can reach out via [GitHub Issues](https://github.com/TzuHuanTai/Pi-Camera/issues).
Thank you for using Pi Camera!

---
