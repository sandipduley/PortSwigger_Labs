## **Lab 4: User role can be modified in user profile**

```go
This lab has an admin panel at /admin. It's only accessible to logged-in users with a roleid of 2.

Solve the lab by accessing the admin panel and using it to delete the user carlos.

You can log in to your own account using the following credentials: wiener:peter 

Steps

1. Access the lab && login
2. Update email
3. Check the change email captured request
4. In response we can see the roleid: 1 in JSON
5. Add the "roleid": 2 in request JSON 

{"email":"apple@mail.com",
"roleid": 2
}

6. Refresh the page && click on the Admin Panel button
7. Delete carlos
8. done
