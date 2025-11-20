## **Lab 11: Method-based access control can be circumvented**

```go
This lab implements access controls based partly on the HTTP method of requests.
You can familiarize yourself with the admin panel by logging in using the credentials administrator:admin.

To solve the lab, log in using the credentials wiener:peter and exploit the flawed access controls to promote yourself to become an administrator.

Steps

1. Login with the credentials  --  administrator
2. Play with the admin panel
3. Again login with administrator  --  try to upgrade carlos user  --  note: it will only say admin in frontend but ! an actual admin role
4. Take the request  **/admin-roles**  and send it to repeater || replay
5. Logout && login with wiener
6. Copy the wiener session cookie  &&  replace with the admin cookie
7. Change the POST method with GET  &&  change carlos with wiener
8. done
