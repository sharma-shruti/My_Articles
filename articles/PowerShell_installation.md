*PowerShell is a command-line shell and scripting language tool built on the .NET Framework. PowerShell allows System Administrators to perform task automation and configuration management.*

# Let’s install PowerShell 7

root@bond:~# wget -q https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb
root@bond:~# sudo dpkg -i packages-microsoft-prod.deb
Selecting previously unselected package packages-microsoft-prod.
(Reading database ... 90577 files and directories currently installed.)
Preparing to unpack packages-microsoft-prod.deb ...
Unpacking packages-microsoft-prod (1.0-3) ...
Setting up packages-microsoft-prod (1.0-3) ...
root@bond:~# sudo apt-get update
Get:1 http://mirrors.digitalocean.com/ubuntu bionic InRelease [242 kB]
Get:2 https://packages.microsoft.com/ubuntu/16.04/prod xenial InRelease [4003 B]                            
Get:3 http://mirrors.digitalocean.com/ubuntu bionic-updates InRelease [88.7 kB]                             
Get:4 http://mirrors.digitalocean.com/ubuntu bionic-backports InRelease [74.6 kB]     
Get:5 https://packages.microsoft.com/ubuntu/16.04/prod xenial/main amd64 Packages [125 kB]           
Get:6 http://mirrors.digitalocean.com/ubuntu bionic-updates/main amd64 Packages [889 kB]                    
Get:7 http://mirrors.digitalocean.com/ubuntu bionic-updates/universe amd64 Packages [1059 kB]
Get:8 http://security.ubuntu.com/ubuntu bionic-security InRelease [88.7 kB]                               
Fetched 2571 kB in 1s (1943 kB/s)                                                   
Reading package lists... Done
root@bond:~# sudo apt-get install -y powershell
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 powershell : Depends: libicu55 but it is not installable
E: Unable to correct problems, you have held broken packages.
root@bond:~#

root@bond:~# pwsh

Command 'pwsh' not found, but can be installed with:

snap install powershell

root@bond:~# sudo add-apt-repository universe
'universe' distribution component enabled for all sources.
Get:1 http://mirrors.digitalocean.com/ubuntu bionic InRelease [242 kB]
Hit:2 https://packages.microsoft.com/ubuntu/16.04/prod xenial InRelease                                     
Hit:3 http://mirrors.digitalocean.com/ubuntu bionic-updates InRelease                                       
Hit:4 http://mirrors.digitalocean.com/ubuntu bionic-backports InRelease                                     
Get:5 http://security.ubuntu.com/ubuntu bionic-security InRelease [88.7 kB]                                 
Get:6 http://archive.ubuntu.com/ubuntu bionic InRelease [242 kB]
Get:7 http://archive.ubuntu.com/ubuntu bionic/universe amd64 Packages [8570 kB]
Get:8 http://archive.ubuntu.com/ubuntu bionic/universe Translation-en [4941 kB]
Fetched 14.1 MB in 5s (2847 kB/s)                               
Reading package lists... Done
root@bond:~# sudo apt-get install -y powershell
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 powershell : Depends: libicu55 but it is not installable
E: Unable to correct problems, you have held broken packages.
root@bond:~# lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 18.04.3 LTS
Release:        18.04
Codename:       bionic
root@bond:~# uname -a
Linux bond 4.15.0-66-generic #75-Ubuntu SMP Tue Oct 1 05:24:09 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
root@bond:~# wget http://security.ubuntu.com/ubuntu/pool/main/i/icu/libicu55_55.1-7ubuntu0.4_amd64.deb
--2020-03-23 10:14:21--  http://security.ubuntu.com/ubuntu/pool/main/i/icu/libicu55_55.1-7ubuntu0.4_amd64.deb
Resolving security.ubuntu.com (security.ubuntu.com)... 91.189.88.152, 91.189.91.39, 91.189.91.38, ...
Connecting to security.ubuntu.com (security.ubuntu.com)|91.189.88.152|:80... connected.
HTTP request sent, awaiting response... 404 Not Found
2020-03-23 10:14:21 ERROR 404: Not Found.

