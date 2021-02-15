# Detailed tutorial on SSH

#### Simple understanding of how SSH works: 
1. When the server installs an openssh-server and you install an openssh-client on your own computer, you can simply log in via ssh for remote control  
2. When logging in, you need to know the account name, ip address of the server, and the port of the server, then run: ssh {user_account}@host_ip_address -p{port_num}  
3. More details: public keys could replace the password for password-free logging in. Each connection will add the host keys of the server into the client for future check  

#### Different levels to work around ssh, depending on your familiarity and demand with ssh, 
        1. If you do not mind log in with other own account and do not want to get into detail, you can just follow guide 1 to install openssh-client and connect to server using others' account (certainly under others' permission)
        2. If you want to create your own account on the server via ssh, follow guide 2 to create your account(will be using others' account temporarily), and folllow 1.3 to connect to the server
        3. If you want to log in your own account wighout password(which is safer), follow guide 3 to generate public key

#### If you encount any problems, check the problem solving in Guide 5 to see if any solution already existed

#### Note: A common mis-manipulation is to run "ssh-keygen" on the server side, which shoule actually be done on your own computer to generate public key, but would affect others' use of ssh if the command is run on server.
