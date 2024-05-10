&nbsp;

## Choose a domain

zinegallery.iffybooks.net

![](/Users/iffybooks/Library/Application%20Support/marktext/images/2024-05-09-10-58-18-image.png)

## Turn on your computer

Plug in your OPZ2W.

After a brief startup sequence, your screen should look like this:

<img src="images/vlcsnap-2024-05-04-18h06m09s993.png" />

&nbsp;

*(Note: From this point forward we'll invert the colors in screen captures in order to use less printer toner in printed copies of this guide.)*

First you'll set a password. Type `passwd` at the command prompt, then press enter.

<img src="images/vlcsnap-2024-05-04-18h08m03s537_border.png" />

&nbsp;

For the current pasword, type `orangepi` and press enter. (You won't see any characters appear onscreen as you type.) Then choose a new password and enter it. Write down your new password or store it in a password manager app.

<img src="images/vlcsnap-2024-05-04-18h08m29s906_border.png" />

&nbsp;

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

![](images/vlcsnap-2024-05-04-18h26m51s348.png)

&nbsp;

Run this command to allow outgoing network connections.

```
sudo ufw default allow outgoing
```

![](images/vlcsnap-2024-05-04-18h26m59s436.png)

&nbsp;

Run the command below to allow incoming TCP connections on port 80:

```
sudo ufw allow 80/tcp
```

![](images/vlcsnap-2024-05-04-18h27m09s846.png)

&nbsp;

Now run the command `sudo ufw enable` to turn on your firewall.

![](images/vlcsnap-2024-05-06-19h10m33s671.png)

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

&nbsp;

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

&nbsp;

## Find your IP address

Run the command `ip addr` to 

![](images/vlcsnap-2024-05-04-18h29m22s232_border.png)

## Test your site on the local network

On a computer connected to the same network as your server, open a web browser, type the server's IP address in the address bar, and press enter. You should see your test website.

## Set a static IP address

<img src="images/vlcsnap-2024-05-04-18h33m11s162_border.png" />

&nbsp;

<img title="" src="images/vlcsnap-2024-05-04-18h33m22s250.png" alt="">

&nbsp;

<img title="" src="images/vlcsnap-2024-05-04-18h33m31s237.png" alt="">

&nbsp;

<img title="" src="images/vlcsnap-2024-05-04-18h34m12s001.png" alt="">

&nbsp;

<img title="" src="images/vlcsnap-2024-05-04-18h34m21s618.png" alt="">

&nbsp;

<img title="" src="images/vlcsnap-2024-05-04-18h34m31s536.png" alt="">

&nbsp;

<img title="" src="images/vlcsnap-2024-05-04-18h34m46s954.png" alt="">

&nbsp;

<img title="" src="images/vlcsnap-2024-05-04-18h34m49s645.png" alt="">

&nbsp;

## Enable SSH access

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h38m01s726_border.png" />

&nbsp;

<img title="" src="images/vlcsnap-2024-05-04-18h38m21s670.png" alt="">

&nbsp;

<img title="" src="images/vlcsnap-2024-05-04-18h38m40s212.png" alt="">

&nbsp;

<img title="" src="images/vlcsnap-2024-05-04-18h38m55s326.png" alt="">

&nbsp;

<img title="" src="images/vlcsnap-2024-05-04-18h39m35s435.png" alt="">

&nbsp;

<img title="" src="images/vlcsnap-2024-05-04-18h39m52s976.png" alt="">

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h40m13s233_border.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h41m07s243_border.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h41m56s939_border.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-18h42m01s997_border.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-22h37m36s356_border.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-22h37m42s430_border.png" />

&nbsp;

## Set up Dynamic DNS

<img src="images/vlcsnap-2024-05-04-22h45m06s912_border.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-22h45m39s104_border.png" />

&nbsp;

<img src="images/vlcsnap-2024-05-04-22h47m49s427_border.png" />

&nbsp;

aaa

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