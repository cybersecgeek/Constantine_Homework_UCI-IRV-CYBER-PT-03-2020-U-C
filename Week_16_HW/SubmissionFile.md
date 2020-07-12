## Week 16 Homework Submission File: Penetration Testing 1

#### Step 1: Google Dorking


- Using Google, can you identify who the Chief Executive Officer of Altoro Mutual is:

  The name of the target is  Karl Fitzgerald.
  Chairman and Chief Executive Officer at Altoro Mutual.


- How can this information be helpful to an attacker:

  It can be used in the reconnaissance  phase to gather more information about the target. ie: possible usernames , passwords.
  It can also be used to launch a social engineering atack.

      ie: When targeting the IT department.


      This is your CEO Karl Fitzgerald... bla bla bla...
      This is an urgernt request.
      Please issue a new VPN certificat and password for my account and send it to me....
      If you wish to continue to be employed tommorow morning...

      Bla Bla Bla...

      I am the CEO.
      Do as I say....
      BLA BLA BLA ...


#### Step 2: DNS and Domain Discovery

Enter the IP address for `demo.testfire.net` into Domain Dossier and answer the following questions based on the results:

  1. Where is the company located:

    The address is not visible in the whois records because the company is using  private registration.


  2. What is the NetRange IP address:

      ???

  3. What is the company they use to store their infrastructure:

    Rackspace

  4. What is the IP address of the DNS server:

    65.61.137.117

#### Step 3: Shodan

- What open ports and running services did Shodan find:


Ports and Services

---------------------------------------------------------------------------------
80
tcp
http

Apache Tomcat/Coyote JSP engineVersion: 1.1
HTTP/1.1 200 OK
Server: Apache-Coyote/1.1
Set-Cookie: JSESSIONID=7B34F05EEDF35FB2985B718229BBD9A0; Path=/; HttpOnly
Content-Type: text/html;charset=ISO-8859-1
Transfer-Encoding: chunked
Date: Sun, 05 Jul 2020 20:58:41 GMT

--------------------------------------------------------------------------------------

443
tcp
https

Apache Tomcat/Coyote JSP engineVersion: 1.1
HTTP/1.1 200 OK
Server: Apache-Coyote/1.1
Set-Cookie: JSESSIONID=9746BA4A66D904A8241E54202613B2CE; Path=/; Secure; HttpOnly
Content-Type: text/html;charset=ISO-8859-1
Transfer-Encoding: chunked
Date: Sat, 04 Jul 2020 07:43:46 GMT

------------------------------------------------------------------------------------
8080
tcp
http-simple-new

Apache Tomcat/Coyote JSP engineVersion: 1.1
HTTP/1.1 200 OK
Server: Apache-Coyote/1.1
Set-Cookie: JSESSIONID=FA3C293F70486F7B554EDB94B1F41A88; Path=/; HttpOnly
Content-Type: text/html;charset=ISO-8859-1
Transfer-Encoding: chunked
Date: Thu, 09 Jul 2020 05:11:01 GMT
----------------------------------------------------------------------------------
tcp
https

Apache Tomcat/Coyote JSP engineVersion: 1.1
HTTP/1.1 200 OK
Server: Apache-Coyote/1.1
Set-Cookie: JSESSIONID=188B88371ABE27FD1C0EAD2019A6AAB6; Path=/; Secure; HttpOnly
Content-Type: text/html;charset=ISO-8859-1
Transfer-Encoding: chunked
Date: Thu, 25 Jun 2020 12:39:26 GMT


----------------------------------------------------------------------------------




#### Step 4: Recon-ng

- Install the Recon module `xssed`.
- Set the source to `demo.testfire.net`.
- Run the module.


recon-ng
marketplace install xssed
modules load xssed
options set SOURCE testfire.net
run

------------
TESTFIRE.NET
------------
`<

[*] Category: XSS
[*] Example: http://demo.testfire.net/search.aspx?txtSearch=%22%3E%3Cscript%3Ealert(%2Fwww.sec-r1z.com%2F)%3C%2Fs<br>cript%3E%22%3E%3C%2Fscript%3E
[*] Host: demo.testfire.net
[*] Notes: None
[*] Publish_Date: 2011-12-16 00:00:00
[*] Reference: http://xssed.com/mirror/57864/
[*] Status: unfixed
[*] --------------------------------------------------

>`


Is Altoro Mutual vulnerable to XSS:

YES


### Step 5: Zenmap

Your client has asked that you help identify any vulnerabilities with their file-sharing server. Using the Metasploitable machine to act as your client's server, complete the following:

- Command for Zenmap to run a service scan against the Metasploitable machine:


      nmap -sV 192.168.0.10




- Bonus command to output results into a new text file named `zenmapscan.txt`:



`nmap -sV -oN zenmapscan.txt --script smb-enum-shares 192.168.0.10`

?

- Zenmap vulnerability script command:


    nmap --script smb-enum-shares 192.168.0.10

    ?


- Once you have identified this vulnerability, answer the following questions for your client:

  1. What is the vulnerability:
    anonymous user have read/write  rights in samba shares.

  2. Why is it dangerous:

  anonymous users can read/write in samba shares.


  3. What mitigation strategies can you recommendations for the client to protect their server:

  Update the samba server
  update core os
  make sure smb v 1 is disabled
  disable  anon access.





---
© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.  
