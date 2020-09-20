---
description: >-
  Its a shell just like your "bash shell" and "sh shell" that linux users use
  daily. Meterpreter shell is a more advance shell and it could do complex jobs
  quickly. It is specially desgined for pentest.
---

# Meterpreter Shell

## Why Meterpreter Shell?

### Why was there a need of another shell? We could pretty much do all the things with normal bash shell or sh shell. Then why do pentester need it?

* Simply, meterpreter shell is a more strong shell that normal linux/unix shells with respect to pentesting.
* It could do complex jobs more easily.
* It was developed for pentesting purposes.
* It is a part of metasploit framework.

### How does "Meterpreter Shell" work ?

* First, search for a practical example of reverse shell and its working. Then read the below working.
* meterpreter shell is realized by, breaking the complete process in two parts of exploitation. 
  * **payload** : The main crux of the complete meterpreter shell is its payload. This payload we need to transport it to the victim machine and then we need to execute the payload to obtain a reverse meterpreter connection with our attacking machine.
  * **meterpreter listne**r : Before executing the payload we need to set a listner so that when the meterpreter payload executes, our attacker system is listening and is able to establish the connection.

