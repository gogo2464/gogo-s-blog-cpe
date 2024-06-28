---
title: "Minecraft on Tor"
date: 2024-06-17T12:37:42+02:00
draft: false
---

# Philosophy

This is a project about to put a minecraft private server on TOR. 

The Minecraft target has the advantages to:
- Provide a private server that does not require to maintain code to work: Private servers only work once you have the private server code ready.
- Allow juridically to deploy a private server: Minecraft provide server binaries. It is then absolutely legal to publish such server.
- Still proprietary target to force the user to dissect the minecraft source code for future purpose: In the future we could write a private server based on p2p instead of TOR.
- Tor can be relatively fast for a darknet. Could still be better for card game or less memory intensive games.

# I / Deploy On A debian 12 Minecraft Server

We are going to run a Minecraft server right now. First, enable TOR server:

```bash
sudo apt install --yes tor &&
sudo apt install --yes nginx &&
wget https://download.oracle.com/java/22/latest/jdk-22_linux-x64_bin.deb -O jdk-22_linux-x64_bin.deb -O jdk.deb &&
wget https://javadl.oracle.com/webapps/download/AutoDL?BundleId=249840_43d62d619be4e416215729597d70b8ac -O jre &&
tar -zxvf jre &&
sudo mv -n jre1.8.0_411/ /usr/java/ &&
sudo apt install --yes ./jdk.deb &&

echo "# nginx
HiddenServiceDir /var/lib/tor/my_website/
HiddenServicePort 80 127.0.0.1:80

# minecraft
HiddenServiceDir /var/lib/tor/my_minecraft/
HiddenServicePort 4444 localhost:4444" > /etc/tor/torrc &&
sudo systemctl restart tor &&

mkdir minecraft-dark-server && cd minecraft-dark-server &&
wget https://piston-data.mojang.com/v1/objects/450698d1863ab5180c25d7c804ef0fe6369dd1ba/server.jar &&
sudo echo "eula=true" > eula.txt &&
sudo cat /var/lib/tor/my_minecraft/hostname &&
java -Xmx1024M -Xms1024M -jar server.jar nogui --port 4444
```

Then check out your domain:

```
sudo cat /var/lib/tor/my_minecraft/hostname
```

# II / Connect From a Whonix Workstation Client

Running `torify minecraft-launcher` is not enough to translate all traffic over tor to reach the server. Then we need to use Whonix. Checkout [the official tutorial](https://www.whonix.org/wiki/Download) and to enable packages installation by `sudo apt full-upgrade` from [kicksecure documentation](https://www.kicksecure.com/wiki/Install_Software#Install_from_Debian_stable). 

We are going to run a video game in a VM. The operation is memory intensive. We have to increase and optimize memory. The VM for the Whonix Workstation should have:
- hyper-v hypervisor
- 3D acceleration enabled
- The maximum of video memory enabled
- VT-X / AMD-X enabled

Check out the output of `sudo cat /var/lib/tor/my_minecraft/hostname` from the Debian server. You should see something similar to: `rde2ynhyv3vyov7rxgp5ko2brwib2jilae5cpviiwp3tyar6mqwq2yid.onion`.

You will require this information latter in order to connect to the server.

```bash
sudo apt install --yes wget && 

wget https://launcher.mojang.com/download/Minecraft.deb &&
sudo apt install --yes ./Minecraft.deb &&
sudo rm -f Minecraft.deb &&
taskset -a "$(minecraft-launcher)"
```

Then connect to the server with the address `rde2ynhyv3vyov7rxgp5ko2brwib2jilae5cpviiwp3tyar6mqwq2yid.onion:4444`.

![image](/gogo-s-blog-cpe/putting-game-private-server-on-the-darknet/minecraft-on-tor/connect.png)

You are now connected!

![image](/gogo-s-blog-cpe/putting-game-private-server-on-the-darknet/minecraft-on-tor/result.png)

Congratulation! You are now able to play minecraft on Tor darknet.