root@bond:~# sudo add-apt-repository universe
'universe' distribution component is already enabled for all sources.
root@bond:~# wget https://github.com/PowerShell/PowerShell/releases/tag/v7.0.0/powershell_7.0.0-1.ubuntu.18.04_amd64.deb
--2020-03-23 10:24:09--  https://github.com/PowerShell/PowerShell/releases/tag/v7.0.0/powershell_7.0.0-1.ubuntu.18.04_amd64.deb
Resolving github.com (github.com)... 52.74.223.119
Connecting to github.com (github.com)|52.74.223.119|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [text/html]
Saving to: ‘powershell_7.0.0-1.ubuntu.18.04_amd64.deb’

powershell_7.0.0-1.ubuntu.1     [ <=>                                     ]  99.66K  --.-KB/s    in 0.003s  

2020-03-23 10:24:10 (29.0 MB/s) - ‘powershell_7.0.0-1.ubuntu.18.04_amd64.deb’ saved [102048]

root@bond:~# sudo dpkg -i powershell_7.0.0-1.ubuntu.18.04_amd64.deb
dpkg-deb: error: 'powershell_7.0.0-1.ubuntu.18.04_amd64.deb' is not a Debian format archive
dpkg: error processing archive powershell_7.0.0-1.ubuntu.18.04_amd64.deb (--install):
 dpkg-deb --control subprocess returned error exit status 2
Errors were encountered while processing:
 powershell_7.0.0-1.ubuntu.18.04_amd64.deb
root@bond:~# sudo dpkg -i powershell_7.0.0-1.ubuntu.18.04_amd64.deb
dpkg-deb: error: 'powershell_7.0.0-1.ubuntu.18.04_amd64.deb' is not a Debian format archive
dpkg: error processing archive powershell_7.0.0-1.ubuntu.18.04_amd64.deb (--install):
 dpkg-deb --control subprocess returned error exit status 2
Errors were encountered while processing:
 powershell_7.0.0-1.ubuntu.18.04_amd64.deb
root@bond:~# pwsh-preview

Command 'pwsh-preview' not found, but can be installed with:

snap install powershell-preview

root@bond:~# sudo dpkg -i powershell-preview_7.0.0-preview.4-1.ubuntu.18.04_amd64.deb
dpkg: error: cannot access archive 'powershell-preview_7.0.0-preview.4-1.ubuntu.18.04_amd64.deb': No such file or directory
root@bond:~# wget https://raw.githubusercontent.com/PowerShell/PowerShell/master/tools/install-powershell.sh
--2020-03-23 10:32:37--  https://raw.githubusercontent.com/PowerShell/PowerShell/master/tools/install-powershell.sh
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 151.101.8.133
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|151.101.8.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 6798 (6.6K) [text/plain]
Saving to: ‘install-powershell.sh’

install-powershell.sh       100%[========================================>]   6.64K  --.-KB/s    in 0s      

2020-03-23 10:32:37 (58.4 MB/s) - ‘install-powershell.sh’ saved [6798/6798]

root@bond:~# chmod 755 install-powershell.sh
root@bond:~# sudo install-powershell.sh -preview
sudo: install-powershell.sh: command not found
root@bond:~# ./install-powershell.sh 
Get-PowerShell MASTER Installer Version 1.2.0
Installs PowerShell and Optional The Development Environment
  Original script is at: https://raw.githubusercontent.com/PowerShell/PowerShell/master/tools\install-powershell.psh
Arguments used: 

Operating System Details:
  OS: linux
  DIST: Ubuntu
  DistroBasedOn: debian
  PSUEDONAME: bionic
  REV: 18.04
  KERNEL: 4.15.0-66-generic
  MACH: x86_64
  OSSTR: 
Configuring PowerShell Environment for: debian Ubuntu 18.04
Could not find "installpsh-debian.sh" next to this script...
Pulling and executing it from "https://raw.githubusercontent.com/PowerShell/PowerShell/master/tools/installpsh-debian.sh"
found and using curl

*** PowerShell Development Environment Installer 1.2.0 for debian
***    Original script is at: https://raw.githubusercontent.com/PowerShell/PowerShell/master/tools/installpsh-debian.psh

*** Arguments used: 

