# Locally App

Send files and text to devices in your WiFi, Hotspot or other local network using Locally App.

## What's new in version 1.1 (January 2024)

* send text;
* on Android share directly from files or gallery;
* on Desktop drag and drop files to send them.

## Downloads

### Linux

* Arch Linux: <a href="locally-1.1.0-1-x86_64.pkg.tar.zst">v1.1</a>

#### Debian based (*.deb)

* Ubuntu 23.10: <a href="ubuntu_23.10_locally_1.1_amd64.deb">v1.1</a>
* Ubuntu 22.04: <a href="kubuntu_22.04_locally_1.0_amd64.deb">v1.0</a>
* Kubuntu 22.04: <a href="kubuntu_22.04_locally_1.0_amd64.deb">v1.0</a>
* Ubuntu 20.04: <a href="ubuntu_20.04_locally_1.0_amd64.deb">v1.0</a>

#### Red Hat based (*.rpm)

* OpenSUSE Tumbleweed: <a href="locally-1.1-1.x86_64.rpm">v1.0</a>

### Windows 11, 10

* Portable zip: <a href="Locally-Portable-1.1.0-x64.zip">v1.1</a>
* Installer <a href="Locally-Installer-1.1.0-x64.exe">v1.1</a>

### Android

[Link to Google Play](https://play.google.com/store/apps/details?id=com.trand.locally).

### iOS

[Link to App Store](https://apps.apple.com/us/app/send-locally/id6475152818).

## Help

On some operating systems you'll need to manually open the port 37789 in order for the app to be discovered and be able to receive files.

### Known operating systems that need manual port opening

1. OpenSUSE Tumbleweed connected to mobile Hotspot network.

    ```
    sudo firewall-cmd --zone=public --add-port=37789/tcp
    ```

    or manually search for _firewall_ in your application menu and open the port 37789.

The app running on a device with restrictive firewall rules will still be able to send files to other devices and discover other devices in the network.

## Contact

<p><a href="mailto:nicktrandafil@gmail.com">Email Nicolai Trandafil</a></p>
