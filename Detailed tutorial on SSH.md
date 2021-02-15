# Detailed tutorial on SSH
## This tutorial includes: 
  1. [Simple understanding of how SSH works](#-1.-Simple-understanding-of-how-SSH-works:-)
  2. [How to set up SSH](#guide-1)
  3. [How to create your own account safely](#guide-2)
  4. [How to log via public keys](#guide-3)
    
#### 1. Simple understanding of how SSH works: 
1. When the server installs an openssh-server and you install an openssh-client on your own computer, you can simply log in via ssh for remote control
2. When logging in, you need to know the account name, ip address of the server, and the port of the server, then run:

               ssh {user_account}@host_ip_address -p{port_num}  
3. More details: public keys could replace the password for password-free logging in. Each connection will add the host keys of the server into the client for future check  


#### 2. Different levels to work around ssh, depending on your familiarity and demand with ssh, 
1. If you do not mind **logging in with other's account** and do not want to get into detail, you can just follow [Guide 1](#guide-1) to install openssh-client and connect to server using others' account (certainly under others' permission)  
2. If you want to **create your own account** on the server via ssh, follow [Guide 2](#guide-2) to create your account(will be using others' account temporarily)  
3. If you want to **log in your own account wighout password** (which is safer), follow [Guide 3](#guide-3) to generate public key


#### 3. If you encount any problems, check [Guide 5](#guide-5) to see if any solution already existed

#### 4. If you are managing SSH server, check some basic operations in [Guide 4](#guide-4)

#### 5. Note: A common mis-manipulation is to run "ssh-keygen" on the server side, which shoule actually be done on your own computer to generate public key, but would affect others' use of ssh if the command is run on server. We should avoid doing this.


#### Guide 1: 
if you are a client connecting to the server: (all commands are run on your local computer)
    1. (first time using ssh) check if ssh client is installed on local computer:
        ssh
    2. (first time using ssh) install ssh client:
        sudo apt-get install openssh-client
    3. connect to server:
        ssh {user_account}@host_ip_address -p{port_num}

    Detailed intro to ssh (including how to install): 
        https://phoenixnap.com/kb/ssh-to-connect-to-remote-server-linux-or-windows
        
#### Guide 2: if you want to create your own account on the server:
    1. log in the server by an existing account:
        ssh {existing_user}@{host_ip_address} -p{port_num}
    2. add new user:
        sudo useradd -s /bin/bash -d /home/{new_user}/ -m -G sudo {new_user}
    3. set the password for the new user:
        sudo passwd {new_user}
    4. (optional) if you mis-create your account, you can delete your account as below, and go back to step 2:
        sudo deluser --remove-home {newuser}
    5. (Note) Do not run ssh-keygen on the server side, this could changed the host keys and others users could not log in

    Detailed explanation on adding account: 
        https://www.cyberciti.biz/faq/create-a-user-account-on-ubuntu-linux/
    
#### Guide 3: If you want to log in without password by setting up public key: (all commands are run on your local computer)
    1. Create RSA key on your own computer:
        mkdir -p $HOME/.ssh
        chmod 0700 $HOME/.ssh
        ssh-keygen -t rsa (Attention: this has been be run on your own computer, rather than on the sever, otherwise other users cannot not log in)
    2. Send RSA key to the server:
        ssh-copy-id -i ~/.ssh/id_rsa.pub {your_user}@{host_ip_address}
    3. log in via ssh free of passwd:
        ssh {your_user}@{host_ip_address} -p{port_num}

    Detailed explanation on logging without password via public key:
        https://www.cyberciti.biz/faq/ubuntu-18-04-setup-ssh-public-key-authentication/


#### Guide 4: if your are managing the server and any thing goes wrong, you can check:
    1. Whether the remote computer is turned on, and has a network connection.
    2. SSH server applications need to be installed and enabled.
        1. check if ssh server is installed: 
            ssh localhost
        2. install ssh server: 
            sudo apt-get install openssh-server ii
    3. You need the IP address or the name of the remote machine you want to connect to.
        IP address: hostname -I
        SSH port: sudo vim /etc/ssh/sshd_config (then serch for "port", update the port if updated)
    4. check the host keys fingerprint as in etc/ssh/ssh_host_rsa_key
        ssh-keygen -l -f ssh_host_rsa_key.pub
        ssh-keygen -l -f ssh_host_dsa_key.pub
        ssh-keygen -l -f ssh_host_ed25519_key.pub
        ssh-keygen -l -f ssh_host_ecdsa_key.pub
    5. Firewall settings need to allow the remote connection.

#### Guide 5: Problem solving
        1. if you are encountering:
                @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
                @    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
                @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
                ...
                The fingerprint for the ECDSA key sent by the remote host is
                SHA256:NjdBmIp/GqlpSvAM69JtFVlGZoQ6VRWnWSXXmpsZIlk.
                ...     
                Offending key for IP in /home/user/.ssh/known_hosts:6
                ...

            problem description:
                Each time the client is connected to the server, the host keys would be saved in the home/local_user_name/.ssh/known_hosts on the client side.  
               The host keys are used to comfirm that the client is connecting to the right server through the route used before, which can avoid being redirected to an imposter computer.     
               When the host keys are different from before, the ssh would warn to request a check on the host keys of the server.  
              
           Quick solution(one of the three would work):
                  1. ssh-keygen -R {host_name}
                 2. rm home/{local_user_name}/.ssh/known_hosts
                  3. just delete the {6 line}(shown in the error message) of the /home/user/.ssh/known_hosts
          
           Detailed solution(when you cannont solve by the quick solution):
              The host keys are automatically generated upon installation of ssh-server. But could also be regenerated.  
              Such problem could simply spring from changes on the server(re-install ssh, ssh-keygen, system upgrade), but coulde also be inccured by a malicious man-in-the-middle attack.  
              For the safety of our resources and codes on the server, we'd better check with the manager to ensure the fingerprint is consistent with that on the server.
             Fingerprint is the short-version host keys, need to be calculated by running some command

          for client: 
             1. Ask the manager for the fingerprint, and compare that with the fingerprint shown in the termnial:
                  1. find which key is shown in the error message: in this example, we get the "ECDSA key"
                  2. find the fingerprint in the error message: in this example, we get the "SHA256:NjdBmIp/GqlpSvAM69JtFVlGZoQ6VRWnWSXXmpsZIlk"
                 3. Compare that with fingerprint provided by the manager. If it's consistent, go on with the quick solution again. If still not work, we are under a malicious attack

         for server: 
             1. according to which key is changed, find the key on the server in the directories: (dsa, ecdsa, ed25519, rsa are different algorithms to generate public key)
                  /etc/ssh/ssh_host_dsa_key
                  /etc/ssh/ssh_host_ecdsa_key
                  /etc/ssh/ssh_host_ed25519_key
                  /etc/ssh/ssh_host_rsa_key
             2. Generate the fingerprint by: 
                  ssh-keygen -l -f ssh_host_rsa_key.pub, 
                provide it to the client for comparison. Note that SHA256 is a new-version encoding of the the keys

             3. The reason: The system may undergoes a majory system upgrade, or the keys are re-generated by reinstalling the ssh or by "ssh-keygen"

         Detailed explanation on public key/host key:
             public key: https://www.ssh.com/ssh/keygen/
             client operation: https://help.dreamhost.com/hc/en-us/articles/217239087-Updating-host-keys
             host key: https://envsci.rutgers.edu/computing_services/docs/Update_Host_Key_in_SSH.pdf
             generate fingerprint: https://www.unixtutorial.org/how-to-inspect-ssh-key-fingerprints/
