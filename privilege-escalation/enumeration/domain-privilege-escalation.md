# Domain Privilege Escalation

* privilege escalation just means that if you are not supposed to have admin rights and you doing some stuff got admin rights, this is called privilege escalation.
* In this article we will discuss on authority of admin account

## Privileges in windows

1. Guest
2. Standard User with UAC restriction
3. Standard User without UAC
4. Admin User `Administrator`
5. System User \(highest privileges\) `NT AUTHORITY\SYSTEM`

## Local level privilege escalation vs Domain level privilege escalation

After Local level privilege escalation we get `NT AUTHORITY\SYSTEM` authorization. There is no possibility of using this account for other machine access.

After Domain level privilege escalation we get`MYDOMAIN\mike` authorization. It could be such that john has authorization to more than one machine.

![local account vs domain account](../../.gitbook/assets/image%20%2810%29.png)

## A hypothetical scenario

* Given we have an internal environment that we are try to get into, say "mydomain.org".
* You found the weakest system in the network, which was running some legacy OS and you successfully compromised it.
* But what to do now? You know what ever information is present in that compromised system. But there are a lot of other system in the network. 
* We then try to get the lateral movement to the other machine using the compromised machine.
* This could be achieve in many ways, but lets considered a way where you found some other machine in the same network of that of the compromised machine, and you started targeting those machine from the compromised machine.
* You then found slowly some vulnerabilities and gradually increased your count of compromised machines. But we have to scan every machine, find the vulnerability and know the exploit for that particular machine, which is a time consuming job.

## Alternative approach

An alternative way could be, say when we compromised the first machine, we fetched 3 different domain accounts.

* These usernames have different types of authorization. Like say you found three users 
  * MYDOMAIN\mike
  * MYDOMAIN\john
  * MYDOMAIN\admin\_kim
* Here "mike" account just have local administration privileges, means the account "mike" is only allowed to login to one system i.e. our compromised machine. The account "mike" is useless if we use it to login to other system, even in the same network or any other network machine. So for analogy mike could be an employee.
* Next we have "john" account, which has more access than "mike" account. Using "john" account I was able to access all the system in the same network of that of the compromised machine. The account "john" has more authorization than account "mike". But account "john" was useless for machines on other networks. For analogy john could be manager of mike.
* Next we have admin\_kim, now using this account I was able to access all the machine either in the network or any other network. Which means admin\_kim has more authorization than john and probably the highest authorization possible. For analogy kim could be a administrator who manages all the system in the complete organization. 
* "admin\_kim" is a more authoritative domain account, as compared to other domains accounts like "mike" and "john"

1. **Local Privilege escalation -** given the machine is not in domain, we create a standard user "account\_all". If after exploit we got "account\_all" credentials we call the attack as local privilege escalation.
2. **Local admin privilege escalation -** if after attack we got `NT AUTHORITY\SYSTEM` privileges then we call it local admin privilege escalation. like if we got access to password of "administrator" for a system.
3. **Domain privilege escalation -** if we got access to `MYDOMAIN\mike`we call it domain privilege escalation. Mike mike do not have authorization for other system in network domain.
4. **Domain admin privilege escalation -** if we got access to `MYDOMAIN\admin_kim` we call it domain admin privilege escalation.

**Network\(all machines of that network\) Privilege escalation vs Machine\(just a single machine\) privilege escalation**

