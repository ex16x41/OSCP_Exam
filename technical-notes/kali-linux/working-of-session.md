# Working of session

* User goes to a website.
* He goes to the login page in the website.
* Given user has an account in this website, he logins with his credentials.
* Once logged in successfully, he/she receives a session ID and authenticated cookie for the authenticated session.
* Hence now every time the user need to access his files in the website, he does not have to authenticate everytime and uses the session ID and authenticated cookie.
  * Why this? Because user is connecting using HTTP or HTTPS protocol which is a stateless protocol. Which means that user need to authenticate every time it has to access his personal data in the website.
  * But using session ID and authenticated cookie, he could use this session ID for consecutive connections. 
  * The session ID does expires depending on the designer who designed the website.
* 
