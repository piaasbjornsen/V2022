# Application Layer: Overview 

## Web and HTTP
* Web pages consist of objects, each of which can be stores on different Web servers
* Object can be HTML file, JPEG image, Java apllet, audio file, ...
* Web page consistst oif base H TML-file which incluides serveral referenced object, each addressasble by URL

## HTTP overview 
* HTTP: HyperText Transfer Protocol 
* Web´s application layer protocol 
* Client/server model:
  * Client: browser that requests, receives, (using HTTP protocol) and "displays" Web objects
  * Server: Web server sends (using HTTP protocol) objects in response to request 
* HTTP uses TCP (one of the two protocols on the transfer layer)
* HTTP uses TCP:
  * Client initiates TCP connection (creates soceket) to server, port 80
  * Server accepts TCP connoction from client
  * HTTP messages (application-layer protocol messages) exchanged between browser (HTTP client) and Web server (HTTP server)
  * TCP connection closed
* HTTP is "stateless"
  * server maintains no information about past client requests 

## HTTP connections: two types
* Non-persistenst HTTP
  * TCP connection opened 
  * at most one object sent over TCP connection
  * TCP connection closed
  * Example: User enters URL: www.someSchool.edu/someDepartment/home.index
    1. HTTP client initiates TCP connection to HTTP server (process) at www.someSchool.edu on port 80
    2. HTTP server at host www.someSchool.edu waiting for TCP connection at port 80 "accepts" connection, notifying client
    3. HTTP client sends HTTP request message (containing URL) intp TCP connection socket. Message indicates that client
    wants object someDepartment/home.index
    4. HTTP server receives message, forms response message containing rewquest object, and sends message into socket
    5. HTTP server closes TCP connection 
    6. HTTP client receives response message containing file, displays html. Parsing html file, finds 10 referenced jpeg 
    object.
    7. Steps 1-5 repeated for each og 10 jpeg object 
    * RTT (definition): time for a small packet to travel from client to server and back
    * HTTP response time (per object): 
      * One RTT to initiate TCP connection
      * one RTT for HTTP request and first few bytes of HTTP response to return 
      * object/file transmission time
* Persistent HTTP 
  * TCP connection opened to a server
  * multiple objects can be sent over single TCP connection between client, and that server
  * TCP connection closed
  * Example:

## HTTP request message
* Two types of HTTP messages: request, response
* HTTP request message:
  * ASCII (human-readable format)
* Other 
  * POST method
    * Web page often includes form input
    * user input sent from client to server in entity body of HTTP POST request message
  * GET method (for sendeing data to server)
    * include user data in URL field of HTTP GET request message (following a '?'):
      * www.somesite.com/animalsearch?monkey&banana
  * HEAD method 
    * requests header (only) that would be returned if specified URL were request with an HTTP GET method
  * PUT method 
    * uploads new file (object) to server
    * completely replaces file that exists at spedified URL with contet in entity body of POST HTTP request message

## HTTP response message
## HTTP repsonse error message
# Maintaining user/server state: cookies 
## HTTP cookies: comments
* What cookies can be used for:
  * authorization 
  * shopping carts
  * recommendations
  * user session state (web e-mail)
* Challenge: How to keep state:
  * Protocol endpoints: maintain state at sender/receiver over multiple transactions
  * cookies: HTTP messages carry state 

# Web caches (proxy sercers)
* Goal: satisfy client request without involving origion server
* User configurations browser to point to a web cache
* browser sends all HTTP requests to cache 
  * if object cache_ cache returns object to client 
  * else cache requests object from origin server, aches received object, then returns object to client 
* Gått litt ut av moten 

# HTTP/2
* Goal: Decresed delay in multi.object HTTP requests
* HTTP1.1 introduced multiple, pipelined GETs over single TCP connection
  * Server responds in-order (FCFS: first-come-first-served scheduling) to GET request
  * With FCFS, small objects may have to wait for transmission (head-of-line (HOL) blocking) behind large objects(s)
  * Loss recovery /retransmitting lost TCP segments) stalls object transmission 
* HTTP/2: increased flexibility at server in sending objects to client:
  * methods, status codes, most header fields unchanged from HTTP 1.1
  * Transmission order of requested objects based on client-specified object priority (not necessarily FCFS)
  * push unrequested objects to client 
  * divide objects into frames, schedule frames to mitigate HOl blocking
  * 

 