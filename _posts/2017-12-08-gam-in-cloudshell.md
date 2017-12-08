---
layout: post
title:  Running the Google Apps Manager (GAM) in Google Cloudshell
---

## Installing GAM
```bash
graham_dunn@cloudshell:~$ bash <(curl -s -S -L https://git.io/install-gam)
Checking GitHub URL https://api.github.com/repos/jay0lee/GAM/releases for latest GAM release...

Getting file and download URL...

Downloading file gam-4.32-linux-x86_64.tar.xz from https://github.com/jay0lee/GAM/releases/download/v4.32/gam-4.32-linux-x86_64.tar.xz to /tmp/tmp.tqWNb5zHeV.

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   618    0   618    0     0   3407      0 --:--:-- --:--:-- --:--:--  3414
100 8810k  100 8810k    0     0  8955k      0 --:--:-- --:--:-- --:--:-- 58.5M
Extracting archive to /home/graham_dunn/bin

Finished extracting GAM archive.

Adding gam alias to profile file /home/graham_dunn/.bashrc.

Can you run a full browser on this machine? (usually Y for MacOS, N for Linux if you SSH into this machine) N

GAM is now installed. Are you ready to set up a Google API project for GAM? (yes or no) no

You can create an API project later by running:

gam create project

Here's information about your new GAM installation:

GAM 4.32 - https://git.io/gam
Jay Lee <jay0lee@gmail.com>
Python 2.7.14 64-bit final
google-api-python-client 1.6.3
oauth2client 4.1.2
Linux-3.16.0-4-amd64-x86_64-with-debian-8.9 x86_64
Path: /home/graham_dunn/bin/gam
GAM installation and setup complete!

Please restart your terminal shell or to get started right away run:

alias gam="/home/graham_dunn/bin/gam/gam"

graham_dunn@cloudshell:~$ alias gam="/home/graham_dunn/bin/gam/gam"
```
* `tar zxvf gam.tgz`
* Upload files gam-onboard.sh support
* ` chmod 755 gam-onboard.sh support-site-access.sh`
* `sudo mv gam-onboard.sh support-site-access.sh /usr/local/bin`
* sudo apt install pwgen


 
## References
- https://github.com/jay0lee/GAM/wiki
