---
{"dg-publish":true,"permalink":"/500-catalog-of-notes/513-web-dev/deno/fresh/routing-and-custom-handlers-2-3-2-5/"}
---

- # 2.3 - Create a Route
    - Routes encapsulate the logic for handling requests to a particular path in your project. They can be used to handle API requests or render HTML pages. For now we are going to do the latter.
    - Routes are defined as files in the routes directory. The file name of the module is important: it is used to determine the path that the route will handle. For example, if the file name is index.js, the route will handle requests to /. If the file name is about.js, the route will handle requests to /about. If the file name is contact.js and is placed inside of the routes/about/ folder, the route will handle requests to /about/contact. This concept is called __File-system routing__. You can learn more about it on the [__Concepts: Routing__](https://fresh.deno.dev/docs/concepts/routing) page.
    - Route files that render HTML are JavaScript or TypeScript modules that export a JSX component as their default export. This component will be rendered for every request to the route's path. The component receives a few properties that can be used to customize the rendered output, such as the current route, the url of the request, and handler data (more on that later).
        - In the demo project we'll create a route to handle the /about page. To do this, one needs to create a new routes/about.tsx file. In this file, we can declare a component that should be rendered every time a user visits the page. This is done with JSX.
        - ℹ️ To learn more about JSX, you can read [this article](https://reactjs.org/docs/introducing-jsx.html) in the React documentation. Beware that Fresh does not use React, but rather [Preact](https://preactjs.com/), a lighter weight virtual dom library that works similar to React.
            - ```javascript
// routes/about.tsx

export default function AboutPage() {
  return (
    <main>
      <h1>About</h1>
      <p>This is the about page.</p>
    </main>
  );
}```
        - The new page renders at http://localhost:8000/about
- # 2.4 - Dynamic Routes
    - Let's create a /greet/:name that will render a page with a greeting that contains the name passed in the path.
    - Before diving in, a quick refresher on "dynamic" routes. Dynamic routes don't just match a single static path, but rather a whole bunch of different paths based on a pattern. For example, the /greet/:name route will match the paths /greet/Luca and /greet/John, but not /greet or /greet/Luca/John.
    - Fresh supports dynamic routes out of the box through file system routing. To make any path segment dynamic, just put square brackets around that segment in the file name. For example the /greet/:name route maps to the file name routes/greet/[name].tsx.
    - Just like the static /about route, the dynamic /greet/:name route will render a page. The module must once again expose a component as a default export. This time the component will receive the matched path segment properties as arguments in its props object though.
        - ```javascript
// routes/greet/[name].tsx

import { PageProps } from "$fresh/server.ts";

export default function GreetPage(props: PageProps) {
  const { name } = props.params;
  return (
    <main>
      <p>Greetings to you, {name}!</p>
    </main>
  );
}```
        - The PageProps interface actually contains a bunch of useful properties that can be used to customize the rendered output. Next to the matched url pattern parameters, the raw url, and the route name can also be found in here.
        - Navigating to https://localhost:8000/greet/Luca will now render a page showing "Greetings to you, Luca!".
- # # 2.5 - Custom Handlers
