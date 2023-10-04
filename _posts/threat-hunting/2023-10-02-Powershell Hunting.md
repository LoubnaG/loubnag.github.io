---
title: "Threat Hunting With Powershell"
description: "Discover how you can  identify threats in a Windows environment."
readtime: 5 minute read
header:
  teaser: /threat-hunting/assets/images/tools-powershell.png
  overlay_image: /threat-hunting/assets/images/tools-powershell.png
  overlay_filter: 0.5

ribbon: Tools
tags:   
  - Threat Hunting
  - Tools
bg: rgb(0, 159, 0)
toc: true
toc_sticky: true
toc_label: "Table of Contents"
# toc_icon: "heart"
toc: true
classes: wide
last_modified_at: 2023-09-02
---
<span style="color:#909090">Discover how you can  identify threats in a Windows environment.</span>

# Powershell Overview
Windows PowerShell is a command-line shell and scripting language that allows developers, IT admins, and DevOps professionals to automate tasks and configurations using code.<br>
Powershell works with objects; in fact, everything in PowerShell is an object. These objects represent attributes (properties) or instructions (methods).<br>
PowerShell manipulates objects with four different types of commands which are:<br>

📍 <span style="color:#7ba4d2">Cmdlets:</span> -- Pronounced as command-lets -- , They are considered the basic single-function commands. A cmdlet typically exists as a small script that is intended to perform a single specific function such as coping files and changing directories.<br>

There are hundreds of cmdlets available by default under today's PowerShell like:
- `Get-Help` : get more information about a desired cmdlet
- `Get-Location` : get the current directory
- `Set-Location` : change the current directory
- `Get-ChildItem` : list items in a directory
- `Copy-Item` : Copy files
- `Move-Item` : move a file
- ... and much more !! <br>

📍 <span style="color:#7ba4d2">Functions:</span> Unlike cmdlets, functions are written in PowerShell language. They are a sequence of instructions that are formed and are to be achieved simply by invoking them.<br>

↪ Example of powershell function that return a message passed in parameter :<br>

| ![Powershell Function With Parameter](/assets/images/threat-hunting/Tools/Powershell/powershell1.png) | 
|:--:| 
| *Powershell Function With Parameter* |

<br>
📍 <span style="color:#7ba4d2">Scripts:</span> PowerShell script is a plain text file that contains one or more PowerShell commands. PowerShell scripts are written with cmdlets and  have a .ps1 file extension.
Running a script is a lot like running a cmdlet.<br>

↪ Example of Powershell script that turn on Hyper -V on Windows:

| ![Powershell Script](/assets/images/threat-hunting/Tools/Powershell/powershell2.png) | 
|:--:| 
| *Powershell Script* |

