# MeQuilibrium 

To build jar:

To run tests: 

This is currently coded to run locally on an individual machine.

This could be invoked as part of a CICD pipeline in a few ways
1. invoke a chromedriver instance within github actions docker container
2. execute against a hosted service such as browserstack, or saucelabs
3. execute against a remote, custom, selenium server, such as a selenium grid or lambda running in AWS

As part of the CICD pipeline, the result of this executable could be checked for success or failure, and either block or continue a deployment.


## Basic FrontEnd  Browser test flexing the following functionality:

1. can successfully login with known good credentials
   2. cannot login with bad credentials
      3. validate API response
      4. check if this is secure 
      5. can I snag a JWT from this request (are they using implicit vs authz code)


2. Can navigate to....



## Login test

1. navigate to `https://mymeq.com/`
2. enter email address into field id = `email` type = `email` email = `shane.burgoon@gmail.com`
   3. click `continue` buttonId = `qa-enter-email-continue`
   4. should result in the same `https://mymeq.com/`
   5. wait for password fieldId = `password` type = `password`
      6. makes this request `https://mymeq.com/json/auth/email` with body `{"mail":"shane.burgoon@gmail.com"}:`
6. enter password `K45ufJ4CfZLhyCb$`
   7. click `Login` buttonId = `qa-enter-password-login`
   8. oh look, a JWT `'eyJzdHJpbmciOiJMb2dpbiIsImhhc2giOiI5ZDYzMjJjMWY0ZDlkM2YzOGFlZDhiZmJlMGIyYmNhZGY2NmFkODJjMDA4NDc2ZmE2MjU0MWZhMDY5MTM4ZTk0In0='`
   9. should land on `https://mymeq.com/my-meq/dashboard/#/my-meq/my-active-skill`
   10. wait for what to load?


## Takeaways and questions

1. hit 429 on login pretty quick, like 5 attempts in a minute
   2. would benefit from a limit reset count in the headers so tests could throttle appropriately instead of making arbitrary waits
   3. is this super prone to DDOS? what ddos protection is in place for the login? IP rate limiting only?
      based on the fact I cannot login anymore, looks like its IP based. This is really easy to break using a distributed DDOS attack
      why is the failed login attempt a 200 with body instead of 401?

## TODO

1. gatling test of the various API endpoints to see how fast they fall over?