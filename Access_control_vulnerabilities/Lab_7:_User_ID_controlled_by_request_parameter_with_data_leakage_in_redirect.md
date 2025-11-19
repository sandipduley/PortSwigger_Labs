## **Lab 7: User ID controlled by request parameter with data leakage in redirect**

```go
This lab contains an access control vulnerability where sensitive information is leaked in the body of a redirect response.

To solve the lab, obtain the API key for the user carlos and submit it as the solution.

You can log in to your own account using the following credentials: wiener:peter 

Steps

1. Access the lab && login
2. Try to change the wiener to carlos in url 
3. We have been thrown to the login page 
4. Analyse the 302
5. The 302 should not reflect the body of carlos account
6. Copy the API key and submit
7. done
