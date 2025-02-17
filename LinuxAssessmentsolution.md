#Firstly we create the "developers" group thus
	sudo groupadd developers
#Then we create the developers' accounts and add them to the developers groupusing a for loop.
#The -m option creates home directory for each developer, -G add the developer to the group, -s bin/bash sets bash as the default shell.
#Follow below link for screenshot
https://github.com/EngrBlinx/DevSecOps/blob/main/DevSecOPs1.PNG

#For the next question, we first ensure that the directory exist, from the screenshot, you can see that it doesn't exist
#So we have to create it, we had to create the path var/www first. the -p option ensures the entire path is created is missing, then we created the projects
#directory.
#next we changed ownership to ensure that the group "developers" has ownership of the directory, then we grant permission.
#Follow below link to see screenshot
https://github.com/EngrBlinx/DevSecOps/blob/main/DevSecOps2.PNG 
