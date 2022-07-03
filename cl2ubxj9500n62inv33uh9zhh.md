## How does CORS work?

If you are a web developer, you must have seen the ***CORS error*** appear on your screen when you try to call the API, but why does that happen?
![CORS Error](https://cdn.hashnode.com/res/hashnode/image/upload/v1651829064148/uvIa971_1.png align="center")
The browser's same-origin policy blocks reading a resource from a different origin to avoid malicious sites from reading another site's data.

## So what is the Same-origin policy🤔?
<small>According to MDN Docs, </small>
The same-origin policy is a critical **security mechanism that restricts** how a document or script loaded by one origin can interact with a resource from another origin.

According to the Same Origin Policy, the Same Origin calls are allowed and Different Origin calls are not allowed.

For example, if you want to access your API hosted at **https://api.github.com** from your client-side frontend application that is hosted at **localhost:3000**, the browser will not allow this request to complete due to restriction of the Same-Origin Policy, but ***Cross-Origin Resource Sharing (CORS)*** fixes this in a standard way.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651831222286/NW4mxEBjQ.png align="left")

## Uhh!! What do you mean by *Origin*?🤨

Origin is defined by the scheme (protocol), hostname (domain), and port of the URL used to access it. Two objects have the same origin only when the scheme, hostname, and port all match.

> ***Let us understand it better with an example***...
If you consider the below snippet, it is **considered as same-origin** because they have the same scheme (HTTP) and hostname (github.com), and the different file path does not matter:
![same-origin.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651829982320/FzxV1-Qnv.png align="left")

Similarly, if you consider the below snippet, These are not of the same origin because they use different schemes

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651830351992/TadHyFE2k.png align="left")

## How does CORS work 🤔?
Cross-Origin Resource Sharing (CORS) is an HTTP-header-based mechanism that allows a server to indicate any origins (domain, scheme, or port) other than its own from which a browser should permit loading resources.

How it is achieved?

- When the browser is making a cross-origin request, the **browser adds an Origin header** with the current origin.
- On the server-side, when a server sees this header and wants to allow access, it needs to **add an Access-Control-Allow-Origin header to the response **specifying the requesting origin (or * to allow any origin.)
- When the browser sees this response with an appropriate **Access-Control-Allow-Origin header**, the **browser allows the response data** to be shared with the client site.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651832245137/bZRZpNReL.png align="left")

## What about Preflight requests in CORS?✈
**According to MDN Docs**, A CORS preflight request is a CORS request that checks to see if the CORS protocol is understood and a server is aware of using specific methods and headers.

If a web app needs a complex HTTP request, **the browser adds a preflight request to the front of the request chain.**
Browsers create a preflight request if it is needed. It's an **OPTIONS request** like below and is sent before the actual request message.

```
OPTIONS /users HTTP/1.1
Origin: localhost:3000
Access-Control-Request-Method: DELETE
``` 
On the server-side, **an application needs to respond** to the preflight request with information about the methods the application accepts from this origin.

```
HTTP/1.1 200 OK
Access-Control-Allow-Origin: localhost:3000
Access-Control-Allow-Methods: GET, DELETE, HEAD, OPTIONS
``` 
To know more about CORS, please visit [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#preflighted_requests) and [web.dev](https://web.dev/cross-origin-resource-sharing/). I strongly recommend joining through official docs.

I write about the web; you can follow me on [Twitter](https://twitter.com/DeRaowl). If you liked the post, give some ❤️!! Cheers
