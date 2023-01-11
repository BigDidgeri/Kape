## What is Target Collection? ##
Targets are a collection of files and directory specifications. KAPE knows how to read these specifications and expand them to files and directories that exist on a target location. Once KAPE has processed all targets and built a list of files, the list is processed, and each file is copied from the source to the destination directory.
![811ceeea4083ab70546d89f5ecfc2f6f](https://user-images.githubusercontent.com/18509521/211716684-9f4555ec-fd6f-4f75-822a-3ef2742f0108.png)
## What is Module Execution? ##
Like Targets, Modules are defined using simple properties and are used to run programs. These programs can target anything, including files collected via the target capabilities as well as any other kinds of programs you may want to run on a system from a live response perspective.

For example, if you collected jump lists, a tool like JLECmd could dump the contents of the jump lists to CSV. If you also wanted to collect the output of netstat or ipconfig, you could do so.

Each of these options would be contained in its own Module and then grouped together based on commonality between the Modules, such as "NetworkLiveResponse" for example.

## Hand-on Challenge ##
### Q1 - Two USB Mass Storage devices were attached to this Virtual Machine. One had a Serial Number  0123456789ABCDE. What is the Serial Number of the other USB Device? ###
```1C6F654E59A3B0C179D366AE&0``` - Whenever we connect a USB drive to a computer a registry key called USBSTOR is created. This registry key stores information regarding that USB device. On a copmuter this is store in ```HKEY_LOCAL_MACHINESYSTEMCurrentControlSetEnumUSBSTOR``` however because we enumerated we will navigate to ```C:\Users\THM-4n6\Desktop\module\Registry\20230111030409\C:\Users\THM-4n6\Desktop\module\Registry\20230111030409\20230111030409_USBSTOR__C_Windows_System32_config_SYSTEM``` Open that and you will find information regarding USB devices from this machine.
![USB Serial Number](https://user-images.githubusercontent.com/18509521/211717951-e8730dc6-697d-4d53-a729-b993e3097e6d.png)

### Q2 - 7zip, Google Chrome and Mozilla Firefox were installed from a Network drive location on the Virtual Machine. What was the drive letter and path of the directory from where these software were installed? ###
```Z:\Setups``` - Here it is telling us these programs were installed so I went into the RecentApps registry to see if there were listed there. Here we can find a list of programs that have been installed including the ones we are looking for.
![application install from zsetup](https://user-images.githubusercontent.com/18509521/211719194-253b1b43-1ffb-4b9a-9469-3726d46ffe23.png)

### Q3 - What is the execution date and time of CHROMESETUP.EXE in MM/DD/YYYY HH:MM? ###
``` 11/25/2021 03:33 ``` - This one was found located in the same location as above.
![chometimestamp](https://user-images.githubusercontent.com/18509521/211719435-c2a623f2-0df5-4c31-9f19-08c33c63f9bf.png)

### Q4 - What search query was run on the system? ###
```RunWallpaperSetup.cmd``` - When a user searches a term in File Explorer windows saves that search term in a registry located at ```NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery``` so still working out of the same directory we can find the file ```20230111030409_WordWheelQuery__C_Users_THM-4n6_NTUSER.DAT``` which appears to be what we want
![wordwheelquery](https://user-images.githubusercontent.com/18509521/211720065-6e9804fd-bb3f-45df-aed0-dee1e1b411b9.png)

### Q5 - When was the network named Network 3 First connected to? ###
```11/30/2021 15:44``` - This can be found in the KnownNetworks file.
![knownNetworks](https://user-images.githubusercontent.com/18509521/211720687-4fa8c0c1-eeba-4bcf-a832-6d8438fa3a8a.png)

### Q6 - KAPE was copied from a removable drive. Can you find out what was the drive letter of the drive where KAPE was copied from? ###
```E:``` - To find this information we can look at Jump Lists. Jump Lists are similiar to windows shortcuts (link files) because they are designed to take a user directly to a specific file or directory that is used frequently or recently. Jump Lists can contain information of file activity that is no longer present in link files and this works vice versa. There are two sets of jump lists - ``` automaticDestinations``` - which are created by the operating system and ```customDestinations``` - which are maintained by a specific application. For this question let's open automaticDestionations.
![eKapeLastQ](https://user-images.githubusercontent.com/18509521/211722638-b4fc8c3a-1ae5-4da0-9d4e-de7ab2605ed7.png)
