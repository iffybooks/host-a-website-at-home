## 

![Host a Website at Home Flyer IG.png](/Users/iffybooks/Documents/GitHub/host-a-website-at-home/images/Host%20a%20Website%20at%20Home%20Flyer%20IG.png)

## 

## Why host a website at home?

- You control what you post.

- You can definitively take down your website by unplugging it. 

- Commercial hosting starts around $5 per month, so hosting at home is cheaper in the long run.

- Learning about networking is fun and useful.

In this project you'll learn to set up an Ubuntu-based web server on a single-board computer, using Apache HTTP Server to serve your website. You'll configure Apache the proper way, letting you host multiple websites on the same machine if you wish. Then you'll set up port forwarding on your router to expose your site to the open web. Finally, you'll configure Dynamic DNS (DDNS) with a domain or subdomain, so your website will be accessible even when your ISP changes your home IP address.

The examples in this zine use the Orange Pi Zero 2W, an inexpensive single-board computer that uses very little power. You can buy an OPZ2W with 1 GB of RAM for around $20, but you'll need some additional hardware to get up and running.

We sell complete home web server kits at Iffy Books. The kit costs $49 and includes the following:

• Orange Pi Zero 2W single-board computer w/1 GB of RAM
• 32 GB microSD card
• microSD card reader
• 2 A USB power supply
• USB-C power cable
• Mini HDMI to HDMI adapter
• USB-C to 2x USB-A adapter
• USB-A to Ethernet adapter
• Ethernet cable

## Choose a domain

### Option 1: Choose a subdomain for a domain you already own.

❏ If you already have a domain and you'd like to create a subdomain for this project, choose a subdomain you aren't already using. We'll update your  domain records later. 

For the examples below we'll use the subdomain **zinegallery.iffybooks.net**.

### Option 2: Buy a domain

❏ Go to a domain registry of your choice and pay to register a domain name. You'll need to create an account and enter your credit card info.

<img src="images/2024-05-11-11-20-50-image.png" title="" alt="" width="496">

### Option 3: Sign up for a free subdomain from a DDNS provider

❏ Go to `dynv6.com` and create a subdomain such as `zinegallery.dynv6.net`. You'll need to enter an email address and create an account.

<img src="images/2024-05-09-10-58-18-image.png" title="" alt="" width="553">

## Flash Ubuntu to your SD card

❏ Next you'll download the Ubuntu OS image for your device. If you're using an Orange Pi Zero 2W, go to the following URL:

http://www.orangepi.org/html/hardWare/computerAndMicrocontrollers/service-and-support/Orange-Pi-Zero-2W.html

❏ Under **Ubuntu Image**, click **Downloads**.



![2024-05-10-17-01-17-image.png](images/33922add635879039cc946803b75c94b9b6c8b04.png)

❏ That link will direct you to Google Drive. Double click **Linux6.1 kernel version image** to open the directory.

![2024-05-10-17-03-25-image.png](images/1e8fffc51365305415c5f0c6044c689c8931e1d6.png)





❏ Double click on the directory **For development boards with 1GB_2GB memory...** to open it.

![2024-05-10-17-03-47-image.png](images/3557a94d9b740e75a61b0048836fda09de70e7ef.png)



❏ Right click the file with **server** in the filename and select **Download** to download the disk image file.

![2024-05-10-17-05-03-image.png](images/e33602777310d07fbf1293e870bca1fc08ba559b.png)

❏ Find the file you just downloaded, `Orangepizero2w_1.0.0_ubuntu_jammy_server_linux6.1.31.7z`, in your File Explorer/Finder. Double click the file to extract its contents.

❏ You'll end up with a directory containing a disk image file ending with `.img`, along with a `.sha` checksum file.

![2024-05-10-17-17-56-image.png](images/0641d8ae0e06f780827ca332fbb71ded7a302a53.png)

❏ Now go to the following URL and download the program balenaEthcher:

