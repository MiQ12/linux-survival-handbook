# linux-survival-handbook
Collection of all the Linux tweaks and modifications I've done and found good.

At least at first all of these apply to only Fedora with KDE Plasma, they might apply to other distros as well but I have not tested that.

## Fedora (KDE)

### Lutris / Wine
By default the wine prefix will make a copy / symlink of your own Documents, Pictures and Videos folders and their contents to the prefix meaning that all apps that use the prefix will be able to see them.
- Winetricks > Select the default wineprefix > Change settings > sandbox (check ON)

### SMB Shares
*Not complete
SMB Shares mount at smb://192.168...../Share but this address is often not supported by external apps such as VLC and this is why they need to have /mnt path

Create .smbcredentials at home path

sudo mount -t cifs //192.168....../Share /mnt/shareExample -o creentials=/home/username/.smbcredentials
