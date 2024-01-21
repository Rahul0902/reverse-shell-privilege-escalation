<h1>Reverse Shell & Privilege Escalation</h1>

<h2>Scenario</h2>
<a href='https://tryhackme.com/room/rrootme'>RootMe Challenge - TryHackMe</a><br><br>

<h3>Reconnaissance</h3>
I initiated an nmap scan to unveil active ports. Port 80 was open, showcasing HTTP, and port 22 revealed itself as accessible via SSH.<br><br>

![Screenshot 2024-01-21 at 17 30 54](https://github.com/Rahul0902/reverse-shell-privilege-escalation/assets/44233038/7b25910e-1e4b-47c4-a9cc-2b8f33515345)

Next, utilising the gobuster tool, I unearthed a hidden directory named /panel/. This covert path presented an intriguing opportunity—a file upload feature perfect for deploying my reverse shell.<br><br>
![Screenshot 2024-01-21 at 17 33 20](https://github.com/Rahul0902/reverse-shell-privilege-escalation/assets/44233038/f7a6d7d7-27ae-4a67-8491-0969760c92cc)

<h3>Obtaining A Shell</h3>

I found a reverse shell here: <a href= 'https://pentestmonkey.net/tools/web-shells/php-reverse-shell'>Pentestmonkey Reverse Shell</a> which I downloaded, and configured the file to utilise my IP and port 4444.<br><br>
![Screenshot 2024-01-21 at 17 49 03](https://github.com/Rahul0902/reverse-shell-privilege-escalation/assets/44233038/c522dd46-d51c-47b1-a7c9-1ba7e28a8b6b)

The site does not allow you to upload .php files but fortunatley allows .php5. I was able to upload the file 'payload.php5' containing the reverse shell.<br><br>
![Screenshot 2024-01-21 at 17 54 43](https://github.com/Rahul0902/reverse-shell-privilege-escalation/assets/44233038/168c8a93-8455-4e6b-8d5c-9d55c8bd083e)

Launching a netcat listener on port 4444, I activated the payload.php5 within the site's uploads.<br><br>
![Screenshot 2024-01-21 at 17 56 51](https://github.com/Rahul0902/reverse-shell-privilege-escalation/assets/44233038/f8b2e503-d7a4-4bd7-8651-6eb74bc96642)<br><br>
![Screenshot 2024-01-21 at 18 02 41](https://github.com/Rahul0902/reverse-shell-privilege-escalation/assets/44233038/487b2e17-dbe1-4b2e-874e-f3113446c302)

<h3>Privilege Escalation</h3>
With a foothold secured I searched for files with SUID permission, and was able to identify the file /usr/bin/python.<br><br>

![Screenshot 2024-01-21 at 18 12 18](https://github.com/Rahul0902/reverse-shell-privilege-escalation/assets/44233038/fb93d03f-1fdc-4fbc-8e6f-9b88198c178a)


From here I leveraged a gtfobins privilege escalation method and ran this within my shell.<br><br>
<img width="818" alt="Screenshot 2024-01-21 at 19 46 39" src="https://github.com/Rahul0902/reverse-shell-privilege-escalation/assets/44233038/82b481bd-9e3c-4913-8638-76ba8750664a"><br><br>

![Screenshot 2024-01-21 at 18 35 20](https://github.com/Rahul0902/reverse-shell-privilege-escalation/assets/44233038/a3726206-c219-437e-97fb-be9adff4d656)

The two flags I needed to identify where found in a root.txt and user.txt file. The root.txt file was within the root directory and I was able to find the user.txt file by running a find command.<br><br>
![Screenshot 2024-01-21 at 18 35 36](https://github.com/Rahul0902/reverse-shell-privilege-escalation/assets/44233038/2d326200-1ddf-4cff-86cd-f4a0c4e9e304)<br><br>
![Screenshot 2024-01-21 at 18 36 03](https://github.com/Rahul0902/reverse-shell-privilege-escalation/assets/44233038/54af7ca8-ba56-473a-94c7-d1262efed4f5)


