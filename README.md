# Ultra-Light-Windows-Installer
A custom WinPE in the form of a light boot.wim, that you can drag and drop in the sources folder of any Win7 and above ISO.

# Why?
As you may know, the Windows installer is:
1- quite finicky
2- kinda bloated.
So, i set out to make a custom WinPE that bypasses all this.
# To know how the ULWI works, you need to know how the stock installer works.
In a windows install media, there is usually 2 .wim files, boot.wim and install.wim. (install.wim may be install.esd, only difference is that .esd has higher solid compression).
boot.wim is a stripped down version of Windows called Windows Pre-Installation Enviroment. or simply shortened to WinPE. It loads itself into the RAM and launches a setup.exe. all the setup.exe is decompress the install.wim (or .esd). what is the install file? its a compressed version of the windows install, for linux users, think of it as the compressed rootfs. once decompressed, it boots from internal and continues setup.
SO: i decided to remake that. I used the Win10 2004 PE as a base, (which can be acquired by installing the Win10 2004 ADK and its matching PE addon) (and i know the actual PE says 1809, that was some mandela affect, ill fix it later on to reference properly 2004), which is good since: its light, base PE with nothing is ~200MB. i then added a light simple shell (WinXShell), and then the main event:
# The Installer.
Basically, it has 2 main components:
1. The Launcher. this is a main menu that allows you to make partitions for UEFI or BIOS systems, and install a ESD or WIM for the UEFI or BIOS systems. When making a partiton, it will auto mount as C:. The UEFI boot partition will auto mount as S:. also use diskpart > list disk to find the disk number you install to!
![Image of the menu](https://hsulwd.on.websim.com/Screenshot%20(14).png)
PLEASE NOTE: If you plan to dualboot, DO NOT USE THESE OPTION! THEY ERASE THE WHOLE DRIVE. Instead, use diskpart > ass letter C to the partiton, and skip to:
3. the installers. these use the open source wimlib project to decompress the ESD or WIM.
![Image of the BIOS installer layout](https://hsulwd.on.websim.com/Screenshot%20(16).png)
![Image of the UEFI installer layout](https://hsulwd.on.websim.com/Screenshot%20(15).png)


