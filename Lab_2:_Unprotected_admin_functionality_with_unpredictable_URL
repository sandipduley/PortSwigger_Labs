## **Lab 2: Unprotected admin functionality with unpredictable URL**

```go
This lab has an unprotected admin panel. It's located at an unpredictable location, but the location is disclosed somewhere in the application.

Steps to reproduce

1. Check for robots.txt, sitemap.xml, .htaccess
2. Check source code
3. Look for this

var isAdmin = false;
if (isAdmin) {
   var topLinksTag = document.getElementsByClassName("top-links")[0];
   var adminPanelTag = document.createElement('a');
   adminPanelTag.setAttribute('href', '/admin-kk1xcu');
   adminPanelTag.innerText = 'Admin panel';
   topLinksTag.append(adminPanelTag);
   var pTag = document.createElement('p');
   pTag.innerText = '|';
   topLinksTag.appendChild(pTag);
}

4. Navigate to this :- /admin-kk1xcu  --  your will be different
5. Delete carlos
6. done
