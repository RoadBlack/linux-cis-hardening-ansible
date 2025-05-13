#  Manual Hardening – Rocky Linux 9 Server (CIS Level 1)

## High severity 
* Configure System cryptography policy
RULE-ID: xccdf_org.ssgproject.content_rule_configure_crypto_policy 
We have to make sure that there is no wide crypto policy set up to legacy
- At first we check if that was false positive by using command 
" update-crypto-policies --show" -> DEFAULT
- Then we have to update it so our system would not accept any SHA1 alogithm( Weak cryptography algorithm) 
sudo update-crypto-policies --set DEFAULT:NO-SHA1

- Let's check if that worked
sudo update-crypto-policies --show
DEFAULT:NO-SHA1
**Sucess**
* Prevent Login to Accounts With Empty Password
RULE-ID: xccdf_org.ssgproject.content_rule_no_empty_passwords
If an account is configured for password authentication but does not have an assigned password, it may be possible to log into the account without authentication. Let's fix that
- We have to check  /etc/pam.d/system-auth&password-auth and see if there is a nullok 
sudo vim /etc/pam.d/system-auth & password-auth 
Nullok has been sucessfully deleted from password sufficient 
- let's check if action was sucessfully applied by adding  a new user named test without any password
sudo adduser test
- Now let's try to log in 
su - test  
su: Authentication failure
**Success**
* Set Boot Loader Password in grub2
- The grub2 boot loader should have a superuser account and password protection enabled to protect boot-time settings. 
- in order to set a password without it being hardcoded in grub.cfg file we will use a simple command 
sudo grub2-setpassword 
**Sucess**
* Disable SSH Access via Empty Passwords 
ID:xccdf_org.ssgproject.content_rule_sshd_disable_empty_passwords
- It is a huge vurnerability, of Course previously we have disabled empty login by PAM but in case someone left it unconfigured we have to configure external shell so there would be no possibilities to make it happen. in order to secure it we need to dive into the SSH config 
sudo vim /etc/ssh/sshd.config 
PasswordAuthentication yes 
PermitEmptyPasswords no 
sudo systemctl restart sshd
- As previously lets see if the change was successfull 
ssh test@192.168.122.170
test@192.168.122.170's password: 
Permission denied, please try again.
**success**
## Medium Severity
* Install Aide, Build the database, configure AIde and make periodic scans using crontab
- What is Aide? aide is a advance intrustion detection system developed by REDHATthat cheks the integrity of the files.
- At first lets install AIDE
sudo dnf install aide -y 
- then lets initialize the aide database 
sudo aide -i 
- then lets move our database and  check it
mv /var/lib/aide/aide.db.new.gz /var/lib/aide/aide.db.gz
sudo aide --check
The attributes of the (uncompressed) database(s):
---------------------------------------------------
/var/lib/aide/aide.db.gz 
(cannot provide the information that is here)
**Success**

* configure AIDE to Verify the audit tools 
ID:xccdf_org.ssgproject.content_rule_aide_check_audit_tools


 
