---
description: Given hash dump we need to crack password
---

# Password list

### Tools

* Hashcat
  * Hashcat have rules that when applied to a list of passwords, created a list of scrambled fuzzing passwords. Rules can be like toggle uppercase and lowercases.
  * hashcat --force --stdout pwlist.txt -r /usr/share/hashcat/rules/best64.rule
  * Note : The list with multiple chained hashcat rules could have duplicates.
* Crunch
* Manually
* Seclists

## Approach 1

1. Create a list of all months
2. Add machine specific details, machine name, domain
3. Add any enumerated passwords
4. Add english seasons
5. Permute this list with year
   1. `for i in $(cat pass.txt); do echo $i; echo ${i}2019; echo ${i}2020; done`
6. Add list of 100 most common passwords
7. Add the below list



* admin:admin, 
* root:root, 
* %username% ,
* pass123, 
* 123456, 
* admin, 
* letmein, 
* admin@123, 
* password, 
* s3cret, 
* 12345678900987654321

## Approach 2

