## **Lab 3: User role controlled by request parameter**

```go
This lab has an admin panel at /admin, which identifies administrators using a forgeable cookie. Solve the lab by accessing the admin panel and using it to delete the user carlos.
You can log in to your own account using the following credentials: wiener:peter

1. Login with the credentials
2. Intercept the request
3. Look for :- Cookie: session=uK27bXLbygpZzhjSIvntoxWwdn; Admin=false  --  your session id will be different
4. Use match && replace functionality && set Admin=false to true
5. Refresh the page && click on the Admin Panel button
6. Delete carlos
7. done

