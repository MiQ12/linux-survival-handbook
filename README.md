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

## TrueNAS Scale

Some users of TrueNAS Apps attempting to configure GPU allocation report the error

    Expected [uuid] to be set for GPU inslot [<some pci slot>] in [nvidia_gpu_selection]) (see (NAS-134152).
    
Users experiencing this error should follow the steps below for a one-time fix that should not need to be repeated.Connect to a shell session and retrieve the UUID for each GPU with the command 

    midclt call app.gpu_choices | jq

For each application that experiences the error, run 

    midclt call -j app.update APP_NAME '{"values": {"resources": {"gpus": {"use_all_gpus": false, "nvidia_gpu_selection": {"PCI_SLOT": {"use_gpu": true, "uuid": "GPU_UUID"}}}}}}' 
    
Where:

APP_NAME is the name you entered in the application, for example, “plex”.

PCI_SLOT is the PCI slot identified in the error, for example “0000:2d:00.0”.

GPU_UUID is the UUID matching the PCI slot that you retrieved with the above command.
