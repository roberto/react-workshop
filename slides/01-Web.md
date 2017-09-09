# Web Architecture

---

## Agenda

* Static
* Everything rendered server side
* Dynamic on client side
  * AJAX
* Single Page Applications (SPA)
  * BFF
* Server Side Rendering
* Progressive Web Apps (PWA)

---

## Static Page

* Good and old HTML


<div class="mermaid">
sequenceDiagram
    Browser->>Server: GET /movie123.html
    Server-->>Browser: HTML
</div>

???
HTML Initial Release: 1993

---

[First page](http://info.cern.ch/hypertext/WWW/TheProject.html)

![First Page](images/first_page.png)

???
First 'public' page(1993), describing W3 itself and releasing the software
needed to run a web server.

---

### First Web Page

* Mobile friendly
* Fast!
* Accessibility

???
All those features using just the basic of HTML :D

---

## Rendered Server Side

* Dynamic content

<div class="mermaid">
sequenceDiagram
{{content}}
    Browser->>Server: GET /movie.asp?id=123;
    Server->>Database: SELECT * FROM MOVIES WHERE ID=123;
    Database-->>Server: Movie data;
    Server->>Server: Render page;
    Server-->>Browser: HTML;
</div>

???
Using dynamic content to render the page response

--
    Browser->>Cache: GET /movie.asp?id=456;
    Cache-->>Browser: HTML;

???
Cache strategy, returning cached page as a static one
---

## Dynamic on client side

* 1993 - WWW (public domain)
* 1995 - JavaScript
* 1996 - iframe (IE)
* 1999 - XMLHttpRequest (IE)
* 2004/2005 - Gmail, Google Maps
* 2005 - Ajax - term by Jesse James Garrett
* 2006 - XMLHttpRequest first draft specification by W3C


???
* obs: XMLHttpRequest created by Outlook Web App Team 1 year before

---

### Ajax

* get more information without requiring to retrieve another full page

<div class="mermaid">
sequenceDiagram
    Browser->>Server: GET /index;
    Server-->>Browser: HTML;
    Browser->>Server: XML HTTP Request GET /movie/123;
    Server->>Database: ... where ID=123;
    Database-->>Server: Movie data;
    Server->>Browser: JSON;
</div>

---

### SPA - Single Page Application

* using Ajax a fuuu

---

### Progressive Web App

---

## References

* [Team rebuilding world's first website](http://edition.cnn.com/2013/04/30/tech/web/first-website-cern)
* [Single Page App Book](http://singlepageappbook.com/)
* [A Short History of JavaScript](https://www.w3.org/community/webed/wiki/A_Short_History_of_JavaScript)
* [A Brief History of JavaScript](https://auth0.com/blog/a-brief-history-of-javascript/)
* [Ajax: A New Approach to Web Applications](http://adaptivepath.org/ideas/ajax-new-approach-web-applications/)
