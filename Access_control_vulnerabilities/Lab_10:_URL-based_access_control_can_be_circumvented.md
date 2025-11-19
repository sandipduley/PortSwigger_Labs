## **Lab 10: URL-based access control can be circumvented**

```go
This website has an unauthenticated admin panel at /admin, but a front-end system has been configured to block external access to that path. 
However, the back-end application is built on a framework that supports the **X-Original-URL** header.

To solve the lab, access the admin panel and delete the user carlos. 

Steps

1. Access the lab 
2. Click on Admin panel && you will get "Access denied"  --  it blocks GET request /admin
3. Check the captured request of **/admin** 
4. Add this X-Original-URL: /apple at the end of the headers  --  403 error  --  !worked  --  make sure to leave two line spaced at the end
5. Try by removing the admin  --  GET / HTTP/1.1  --  worked  --  404 client side error
6. Remove the admin and add  X-Original-URL: /admin
7. Send the request and look for   <a href="/admin/delete?username=carlos">Delete</a> 
8. Follow the href link: 400 Bad Request  "Missing parameter 'username'"
9. Put both headers: X-Original-URL: /admin/delete   GET /?username=carlos HTTP/1.1
10. Send the request && reload the page
11. done 
