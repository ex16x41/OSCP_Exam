# Online password Cracking

* password security audits.
* Note that blindly running online brute force attack could violate a security policy and would automatically disable the service.
  * leaving the service in accessible until a administrator enables it.
  * we should be very careful and stealth.

## Key to a successful online password cracking

Step 1 : Enumerate and verify all the possible username and verify them.

Step 2 : Find suspicious webpages on which we could run "cewl" tool to get a good and rich password list, instead of just randomly password list.

Step 3 : Create one more copy of the password list in reverse order, this is helpful in CTF, and other penetration testing exams. `tac pass.txt > rev_pass.txt`

Step 3 :

1. Choosing your target
2. \(optional, if step 1 is unsuccessful then use this step\) Choose your user list
3. \(optional, if step 2 is unsuccessful then use this step\) Choose your password list
4. Grep output of incorrect responses to differentiate between a successful login vs unsuccessful one. E.g. "incorrect" "error" used in 3rd parameter in hydra.

d

