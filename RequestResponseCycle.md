## ***Request Response Cycle***

![Request Response Cycle](https://lh3.googleusercontent.com/Y04uUI2VdezFSZrAXqf4ouRgA04xxevHXSo-eyRe7_9U5Nk7FmSl0iTVIE4-6UhbtOHyoixbPtGkTnBzDit4rGqBSJUWUGFVdAJ13_zc9qdCeu9bbHFWUymElbxZxVH_z87PHLvXgRkOfjrBGFtUAiIQxprYPHUNFGJK1x47ndd-H815aWbMcuCe9yZfQQ)

*Here's what happens when you type a website into your address bar.*

When you type a website into an address bar, a lot of things happen that a lot of people don't realize or understand. I will explain this process to make it much easier to understand whether you are an engineer, or just have a curious mind. 

## URL Parsing and DNS Lookup

When you type in a website, the first thing that happens when you press enter on your keyboard, the browser parses (breaks down) the [URL](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Web_mechanics/What_is_a_URL) (Uniform Resouce Locator), and  looks for the [domain name](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Web_mechanics/What_is_a_domain_name) ex (google.com). Your browser checks your cache to see if the domain name exists. The cache for your browser stores copies of web pages, images, as well as other resources. The browser loads these resources from the cache instead of the downloading them again which speeds up load times. 

If the domain name exists in your cache, it continues to the next step, if not, the browser sends a request to the (DNS)[https://www.fortinet.com/resources/cyberglossary/what-is-dns] (Domain Name System). If the domain is not found, an error will be returned to the user, if it exists, the DNS responds with an [IP address](https://www.whatismyip.com/) 

## TCP/IP Agreement and Secure Connection

Using the IP address the browser establishes a connection with the web server through a three step process.

1. The browser sends a SYN (Synchronize) packet to the web server. This is the initial packet sent to establish a connection between the client and the server.

2. The server responds with a SYN-ACK (Synchronize-Acknowledgment) packet which is the combined response from the server during the TCP agreement to acknowledge the receipt of the SYN packet and signals if a connect is ready to be established. 

3. The browser send back an ACK(Acknowledgement) to confirm that the packet was recieved.


If the browser uses HTTPS (Hypertext Transfer Protocol Secure), ex (https://www.google.com), the browser and the server performs a TSL handshake to establish a secure, encrypted communication channel. This ensures data is protected when it is transported between the server and the client. HTTPS is HTTP(Hypertext Transfer Protocol) + TSL(Transport Security Layer) which has replaced SSL(Secure Socket Layer).

The TSL handshake includes:

- The browser requesting the servers TSL certificate
- The server and the browser agreeing on an encryption algorithm and exchange session keys to store data. 

## Browser Sends an HTTP Request

Once a connection is established, the browser constructs and HTTP request. This request includes:

- ***GET*** Method: Is used to view data from pages.
- ***URL Path***: ex '/about-me'
- **Headers**: which includes [cookies](https://usa.kaspersky.com/resource-center/definitions/cookies), [user agents](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent), and accepted formats.
- ***Body***: For PUT/PATCH (Used to update), or POST (Used to create).
This request is sent to the web server.

## Server Processes the Request

The web server receives the HTTP request and processes it. This involves: 

- *Serving Static Content*: If the requested resource is a static file like an HTML page, CSS, javascript or image, the server retrieves it from its file system. 
- *Dynamic Content Generation*: If the request requires dynamic content (like results from the database), the server runs the appropriate backend logic like querying the database or running a script. 

- The server then builds an HTTP response that contains:
    - Status Code: 200 OK, 404 Not Found, 500 Server Error
    - Headers: content type, caching policies, cookies
    - Body: the actual web page

## Server Sends HTTP Response

- The server sends the response back to the browser including any requested resources like HTML files, CSS, javascript, and images.

## Browser Receives the Response

- The browser recieves the HTTP response and starts to render the page, in order by HTML, CSS, then any javascript files. 

    - HTML parsing: The browser parses the HTML and builds the [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction) (Document Object Model)
    - CSS parsing: The browser parses the [CSS](https://developer.mozilla.org/en-US/docs/Learn/CSS/First_steps/What_is_CSS) (Cascading Style Sheet) and applies any style to to the DOM element. 
    - Javascript execution: If there are any linked javascript files, the browser fetches and executes them

## Rendering Addtional Resources

- As the browser renders the HTML, if it encounters any additional resources like any fonts, images, or scripts, it sends additional HTTP requests to retrieve these resources.
- The browser continues to rebuild the webpage as addtional resources are loaded and applied.

## User Interactions and Further Requests

- After the page loads, the user may react with the page to trigger addtional HTTP requests like POST (creating) or PUT (updating) for submitting data to a server. 
- AJAX/ Fetch requests: Modern websites often use AJAX or Fetch API to send data [asynchronously](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest_API/Synchronous_and_Asynchronous_Requests) without refreshing the entire page. 


In short the user the types in a website, which the browser check to see if it exists in your cache, if not it check the DNS. The DNS converts that to an IP Address. There is then a TCP/IP address agreement which ensures the data that is transported between the browser and the server are secure. 

The browser then sends an HTTP request, and the server processes the request and send a response. Finally, the browser receives and renders that data. I hope this summary was helpful if the longer explanation wasn't. 


