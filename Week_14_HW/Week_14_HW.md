## Unit 14 Homework: Web Development

### Instructions

In this homework, we will review the many of the concepts and tools covered in the web development unit. If needed, refer to the [HTTP](./HTTP_Reference.md) and [curl](./cURL_Reference.md) reference sheets provided to you.

For submission, create a new file containing the answers to the question.

#### HTTP Requests and Responses

Answer the following questions about the HTTP request and response process.

1. What type of architecture does the HTTP request and response process occur in?

    Client - Server

2. What parts make up an `HTTP request`?

    The request line, the headers, and the body of the request. 

    

3. What is the optional part of an HTTP request?

    The body of the request.

4. What three parts make up an HTTP response?

    A Status-line.
    Zero or more header (General|Response|Entity) fields followed by CRLF.
    An empty line (i.e., a line with nothing preceding the CRLF) indicating the end of the header fields. 
    Optionally a respose-body.

5. Which number class of status codes represent errors?
    

    400     ie: ERR404:Page Not Found

6. What are the two most common request methods that a security professional will come across?

    GET & POST 

7. Which type of HTTP request method is used for sending data?

POST

8. Which part of an `HTTP request` contains the data being sent to the server?

The request body.

9. In which part of an HTTP response would the browser receive the web code to generate and style a web page?

The response body.

#### Using cURL

Answer the following questions about `curl`:

10. What are the advantages of using curl over the browser?


    
    ? allows you to easily see the response status lines, is repeatable, can be automated, and can be edited on the fly. 
    
     It is fast and it  has no GUI. !!!!     Check !


11. Which curl option is used to change the request method?

    -X 

12. Which curl option is used to set request headers?

    -H

13. Which curl option is used to view the response header?

    -I

14. Which request method might an attacker use to scope out usable HTTP requests that an HTTP server will accept?

    OPTIONS ?

#### Sessions and Cookies

Recall that HTTP servers need ways to recognize clients from one another. These are implemented through sessions and cookies.

Answer the following questions about sessions and cookies.

15. Which response header sends a cookie to the client?

    ```HTTP
    HTTP/1.1 200 OK
    Content-type: text/html
    Set-Cookie: cart=Bob   <--- This one - Nom! Nom! Nom!
    ```

16. Which request header sets a cookie in the client?

    ```HTTP
    GET /cart HTTP/1.1
    Host: www.example.org
    Cookie: cart=Bob       <--- This one - Nom! Nom! Nom! 
    ```

#### Example HTTP Requests and Responses

Look through the following example HTTP request and response and answer the following questions.

#### HTTP Request Example

```HTTP
POST /login.php HTTP/1.1
Host: example.com
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
Content-Length: 34
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.132 Mobile Safari/537.36

username=Barbara&password=password
```

17. What was the request method?

    POST

18. Was the request encrypted or unencrypted?

    unencrypted

19. Does the request have a user session associated to it?

    Nope

20. What kind of data is being sent from this request body.

A username and a password used for loging in to a website / web app.

#### HTTP Response Example

```HTTP
HTTP/1.1 200 OK
Date: Mon, 16 Mar 2020 17:05:43 GMT
Last-Modified: Sat, 01 Feb 2020 00:00:00 GMT
Content-Encoding: gzip
Expires: Fri, 01 May 2020 00:00:00 GMT
Server: Apache
Set-Cookie: SessionID=5
Content-Type: text/html; charset=UTF-8
Strict-Transport-Security: max-age=31536000; includeSubDomains
X-Content-Type: NoSniff
X-Frame-Options: DENY
X-XSS-Protection: 1; mode=block

[page content]
```

21. What was the response status code?

200 OK

22. Was the response encrypted or unencrypted?

 NOPE

23. Does this response have a user session associated to it?

Yup. There is an acctive cookie wth a sessionID [ - Set-Cookie: SessionID=5 ]

24. What kind of content is likely to be in the [page content] response body?

 code that renders the body of the page.

25. If your class covered security headers, what security request headers have been included?

HTTP Strict Transport Security (HSTS) ??

#### Monoliths and Microservices

Answer the following questions about monoliths and microservices:

26. What are the individual components of microservices called?

services 

27. What is a service that writes to a database and communicates to other services?

APIs ?


28. What type of underlying technology allows for `microservices` to become scalable and have redundancy?

Containers
    
#### Container Vulnerability Filtering

Answer the following questions about vulnerability filtering `Trivy` scans with `jq`:

29. Do `microservices` share the same kind of vulnerabilities as regular operating systems?

Yes

30. Would an organization be more concerned with `Low` severity vulnerabilities as much as `Critical`?

Nope. But it would be better if some of the low vulnerabilities are mitigated.

31. Would the bash tool `jq` be useful in finding certain kinds of vulnerabilities within a vulnerability report?

#### Deploying and Testing a Container Set

Answer the following questions about multi-container deployment:

32. What is a tool that can be used to deploy multiple containers at once?

Docker-Compose ?

33. What kind of file format was required for us to deploy a container set?

A .YAML file. 

#### Container Runtime Intrusion Detection Systems

34. What is a tool used to actively detects intrusion behavior within containers?

Falco ?

35. What high-value system file might an intruder view that would trigger a `sensitive file opening` alert?

/etc/shadow

36. What kind of intruder action might trigger an alert from a container IDS that says `shell configuration file has been modified`?

    Creating user accounts 

---

© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.
