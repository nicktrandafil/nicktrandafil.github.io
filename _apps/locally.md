---
layout: default
title: "Locally: Device Ecosystem"
excerpt: Locally is a cross-platform, peer-to-peer text and file exchange app focused on making data transfer between devices as seamless as possible.
---

Locally: Device Ecosystem

Locally is a cross-platform, peer-to-peer text and file exchange app focused on making data transfer between devices as seamless as possible.

Features:
* Transfers never leave the local network — no Internet required.
* Instant device discovery on the same network.
* Unfinished transfers are saved and can be resumed later.
* Transfers are as fast as your network allows — up to 40 MB/s on a home network, and 80 MB/s via mobile hotspot.

## Downloads

### Android

[Link to Google Play](https://play.google.com/store/apps/details?id=com.trand.locally).

### iOS, macOS, iPadOS

[Link to App Store](https://apps.apple.com/us/app/send-locally/id6475152818).

### Windows 11, 10

* Portable zip: <a href="/other/Locally-Portable-1.5.12-x64.zip">v1.5.12</a>
* Installer <a href="Locally-Installer-1.5.12-x64.exe">v1.5.12</a>

### Linux

* Arch Linux: <a href="archlinux-locally-1.5.12-1-x86_64.pkg.tar.zst">v1.5.12</a>

#### Debian based (*.deb)

* Ubuntu 24.04: <a href="ubuntu_24.04_locally_1.5.12_amd64.deb">v1.5.12</a>
* Ubuntu 23.10: <a href="ubuntu_24.04_locally_1.5.12_amd64.deb">v1.5.12</a>
* Ubuntu 22.04: <a href="ubuntu_22.04_locally_1.5.12_amd64.deb">v1.5.12</a>
* Kubuntu 22.04: <a href="ubuntu_22.04_locally_1.5.12_amd64.deb">v1.5.12</a>
* Ubuntu 20.04: <a href="ubuntu_20.04_locally_1.5.12_amd64.deb">v1.5.12</a>

#### Red Hat based (*.rpm)

* OpenSUSE Tumbleweed: <a href="opensuse-tumbleweed-locally-1.5.12-1.x86_64.rpm">v1.5.12</a>

## Help

On some operating systems, you may need to manually open port 37789 to enable device discovery and file reception.

### Known operating systems that need manual port opening

1. OpenSUSE Tumbleweed connected to mobile Hotspot network.

    ```
    sudo firewall-cmd --zone=public --add-port=37789/tcp
    sudo firewall-cmd --zone=public --add-port=37789/udp
    ```

    or manually search for _firewall_ in your application menu and open the port 37789.

Even with restrictive firewall rules, the app can still discover other devices and exchange files — as long as the other device allows incoming connections.

## Contact

<p><a href="mailto:nicktrandafil@gmail.com">nicktrandafil@gmail.com</a></p>

## Gallery

<!-- iOS Screenshots Section -->
<h2 style="text-align: center;">iOS</h2>
<div class="screenshot-row">
  <div class="phone-frame">
    <img src="/assets/images/ios_nearby_devices.png" alt="Nearby Devices">
  </div>
  <div class="phone-frame">
    <img src="/assets/images/ios_chat.png" alt="Chat">
  </div>
  <div class="phone-frame">
    <img src="/assets/images/ios_settings.png" alt="Settings">
  </div>
</div>


<!-- Android Screenshots Section -->
<h2 style="text-align: center;">Android</h2>
<div class="screenshot-row">
  <div class="phone-frame">
    <img src="/assets/images/android_nearby_devices.jpg" alt="Android Nearby Devices">
  </div>
  <div class="phone-frame">
    <img src="/assets/images/android_chat.jpg" alt="Android Chat">
  </div>
  <div class="phone-frame">
    <img src="/assets/images/android_networks.jpg" alt="Android Networks">
  </div>
</div>


<!-- macOS Screenshot Section -->
<h2 style="text-align: center;">macOS</h2>
<div class="screenshot-row">
  <div class="phone-frame">
    <img src="/assets/images/macos.png" alt="macOS Screenshot">
  </div>
</div>


<!-- iPad Screenshot Section -->
<h2 style="text-align: center;">iPad</h2>
<div class="screenshot-row">
  <div class="phone-frame">
    <img src="/assets/images/ipad.png" alt="iPad Screenshot">
  </div>
</div>

<!-- Linux Screenshot Section -->
<h2 style="text-align: center;">Linux</h2>
<div class="screenshot-row">
  <div class="phone-frame">
    <img src="/assets/images/linux.png" alt="Linux Screenshot">
  </div>
</div>

