# manjaro-cinnamon-dell-7559
![image](https://github.com/oguzkaganeren/manjaro-cinnamon-dell-7559/blob/master/Screenshot%20from%202019-10-26%2013-15-57.png)
```
sudo nano /etc/default/grub 
```
> GRUB_CMDLINE_LINUX_DEFAULT="quiet acpi_osi=! acpi_osi=\ "Windows 2009\ " acpi_backlight=vendor"

### Fastest Mirror List
```
sudo pacman-mirrors --fasttrack 5
```

### Packages I use
```
sudo pacman -S aria2 ttf-ubuntu-font-family speedtest-cli deepin-movie deepin-calculator telegram-desktop kdenlive inkscape create_ap gedit virtualbox fish flameshot deepin-terminal neofetch soundconverter gtop firefox-developer-edition
```
### Change the shell
```
chsh -s /usr/bin/fish
curl -L https://get.oh-my.fish | fish
omf install bobthefish
```
## Customize shell and terminal
Change `.config/fish/omf.fish` with [this](https://github.com/oguzkaganeren/manjaro-cinnamon-dell-7559/blob/master/.config/fish/omf.fish)
Set default deepin terminal then open it. Right click on the terminal and switch theme `argonaut`.
### Aur Packages I use
```
yay -S materia-theme opera ungoogled-chromium-bin ttf-font-awesome ttf-font-awesome-4 ttf-roboto android-studio woeusb-git jdownloader2 ttf-ms-fonts vscodium-bin breeze-blurred-git otf-san-francisco xdman gwe svr zettlr-bin fslint waterfox-bin odio-appimage skypeforlinux-stable-bin posy-cursors
```
### If skype not run
```
sudo sysctl kernel.unprivileged_userns_clone=1
```
### If headphones not detected when restart or after startup
```
sudo nano /etc/pulse/default.pa
```
at the bottom under `### Make some devices default` put
```
set-default-sink 1
```
### Wrong clock
```
timedatectl set-local-rtc 1 --adjust-system-clock
```
### Firefox screen tearing during scrolling Issue
```
sudo gedit /etc/profile.d/kwin.sh
```
then put this in it,
```
#!/bin/sh

export KWIN_TRIPLE_BUFFER=1
```
After that, 
```
sudo gedit ~/.config/kwinrc
```
Add those parameters at the bottom,

```
MaxFPS=60
RefreshRate=60
```
Save it and reboot. 
Open firefox and 
**about:config**
then search  **layers.acceleration.force-enabled**
It should be true.
Done.
### Adblock Spotify
```
yay -S --mflags --skipinteg --needed spotify spotify-adblock
```
>  :exclamation: If you have a SSD, you should enable fstrim.
```
sudo systemctl enable fstrim.timer
```
### Spotify Themes
```
yay -S spicetify-cli
sudo chmod 777 /opt/spotify -R
```
then copy the `google-spicetify` to `.config/spicetify/Themes/`
```
spicetify backup apply
```
#### White
```
spicetify config current_theme google-spicetify; spicetify config color_scheme base; spicetify apply
```
#### Gow
```
spicetify config current_theme google-spicetify; spicetify config color_scheme gow; spicetify apply
```
#### Dark
```
spicetify config current_theme google-spicetify; spicetify config color_scheme dark; spicetify apply
```
### For Other Partitations
If you have another partition(E, D etc.). You can mount it on the startup. Thus some applications which are using other partitions don't get an error.

```
lsblk -f
```
The command shows your disks uuid.
```
sudo gedit /etc/fstab 
```
Open your fstab config with the command. You should add codes similar to the following example. You should change UUID and /run/media/yourUserName/Partition.
```
UUID=b336b98e-d0b5-4254-b6aa-9e66f85b0dfc /run/media/oguz/Files ext4 defaults  0 0
UUID=daffc947-3129-446b-ad35-8a730d7d7203 /run/media/oguz/Media ext4 defaults  0 0
```

>  :exclamation: If you use manjaro with dual boot, you should close fast-startup,hibarnate on your Windows, otherwise, you have not a write permission for other partitions.

### Installing Nvidia Drivers
Use Manjaro Setting Manager > Hardware Configuration > Auto Install Proprietary Driver
After Installation,
```
sudo gpasswd -a <user> bumblebee
reboot
```
### Open gwe
```
optirun gwe --ctrl-display ":8"
```
### Open Wifi Hotspot
```
sudo create_ap wlp5s0 wlp5s0 MyAccessPoint password
```
### Format USB with Terminal
```
sudo umount /dev/sdxx
sudo mkdosfs -F 32 -I /dev/sdxx
```
## For Developers
### Docker
```
sudo pacman -S docker-compose 
sudo usermod -aG docker oguz 
sudo systemctl start docker
sudo systemctl enable docker

reboot
```
### PostgreSQL
```
sudo pacman -S postgresql
sudo su postgres -l # or sudo -u postgres -i
initdb --locale $LANG -E UTF8 -D '/var/lib/postgres/data/'
exit
sudo systemctl enable --now postgresql.service
sudo pacman -S pgadmin4

```
ERROR: Node.js version 11.15.0 is no longer supported.
sudo npm install -g n
sudo n latest

### Nvidia Overclock
```
sudo gedit /etc/X11/xorg.conf
```
Unlock everything under Nvidia X Server Settings gui including fan control and overclocking. Add this under both “Device” and “Screen” sections.
```
Option         "Coolbits" "31"

```
Also, enable TripleBuffer under the “Device” section.

By default TripleBuffer is disabled. This even in some cases can help load times with the driver and games.

```
Option 	   "TripleBuffer" "True"
```
To bypass PowerMizer and Adaptive Clocking add this under the “Device” section.
```
Option         "RegistryDwords" "PowerMizerEnable=0x1; PerfLevelSrc=0x3322; PowerMizerDefaultAC=0x1"
```

    PowerMizerEnable=0x1 turns on PowerMizer.
    PerfLevelSrc=0x2222 tells the video card to operate at full on both AC & battery.
    PowerMizerDefaultAC=0x1 tells the card to behave as if AC power is connected.
PerfLevelSrc=0x2222 is for desktops.

Source https://forum.level1techs.com/t/nvidia-gpu-settings-guide-for-better-performance/131660

## Change Default Java Version
```
sudo archlinux-java status
sudo archlinux-java set java-10-openjdk
```
