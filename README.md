&nbsp;

Plug in your OPZ2W.

After a brief startup sequence, your screen should look like this:

<img src="images/vlcsnap-2024-05-04-18h06m09s993.png" />

&nbsp;

First you'll set a password. Type `passwd` at the command prompt, then press enter.

<img src="images/vlcsnap-2024-05-04-18h08m03s537.png" />

&nbsp;

For the current pasword, type `orangepi` and press enter. (You won't see any characters appear onscreen as you type.) Then choose a new password and enter it. Write down your new password or store it in a password manager app.

<img src="images/vlcsnap-2024-05-04-18h08m29s906.png" />

&nbsp;

You're currently logged in as a user called `orangepi`. Next you'll switch to the `root` user and change its password.

Type `su root` and press enter. At the prompt, enter the default password `orangepi`.

<img title="" src="images/vlcsnap-2024-05-04-22h40m23s942.png" alt="" width="543">

Now type `passwd` and press enter to set a new password for your `root` account.

<img title="" src="images/vlcsnap-2024-05-04-22h41m36s044.png" alt="" width="497">

&nbsp;

When you're done, run the command `su orangepi` to switch back to the user `orangepi`.

<img title="" src="images/vlcsnap-2024-05-04-22h42m26s544.png" alt="" width="468">

&nbsp;

The default font size is pretty small, so you may want to increase the size. Run the following command to open the `console-setup` preferences file with the text editor `nano`:

```
sudo nano /etc/default/console-setup
```

<img src="images/vlcsnap-2024-05-04-18h09m12s644.png" />

&nbsp;

Use the arrow keys on your keyboard to move the cursor to the line beginning with `FONTSIZE=`. Delete the value `8x16` and replace it with `16x32`.

<img src="images/vlcsnap-2024-05-04-18h09m36s520.png" />

&nbsp;

When you're finished press `ctrl + X` on your keyboard to close the file. At the bottom left of your screen you'll see the prompt "Save modified buffer?" Type `y` for "yes," then press enter.

<img src="images/vlcsnap-2024-05-04-18h10m21s175.png" />

&nbsp;

Press enter again to confirm the filename.

<img src="images/vlcsnap-2024-05-04-18h10m23s765.png" />

&nbsp;

*Tip: You can use the command `clear` at any time to clear the whole screen.*

<img src="images/vlcsnap-2024-05-04-18h10m40s187.png" />

&nbsp;

Now run the command `sudo update-initramfs -u` to confirm the new font size.

<img src="images/vlcsnap-2024-05-04-18h11m04s235.png" />

&nbsp;

Reboot your computer with `sudo reboot`.

<img src="images/vlcsnap-2024-05-04-18h11m41s482.png" />

&nbsp;

When your computer finishes rebooting, you'll be using a larger font.

## Connect to the internet

If you have a USB-to-Ethernet adapter and you're close to your router, connect your computer to the back of the router. You can skip the rest of this section.

If you're using wi-fi instead, follow the steps below.

Run the command `sudo orangepi-config` to launch the Orange Pi configuration utility. (On a Raspberry Pi, use `sudo raspi-config` instead.)

<img src="images/vlcsnap-2024-05-04-18h12m09s218.png" />

&nbsp;

You'll see a prompt that reads "Configuration cannot work properly without a working internet connection." Press any key to continue.

<img src="images/vlcsnap-2024-05-04-18h12m53s220.png" />

&nbsp;

Use the down arrow key to select the `Network` menu, then press enter.

<img src="images/vlcsnap-2024-05-04-18h13m01s027.png" />

&nbsp;

Use the down arrow key to select the `WiFi` menu, then press enter.

<img src="images/vlcsnap-2024-05-04-18h13m11s710.png" />

&nbsp;

You'll see a list of available wi-fi networks. Select your home network, then press enter. *(Note: Some routers let you create a secondary wi-fi network, intended to keep IoT (Internet of Things) devices like security cameras separate from your primary network. If you're planning to leave your server connected to wi-fi, you may want to use your router's IoT network as a security precaution.)*

<img src="images/vlcsnap-2024-05-04-18h13m15s945.png" />

&nbsp;

Enter your password at the prompt.

<img src="images/vlcsnap-2024-05-04-18h13m28s733.png" />

&nbsp;

Use the arrow keys to select `Quit`, then press enter.

<img src="images/vlcsnap-2024-05-04-18h13m57s055.png" />

&nbsp;

Use the arrow keys to select `Back` , then press enter.

<img src="images/vlcsnap-2024-05-04-18h14m41s289.png" />

&nbsp;

Now select `Exit`, then press enter to close the configuration menu.

<img src="images/vlcsnap-2024-05-04-18h14m47s352.png" />

&nbsp;

## Update your system software

Now that you're connected to the internet, you'll want to update your software packages. This step is important because some packages may need updates for security reasons.

Type the command below (actually two commands separated by `&&`, then press enter. 

```
sudo apt update && sudo apt-y upgrade
```

<img src="images/vlcsnap-2024-05-04-18h15m11s937.png" />

&nbsp;

Enter your password at the prompt and press enter. It may take 10+ minutes for your packages to download and update.

<img src="images/vlcsnap-2024-05-04-18h15m32s775.png" />

&nbsp;

&nbsp;

&nbsp;

## Update your hostname

&nbsp;

Type the command `hostname` and press enter. You'll see the default hostname, `orangepizero2w`.

<img src="images/vlcsnap-2024-05-04-18h18m20s739.png" />

&nbsp;

Now run the command below, replacing "Zine-Gallery" with a descriptive name for your server. You'll be prompted to enter your password.

```
hostnamectl set-hostname Zine-Gallery
```

<img src="images/vlcsnap-2024-05-04-18h18m33s779.png" />

&nbsp;

## Set up a firewall

A firewall is a piece of software that restricts access to your device over the network, allowing certain kinds of network traffic and blocking the rest.

You'll start by installing a firewall program called `ufw` (short for "Uncomplicated Firewall"). Run the command `sudo apt install ufw`, then follow the prompts.

<img src="images/vlcsnap-2024-05-04-18h19m02s699.png" />

&nbsp;

![](images/vlcsnap-2024-05-04-18h26m51s348.png)

&nbsp;

![](images/vlcsnap-2024-05-04-18h26m59s436.png)

&nbsp;

![](images/vlcsnap-2024-05-04-18h27m09s846.png)

&nbsp;

![](images/vlcsnap-2024-05-06-19h10m17s514.png)

&nbsp;

![](images/vlcsnap-2024-05-06-19h10m33s671.png)

## Install Apache

<img src="images/vlcsnap-2024-05-04-18h19m14s181.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h19m39s448.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h19m57s347.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h20m16s818.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h20m42s389.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h21m02s005.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h21m31s495.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h22m07s283.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h22m28s109.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h23m15s189.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h23m30s347.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h23m53s870.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h25m02s853.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h25m41s342.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h25m53s476.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h26m15s464.png" />

&nbsp;

&nbsp;

## UFW Temp

<img src="images/vlcsnap-2024-05-04-18h28m30s592.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h28m38s809.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h28m59s891.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h29m08s844.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h29m22s232.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h33m11s162.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h33m22s250.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h33m31s237.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h34m12s001.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h34m21s618.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h34m31s536.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h34m46s954.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h34m49s645.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h37m08s128.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h38m01s726.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h38m21s670.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h38m40s212.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h38m55s326.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h39m35s435.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h39m52s976.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h40m13s233.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h41m07s243.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h41m56s939.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h42m01s997.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-22h37m36s356.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-22h37m42s430.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-22h45m06s912.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-22h45m39s104.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-22h47m49s427.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-22h49m15s041.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-22h49m30s172.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-22h50m34s877.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-22h51m31s509.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-22h54m10s797.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-22h54m14s305.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-22h54m16s347.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-22h54m19s696.png" />

&nbsp;