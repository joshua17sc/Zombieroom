# Zombieroom

Zombie Apocalypse TryHackMe room

Hasniak Inc has created a new drug for fighting the common cold. It has some weird side effects. Apparently, it makes zombies.
It spreads just as easily as the common cold, if not easier.
It has gotten out and is wreaking havoc on civilization as infected zombies seek out living victims. The virus creates a symbiotic relationship, but the human host dies much too quickly for the virus, so it seeks new hosts in order to live.

Virus got out because one of the scientists (Dr. Shoe) is evil. Dr. Rosenthal is suspicious of shoe. Shoe has created a cure, in secret. He has also kept a diary. But, it appears he has disappeared.

There is a survivor community. They have the means to spread the cure if they can get Dr. Rosenthal's research notes.

TryHackMe room will introduce the scenario, and walk the player through to finding the research notes. 

Tasks:

Rabbit hole:  ftp anonymous share with user.txt giving ftp forJohn:password(maybe no password for a brute force(quick one, first 500 or rockyou)) => nothing 

1 - Hasniak site on Ubuntu Webserver
     Landing page with Hasniak logo, a few words about saving the world and the drug they're getting approved by the FDA. Also, introduces the CEO, Shoe, and Rosenthal.
Clues in their bios will be used later.
2 - Hasniak login page (sqli)
3 - file upload, or webshell behind the login page

4 - gets access to the Webserver itself, find the emails from the CEO about infighting between Shoe and Rosenthal, 
5 - privesc - Find the super hard password required for accessing the next machine

6 - Shoe's computer - RDP win10 machine
Find the evil plan
7 - privesc - find the evil formula that has a piece of information needed to go with Rosenthal's research for the final solution (last flag) and more about Rosenthal, reminder of bio stuff for better-guessing login

8 - Rosenthal's computer - Ubuntu desktop with ssh. Find personal notes.
9 - privesc - find research notes and second half of final flag





Just playing around let me know if you want more logo options or which one you like? Not sure about the border came with my hijacked logo image, 





Masked ppl 
creepy
https://unsplash.com/photos/wDz6iigThrg




Zombies

https://unsplash.com/photos/f7NnOkM1yeU

https://unsplash.com/photos/pF81NgZQsmw


Doctors
Masked doctor
https://unsplash.com/photos/l-NIPb-9Njg



Ideas -  I think I got shoe and rose mixed up.  

Machine 1 tasks:
1 Use SQL injection to exploit form to get patient portal creds.
2 Use upload form inside patient portal to get a shell
3 Find chat logs and encryption key in Shoe's folder.
4 download the encrypted file from FTP, decrypt.  
5 Use decrypted ingredient list as wordlist to obtain Rosenthals password.  (his user/hash is in the sql db, or could be verified by connection to machine 2.

Some sort of privesc to get access to root flag and Shoe's folder.  Thinking something easy like sudo with Rosenthal's creds 

Machine 1:
Port 21:  Anonymous login

incomingtransfer.log: Upload from user shoe, lab machine IP, timestamp, cureingredients.encrypted:  Encrypted file with complex key. 

Unencrypted file:
drug1 10%
drug2 15%
drug3 12%
ketamindolphin  50%   
(drug stuff) 


Port 80/443:  
Hasniak site on Ubuntu Webserver. Could be custom-created or popular CMS like WP, Joomla, etc.

Landing page: 
Hasniak logo, a few words about saving the world, and the cure for the common cold they're getting approved by the FDA.  A megacorp company

About us page:  
Also, introduces the senior researcher Shoe, and junior researcher Rosenthal.  

Clinical Trials:
We will pay you $10,000 to become a volunteer to test vaccines.  
This is a SQLi form, not a new registered user form.  

Patient Portal Login:
Log in to a patient portal.  The credentials to log in can be found in the patient's table in the DB through the sqli

Patient Portal:
Shows patient info and has an upload box for "important medical documents"
This form is exploitable to upload a web shell or reverse shell.

Foothold:
upon getting access to the machine, there are 2 user folders in the home dir

Rosenthal's Folder
-->Chatlog1.txt

Shoe:  Hey Rosenthal, how is that cure coming?  I am getting a lot of pressure from Megacorp.  They want to go into production by Q3.

Rosenthal:  It's not ready, if it was easy then it would have already been done. 

Shoe:  I know it's not easy, that's why I hired you. I need to tell them something before we both get fired.  Megacorp has so much money invested, we have to deliver!

Rosenthal:  Here we go again, all everyone cares about is money and profits, I wish there was a cure for that!  I am trying to cure something that billions of people get sick from every year, that's what I care about.  

Shoe: I care about the people too, please hurry!

-->Chatlog2.txt

Shoe:  I just got out of a meeting, we have until the end of the week to finish the cure.  I've got kids, I can't lose this job!  

Rosenthal: Shoe, I am tired of you pestering me, I would be done by now if you weren't hounding me all the time.  I can't believe you're the senior researcher, I've been doing all your work for years!  

Shoe:  It doesn't have to be perfect, just encrypt what you have and put it on the FTP server, and send me the key, by Friday!

Friday timestamp:
Rosenthal:  I had a breakthrough last night, it's perfect!  This will cure everything wrong in this world!  I've uploaded the file to the FTP and the key is: pa1ien1-z3r0 

Shoe: Great news!  I just sent it to megacorp and our clinic to begin trials!  I knew you could do it!

Rosenthal has left the chat.

Shoe: Rosenthal?
Shoe: Rose?
Shoe: Rosenthal?

note1:
The human race is so stupid, they only care about themselves and money.  If they can't think.... There would be no problem

pa1ien1-z3r0 




Shoe's Folder ( must privesc)
-->email1.eml

to Joe@megacorpone.com

Shoe:  Mr. CEO,  I am pleased to tell you that we have completed our research and it is located on the FTP site.  

Joe Sheer:  About Time! You're lucky I haven't fired you yet, maybe I still will.  If there is just ONE hiccup with the FDA or clinical trials, you will be cleaning monkey poop for the rest of your life! 

--> email2.eml

From Joe@megacorpone.com:
To: allemployees@hasniak.com

What have you done!?!?!? This is not the cure you promised, it is a plague, it's a zombie Apocalypse!   There isn't much time, we've never seen anything spread so quickly.   The only hope the human race has is if we can somehow reverse it, but we need access to your network!   Our VPN connection to your network is down, is the service running?   Someone with privileges must launch the megacorp_vpn service on the lab machine before we are all infected. 



Machine 2 (lab machine) tasks:
using information from ftpupload.log and Rosenthal's password, connect to using rdp/vnc.  

Shortcut to start megacorp_vpn service on desktop, needs admin privs to run it though.  

research document in my docs.  Something here is the key to escalate and/or to path to another machine.  





