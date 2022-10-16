---
title: Set Up Your Own Password Manager and Sync Simultaneously Between Devices
tags: [Privacy]
style: fill
color: light
image: https://ik.imagekit.io/dsg/arytapermana/post/regularguy-eth-q7h8LVeUgFU-unsplash_OUIyvNbZF.jpg?ik-sdk-version=javascript-1.4.3&updatedAt=1665928312563
description: Set up your own password manager using KeePass, Resilio Sync, and a VPS server for more security and reliability.
---

A password manager is very important in the digital era. So many applications, social media, and other important accounts use passwords even other credential information, remembering one by one account and password is very hard, because of that a password manager is needed like 1Password, Bitwarden, LastPass, and many more, but this is the problem about third-party password manager, all data of your password is managed not just by you, but managed by company you trust too.

Every third-party password manager has a different privacy policy and terms of service depending on where country their company operated. When the password manager company operated in a country with no strict regulations relative to privacy consumers, they can take your data even your account information to their government. A password manager you can manage on your own is important here because all data is yours no third party and no government can access your data.

Now we will set up a password manager that's will be managed completely by yours, even can be synchronously on every device, and of course, it's more secure!

First, we will use KeePass as a password manager app to easily and securely save and manage the data on a database with AES-256 encryption (one of the most secure encryption algorithms) and its open source! so many types of KeePass apps developed by the community you can use, but I recommend using KeePassXC on Windows and KeePassDX on android, if you're using a mac or ios you can select the recommended app on the official KeePass website [here](https://keepass.info/download.html).

Next, we will need a server to sync your password anywhere and everywhere, you can use any VPS you trust like Digital Ocean, Amazon AWS, or Vultr, just chose a cheap one, because it's didn't need huge performance to sync. Resilio Sync is a peer-to-peer file synchronization tool we used to sync passwords from KeePass Database because Resilio Sync can sync files by the internet even local network between devices which is connected.

## Step by Steep

### First/Main Device (PC)