📍 <span style="color:#7ba4d2">Executable commands:</span> They are commands used in running executable files. There are three commands used in running .exe files:
- The first one is `start-process` cmdlet. For example `Start-Process -FilePath "notepad.exe"`
- The second one is with  the `Invoke-expression` command
- The third option is typing `.\` before the file’s name.

# Poweshell Hunting Commands
## Schedule Tasks Commands
<span style="color:#7ba4d2">Get-ScheduledTask:</span> This cmdlet gets the task definition object of a scheduled task that is registered on a computer.<br>
<table>
  <tr style="border:2px solid #b3adad;">
    <th style="border:2px solid #b3adad;">Command</th>
    <th style="border:2px solid #b3adad;">Description</th>
    <th style="border:2px solid #b3adad;">Example</th>
  </tr>
  <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;">Get-ScheduledTask -TaskName "Name”</td>
     <td style="border:2px solid #b3adad;">Get a scheduled task definition object</td>
    <td style="border:2px solid #b3adad;">Get-ScheduledTask -TaskName "SystemScan"</td>
  </tr>
   <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;">Get-ScheduledTask -TaskPath "\Path\*"</td>
     <td style="border:2px solid #b3adad;">Get an array of scheduled task definition objects from a specific path</td>
    <td style="border:2px solid #b3adad;">Get-ScheduledTask -TaskPath "\UpdateTasks\*"</td>
  </tr>
</table>  

## Services Command
<span style="color:#7ba4d2">Get-Service:</span> This cmdlet gets objects that represent the services on a computer, including running and stopped services.<br>
<table>
  <tr style="border:2px solid #b3adad;">
    <th style="border:2px solid #b3adad;">Command</th>
    <th style="border:2px solid #b3adad;">Description</th>
    <th style="border:2px solid #b3adad;">Example</th>
  </tr>
  <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;">Get-Service "Nam*"</td>
    <td style="border:2px solid #b3adad;">Get services that begin with a search string</td>
    <td style="border:2px solid #b3adad;">Get-Service "wmi*"</td>
  </tr>
   <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;">Get-Service -Displayname "*Name*"</td>
    <td style="border:2px solid #b3adad;">Display services that include a search string</td>
    <td style="border:2px solid #b3adad;">Get-Service -Displayname "*network*"</td>
  </tr>
  <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;">Get-Service | Where-Object {$_.Status -eq "Running"}</td>
    <td style="border:2px solid #b3adad;">Display services that are currently active</td>
    <td style="border:2px solid #b3adad;">Get-Service | Where-Object {$_.Status -eq "Running"}</td>
  </tr>
  <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;">Get-Service "s*" | Sort-Object status</td>
    <td style="border:2px solid #b3adad;">Sort services by property value</td>
    <td style="border:2px solid #b3adad;">Get-Service "s*" | Sort-Object status</td>
  </tr>
</table>  

# Baseline
A Baseline is a file that holds the base security control, file system state, etc. and it is used to compare the current machine state with the base state that this baseline represents.<br>

The usage of baselines will help you detect anomalies inside your environment, malicious files, processes, etc.<nr>

When analyzed with strong detail, baselines make threat detection easier and more accurate.<br>

📍 <span style="color:#7ba4d2">BaseLining Processes, Services, Tasks:</span> 
- `Get-Process | Select-Object -Property Name > processes.txt` <br>
↪ This command will save the Get-Process command output to process.txt file
- `Get-Scheduledtask | Select-Object TaskName > scheduledtasks.txt`<br>
↪ This command will save the Get-Scheduledtask command output to scheduledtasks.txt file
- `Get-Service | Select-Object -Property Name > services.txt`<br>
↪ This command will save the Get-Service command output to services.txt file<br>

📍 <span style="color:#7ba4d2">Comparing Baselines:</span> 
```jsx
$baseline = Get-Content .\baseline-services.txt 
$current = Get-Content .\current-services.txt
Compare-Object $baseline $current
```

# Hunting Web Shells
This command will retrieve the files of a directory recursively then obtain the SHA1 hash of each file and store them in a CSV file.<br>
Now we can use this exported file as a BaseLine for future use when we need to compare our existing files with our BaseLine.<br>
For web shells, we can get a BaseLine of our web server’s directory.<br>

```jsx
Get-ChildItem -Path PATH -File -Recurse | Get-FileHash -Algorithm SHA1 | Export-Csv C:\EXPORTPATH 
```
<br>
After Getting the SHA1 hash of each file, We can use the following script from GitHub to do the comparison between the two CSV files: 
<span style="color: #6594e0; text-decoration-line: underline;"> [Compare-FileHashesList.ps1](https://github.com/SamuelArnold/StarKill3r/blob/master/Star%20Killer/Star%20Killer/bin/Debug/Scripts/SANS-SEC505-master/scripts/Day1-PowerShell/Compare-FileHashesList.ps1)</span><br>

# Powershell Hunting Tools
## Powershell ISE
The Windows PowerShell Integrated Scripting Environment (ISE) is a host application for Windows PowerShell.<br>
In the ISE, you can run commands and write, test, and debug scripts in a single Windows-based graphic user interface.

| ![Powershell ISE](/assets/images/threat-hunting/Tools/Powershell/powershell3.png) | 
|:--:| 
| *Powershell ISE* |

## Powershell AMSI
Antimalware Scan Interface (AMSI) was developed by Microsoft to protect users from malware and introduced for the first time in Windows 10. It allows an application to interact with any anti-virus installed on the system and prevent dynamic, script-based malware from executing.<br>
AMSI intercepts PowerShell, JavaScript, VBScript, VBA, or .NET scripts and commands in real time and sends them to the antivirus software for scanning, and this is where you can get the familiar message
"This script contains malicious content and has been blocked by your antivirus software".<br>

## PSHunt
PSHunt is a Powershell Threat Hunting Module designed to scan remote endpoints for indicators of compromise or survey them for more comprehensive information related to state of those systems (active processes, autostarts, configurations, and/or logs).<br>

📍 <span style="color:#7ba4d2">PSHunt Components/Modules:</span>
PSHunt is divided into several modules, functions, and folders. These modules are:
- Scanners 
- Surveys
- Discovery
- Utilities
- Analysis

Let's dive into these Components:<br>

↪ <span style="color:#7ba4d2">Scanners:</span> Used to rapidly scan remote systems for a single pience of information using remote queries.
  - Input: Target (DNS or IP)
  - Output: One Line (String or CSV)
  - Command: `Invoke-HuntScan.ps1` <br>

↪ <span style="color:#7ba4d2">Surveys:</span> Used to collect from each windows host comprehensive information such as:
  - Active Processes
  - Loaded Modules/Drivers
  - Active Connections
  - Accounts
  - Key Event Logs 
  - ... etc <br>

  ↪ <span style="color:#7ba4d2">Discovery:</span> Discovery functions and cmdlets are used to identify hosts on the network and build a target list that can be ingested by the scanners and survey deployment cmdlets. The following commands can be used: `Get-HuntTargets` and  `Invoke-HuntPortScan`. <br>

  ↪ <span style="color:#7ba4d2">Analysis:</span> This module provide 2 functions:
  - <span style="color:#a8a8a8">Survey Analysis:</span> Comapare survey results against reputation data from local store and VirusTotal. The commands used are for example `Update-HuntObject` and `Initialize-HuntReputation`.
  - <span style="color:#a8a8a8">File Analysis:</span> These functions are a set of utilities to analyze files and malware. The commands used are for example `Get-VTReport`, `Get-VTStaus` and `Get-Hashes`.

   ↪ <span style="color:#7ba4d2">Utilities:</span> Utility functions provide the base functionality for deployment and execution of surveys and scans. We can use `Invoke-HuntSurvey`, `Get-HuntSurveyResults` and `Invoke-HuntScanner`. <br>

  Installation: <span style="color: #6594e0; text-decoration-line: underline;"> [PSHunt](https://github.com/Infocyte/PSHunt)</span> 

## Kansa
Kansa is another tool that can be hugely useful for both threat hunting and incident response. It is decribed as "modular incident response framework in Powershell".<br>
For hunters, one of the biggest challenges they face can be establishing the baseline of "what is normal" in their environment. Kansa can help speed up that task tremendously.<br>
Installation: <span style="color: #6594e0; text-decoration-line: underline;"> [Kansa](https://github.com/davehull/Kansa)</span> 














    

   









<hr>
<!-- - <span style="color:#cad2ed"> Phishing: </span> <br> -->
 
> "To beat a hacker, you have to think like a hacker" 💙
<hr>
<p align="center">
  <img src="/assets/images/icons/cat.jpg" alt="Terminal Shortcuts" style="width:420px;height:320px;">
</p>
---
