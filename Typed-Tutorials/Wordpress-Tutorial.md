# Wordpress Install on Windows

[![How to Install Wordpress + Caddy Natively on Windows](https://img.youtube.com/vi/0A03C_NlMy0/0.jpg)](https://www.youtube.com/watch?v=0A03C_NlMy0)

### Downloads

[NSSM](https://nssm.cc/release/nssm-2.24.zip)

[Wordpress](https://wordpress.org/download)

[PHP 7.4](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbUlNZEU4dkE2bmVPMlN4WTFfOVJiOEFNU29DZ3xBQ3Jtc0tuMUdUQWp4SWhUNEM4VTRxblZvSEtqZDBOUGRlcnA5MXBGMXNCeldLdklYRTdRR3pzYk5KMDhFTTl6cEdiTG1jYVk4OXRvbU5JTmZaVzdva0lIVGhVX2VneHJlWGxFUEY4WHZXNUN6R3VjOElmaHlLVQ&q=https%3A%2F%2Fwindows.php.net%2Fdownloads%2Freleases%2Fphp-7.4.33-nts-Win32-vc15-x64.zip&v=0A03C_NlMy0)


**MAKE SURE YOU DOWNLOAD THE RC (RELIABLE CHANNEL) MSI**
**RUN THE GUI MSI Installer**
[MariaDB](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbTM1cS05N3cyNGhpNXV5Y0U3Q3hqN1VRSlJlQXxBQ3Jtc0tsOGFqa29zWHQwcnhFY3VldlMxWlNuM05JQ1JZR3owUHd5WUZHSXM2T0lDN3JiYy1pWTZtSUl6dnI0WU9veHFrOFZ0WVl6Y0NYc29qQ3E3Zm04ZHNVTXEybG10aUVwUHFQUTVxRjgwT2NTaXdWOEVmdw&q=https%3A%2F%2Fmariadb.org%2Fdownload%2F%3Ft%3Dmariadb%26p%3Dmariadb%26r%3D10.11.1%26os%3Dwindows%26cpu%3Dx86_64%26pkg%3Dmsi%26m%3Dacorn&v=0A03C_NlMy0)


### Setting Up PHP 7.X

1. Create a Directory in your C:\ for Tools IE. C:\Tools
2. Create two subdirectories in Tools
    2.1 NSSM
    2.2 php 
3. Extract php-7.xx insides to another directory
4. Extract NSSM.exe from \nssm-2.24\win64 to `C:\Tools\NSSM`

ie. C:\Tools\php

Add it to the enviroment variable paths
1. Search Advanced System Settings
 
 ![image](https://user-images.githubusercontent.com/35183970/213555428-c619d95f-58c6-4061-98a5-18b2e32bed7e.png) 

2. Select Enviroment Variables

![image](https://user-images.githubusercontent.com/35183970/213555578-278734bc-3658-40d8-ab41-215bbd49b9d8.png)

3. Select System Variables Path by double clicking

![image](https://user-images.githubusercontent.com/35183970/213555654-d7bc0204-cedc-4de2-853e-7bdc3fc2b645.png)

4. Add a New Path and type `C:\Tools\php`
5. Add another new path this time for NSSM `C:\Tools\NSSM`
6. Select OK
7. Select OK again
8. Then Select OK to cloe the systemp properties box
9. Close all Powershells and Terminal Windows So these settings Save

Uncomment These Settings
IE. Removing # from before each line
You can Search in Your Text Editor by Clicking CTRL+ F

```
*PHP.ini Settings*

    Navigate to the “increase memory_limit” line in the file and change the value from 128M to 512MB.
    The next step is to uncomment the following lines by removing ‘;’ before the lines. For example the “;extionsion_dir=ext” should become “extionsion_dir = ext”.
    Similarly uncomment the following lines by removing ‘;’ from the beginning of the line.

extension=bz2
extension=curl
extension=ffi
extension=fileinfo
extension=gd2
extension=gettext
extension=gmp
extension=intl
extension=mbstring
extension=exif
extension=mysqli
extension=odbc
extension=openssl
extension=pdo_mysql
extension=pdo_odbc
extension=pdo_sqlite
```


### Setting up PHP-CGI

1. Open up an Administrative Powershell.
2. type inside that powershell `NSSM install PHP`
3. Add to Path 
   
   3.1 `C:\Tools\php\php-cgi.exe`
   
   Add to Startup Dirctory
    
    3.2 `C:\Tools\php`
   
   Add to Argument
    
    3.3 `-b 127.0.0.1:9000`
4. Click Save
5. Start the Service
   `nssm Start php`

### MariaDB Setup


*RUN THE GUI MSI Installer*

1.TUTORIAL (FOLLOW STEPS 1-4)
       
  [MariaDB Install Guide](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbWl1SGRXNEMtTUFldVh2eGEweURDWm9MOUVNQXxBQ3Jtc0tsZk5HTFhCUm13eVF0M2p5QXlIREh5cWVFT3FHcnVTZkhDZ0ZUT01ZOWhiWWl2U1Y3bmN4bW9PdTRSSjdFSFdQNmVDdE1VWUtaamh4RE5kdTJhZHRhbnBreThjZFZVOFdKTWpPNGEwSUdma2YtZXhMTQ&q=https%3A%2F%2Fmariadb.org%2Fdownload%2F%3Ft%3Dmariadb%26p%3Dmariadb%26r%3D10.11.1%26os%3Dwindows%26cpu%3Dx86_64%26pkg%3Dmsi%26m%3Dacorn&v=0A03C_NlMy0)

2. TYPE MARIADB INSIDE YOUR SEARCH BAR

![image](https://user-images.githubusercontent.com/35183970/213558042-716e6651-39f1-4516-aead-341be0182cf9.png)

3. TYPE THE PASSWORD YOU CREATED in your installation
4.THEN Edit To Your liking
```
CREATE DATABASE wordpress;
use wordpress;
CREATE USER 'user'@'localhost' IDENTIFIED BY 'pass12345678?';
GRANT ALL ON *.* TO 'user'@'localhost';
flush privileges;
```
5. **If you cant remember your password for your MYSQL User* Use this command**

`DROP USER 'devilsdesigns'@'localhost';`

**Then re-enter this below**

```
use wordpress;
CREATE USER 'user'@'localhost' IDENTIFIED BY 'pass12345678?';
GRANT ALL ON *.* TO 'user'@'localhost';
flush privileges;
```

### Setting up Caddy

**Caddyfile Download**

[Wordpress Caddyfile](https://github.com/DevilsDesigns/Youtube-Docs/blob/main/Caddy-Examples/Wordpress/Caddyfile)

**Running Caddy inside the Caddy.exe Directory**

1. `cd C:\Caddy\Directory`
    ie. cd C:\Tools\Caddy

2. Running Caddy Manually
3. `./caddy run --config Caddy`
4. **Accept both permissions if a windows Pops up**

### TROUBLESHOOTING
**IF ITS NOT LOADING**
#### Allow App Through Advanced Firwall
1. Go to Control Panel
2. Search Firewall and Select Windows Defender Firewall

![image](https://user-images.githubusercontent.com/35183970/213559749-38c2c954-b6dc-410f-9a49-37e053009b5a.png)

3. Select Advanced Settings

![image](https://user-images.githubusercontent.com/35183970/213559824-42e45c0b-6fbf-40d9-a48b-ef207d2bb2ce.png)

4. Click Inbouns Rules

![image](https://user-images.githubusercontent.com/35183970/213559889-d4b5babc-fd5f-4281-91e9-a1a3e76cc615.png)

5. Click New Rule

![image](https://user-images.githubusercontent.com/35183970/213559970-66286a1b-96bc-4f70-8723-fc38c68c3446.png)

6. Check Port

![image](https://user-images.githubusercontent.com/35183970/213560049-55e11cc7-2bfc-4e19-b9b0-d6a42fa47bc1.png)


7. Add TCP Ports 9000  **(IF YOU HAVENT ADDED CADDY PORT YET DO SO AS WELL FOR 443, 80, 2019)**

![image](https://user-images.githubusercontent.com/35183970/213560266-e7541f33-ccac-481d-b23a-4488f92d7373.png)

8. Leave Default Click Next

![image](https://user-images.githubusercontent.com/35183970/213560324-1f5967a7-99ea-4865-a6b3-dbfb13244b14.png)


9. Leave Default Click Next

![image](https://user-images.githubusercontent.com/35183970/213560399-7dde8eb0-20dd-4026-b4e5-040b0c981b31.png)

10. Name the rule whatever you want

![image](https://user-images.githubusercontent.com/35183970/213560483-4553e086-acef-46ae-8241-deb9c1a1f315.png)

#### Checking Your Ports
1. Go to https://portchecker.co/ and see if your port 443 and 80 are open.
2. If they are not you need to make sure your router connected to your modem has those ports portforwarded for your computer hosting caddy.

Check out Our Discord if you need more help!
https://discord.gg/DtHUvGrp
