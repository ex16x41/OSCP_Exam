# PHP notes

* 
## PHP Known vulnerabilities

* PHP Type Judging
  * Versions vulnerable : 
  * Summary exploit
    * password\[\]=
  * [link](https://www.owasp.org/images/6/6b/PHPMagicTricks-TypeJuggling.pdf).



* PHP 5.5.9
  * php 5.5.9 and the idea of modifying the URL path to bypass authorization. It seems odd that this could be a thing that is possible but it worked.
    * original URL = admin.auth.inc.php
    * modified URL = admin.inc.php
  * Simply using the modified URL, it bypassed the authentication page completely.

