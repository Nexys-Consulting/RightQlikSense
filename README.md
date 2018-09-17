# What is diferent from original
Original version use wrong method for url encode. When directory name or QVF name include spaces it does not work.

I replaced method "[System.Web.HttpUtility]::UrlEncode" with "[uri]::EscapeDataString".


# RightQlikSense

Just a quick hack to add Windows context menu to open QVF files in default web navigator (and in Qlik Sense Desktop) even if the application is not in the directory `C:\Users\[Username]\Documents\Qlik\Sense\Apps`



> Qlik Sense Desktop need to be started before action work


![1511768444348](imgs/1511768444348.png)


two menus is added:

- **Qvf Open in Desktop**: Open qvf application in navigator (Double click on qvf file work and open application in navigator)
- **Qvf Open in Desktop without data**: Open qvf application in navigator without data


Only tested on Windows 10 



## Installation



- Download files here https://github.com/sssimon-phoenix/RightQlikSense/archive/master.zip
- Unzip `master.zip`
- Double click on `Install-RightQlikSense.reg` to import context menu script in Windows registry



## Remove

If you want remove context menu Double click on `Remove-RightQlikSense.reg` to delete context menu for .qvf files.


## PowerShell code

For curious here the PowerShell code used in menu:

**Open**:

```powershell
Add-Type -AssemblyName System.Web;
$EncodedUrl = [uri]::EscapeDataString("%V");
start "http://localhost:4848/sense/app/$EncodedUrl";
```

**Open without data:**

```powershell
Add-Type -AssemblyName System.Web;
$EncodedUrl = [uri]::EscapeDataString("%V");
start "http://localhost:4848/sense/app/$EncodedUrl/noData/true";
```

