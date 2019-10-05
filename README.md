# manjaro-cinnamon-dell-7559
![image](https://github.com/oguzkaganeren/manjaro-cinnamon-dell-7559/blob/master/Screenshot%20from%202019-09-27%2016-47-57.png)
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
sudo pacman -S aria2 ttf-ubuntu-font-family speedtest-cli deepin-movie deepin-calculator telegram-desktop kdenlive inkscape create_ap gedit virtualbox fish flameshot deepin-terminal neofetch
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
yay -S materia-theme opera chromium ttf-font-awesome ttf-font-awesome-4 ttf-roboto android-studio woeusb-git jdownloader2 ttf-ms-fonts vscodium-bin breeze-blurred-git otf-san-francisco
```
### If headphones not detected when restart or after startup
```
sudo nano /etc/pulse/default.pa
```
at the bottom under `### Make some devices default` put
```
set-default-sink 1
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
UUID=DAF6FE7CF6FE5869 /run/media/oguz/D ntfs-3g defaults  0 0
UUID=C480917680917022 /run/media/oguz/E ntfs-3g defaults  0 0
```

>  :exclamation: If you use manjaro with dual boot, you should close fast-startup,hibarnate on your Windows, otherwise, you have not a write permission for other partitions.

### Installing Nvidia Drivers
Use Manjaro Setting Manager > Hardware Configuration > Auto Install Proprietary Driver
After Installation,
```
sudo gpasswd -a <user> bumblebee
reboot
```
### Open Wifi Hotspot
```
sudo create_ap wlp5s0 wlp5s0 MyAccessPoint password
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