*** Installing PowerShell for debian...
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 58908  100 58908    0     0  99675      0 --:--:-- --:--:-- --:--:-- 99506
*** Current version on git is: 7.0.0, repo version may differ slightly...
*** Setting up PowerShell repo...
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   983  100   983    0     0   6301      0 --:--:-- --:--:-- --:--:--  6301
OK
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100    77  100    77    0     0   1638      0 --:--:-- --:--:-- --:--:--  1638
Hit:1 https://packages.microsoft.com/ubuntu/16.04/prod xenial InReleasec main
Get:2 http://mirrors.digitalocean.com/ubuntu bionic InRelease [242 kB]                                      
Get:3 https://packages.microsoft.com/ubuntu/18.04/prod bionic InRelease [4003 B]                            
Hit:4 http://mirrors.digitalocean.com/ubuntu bionic-updates InRelease                                       
Hit:5 http://mirrors.digitalocean.com/ubuntu bionic-backports InRelease                                     
Hit:6 http://archive.ubuntu.com/ubuntu bionic InRelease                                                     
Get:7 https://packages.microsoft.com/ubuntu/18.04/prod bionic/main amd64 Packages [99.3 kB]
Get:8 http://security.ubuntu.com/ubuntu bionic-security InRelease [88.7 kB]         
Fetched 434 kB in 1s (363 kB/s)                                                     
Reading package lists... Done
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following package was automatically installed and is no longer required:
  grub-pc-bin
Use 'apt autoremove' to remove it.
The following additional packages will be installed:
  liblttng-ust-ctl4 liblttng-ust0 liburcu6
The following NEW packages will be installed:
  liblttng-ust-ctl4 liblttng-ust0 liburcu6 powershell
0 upgraded, 4 newly installed, 0 to remove and 56 not upgraded.
Need to get 58.6 MB of archives.
After this operation, 160 MB of additional disk space will be used.
Get:1 https://packages.microsoft.com/ubuntu/18.04/prod bionic/main amd64 powershell amd64 7.0.0-1.ubuntu.18.04 [58.3 MB]
Get:2 http://mirrors.digitalocean.com/ubuntu bionic/universe amd64 liblttng-ust-ctl4 amd64 2.10.1-1 [80.8 kB]
Get:3 http://mirrors.digitalocean.com/ubuntu bionic/main amd64 liburcu6 amd64 0.10.1-1 [52.1 kB]
Get:4 http://mirrors.digitalocean.com/ubuntu bionic/universe amd64 liblttng-ust0 amd64 2.10.1-1 [154 kB]
Fetched 58.6 MB in 1s (56.1 MB/s)                                         
Selecting previously unselected package liblttng-ust-ctl4:amd64.
(Reading database ... 90582 files and directories currently installed.)
Preparing to unpack .../liblttng-ust-ctl4_2.10.1-1_amd64.deb ...
Unpacking liblttng-ust-ctl4:amd64 (2.10.1-1) ...
Selecting previously unselected package liburcu6:amd64.
Preparing to unpack .../liburcu6_0.10.1-1_amd64.deb ...
Unpacking liburcu6:amd64 (0.10.1-1) ...
Selecting previously unselected package liblttng-ust0:amd64.
Preparing to unpack .../liblttng-ust0_2.10.1-1_amd64.deb ...
Unpacking liblttng-ust0:amd64 (2.10.1-1) ...
Selecting previously unselected package powershell.
Preparing to unpack .../powershell_7.0.0-1.ubuntu.18.04_amd64.deb ...
Unpacking powershell (7.0.0-1.ubuntu.18.04) ...
Setting up liburcu6:amd64 (0.10.1-1) ...
Setting up liblttng-ust-ctl4:amd64 (2.10.1-1) ...
Setting up liblttng-ust0:amd64 (2.10.1-1) ...
Setting up powershell (7.0.0-1.ubuntu.18.04) ...
Processing triggers for libc-bin (2.27-3ubuntu1) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
Congratulations! PowerShell is installed at /opt/microsoft/powershell/7.
Run "pwsh" to start a PowerShell session.

*** NOTE: Run your regular package manager update cycle to update PowerShell
*** Install Complete
root@bond:~# pwsh
PowerShell 7.0.0
Copyright (c) Microsoft Corporation. All rights reserved.

https://aka.ms/powershell
Type 'help' to get help.

PS /root> exit
root@bond:~#


==================THE END=============================
