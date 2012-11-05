nettycat
========

This project is meant to take Netty (a library for developing TCP based applications) and create a server framework around it - basically, do what tomcat does for HTTP based applications: provide scripts to start/stop the server, provider classloaders to support multiple applications (or versions of applications), log file management, etc.

### Minimum viable product
* start/stop scripts
* server.xml
* echo-1.0 app with its own classloader

### Dump of things to think about
* startup scripts
* class-loader - framework, shared and app-specific
* thread-pools
* timeouts
* error handling
* configuration - framework, shared and app-specific
* logging - application logging as well as framework tracing
* additional configuration management support
* monitoring / JMX
* security / SSH
  * DOS attacks
* short-lived vs. persistent connections
  * keep-alives
* request-response vs. event-subscription
* contrast with http
  * virtual hosts? Hmm.. will need an additional line to indicate the requested hostname
  * context-path? <app-name>/<app-version>
  * http methods? Too deep into the app protocol.
  * headers?
  * cookies?
  * session?
* message framing: length based vs. delimiter based
* service registry - dynamic lookup and binding
* peer-to-peer model i.e. flip roles occasionally where server asks clients for data.
* pipelining - multiple requests lined up to be executed serially
* ping message
* health-check / ecv (extensible by app?)
* support explicit routing rules to provide defaults and/or override default behavior
* graceful shutdown

### Terminology

* framing: which tells how the beginning and ending of each message is delimited
  * flow control and segmentation: send messages only when flow control allows us to, and segment them if they're larger than the available window (or too large for comfort). segmentation allows chunking, where you can start sending data before you know the full length
* encoding: which tells how a message is represented when exchanged
* reporting: which tells how errors are described
* asynchrony: which tells how independent exchanges are handled
* authentication: which tells how the peers at each end of the connection are identified and verified
  * SASL: simple authentication and security layer
* privacy, which tells how the exchanges are protected against third-party interception or modification
* naming: ?
* authorization: ?

### NFR

* Scalability
* Efficiency
* Simplicity
* Extensibility
* Robustness


### Reference

* http://www.slideserve.com/hope/designing-application-protocols-for-tcp
* http://beepcore.org/doc.html and more specifically: http://www.rfc-editor.org/rfc/rfc3117.txt
* http://en.wikipedia.org/wiki/Service_Location_Protocol
* http://gee.cs.oswego.edu/dl/cpjslides/nio.pdf
