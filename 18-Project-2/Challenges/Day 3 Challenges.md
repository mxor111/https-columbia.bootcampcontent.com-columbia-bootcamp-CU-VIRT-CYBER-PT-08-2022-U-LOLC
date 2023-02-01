## Day 3 Solution File: Attacking Rekall's Windows Servers

### Flag Solutions

#### Flag 1: 

* Searching GitHub should lead to finding the [totalrekall GitHub page](https://github.com/totalrekall). Searching the `site` repository will lead to the [`xampp.users` page], which contains the credentials ``, as the following image shows: 

#### Flag 2: 

* From the Kali machine, a port scan of the subnet that the Kali machine is on: 
	
* The port scan will reveal several ports open on Win10, one of which is HTTP, as the following image shows: 

* Going to this page displays a prompt for credentials, as the following image shows:

* The credentials cracked from the discovered GitHub page, will grant access.

* Inside is `***.txt`, as the following image shows: 

#### Flag 3: 

* Returning to the port scan results will show as the following image shows: 

* Once logged into as anonymous, you can download and read the flag.

#### Flag 4: 

* Return to the port scan results, and note that the SLMail service is running on port AND on port, as the following image shows:


  - Port * is the port required for this exploit.

* Using `searchsploit` shows a Metasploit module for that version of SLMail, as the following image shows:

* Loading up Metasploit via MSFconsole, loading the SLMail module and setting the RHOSTS to *, and then running the exploit will grant a Meterpreter shell, as the following image shows:

* Listing the directory files will show `', which can be read with `cat` from within Meterpreter, as the following image shows:

#### Flag 5: 

* The hint about "scheduled tasks" should suggest looking at scheduled tasks on the system. 

#### Flag 6: 

* After compromising SLMail using Metasploit, the Meterpreter shell will be the `SYSTEM` user. `kiwi` can then be loaded, as the following image shows:

* By using the command `lsa_dump_sam`, `kiwi` will reveal a user named ``, as the following image shows:

* Cracking the NTLM password will reveal Flag 6: 

#### Flag 7

* Using the `search` command in Meterpreter.

#### Flag 8: 

* Using `kiwi` to dump the cached credentials on Win10 will reveal cached:

* Store the username and hashed password into a file, then crack it

* These new credentials have access to the Server2019 machine.

* By entering a command shell within Meterpreter, you can list the users:

#### Flag 9: 

* Listing the files, `` can be read via `cat` in Meterpreter

#### Flag 10:

* Using `kiwi` to DCSync the `` user on will reveal their NTLM password hash, which is.

  ![A screenshot depicts listing `flag10` via DCSync.](Images/flag10.PNG)

---
© 2022 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.  
