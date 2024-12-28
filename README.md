## Postman automation tests:
- https://github.com/erev0s/VAmPI VamPI project
- Postman
- OWASP Top 10 API Security Risks – 2019

## List of application API Vulnerabilities found and their OWASP equivaltens:
- ***API8:2019 - Injection***:
  - SQL Injection vulnerability found with **sqlmap** tool:
  ```bash
    sqlmap --url="http://localhost:5000/users/v1/name" -p name --dump
  ```
  ![Database dump](https://raw.githubusercontent.com/kocurc/VAmPI-API-Tests/refs/heads/main/Pictures/sqlmap.png)

- ***API5:2019 - Broken Function Level Authorization***:
  - Unauthorized Password Change of anthor registered user
  ![BFLA for another user's password](https://raw.githubusercontent.com/kocurc/VAmPI-API-Tests/refs/heads/main/Pictures/bfla.png) 

- ***API1:2019 - Broken Object Level Authorization***:
  - Broken Object Level Authorization when checking another user's secrets
  ![BOLA for another user's secrets](https://raw.githubusercontent.com/kocurc/VAmPI-API-Tests/refs/heads/main/Pictures/bola.png) 

- ***API6:2019 - Mass Assignment***:
  - Mass Assignment vulnerability for user registration with extra admin: true value
  ![Adding extra admin-true parameter](https://raw.githubusercontent.com/kocurc/VAmPI-API-Tests/refs/heads/main/Pictures/extraAdminParameter.png) 
  ![Validating mass assignment](https://raw.githubusercontent.com/kocurc/VAmPI-API-Tests/refs/heads/main/Pictures/massAssignment.png)


- ***API9:2019 - Improper Assets Management***:
  - Excessive Data Exposure through debug endpoint
  ![Publicly available debug endpoint](https://raw.githubusercontent.com/kocurc/VAmPI-API-Tests/refs/heads/main/Pictures/debug%20endpoint.png)

- ***API3:2019 - Excessive Data Exposure***:
  - As the consequence of the SQL database dump we can enumerate Users data

- ***API4:2019 - Lack of Resources & Rate Limiting***:
  - There are no requests limits set, which makes brute force attacks for login possible
  ![Burp Suite brute force attack](https://raw.githubusercontent.com/kocurc/VAmPI-API-Tests/refs/heads/main/Pictures/burp.png)

- ***API2:2019 - Broken User Authentication***:
    - JWT authentication bypass via weak signing key
    - ***Token***: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE3MzMyNjU5MDYsImlhdCI6MTczMzI2NTg0Niwic3ViIjoibmFtZTEifQ.k2tnsTyw2ZyXcLCq5sUZGF_i5aC0fMGldq_74C0zCL8

    - ***Hashcat usage***: hashcat --hash-type 16500 --attack-mode 3 jwt.txt --show

    - ***Output***: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE3MzMyNjU5MDYsImlhdCI6MTczMzI2NTg0Niwic3ViIjoibmFtZTEifQ.k2tnsTyw2ZyXcLCq5sUZGF_i5aC0fMGldq_74C0zCL8:**random**

    - ***Conclusion***: **random** is the plaintext key or password used to generate the signature (HMAC) for the JWT.

- ***API7:2019 - Security Misconfiguration***:
  - Server revelas technology being used data
    ```javascript
    pm.test('Server header does not reveal used technologies', function () 
    {
        pm.expect(headers.get('Server')).does.not.contain('Werkzeug/');
        pm.expect(headers.get('Server')).does.not.contain('Python/');
    });
    ```
  - HEAD or other unnecessary HTTP verbs should be disabled:
  ![405 error code](https://raw.githubusercontent.com/kocurc/VAmPI-API-Tests/refs/heads/main/Pictures/405.png)

- ***API10:2019 - Insufficient Logging & Monitoring***:
  - There is no record of which IP address, user agent, or timestamp is associated with each request
