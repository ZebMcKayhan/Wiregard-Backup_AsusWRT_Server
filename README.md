# Wiregard-Backup_AsusWRT_Server
Config/Help files for backing up Wireguard server config on AsusWRT

Steps to backup your Wireguard server for future restore:

1. Install [@Martinski4GitHub](https://github.com/Martinski4GitHub) script for saving subset of NVRAM variables:
```sh
mkdir -m 755 -p /jffs/addons/SaveRestoreNVRAM
curl  -kLSs --retry 3 --retry-delay 5 --retry-connrefused https://raw.githubusercontent.com/Martinski4GitHub/CustomMiscUtils/master/NVRAM/SaveRestoreNVRAMvars.sh -o /jffs/addons/SaveRestoreNVRAM/SaveRestoreNVRAMvars.sh && chmod 755 /jffs/addons/SaveRestoreNVRAM/SaveRestoreNVRAMvars.sh
```

2.Download the config file from this repository to only save the nvram variables assiciated with Wireguard Server:
```sh
curl  -kLSs --retry 3 --retry-delay 5 --retry-connrefused https://raw.githubusercontent.com/ZebMcKayhan/Wireguard-Backup_AsusWRT_Server/master/NVRAM_VarList_wg-server.txt -o /jffs/addons/SaveRestoreNVRAM/NVRAM_VarList.txt
```

3. Run the script in menu mode:
```sh
/jffs/addons/SaveRestoreNVRAM/SaveRestoreNVRAMvars.sh -menu
```
Check under "dp" option so the path for saving backups are correct and proper. choose something differently if needed by selecting this option.
Check under "fl" that the config file we edited are used, if not, adjust by selecting this option.


4. For backing up your Wireguard server, select option "bk". If everything is alright, the script will output each NVRAM variable its backing up. For sanity check, there should be 10 entries for the server peer itself and additionally 9 entries for each client peer. in my case with the server and 2 client I have 28 entries backed up.
If you ever want to double check which NVRAM variables are included in a backup file, use option "ls".

5. When you need to restore your wireguard server after a factory reset for example, you will need to install and run the script again (repeat #1-#3). 
In the script, make sure option "dp" points to where the backups are from your previous backup.
To start restore, select option "rt". You will be prompted about which backup file in the target you wish to restore.

Reboot your router after a restoration.
```sh
service reboot
```
