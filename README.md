## Postman automation tests:
- https://github.com/erev0s/VAmPI VamPI project
- Postman
- OWASP Top 10 API Security Risks – 2019

## List of application API Vulnerabilities found and their OWASP equivaltens:
- ***API8:2019 - Injection***:
  - SQLi Injection

- ***API5:2019 - Broken Function Level Authorization***:
  - Unauthorized Password Change

- ***API1:2019 - Broken Object Level Authorization***:
  - Broken Object Level Authorization

- ***API6:2019 - Mass Assignment***:
  - Mass Assignment

- ***API9:2019 - Improper Assets Management***:
  - Excessive Data Exposure through debug endpoint
  ![Publicly available debug endpoint](https://raw.githubusercontent.com/kocurc/VAmPI-API-Tests/refs/heads/main/Pictures/debug%20endpoint.png)

- ***API3:2019 - Excessive Data Exposure***:
  - User and Password Enumeration

- ***API4:2019 - Lack of Resources & Rate Limiting***:
  - RegexDOS (Denial of Service)

- ***API4:2019 - Lack of Resources & Rate Limiting***:
  - Lack of Resources & Rate Limiting

- ***API2:2019 - Broken User Authentication***:
    - JWT authentication bypass via weak signing key
    - ***Token***: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE3MzMyNjU5MDYsImlhdCI6MTczMzI2NTg0Niwic3ViIjoibmFtZTEifQ.k2tnsTyw2ZyXcLCq5sUZGF_i5aC0fMGldq_74C0zCL8

    - ***Hashcat usage***: hashcat --hash-type 16500 --attack-mode 3 jwt.txt --show

    - ***Output***: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE3MzMyNjU5MDYsImlhdCI6MTczMzI2NTg0Niwic3ViIjoibmFtZTEifQ.k2tnsTyw2ZyXcLCq5sUZGF_i5aC0fMGldq_74C0zCL8:**random**

    - ***Conclusion***: **random** is the plaintext key or password used to generate the signature (HMAC) for the JWT.

- ***API7:2019 - Security Misconfiguration***:
  - 
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