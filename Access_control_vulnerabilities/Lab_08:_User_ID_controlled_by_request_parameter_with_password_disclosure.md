## **Lab 8: User ID controlled by request parameter with password disclosure**

```go
This lab has a user account page that contains the current user's existing password, prefilled in a masked input.

To solve the lab, retrieve the administrator's password, then use it to delete the user carlos.

You can log in to your own account using the following credentials: wiener:peter

Steps

1. Access the lab && login
2. Try to change the wiener to administrator in the URL
3. Successfully authenticated to the administrator account
4. Inspect the page source and locate the password input field to reveal the actual password value
5. Copy the password && log in as administrator
6. Delete carlos
7. done
