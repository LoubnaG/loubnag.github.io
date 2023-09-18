---
layout: single
author_profile: true
readtime: 3 minute read
title: "Remote Working Challenge - LetsDefend"
description: "Analyzing XLS File"
header:
  teaser: /ctf-writeups/assets/images/RW.jpg
  overlay_image: /ctf-writeups/assets/images/RW.jpg
  overlay_filter: 0.5
classes: wide
ribbon: Challenge
bg: "#e87e0d"
last_modified_at: 2023-09-10
---
<span style="color:#909090">Analyzing XLS File</span>

Today we will solve the "Remote Working" challenge on LetsDefend. We will work on an XLS zipped file to answer the questions and complete the challenge.<br>

📌 File Downlaod : <br>
<span style="color:#da2039">NOTE : Do not open on your local environment. It is a malicious file.</span><br>
First we will download the zip file and extracted in our virtual environment to keep our local machine safe.<br>
The XLS file that should be analyzed is called "ORDER SHEET & SPEC.xlsm" as shown in the screenshot below :

| ![The Extracted XLS File](/assets/images/ctf-writeups/Remote-Work/RW1.png) | 
|:--:| 
| *The Extracted XLS File* |

📌 Analysis With VirusTotal : <br>
We uploaded the XLS File into VT and it seems to be malicious as indicated below : 

| ![File Analysis with VT](/assets/images/ctf-writeups/Remote-Work/RW2.png) | 
|:--:| 
| *File Analysis with VT* |

We will examine all the information provided by VT to answer the challenge questions.

🚩 What is the date the file was created? <br>
To answer this question, we will open up the *Details tab* and scroll down to *History* section where the creation time is indicated as below :

| ![File Creation Time](/assets/images/ctf-writeups/Remote-Work/RW3.png) | 
|:--:| 
| *File Creation Time* |

| ![Challenge Question 1](/assets/images/ctf-writeups/Remote-Work/RW4.png) | 
|:--:| 
| *Challenge Question 1* |

🚩 With what name is the file detected by Bitdefender antivirus? <br>
back again the *Detection tab*, we will look in the *Security Vendor'S Analysis* list for BitDefender.

| ![Malicious File name according to BitDefender](/assets/images/ctf-writeups/Remote-Work/RW5.png) | 
|:--:| 
| *Malicious File name according to BitDefender* |

The malicious XLS File is detected by BitDefender as *"trojan.generickd.36266294"* 

| ![Challenge Question 2](/assets/images/ctf-writeups/Remote-Work/RW6.png) | 
|:--:| 
| *Challenge Question 2* |

🚩 How many files are dropped on the disk?<br>
According to VirusTotal, ``files_dropped`` contains a list of all files are files specifically created and written to during an execution recording. These files are found under *Behavior tab* in the SandBox reports. We will go for Zenbox which indicate 3 dropped files.

| ![Dropped Files](/assets/images/ctf-writeups/Remote-Work/RW7.png) | 
|:--:| 
| *Dropped Files* |

We have 3 dropped files !

| ![Challenge Question 3](/assets/images/ctf-writeups/Remote-Work/RW8.png) | 
|:--:| 
| *Challenge Question 3* |

🚩 What is the sha-256 hash of the file with emf extension it drops? <br>
Always under *Behavior tab*, we ca find more details about these dropped files such as full path, file name and SHA256 Hash in the *Dropped Files* section :

| ![SHA256 Hash of dropped file with emf extension](/assets/images/ctf-writeups/Remote-Work/RW9.png) | 
|:--:| 
| *SHA256 Hash of dropped file with emf extension* |

| ![Challenge Question 4](/assets/images/ctf-writeups/Remote-Work/RW10.png) | 
|:--:| 
| *Challenge Question 4* |

🚩 What is the exact url to which the relevant file goes to download spyware? <br>
All URLs related to a malicious file are given under *Relations tab* in *Contacted URLs* section.<br>
VT has identified 2 URLs :

 | ![Contacted URLs](/assets/images/ctf-writeups/Remote-Work/RW11.png) | 
|:--:| 
| *Contacted URLs* |

| ![Challenge Question 5](/assets/images/ctf-writeups/Remote-Work/RW12.png) | 
|:--:| 
| *Challenge Question 5* |

<hr>
The Remote Working Challenge is completed successfully. This *Easy Level* challenge allows us to use VirusTotal and analyze a malicious XLS File to find creation time, dropped files, C2 URLs and much more !

| ![Challenge Badge](/assets/images/ctf-writeups/Remote-Work/RW13.png) | 
|:--:| 
| *Challenge Badge* |

<hr>
<p align="center">
  <img src="/assets/images/icons/cat.jpg" alt="Terminal Shortcuts" style="width:420px;height:320px;">
</p>
---
"To beat a hacker, you have to think like a hacker" 💙 
