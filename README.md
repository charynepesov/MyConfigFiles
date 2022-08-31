# MyConfigFiles - v0.01 alpha
- - -
# My Debian testing installation
# Install base debian with expert install. On software selection uncheck Gnome.
# Reboot
# Login with root user if you did not disabled that earlier
su -

# Give sudo for regular user.
# https://wiki.debian.org/sudo/
apt install sudo
adduser your_username_here sudo

# Install nala package manager for apt
sudo apt install nala

# Install firmware-linux for drivers
5. sudo nala update && sudo nala install firmware-linux

- - -
# Configure your network
- - -
# https://wiki.debian.org/NetworkConfiguration
# Check your network device list
ls /sys/class/net

# Install wifi drivers if it is not already installed
# https://wiki.debian.org/WiFi
sudo apt install firmware-b43-installer

# Install NetworkManager or iwd 
# https://wiki.debian.org/NetworkManager
# https://wiki.debian.org/WiFi/HowToUse
sudo nala install network-manager
OR
sudo nala install iwd

# Disable wpa_supplicant
sudo systemctl --now disable wpa_supplicant

# Enable iwd
sudo systemctl --now enable iwd

# Enable essential features of iwd from config file: /etc/iwd/main.conf
[General]
EnableNetworkConfiguration=true
[Network]
EnableIPv6=true

# Restart the iwd
sudo service iwd restart

# Configure iwd with iwctl. Run iwctl by your normal user not root
iwctl

- - -
# Audio Configuration
#################################################################
# Install wireplumber pipewire-pulse
sudo apt install wireplumber pipewire-pulse pulseaudio-utils pipewire-audio-client-libraries libspa-0.2-jack libspa-0.2-bluetooth bluez-y

systemctl --user --now enable wireplumber.service
systemctl --user --now enable pipewire-pulse.service
sudo reboot

LANG=C pactl info | grep '^Server Name'

sudo cp /usr/share/doc/pipewire/examples/alsa.conf.d/99-pipewire-default.conf /etc/alsa/conf.d/

sudo cp cp /usr/share/doc/pipewire/examples/ld.so.conf.d/pipewire-jack-*.conf /etc/ld.so.conf.d/

sudo ldconfig

##################################################################
# Display Manager
##################################################################
# https://wiki.debian.org/LightDM
# https://wiki.archlinux.org/title/LightDM
# Display manager (if you want) LightDM with webkit greeter
sudo apt install lightdm

# Default configuration file at /etc/lightdm/lightdm.conf
# Make a directory for our own configuration and place our config files there
sudo mkdir /etc/lightdm/lightdm.conf.d/

# To change the current default Display Manager, run 
sudo dpkg-reconfigure lightdm

# Enable Lightdm
sudo systemctl enable lightdm.service

# Set default greeter by changing [Seat:] section on default config file
[Seat:*]
...
greeter-session=lightdm-yourgreeter-greeter







###################################################################
# Window Manager
###################################################################
# Install Window Manager Sway
sudo apt install sway swayidle swaylock swaybg sway-backgrounds kitty chromium brightnessctl xwayland xdg-desktop-portal qtwayland5  

# Configure sway
mkdir ~/.config/sway
cp /etc/sway/config ~/.config/sway/config
# It is already included by package (include /etc/sway/config.d/*)

# Configure your keyboard
swaymsg -t get_inputs

# And add this to your config file
input - xkb_layout "us,tr,ru"
input - xkb_options "grp:win_space_toggle"

# man sway
# man 5 sway
# man 5 sway-input
# man 5 sway-output
# man 5 sway-bar
# man 7 swaybar-protocol
# man swaybg
# man swaynag
# man 1 swaymsg
# man 7 swayips
# https://docs.gtk.org/Pango/type_func.FontDescription.from_string.html#description
#############################################################
# Wayland Configuration
#############################################################
# Install packages
sudo apt install qtwayland5 libreoffice-gtk3

# https://www.freedesktop.org/software/systemd/man/environment.d.html
# Add Environment Variables In order to programs work on wayland
# add /etc/environment.d/10-wayland.conf file and append this lines
# ~/.config/environment.d/*.conf file
GDK_BACKEND=wayland		#for GTK apps
CLUTTER_BACKEND=wayland		#for clutter apps
QT_QPA_PLATFORM=wayland;xcb	#for QT apps
SDL_VIDEODRIVER=wayland		#for SDL2 apps
MOZ_ENABLE_WAYLAND=1		#for Firefox
SAL_USE_VCLPLUGIN=gtk3		#for libreoffice
_JAVA_AWT_WM_NONREPARENTING=1	#for JAVA apps
ELM_DISPLAY=wl			#for EFL apps

# For Chromium run program with
--ozone-platform=wayland
# For backwards compatability install xwayland
sudo apt install xwayland










# Create user directories with this package
# https://www.freedesktop.org/wiki/Software/xdg-user-dirs/
# https://github.com/swaywm/sway/wiki/i3-Migration-Guide















﻿Firmware-iwlwifi
tlp
intel-microcode
firmware-linux
apt-file
ttf-mscorefonts-installer
libavcodec-extra
gstreamer1.0-libav
gstreamer1.0-plugins-ugly
gstreamer1.0-vaapi
fonts-crosextra-carlito
fonts-crosextra-caladea
ufw
timeshift
vim
vim-doc
vim-scripts
universal-ctags
kitty
imagemagick
neofetch
git
git-gui

