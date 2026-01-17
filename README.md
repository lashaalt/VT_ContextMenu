# 🚀 Verify file on Virus Total using right click

I was tired of manually checking every binary file against VT. There are probably utilities to automate this, but in many environments, unvetted software installation is not allowed, and honestly, I would rather use standard Windows capabilities than install yet another utility.

Here is a simple Windows `VirusTotal_RightClick.reg` file that allows quickly calculate any file hash and verify it on VirusTotal by right-clicking and selecting "Verify Hash on VirusTotal" in the context menu.

It simply runs the below command
```
cmd /c for /f %%H in ('certutil -hashfile \"%1\" SHA256 ^| findstr /R /V \"hash\"') do \"C:\\Program Files (x86)\\Microsoft\\Edge\\Application\\msedge.exe\" https://www.virustotal.com/gui/file/%%H
```

The command does two things:
1. Calculates SHA256 hash using Windows standard certutil , and
2. Opens Virus Total url constructed as `https://www.virustotal.com/gui/file/<hash value>` in MS Edge.


Context menu looks like this. 

![Context Menu Image](./img/context-menu.png)


BTW, if you want to change the icon of the command, replace the icon index number in `"Icon"="imageres.dll,-104"`.

The number should match the "Icon Group" Index number in `C:\Windows\SystemResources\imageres.dll.mun`. 
There are a few free PE resource browsers out there. 

Enjoy, 
L
