# CORS - Cross-Origin Resource Sharing

## Process
Web browsers use Cross-Origin Resource Sharing (CORS) to manage requests made to a different domain than the one serving the web page. It's a security mechanism to mitigate the risks of cross-site request forgery and other cross-site attacks.

To get a clear picture of how it works, let’s break down the CORS workflow:

1) Initiation of a request from a web page
   The process starts with a web page (origin A) trying to access a resource of a different origin (origin B).

2) “Simple” or “non-simple” request check
   Before initiating the actual request, the browser checks if the request is "simple" or "non-simple". A "simple" request typically includes methods like GET, POST, or HEAD and a limited set of headers. If the request is "non-simple", the browser initiates a preflight request.

3) Preflight request (for non-simple requests)
   After the browser has completed its “non-simple” request check, if the request is “non-simple”, it will send an OPTIONS request to the target origin (origin B). The headers included will provide details of the actual request it wants to make.

4) Server response to preflight request
   Once the server (origin B) receives the preflight request, it will send a response. If the server decides that the origin is allowed to access the resource, it will respond with a set of headers that stipulate so. The browser will reject the actual request if the server doesn't provide the right headers or if those headers don't match the details of the request itself.

5) The actual request is sent
   Now that the preflight request is all out of the way (successful or not required), the browser can make the actual request to origin B. The request will include any necessary headers, credentials, or data.

6) Server response to the actual request
   Once the server (origin B) receives the request, it then processes it and sends a response. Along with the response, the server will still send the appropriate CORS-related headers.

7) Browser enforcement
   Last but not least, the browser will check the CORS headers in the response a final time. If everything checks out then the browser provides the response to the web page’s JavaScript. If not, then the browser will block access to the response and log a CORS error in the console.

CORS ensures that servers have control over who can access their resources. Browsers enforce these rules to protect users from potential security threats. Whilst CORS does introduce an additional layer of complexity, it provides an effective security measure to ensure safe cross-origin data sharing.

- https://x.com/NikkiSiapno/status/1735060129022881927?s=20