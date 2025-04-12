
### Motivations + Introduction

- web server serves **static content** but the web application serves **dynamic content** 
- javascript follows DOM (Document Object Model) so it can manipulate elements in the HTML document 
- DOM creates the DOM tree out of the webpage with nodes as the objects in the HTML code, its essentially an API
- AJAX (Async JS and XML) - allows webpages to communicate with web server asynchronously, can update parts of the website without a full page reload (faster response!), modern ajax use JSON (instead of XML) cuz lightweight, easily parse-able 

---

### Browser Internals 

- In the Browser, there's multiple processes and threads running and each of them is associated disjoint chunks of memory resources by the OS (for security through isolation)
- processes and worker processes (forked from parent) communicate with each other through the `Inter-Process Communication (IPC)` 
- When we start browser, there's like 6 processes started by default :

![processes](/assets/browser-processes.png)

- Browsers are smart and well-developed softwares :
>  - if good hardware detected --> create & split into multiple processes with own threads for more stability
> - if bad hardware detected --> create a single process and run to save memory

- Renderer Process' main thread parses the `DOM + CSSOM = renderer Tree` to construct the webpage efficiently 
- Security mechanisms implemented by browsers include _sandboxing_, _Same Origin Policy (SOP)_, _HTTPS (SSL/TLS)_ protocols, OS/runtime level protection --> **DEP** (data execution prevention) marks memory pages as _non executable (NX)_, **ASLR** (prevent guessing memory location + buffer overflows)
- Same Origin Policy (SOP) - Restricts how a document/script loaded by one origin can interact with a resource from another origin 

![SOP](SOP.png)

---
### Web Protocols 

- HTTP operates over `TCP protocol` cuz TCP guarantees ordered, error-free data transmission, making it more suitable for web traffic, it is a **_stateless protocol_**

![methods](http-methods.png)

**Status Codes :**
![statuscodes](status-codes.png)


##### HTTPS implementation

![implement](https-implement.png)

##### Data Transfer Mechanism
![datatransfer](data-transfer.png)

##### DNS Protocol
![dns](dns-protocol.png)

---
### Session Management (cookies + tokens)

Session Tracking:

![session](session-track.png)

- JSON Web Tokens (JWT) is a standardized format for sending cryptographically signed JSON data
![JWT-FORMAT](JWT.png)

> - **cookies/session IDs** are used in _stateful applications_ where the server looks it up in a database
> - In JWT, no database query made (_stateless applications_), for server-to-server connections and `enhanced scalability (no database lookup)` especially in _distributed/microservices architecture_ 

---
### Server Internals 

- static content is served by web servers like `Apache, Nginx`
> 1. Apache has `process driven architecture` - _not very memory efficient_
> 2. Nginx is lightweight, high-performance web server with `event driven architecture` - handles concurrency very well, supports reverse proxy

- **Web Directory Structure (Linux)**: 

1. web server root is the base directory from which web server serves the files (html, css, js files are stored here)
> - for Apache --> `/var/www/html`
> - for Nginx --> `/usr/share/nginx/html`

2. Server Configuration files for web server are usually found in `/etc` and Logs are found in `/var/log`
> - for Apache --> `/etc/apache2` & `/var/log/apache2`
> - for Nginx --> `/etc/nginx` & `/var/log/nginx`

**_Note - `.htaccess` may allow to override global configurations set in `.conf` files_**





