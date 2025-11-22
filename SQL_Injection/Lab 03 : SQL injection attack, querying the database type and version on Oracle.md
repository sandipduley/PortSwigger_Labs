```bash
-- SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query

1. access the lab & click any product category filter option  --  after intercepting send to repeater
2. rules to use the UNION query:
   -- Same number of columns in each SELECT.
   -- Same or compatible data types in corresponding columns.

3. to know how much database

TEST CASE
GET /filter?category='  --  response: 500  --  SQL confirmed

v$version
```
