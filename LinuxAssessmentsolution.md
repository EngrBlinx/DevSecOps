Firstly we create the "developers" group thus
	sudo groupadd developers
Then we create the developers' accounts and add them to the developers group using a for loop.
The -m option creates home directory for each developer, -G add the developer to the group, -s bin/bash sets bash as the default shell.
Follow below link for screenshot
https://github.com/EngrBlinx/DevSecOps/blob/main/DevSecOPs1.PNG

------------------------------------------------------------------------------
For the next question, we first ensure that the directory exist, from the screenshot, you can see that it doesn't exist
So we have to create it, we had to create the path var/www first. the -p option ensures the entire path is created is missing, then we created the projects
directory.
next we changed ownership to ensure that the group "developers" has ownership of the directory, then we grant permission.
Follow below link to see screenshot
https://github.com/EngrBlinx/DevSecOps/blob/main/DevSecOps2.PNG

-------------------------------------------------------------------------------
Next, we restrict SSH for two developers.
To do this, we edit the SSH config file -> sudo nano /etc/ssh/sshd_config this will open the file in the nano text editor, then add these lines and save
Match User dev1,dev2
	PasswordAuthentication no
	PermitTTY no
Assuming we want to restrict dev1 and dev2
Then retart SSH service to apply changes
	sudo systemctl restart sshd
See screenshot -> https://github.com/EngrBlinx/DevSecOps/blob/main/DevSecOps3.PNG

----------------------------------------------------------------------------------
The next question is about system monitoring

Check Overall Disk Usage
	df -h
Find Large Log Files
	du -ah /var/log | sort -rh | head -10

To get the top CPU-consuming processes in a sorted list:
	ps aux --sort=-%cpu | head -10
Check Memory Usage
	ps aux --sort=-%mem | head -10
See the screenshot ->https://github.com/EngrBlinx/DevSecOps/blob/main/DevSecOPs5.PNG
 
To monitor real-time system log
        htop
See the screenshot -> https://github.com/EngrBlinx/DevSecOps/blob/main/DevSecOPs4.PNG

------------------------------------------------------------------------------------
The next question is Application management

Firstly, we install nginx thus
	sudo apt update && sudo apt install -y nginx
The -y option answers yes to all prompts
See screenshot -> https://github.com/EngrBlinx/DevSecOps/blob/main/DevSecOPs6.PNG

Then we enable nginx to start on boot thus
	sudo systemctl enable nginx
Then start the nginx service
	sudo systemctl start nginx
To check if nginx is running properly
	sudo systemctl status nginx
See screenshot -> https://github.com/EngrBlinx/DevSecOps/blob/main/DevSecOPs7.PNG

To ensure it starts automatically if it crashes, we have to setup systemd to do so
	sudo systemctl edit nginx
then add the following lines under [Service]
	Restart=always
	RestartSec=5s
Save the file and reload systemd
	sudo systemctl daemon-reload
	sudo systemctl restart nginx
See screenshot -> https://github.com/EngrBlinx/DevSecOps/blob/main/DevSecOps9.PNG
To confirm the restart, manually kill the service
	sudo pkill -9 nginx
After about 5 seconds, check status
	sudo systemctl status nginx

-----------------------------------------------------------------------------------
We will use an uncomplicated firewall to block all incoming traffic except SSH and HTTP

 Install ufw if not already installed
	sudo apt update && sudo apt install ufw -y

Allow SSH (port 22) and HTTP (port 80)
	sudo ufw allow 22/tcp
	sudo ufw allow 80/tcp

Deny all other incoming traffic
	sudo ufw default deny incoming
	sudo ufw default allow outgoing

 Enable the firewall
	sudo ufw enable

See screenshots -> https://github.com/EngrBlinx/DevSecOps/blob/main/DevSecOPs10.PNG
https://github.com/EngrBlinx/DevSecOps/blob/main/DevSecOPs11.PNG

Next use ss to check for open ports
	sudo ss -tulnp
See screenshot -> https://github.com/EngrBlinx/DevSecOps/blob/main/DevSecOPs12.PNG
