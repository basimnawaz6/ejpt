
**Key info for vulnerability scanning is Service Version**

 #COMMAND 
- search type:exploit name:MySQL 5.5

#SearchSploit 
- gives exploits within msf framework and exploit db
- **searchsploit**  "Microsoft Windows SMB" | grep -e "Metasploit"
  
#Metasploit-autopwn 
- Its a plugin as a (github repo) that lists all the available exploits for open port and running services on runtime.
- db_autopwn -b -t -PI 445

#Windows-IIS
- A web server by ms that can host asp.net and php web apps  

#WebDAV (**Web-based Distributed Authoring and Versioning**)
- Set of extensions to **HTTP** allowing users to collaboratively edit and manage files on remote servers.
- **WebDAV requires authentication**

#davtest
- Used to scan/authenticate/exploit WebDAV server (Pre-installed) 
- davtest -auth bob:password -url http://10.1.1.17/webdav 
- incase of unauthorization (-auth bob:password)
- the above cmd checks what type of files can be executed/uploaded on the webdav server


  #cadaver
- For file upload, download, on-screen display for webdav.
- It provides a shell like ftp/ssh

#Hydra 
- hydra -L /target/to/user.txt -P /target/to/passwords.txt 10.1.1.17 http-get /target/dir
- target directory to be mentioned if target has multiple directories
- http-get for web servers

#PRO-TIP
Be very vigilant for brute force attacks as they may initiate **DOS ATTACKS** 

**What is a backdoor?**  #Inside-secret-room
A backdoor is tool/script, often malicious code or a special account, that lets an attacker gain unauthorized access to a system, bypassing its standard security checks.

**What is Remote Code Execution?**  #Entrypoint
Attacker remotely writes commands/codes to target.

**RCE can be used to create a backdoor**