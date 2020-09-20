# Handling WAF

* Main technique is to add a timeout for every request

### Example 1

* original command
  * wfuzz -u [http://10.10.10.179/api/getColleagues](http://10.10.10.179/api/getColleagues) -w ~/Documents/special\_cars.txt -d '{"name":"FUZZ"}'
* new command with timeout
  * wfuzz -u [http://10.10.10.179/api/getColleagues](http://10.10.10.179/api/getColleagues) -w ~/Documents/special\_cars.txt -d '{"name":"FUZZ"}' -s 1