[https://etcher.balena.io](https://etcher.balena.io)

❏ Insert your micro SD card into a USB card reader and plug it into your computer.

❏ Open balenaEtcher, click **Flash from file**, and select the `.img` disk image file you just extracted.

![2024-05-10-17-19-44-image.png](images/50a411dc182f8774c2138d5b882e09fab01f340a.png)

❏ In balenaEtcher, click **Select target** and select your SD card.

❏ Click **Flash!** to write the Ubuntu disk image to your SD card, which will take 5 minutes or so.

## Set up your computer

❏ Insert your newly flashed micro SD card into the card slot on your single-board computer.

❏ Connect a monitor to your single-board computer. The OPZ2W has a Mini HDMI port, so you'll need an adapter to connect an HDMI cable.

❏ Connect a USB keyboard to your computer. With an OPZ2W you'll need to use a USB-C to USB-A adapter.

## Turn on your computer

❏ Plug a USB-C cable into your computer and connect it to a USB power supply (2 amps or more).

❏ After a brief startup sequence, your screen should look like this:

<img src="images/vlcsnap-2024-05-04-18h06m09s993.png" />

*(Note: From this point forward we'll invert the colors in screen captures in order to use less printer toner.)*

First you'll set a password. Type `passwd` at the command prompt, then press enter.

<img src="images/vlcsnap-2024-05-04-18h08m03s537_border.png" />

&nbsp;

For the current pasword, type `orangepi` and press enter. (You won't see any characters appear onscreen as you type.) Then choose a new password and enter it. Write down your new password or store it in a password manager app.

<img src="images/vlcsnap-2024-05-04-18h08m29s906_border.png" />

You're currently logged in as a user called `orangepi`. Next you'll switch to the `root` user and change its password.

Type `su root` and press enter. At the prompt, enter the default password `orangepi`.

<img title="" src="images/vlcsnap-2024-05-04-22h40m23s942_border.png" alt="" width="543">

Now type `passwd` and press enter to set a new password for your `root` account.

<img title="" src="images/vlcsnap-2024-05-04-22h41m36s044_border.png" alt="" width="497">

&nbsp;

When you're done, run the command `su orangepi` to switch back to the user `orangepi`.

<img title="" src="images/vlcsnap-2024-05-04-22h42m26s544_border.png" alt="" width="468">

&nbsp;

The default font size is pretty small, so you may want to increase the size. Run the following command to open the `console-setup` preferences file with the text editor `nano`:

```
sudo nano /etc/default/console-setup
```

<img src="images/vlcsnap-2024-05-04-18h09m12s644_border.png" />

&nbsp;

Use the arrow keys on your keyboard to move the cursor to the line beginning with `FONTSIZE=`. Delete the value `8x16` and replace it with `16x32`.

<img src="images/vlcsnap-2024-05-04-18h09m36s520_border.png" />

&nbsp;

When you're finished press `ctrl + X` on your keyboard to close the file. At the bottom left of your screen you'll see the prompt "Save modified buffer?" Type `y` for "yes," then press enter.

<img src="images/vlcsnap-2024-05-04-18h10m21s175_border.png" />

&nbsp;

Press enter again to confirm the filename.

<img src="images/vlcsnap-2024-05-04-18h10m23s765_border.png" />

&nbsp;

*Tip: You can use the command `clear` at any time to clear the whole screen.*

<img src="images/vlcsnap-2024-05-04-18h10m40s187_border.png" />

&nbsp;

Now run the command `sudo update-initramfs -u` to confirm the new font size.

<img src="images/vlcsnap-2024-05-04-18h11m04s235_border.png" />

&nbsp;

Reboot your computer with `sudo reboot`.

<img src="images/vlcsnap-2024-05-04-18h11m41s482_border.png" />

&nbsp;

When your computer finishes rebooting, you'll be using a larger font.

## Connect to the internet

If you have a USB-to-Ethernet adapter and you're close to your router, connect your computer to the back of the router. You can skip the rest of this section.

If you're using wi-fi instead, follow the steps below.

Run the command `sudo orangepi-config` to launch the Orange Pi configuration utility. (On a Raspberry Pi, use `sudo raspi-config` instead.)

<img src="images/vlcsnap-2024-05-04-18h12m09s218_border.png" />

&nbsp;

You'll see a prompt that reads "Configuration cannot work properly without a working internet connection." Press any key to continue.

<img src="images/vlcsnap-2024-05-04-18h12m53s220_border.png" />

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

<img src="images/vlcsnap-2024-05-04-18h15m11s937_border.png" />

&nbsp;

Enter your password at the prompt and press enter. It may take 10+ minutes for your packages to download and update.

<img src="images/vlcsnap-2024-05-04-18h15m32s775_border.png" />

&nbsp;

&nbsp;

&nbsp;

## Update your hostname

&nbsp;

Type the command `hostname` and press enter. You'll see the default hostname, `orangepizero2w`.

<img src="images/vlcsnap-2024-05-04-18h18m20s739_border.png" />

&nbsp;

Now run the command below, replacing "Zine-Gallery" with a descriptive name for your server. You'll be prompted to enter your password.

```
hostnamectl set-hostname Zine-Gallery
```

<img src="images/vlcsnap-2024-05-04-18h18m33s779_border.png" />

&nbsp;

## Set up a firewall

A firewall is a piece of software that restricts access to your device over the network, allowing certain kinds of network traffic and blocking the rest.

You'll start by installing a firewall program called `ufw` (short for "Uncomplicated Firewall"). Run the command `sudo apt install ufw`, then follow the prompts.

<img src="images/vlcsnap-2024-05-04-18h19m02s699_border.png" />

&nbsp;

Run the command below to deny incoming network connections by default.

```
sudo ufw default deny incoming
```

![](images/vlcsnap-2024-05-04-18h26m51s348_border.png)

&nbsp;

Run this command to allow outgoing network connections.

```
sudo ufw default allow outgoing
```

![](images/vlcsnap-2024-05-04-18h26m59s436_border.png)

&nbsp;

Run the command below to allow incoming TCP connections on port 80:

```
sudo ufw allow 80/tcp
```

![](images/vlcsnap-2024-05-04-18h27m09s846_border.png)

&nbsp;

Now run the command `sudo ufw enable` to turn on your firewall.

![](images/vlcsnap-2024-05-06-19h10m33s671_border.png)

## Install Apache

Next you'll install Apache HTTP Server, one of the most widely used web server programs. *(Note: The term "web server" can refer to a piece of software that serves websites, like Apache. "Web server" can also refer to the computer the software is running on.)*

Run the command below to install Apache. You'll be prompted to enter your password.

```
sudo apt install apache2
```

<img src="images/vlcsnap-2024-05-04-18h19m14s181_border.png" />

&nbsp;

Next you'll make a directory to store your website files in. The `mkdir` command makes a directory, and the `-p` option creates any parent directories in the path if they don't already exist.

Type the command below to create the directory you'll use for your website files, replacing `zinegallery.iffybooks.net` with the domain you chose earlier.

```
sudo mkdir -p /var/www/zinegallery.iffybooks.net
```

<img src="images/vlcsnap-2024-05-04-18h19m39s448_border.png" />

&nbsp;

Now you'll use `chown` to set the current user (`orangepi`) as the owner of the directory you just created. (Replace `zinegallery.iffybooks.net` below with the name of the dictory you just created.)

```
sudo chown -R $USER:$USER /var/www/zinegallery.iffybooks.net
```

<img src="images/vlcsnap-2024-05-04-18h19m57s347_border.png" />

&nbsp;

Next you'll use `chmod` to set read-write-execute permissions for the directory `/var/www/`. The `755` option means only the owner (`orangepi`) can write to the directory, while all users will have read and execute permissions.

```
sudo chmod -R 755 /var/www/
```

<img src="images/vlcsnap-2024-05-04-18h20m16s818_border.png" />

&nbsp;

Use `cd` to change your current working directory to the directory you just created. *(Tip: After typing `/var/www/` and the first letter or two of your directory name, press **tab** to autocomplete the rest of the pathname.)*

```
cd /var/www/zinegallery.iffybooks.net/
```

<img src="images/vlcsnap-2024-05-04-18h20m42s389_border.png" />

&nbsp;

Next you'll use the text editor `nano` to create a file called `index.html`. This will be the first page people will see when they visit your website.

```
sudo nano index.html
```

<img src="images/vlcsnap-2024-05-04-18h21m02s005_border.png" />

&nbsp;

Now you'll type out some HTML code for a basic web page, just to use as a test. You can adapt the code below, or do a web search for example web pages.

```
<!DOCTYPE html>
<html>
    <head>
        <title>Zine Gallery</title>
    </head>
    <body>
        <h1>Welcome to the Zine Gallery!</h1>
        <p>(still under construction!)</p>
    </body>
</html>
```

<img src="images/vlcsnap-2024-05-04-18h21m31s495_border.png" />

&nbsp;

When you're ready to save your file, press **ctrl+X** to exit. Follow the prompts at the bottom of the screen to save the file.

## Create Apache configuration file

Run the command below to change your current working directory to `/etc/apache2/sites-available`.

```
cd /etc/apache2/sites-available/
```

<img src="images/vlcsnap-2024-05-04-18h22m07s283_border.png" />

&nbsp;

Type `ls` and press **enter** to see what files are in the current directory.

<img src="images/vlcsnap-2024-05-04-18h22m28s109_border.png" />

&nbsp;

Use `cp` to make a copy of the file `000-default.conf`. In the example below, the new file will be called `zinegallery.iffybooks.net.conf`; yours should be the domain you chose earlier followed by `.conf`.

```
sudo cp 000-default.conf zinegallery.iffybooks.net.conf
```

<img src="images/vlcsnap-2024-05-04-18h23m15s189_border.png" />

&nbsp;

Now you'll use `nano` to open the configuration file you just created.

```
sudo nano zinegallery.iffybooks.net.conf
```

<img src="images/vlcsnap-2024-05-04-18h23m30s347_border.png" />

&nbsp;

Use your arrow keys to move the cursor to the line `DocumentRoot /var/www/html`. Delete `html` at the end and replace it with the name of the directory where your website files are located (i.e., the domain you chose). Here's an example:

```
DocumentRoot /var/www/zinegallery.iffybooks.net
```

<img src="images/vlcsnap-2024-05-04-18h23m53s870_border.png" />

&nbsp;

Create two new lines above the one you just edited, and type out the following options. (If you decide to host more than one website on your server, you'll update these lines later.) When you're done, press **ctrl + X** and follow the prompts to save the file.

```
ServerName localhost
ServerAlias localhost
```

<img src="images/vlcsnap-2024-05-04-18h25m02s853_border.png" />

&nbsp;

## Enable your website

Run the following command to have Apache enable your website:

```
sudo a2ensite zinegallery.iffybooks.net.conf
```

<img src="images/vlcsnap-2024-05-04-18h25m41s342_border.png" />

&nbsp;

Next, run this command to disable the site Apache runs by default:

```
sudo a2dissite 000-default.conf
```

<img src="images/vlcsnap-2024-05-04-18h25m53s476_border.png" />

&nbsp;

Restart Apache with the following command:

```
systemctl reload apache2
```

<img src="images/vlcsnap-2024-05-04-18h26m15s464_border.png" />

&nbsp;

## Set up ports.conf

Run the command `cd /etc/apache2/` to change your curent working directory to `/etc/apache2/`. Then use `ls` to view the directory's contents.

<img src="images/vlcsnap-2024-05-04-18h28m38s809_border.png" />

&nbsp;

Use the following command to open the configuration file `ports.conf` with the text editor `nano`.

```
sudo nano ports.conf
```

<img src="images/vlcsnap-2024-05-04-18h28m59s891_border.png" />

&nbsp;

Find the line beginning with "Listen" and update it to match the line below. This change will expose your Apache website to other devices on your network.

```
Listen 0.0.0.0:80
```

<img src="images/vlcsnap-2024-05-04-18h29m08s844_border.png" />

&nbsp;

## Find your IP address

Run the command `ip addr` to find your IP address on the local network. Look for a line beginning with `inet 192.168.`, which will be under `eth0` if you're using ethernet or `wlan0` if you're using wi-fi. In the example below, the server's local IP address is `192.168.1.44`.

![](images/vlcsnap-2024-05-04-18h29m22s232_border.png)

## Test your site on the local network

On a computer connected to the same network as your server, open a web browser, type the server's IP address in the address bar, and press enter. You should see your test website!

![Screenshot 2024-05-04 at 15.33.35.png](/Users/iffybooks/Desktop/Screenshot%202024-05-04%20at%2015.33.35.png)

## Set a static IP address

Ordinarily, when you connect a computer to a network it's assigned a local IP address by a DHCP server program running on the router. Every time you connect to the network your machine will be given an arbitrary address that isn't already taken, typically beginning with `192.168`.

Alternatively, you can give your computer a static IP address that never changes. In this case, a static IP address is required to set up port forwarding, which we'll cover in a future step.

Run the command `sudo orangepi-config` to launch the Orange Pi configuration utility. (On a Raspberry Pi, use `raspi-config` instead.)

<img src="images/vlcsnap-2024-05-04-18h33m11s162_border.png" />

&nbsp;

Select the `Network` menu and press enter.

<img title="" src="images/vlcsnap-2024-05-04-18h33m22s250.png" alt="">

&nbsp;

Select `IP` and press enter.

<img title="" src="images/vlcsnap-2024-05-04-18h33m31s237.png" alt="">

&nbsp;

Select the `eth0` option if your computer is connected via Ethernet, or select the option beginning with `en` if you're using wi-fi. (We recommend using Ethernet if possible, but we're using wi-fi in the example below.)

<img title="" src="images/vlcsnap-2024-05-04-18h34m12s001.png" alt="">

&nbsp;

Select the `Static` option and press enter.

<img title="" src="images/vlcsnap-2024-05-04-18h34m21s618.png" alt="">

&nbsp;

Next to `Address`, enter the local IP address you'd like to use. It should begin with `192.168.1.` and end with a number from 2 to 255. You may want to leave this option as-is, because you know your DHCP-assigned IP address isn't being used by another device. Select `OK` and press enter to save your configuration.

<img title="" src="images/vlcsnap-2024-05-04-18h34m31s536.png" alt="">

&nbsp;

Select `Back` and press enter.

<img title="" src="images/vlcsnap-2024-05-04-18h34m46s954.png" alt="">

&nbsp;

Select `Exit` and press enter to close the configuration utility.

<img title="" src="images/vlcsnap-2024-05-04-18h34m49s645.png" alt="">

&nbsp;

## Enable local SSH access

&nbsp;

Run the command `so orangepi-config` to open the Orange Pi configuration utility.

<img src="images/vlcsnap-2024-05-04-18h38m01s726_border.png" />

&nbsp;

Select `System` and press enter.

<img title="" src="images/vlcsnap-2024-05-04-18h38m21s670.png" alt="">

&nbsp;

Select `SSH` and press enter.

<img title="" src="images/vlcsnap-2024-05-04-18h38m40s212.png" alt="">

&nbsp;

The first three options (`PermitRootLogin`, `Password Authentication`, and `PubkeyAuthentication`) should be selected by default. Move your cursor to `Save` and press enter to enable SSH access.

<img title="" src="images/vlcsnap-2024-05-04-18h38m55s326.png" alt="">

&nbsp;

Select `Back` and press enter.

<img title="" src="images/vlcsnap-2024-05-04-18h39m35s435.png" alt="">

&nbsp;

Select `Exit` and press enter to close the configuration utility.

<img title="" src="images/vlcsnap-2024-05-04-18h39m52s976.png" alt="">

&nbsp;

SSH is now enabled, but your firewall is configured to deny incoming connections.

Run the following command to allow TCP connections on port 22:

```
sudo ufw allow 22/tcp
```

<img src="images/vlcsnap-2024-05-04-18h41m07s243_border.png" />

&nbsp;

Run the command `sudo ufw status` to see a list of your firewall rules.

<img src="images/vlcsnap-2024-05-04-18h41m56s939_border.png" />

&nbsp;

Run the command `reboot` to reboot your computer.

## ![](images/vlcsnap-2024-05-04-18h40m13s233_border.png)

## Test your SSH connection

![Screenshot 2024-05-04 at 15.39.44.png](/Users/iffybooks/Documents/GitHub/host-a-website-at-home/images/Screenshot%202024-05-04%20at%2015.39.44.png)

![Screenshot 2024-05-04 at 15.39.49.png](/Users/iffybooks/Documents/GitHub/host-a-website-at-home/images/Screenshot%202024-05-04%20at%2015.39.49.png)

![Screenshot 2024-05-04 at 15.40.00.png](/Users/iffybooks/Documents/GitHub/host-a-website-at-home/images/Screenshot%202024-05-04%20at%2015.40.00.png)

## Update your website from another computer using scp

![Screenshot 2024-05-04 at 15.55.57.png](/Users/iffybooks/Desktop/Screenshot%202024-05-04%20at%2015.55.57.png)

![Screenshot 2024-05-04 at 15.43.08.png](/Users/iffybooks/Documents/GitHub/host-a-website-at-home/images/Screenshot%202024-05-04%20at%2015.43.08.png)

![Screenshot 2024-05-04 at 15.56.17.png](/Users/iffybooks/Desktop/Screenshot%202024-05-04%20at%2015.56.17.png)

![Screenshot 2024-05-04 at 15.57.08.png](/Users/iffybooks/Documents/GitHub/host-a-website-at-home/images/Screenshot%202024-05-04%20at%2015.57.08.png)

## Set up port forwarding on your router

Open a web browser on a desktop computer and enter the IP address for your router's admin panel. There's a good chance the IP address is `192.168.1.1`. Press enter, then log in with your admin password.

If your ISP is Verizon, you'll need to click **Advanced** at the top of the window to switch to the advanced admin panel.

![](/Users/iffybooks/Library/Application%20Support/marktext/images/2024-05-11-09-42-15-image.png)

Navigate to **Security & Firewall**, then **Port Forwarding**.

![](/Users/iffybooks/Library/Application%20Support/marktext/images/2024-05-11-10-19-16-image.png)

Under **Application**, give your server a name. The example is called `Zine Gallery Server`. For **Original Port** and **Forward to Port**, enter `80`. **Protocol** should be set to `TCP`. Under **Fwd to Addr**, type your server's static IP address. When you're done, click **Add to list** to create your port forwarding rule.

![](/Users/iffybooks/Library/Application%20Support/marktext/images/2024-05-11-10-21-21-image.png)

To confirm port forwarding works, go to `ipchicken.com` and find your home IP address.

![](/Users/iffybooks/Library/Application%20Support/marktext/images/2024-05-11-10-31-00-image.png)![](/Users/iffybooks/Library/Application%20Support/marktext/images/2024-05-11-10-31-00-image.png)![](/Users/iffybooks/Library/Application%20Support/marktext/images/2024-05-11-10-31-00-image.png)

Copy and paste your home IP address into your URL bar and press enter, and you should see your website.

## Set up DDNS for your own domain or subdomain

*Note: If you created a subdomain through dynv6 at the beginning of the project, you can skip this step.*

Go to **dynv6.com** and create an account. Then go to **My Domains** and click **Add Domain**.

![](/Users/iffybooks/Library/Application%20Support/marktext/images/2024-05-11-10-43-30-image.png)

Type your domain or subdomain in the box and click **Add domain**.

![](/Users/iffybooks/Library/Application%20Support/marktext/images/2024-05-11-10-42-39-image.png)

Next you'll update your domain settings to use the following three name servers for your domain or subdomain:

- `ns1.dynv6.com.`
- `ns2.dynv6.com.`
- `ns3.dynv6.com.`

If you're using a domain you just registered, you can update your domain records on the site where you registered it.

If you're using a subdomain with a domain you're already using, you can update your domain records through your VPS provider or hosting service. On DigitalOcean, for example, you can find domain settings under **Manage > Networking > Domains**.

Create a new **NS** (name server) record for the domain or subdomain you're using, and enter `ns1.dynv6.com` as the same server. Click **Create Record**.

![](/Users/iffybooks/Library/Application%20Support/marktext/images/2024-05-11-10-46-59-image.png)

Repeat the previous step two more times, creating **NS** records that point to `ns2.dynv6.com` and `ns3.dynv6.com`.

## Install ddclient

Go to `dynv6.com` on your desktop computer. Click **My Zones** and select your domain/subdomain from the dropdown menu.

![](/Users/iffybooks/Library/Application%20Support/marktext/images/2024-05-11-10-57-24-image.png)

Click on **Instructions**, then scroll down to the section titled **ddclient**. Keep this browser window open so you can access the password in a few steps.

![](/Users/iffybooks/Library/Application%20Support/marktext/images/2024-05-11-11-00-07-image.png)

On your single-board computer, run the command below to install `ddclient`. Type `y` at the propmpt and press enter to confirm.

```
sudo apt install ddclient
```

<img src="images/vlcsnap-2024-05-04-22h45m06s912_border.png" />

&nbsp;&nbsp;

Once `ddclient` is installed, a setup wizard will launch. Select **other** from the list of service providers and type `dynv6.com`. 

<img src="images/vlcsnap-2024-05-04-22h49m15s041.png" />

&nbsp;

Leave the **Username** field blank. Select `Ok`.

<img src="images/vlcsnap-2024-05-04-22h49m30s172.png" />

&nbsp;

Enter the password from the `dynv6.com` website. You'll be prompted to enter it again to confirm.

<img src="images/vlcsnap-2024-05-04-22h50m34s877.png" />

&nbsp;

Select **Web-based IP discovery service**, then **Ok**.

<img src="images/vlcsnap-2024-05-04-22h51m31s509.png" />

&nbsp;

Select any option from the list of IP discovery services, then **Ok**.

<img src="images/vlcsnap-2024-05-04-22h54m10s797.png" />

&nbsp;

Set how frequently your server should check its IP address. The default is 5 minutes.

<img src="images/vlcsnap-2024-05-04-22h54m14s305.png" />

&nbsp;

You can choose select your domain name from a list or enter it manually. Select **Ok**.

<img src="images/vlcsnap-2024-05-04-22h54m16s347.png" />

<img src="images/vlcsnap-2024-05-04-22h54m19s696.png" />

&nbsp;

Now go to a browser on your desktop computer and enter your domain or subdomain in the URL bar. You should see your website! If not, wait a few minutes for DNS settings to update and try again.