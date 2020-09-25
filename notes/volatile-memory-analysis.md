# Volatile Memory Analysis

* Install volatility
  * sudo apt install volatility
* check the type of memory dump
  * file name.dmp
* Get the windows profile
  * volatility -f name.dmp imageinfo
  * Output : Win2012R2x64
* Dump hashes for this profile
  * volatility -f name.dmp --profile Win2012R2x64 hashdump

