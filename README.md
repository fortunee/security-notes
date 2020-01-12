# Security

The use of the Open Web Application Security project (OWASP) Application Security Standards ensures that consistency in security is maintained across web applications, the project defines 3 security verification levels of applications with increasing depth that require different levels of implementation. 

Level 1 is meant for all softwares, level 2 is for applications that contain sensitive data, while level 3 is for most critical applications that perform high value transactions, contains sensitive medical information and applications that require the highest level of trust.

## Transport Level Security
It secures the actual transport (i.e. the pipe) over which the message passes through from client to a service.


HTTP, the most used internet communication protocol, it's currently also the most popular protocol for web services. HTTP is an inherently insecure protocol because all information is sent in clear text between unauthenticated peers over an insecure network. It uses the Secure Sockets Layer (SSL) or Transport Layer Security (TLS) which runs beneath HTTP.


SSL and TLS provide security features including authentication, data protection, and cryptographic token support for secure HTTP connections. To run with HTTPS, the service port address must be in the form `https://`. 


The integrity and confidentiality of transport data, including SOAP messages and HTTP basic authentication, is confirmed when you use SSL and TLS.


Transport Level Security doesn’t support scenarios when Intermediaries involved. It only support sending a message directly from client to service without an intermediate system.

## Message Level Security
It secures the message itself that is being transported from client to a service and vice versa.

Unlike in the transport level security, it supports intermediaries, there's usually no problem at all in scenarios even if message routed through multiple intermediate systems.

Message-level security is essential to the web service applications. HTTP basic authentication uses a username and password to authenticate a service client to a secure endpoint. The basic authentication is encoded in the HTTP request that carries the SOAP message. When the application server receives the HTTP request, the username and password are retrieved and verified using the authentication mechanism specific to the server.

### Popular threats 

#### SQL injection:
Placement of malicious code in SQL statements through a web page input.
It occurs when a user instead of entering the expected data into web page inputs, like forms, sends an SQL statement instead which you will unknowingly run on the database. 

##### Prevention:
- Use of Prepared Statements (with Parameterized Queries)
- Use of Stored Procedures
- White List Input Validation
- Escaping All User Supplied Input


#### Clickjacking:
Clickjacking, also known as a "UI redress attack", is when an attacker uses multiple transparent or opaque layers to trick a user into clicking on a button or link on another page when they were intending to click on the the top level page. Thus, the attacker is "hijacking" clicks meant for their page and routing them to another page, most likely owned by another application, domain, or both.

##### Prevention:
##### There are two main ways to prevent clickjacking:


Sending the proper Content Security Policy (CSP) frame-ancestors directive response headers that instruct the browser to not allow framing from other domains. (This replaces the older X-Frame-Options HTTP headers.)
Employing defensive code in the UI to ensure that the current frame is the most top level window

#### Cross Site Request Forgery (CSRF):

Cross-Site Request Forgery (CSRF) is an attack that forces an end user to execute unwanted actions on a web application in which they're currently authenticated. CSRF attacks specifically target state-changing requests, not theft of data, since the attacker has no way to see the response to the forged request. With a little help of social engineering (such as sending a link via email or chat), an attacker may trick the users of a web application into executing actions of the attacker's choosing. If the victim is a normal user, a successful CSRF attack can force the user to perform state changing requests like transferring funds, changing their email address, and so forth. If the victim is an administrative account, CSRF can compromise the entire web application.

##### Prevention:
##### Anti-CSRF Tokens:

Anti-CSRF Tokens are cryptographically secure random numbers, linked to a session identifier, and required to be submitted with every non-GET request in a location that doesn’t submit automatically
JSON-Web-Tokens ( JWT )/Bearer Tokens: 
This is without a doubt one of the best methods of preventing CSRF. The underlying mechanism is simple: Don’t use cookies to store sessions. Instead, a value saved in local or session storage is used, such as a JWT, and then sent as a header with every request. The downside to this method is that every request must be sent via XHR, and while that is not a problem with modern single page web applications, older applications written in pure HTML will not find implementing this method to be an easy task.