1. Download KeePass App to your devices from the [official website](https://keepass.info/download.html), or you can click below. <br />
   [KeePassXC](https://keepassxc.org/)
2. After you download it creates a database and saves the database on a specific folder, later that folder will be used as a sync folder for Resilio Sync.
3. Download Resillio Sync from the [official website](https://www.resilio.com/individuals/), I prefer to install it as a windows service but you can choose to install it as an app.
   {% include elements/figure.html image="https://ik.imagekit.io/dsg/arytapermana/post/Running-Sync-as-a-service-on-Windows_OP6J8KnRQ.png?ik-sdk-version=javascript-1.4.3&updatedAt=1665915807022" caption="Resilio Sync install as windows services" %}
4. After installed, open Resilio Sync, if you installed it as windows services open a web browser and type [http://127.0.0.1:8888/](http://127.0.0.1:8888/) on the URL bar, if you install it as an app just open it from the app menu.
5. Now click the "+" button and select "Standard Folder" to add a sync folder and chose the folder you use to save the KeePass database before. Now your folder is ready to share for sync to another device.
   {% include elements/figure.html image="https://ik.imagekit.io/dsg/arytapermana/post/Screenshot_2022-10-16_182717_OCY5mZsq8.jpg?ik-sdk-version=javascript-1.4.3&updatedAt=1665916052350" caption="Add KeePass database to Resilio Sync" %}
6. Back to the main menu of Resilio Sync, right-click on the folder before you add, and select the share button. Select the "key" tab then copy the read & write key. Save the key to use on another device step.
   {% include elements/figure.html image="https://ik.imagekit.io/dsg/arytapermana/post/Screenshot_2022-10-16_183407_h_qknJzGf.jpg?ik-sdk-version=javascript-1.4.3&updatedAt=1665916463053" caption="Share key" %}

### Second Devices (Android)

1. Download KeePass App to your devices from the [official website](https://keepass.info/download.html), or you can click below. <br />
   [KeePassDX](https://www.keepassdx.com/)
2. Download Resillio Sync from the [Play Store](https://play.google.com/store/apps/details?id=com.resilio.sync).
3. Open Resilio Sync and click the "+" button (bottom-right screen) and chose "Enter a key or link", paste your key copied before there, and then click "Add". Select the directory of the sync folder on your phone after that. Give a few seconds to Resilio Sync to sync your file.
   {% include elements/figure.html image="https://ik.imagekit.io/dsg/arytapermana/post/photo_2022-10-16_18-40-37_kAVnjWAkW.jpg?ik-sdk-version=javascript-1.4.3&updatedAt=1665917168786" caption="Add folder Resilio Sync" %}
4. Now open KeePass on your phone and add an existing database, open the folder of Resilio Sync that has been synced before on the directory you chose before.
5. Type the password and open it. Now your database is ready set and synchronized between PC and mobile. Every time your PC and your phone are online Resilio Sync automatically syncs your password database between devices.

### Third (Server)

The last is to set up a server to easily sync all your KeePass database 24/7 over the internet, of course, it's safe! because Resilio Sync uses AES-128 encryption and KeePass uses AES-256 encryption which needs billions of years to brute force and cracks the encryption.

1. First, we need VPS, I use AWS Lightsail with Ubuntu 20.04 LTS here, you can use another VPS but the settings panel little different but the concept is the same.
2. Before setting the app open port 8888 UDP and TCP on the VPS, this port is used by Resilio Sync to sync the files between and add/set static IP to the VPS to make access easier.
   {% include elements/figure.html image="https://ik.imagekit.io/dsg/arytapermana/post/Screenshot_2022-10-16_184928_dDFsZsauA.jpg?ik-sdk-version=javascript-1.4.3&updatedAt=1665917404451" caption="Open port 8888 TCP and UDP" %}
3. Open the VPS terminal and create a folder
   ```
   sudo mkdir [your-folder-name]
   ```
   add directory permission access
   ```
   sudo chmod -R 700 [your-folder-name]
   ```
4. Next add this Resillio repositories
   ```
   echo "deb http://linux-packages.resilio.com/resilio-sync/deb resilio-sync non-free" | sudo tee /etc/apt/sources.list.d/resilio-sync.list
   ```
5. Add a public key
   ```
   wget -qO - https://linux-packages.resilio.com/resilio-sync/key.asc | sudo apt-key add -
   ```
6. Now update and install Resilio Sync
   ```
   sudo apt-get update
   sudo apt-get install resilio-sync
   ```
7. Enable auto-start to Resillio Sync
   ```
   sudo systemctl enable resilio-sync
   ```
8. Check the status, is Resilio running?
   ```
   systemctl status resilio-sync
   ```
   Sample return code of Resilio is running
   ```
   ● resilio-sync.service - Resilio Sync service
     Loaded: loaded (/lib/systemd/system/resilio-sync.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2022-10-10 02:22:15 UTC; 6 days ago
       Docs: https://help.resilio.com
   Main PID: 43801 (rslsync)
      Tasks: 17 (limit: 560)
     Memory: 62.5M
     CGroup: /system.slice/resilio-sync.service
             └─43801 /usr/bin/rslsync --config /etc/resilio-sync/config.json
   Oct 10 02:22:14 ip-172-26-11-240 systemd[1]: resilio-sync.service: Succeeded.
   Oct 10 02:22:14 ip-172-26-11-240 systemd[1]: Stopped Resilio Sync service.
   Oct 10 02:22:14 ip-172-26-11-240 systemd[1]: Starting Resilio Sync service...
   Oct 10 02:22:15 ip-172-26-11-240 systemd[1]: Started Resilio Sync service.
   ```
9. Next, we will edit the Resillio Sync configuration to the public so that later we can open from the web by IP and set up Resilio Sync to sync the KeePass database. <br />
   Open the configuration file of Resilio Sync
   ```
   sudo nano /etc/resilio-sync/config.json
   ```
   Sample output
   ```
   {
    "storage_path" : "/var/lib/resilio-sync/",
    "pid_file" : "/var/run/resilio-sync/sync.pid",
    "webui" :
    {
        "force_https": true,
        "listen" : "0.0.0.0:8888"
    }
   }
   ```
   Change these line
   ```
   "listen" : "127.0.0.1:8888"
   ```
   to these
   ```
   "listen" : "0.0.0.0:8888"
   ```
   save after that
10. Now restart Resillio Sync
    ```
    sudo systemctl restart resilio-sync
    ```
11. Access Resilio Sync from https://[your-vps-ip]:8888
12. set-up like before, click the "+" button, select "Enter a key or link", and paste the key of Resilio Sync before, set the folder to the folder you create before on VPS, and done all set!

Now all devices are synchronized 24/7!
