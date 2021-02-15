# Server-Protocol
This protocol is set to for effectiveand and safe use of the server, as well as avoiding usage conflict.   
The content includes usage scheduling, remote control of the server, several rules to follow, a detailed tutorial on the use of ssh.

#### 1. When you plan to use the server, you'll need to schedule and check the [Server Availability Sheet](https://docs.google.com/spreadsheets/d/1SJabt0CI8YMfprissTm2YH9iNwee4MdWShxkVchYhOw/edit?usp=sharing):  
            1. Sign your name and highlight the intensity of resource comsuption.  
                Server Availability Sheet:   https://docs.google.com/spreadsheets/d/1SJabt0CI8YMfprissTm2YH9iNwee4MdWShxkVchYhOw/edit?usp=sharing
                Green means you're doing some light jobs that do not compete on the resources with other users.   
                Red means the load is intense and do not recommend simultaneous usage.   
                
            2. If there is already someone else occupying the time slot:  
                When the slot is green, you can append your name in the sheet and do some light jobs on the server. But high-intensity work is not recomended.   
                When the slot is red, you're not recommended to use the server at the same time. you can schedule a late time or coordinate with the current user if you're in hurry.  
                
### 2. The command to ssh into the server:
            '''
            ssh {user_account}@host_ip_address -p{port_num}
            '''
           If you cannont log in, it is highly possible that the port_num is changed. Check the update in the "server" channel on slack
           
           (TODO: server channel)


### 3. It's recomended to create your own virtual environment, so you're free to set your own settings and avoid setting conflict.
### 4. Do not manipulate others' account and the backend files before communicating with others and the server manager. 
### 5. If you're not sure about using ssh, it's recommended to refer to the "Detailed tutorial on ssh", so that no further trouble is made to other users.

The Server Policy in ICL
