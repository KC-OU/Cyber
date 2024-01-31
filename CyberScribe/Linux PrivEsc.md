![[Linux-PrivEsc-banner.webp|banner]]

# Linux Privilege Escalation

**Understanding Privileges in Linux:**

- **Multi-user system:** Linux allows multiple users to share the same system, each with varying levels of access and permissions.
- **Root user:** The most powerful account, able to control everything on the system.
- **Regular users:** Have limited privileges, restricted from performing certain actions that could compromise system integrity.

**Privilege Escalation:**

- **Concept:** The process of exploiting vulnerabilities or misconfigurations to gain unauthorized access to higher privileges, typically aiming for root access.
- **Attacker's goal:** Obtain complete control over the system to:
    
    - Steal sensitive data
    - Install malware
    - Modify system settings
    - Disrupt operations
    

**Common Techniques:**

2. **Exploiting Software Vulnerabilities:**
    
    - Attackers target bugs in applications or the operating system itself to gain elevated privileges.
    - **Example:** A buffer overflow vulnerability in a web server could allow an attacker to inject malicious code and execute it with root privileges.
    
4. **Abusing Configuration Errors:**
    
    - Misconfigured settings or weak security practices can create opportunities for privilege escalation.
    - **Examples:**
        
        - Writable system files that can be modified for privilege escalation
        - World-writable directories allowing the creation of malicious files
        - Weak passwords for privileged accounts
        - Incorrect file permissions
        
    
6. **Utilizing Social Engineering:**
    
    - Attackers deceive users into performing actions that grant them unintended privileges.
    - **Example:** Tricking a user into running a malicious script that grants the attacker root access.
    
8. **Leveraging SUID/SGID Binaries:**
    
    - Programs that run with elevated privileges, even when executed by non-privileged users.
    - **Example:** An attacker exploiting a vulnerability in an SUID binary to gain root access.

## Finding the users or system infomation

Finding the users system information is useful in Linux Privilege Escalation because depending on the system's version, release or even usable writable user paths and environment information can determine what Privilege Escalation can be used

### OS  Information 

```bash
(cat /proc/version || uname -a ) 2>/dev/null
lsb_release -a 2>/dev/null # old, not by default on many systems
cat /etc/os-release 2>/dev/null # universal on modern systems
```

**Example**
```bash
lsb_release -a 2>/dev/null # old, not by default on many systems
cat /etc/os-release 2>/dev/null # universal on modern systems
Linux version 6.5.0-14-generic (buildd@lcy02-amd64-031) (x86_64-linux-gnu-gcc-13 (Ubuntu 13.2.0-4ubuntu3) 13.2.0, GNU ld (GNU Binutils for Ubuntu) 2.41) #14-Ubuntu SMP PREEMPT_DYNAMIC Tue Nov 14 14:59:49 UTC 2023
Distributor ID:	Ubuntu
Description:	Ubuntu 23.10
Release:	23.10
Codename:	mantic
PRETTY_NAME="Ubuntu 23.10"
NAME="Ubuntu"
VERSION_ID="23.10"
VERSION="23.10 (Mantic Minotaur)"
VERSION_CODENAME=mantic
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=mantic
LOGO=ubuntu-logo
```

#### Path

Finding what paths, that you have permission to write to, or modify to hijack libraries or binaries

```bash
echo $PATH
```

**Example**
```bash
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
```
