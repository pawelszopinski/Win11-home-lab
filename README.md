# Win11-home-lab
30.06.24
After I failed to participate in ITF+ cert exam(due to technical issues) I decided to go back to do some hands-on projects after nearly 6 months break.

I chose Windows 11 and Office 365 Deployment Lab Kit. This is because I am redirecting to more support/security roles and wanted to know how is deployment and management of Windows and other Ms apps is working.

It wasn't easy to even kick off.

You need to have Hyper-V installed on your machine. Hyper-V is virtualization software provided by MS in their Win10/Win11 Pro,Enterprise and Education editions. The problem was I had Windows 11 Home on my machine.  I could go to cloud straight away but i wanted to start locally.

## How to turn on Hyper-V on Win11 Home?

After some research I found a script that worked

```bash
pushd "%~dp0"
dir /b %SystemRoot%\servicing\Packages\*Hyper-V*.mum >hyper-v.txt
for /f %%i in ('findstr /i . hyper-v.txt 2^>nul') do dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%%i"
del hyper-v.txt
Dism /online /enable-feature /featurename:Microsoft-Hyper-V -All /LimitAccess /ALL
pause

```

## How to turn on internet connection on Vms?
Official readme describes this process but it misses one point. After you create external switch you have to turn it on. Pick a VM you want to use > right click >properties > look for network adapter's virtual switch and pick your external switch from the list

## Official manual (Win11_23H2_Lab Guide_5.15
)
Unfortunately it's outdated. To name one point, there is nothing about MS Entra or Entra Connect. All runs on Azure Active Directory. Although it's very similar configuration in most cases, you will have to use common sense and omit certain areas. New edition of this manual should be released this August(2024) and let's hope it will be updated.