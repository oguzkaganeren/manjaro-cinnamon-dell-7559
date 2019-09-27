# manjaro-cinnamon-dell-7559

sudo pacman -S aria2 ttf-ubuntu-font-family speedtest-cli deepin-movie deepin-calculator telegram-desktop kdenlive inkscape create_ap gedit virtualbox fish flameshot


yay -S materia-theme opera chromium ttf-font-awesome ttf-font-awesome-4 powerline-fonts ttf-roboto adobe-source-sans-pro-fonts android-studio woeusb-git jdownloader2 ttf-ms-fonts ephifonts otf-exo thermald vscodium-bin breeze-blurred-git otf-san-francisco


yay -S --mflags --skipinteg --needed spotify spotify-adblock

sudo pacman -S docker-compose 
sudo usermod -aG docker oguz 
sudo systemctl start docker
sudo systemctl enable docker

reboot

ERROR: Node.js version 11.15.0 is no longer supported.
sudo npm install -g n
sudo n latest
