# Server Protocol in ICL
This protocol is set for effective and safe use of the server.  
The protocol includes usage scheduling, remote control of the server, several rules to follow, and a detailed tutorial on the use of ssh.

#### 1. When you plan to use the server, you'll need to check and schedule on the [Server Availability Sheet](https://docs.google.com/spreadsheets/d/1SJabt0CI8YMfprissTm2YH9iNwee4MdWShxkVchYhOw/edit?usp=sharing):  
            1. Sigh up: sign your name and highlight the intensity of resource consumption.  
                Green means you're doing some light-load jobs, so that others are allowed to do light-load tasks simultaneously.  
                Red means your task is load-intense and do not recommend simultaneous use from other users.   
                
            2. Check: If there is already someone else occupying the time slot:  
                When the slot is green, you can append your name in the sheet and do some light jobs on the server. But high-intensity work is not recomended.   
                When the slot is red, you're not recommended to use the server at the same time. you can schedule a late time or coordinate with the current user if you're in hurry.  
                
#### 2. Remote control of the server:
            1. The command to ssh into the server:
                        ssh {user_account}@{host_ip_address} -p{port_num}
                        
            2. Currently, you can use:
                        ssh {user_account}@0.tcp.ngrok.io -p12783
                        
            3. If you cannont log in, it is highly possible that the port_num is changed. Check and ask for the update in the "stack-overflow" channel on slack
            
            4. For the server manager: you can update the port_num in the slack whenever you find a change, so that you won't be bothered by questions from clients
            
#### 3. If you're new or having problems with ssh, it's recommended to refer to the [Detailed tutorial on ssh](https://github.com/Letian-Wang/Server-Protocol/blob/main/Detailed%20tutorial%20on%20SSH.md), so that no further trouble is made to other users. The tutorial includes:
            1. Simple understanding of how SSH works
            2. Different levels to work around ssh
            3. How to set up SSH
            4. How to create your own account safely
            5. How to log via public keys
            6. How to manage the server
            7. Solutions to some frequent problems

#### 4. Rule: do not manipulate others' account and the backend files before communicating with others and the server manager. 

#### 5. Recommendation: create your own virtual environment, so you're free to set your own settings and avoid setting conflict.




