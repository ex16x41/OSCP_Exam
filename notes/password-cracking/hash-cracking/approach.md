# Approach

### Approach 1

1. Create a list of all months
2. Add machine specific details, machine name, domain
3. Add any enumerated passwords
4. Add english seasons
5. Permute this list with year
   1. `for i in $(cat pass.txt); do echo $i; echo ${i}2019; echo ${i}2020; done`
6. Add list of 100 most common passwords



