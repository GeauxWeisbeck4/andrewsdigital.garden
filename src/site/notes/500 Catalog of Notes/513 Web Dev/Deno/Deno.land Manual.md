---
{"dg-publish":true,"permalink":"/500-catalog-of-notes/513-web-dev/deno/deno-land-manual/"}
---

- # Deno.land Manual
    - ## 1. Introduction
    - ## 2. Getting Started
        - ### 2.1 Installation
        - ### 2.2 Set Up Your Environment
        - ### 2.3 First Steps
            - Hello World
            - Running Deno Programs
            - Making an HTTP Request
            - Reading a File
            - Putting it all together in an HTTP Server
                - **https_server.ts**
                - ```typescript
import { serve } from "https://deno.land/std@0.157.0/http/server.ts";

const port = 8080;

const handler = async (request: Request): Promise<Response> => {
  const resp = await fetch("https://api.github.com/users/denoland", {
    // The init object here has an headers object containing 
    // a
    // header that indicates what type of response we accept.
    // We're not specifying the method field since by default
    // fetch makes a GET request.
    headers: {
      accept: "application/json",
    },
  });
  return new Response(resp.body, {
    status: resp.status,
    headers: {
      "content-type": "application/json",
    },
  });
};

console.log("Listening on http://localhost:8000");
serve(handler);```
                - Here's what is hapening:
                    - 1. Import the http server from std/http (standard library)
                    - 2. import a third party module url_join which is hosted at deno.land/x (Better to import and re export into deps.ts file.)
                    - 3. HTTP servers handler functin is called for every request that comes in and must return a  response. 
                    - 4. In the handler function use url_join to join a complex GitHub url
                    - 5. Use fetch to fetch the url
                    - 6. Write the response body to a local file
                    - 7. Return the GitHub response as a response to the handler
