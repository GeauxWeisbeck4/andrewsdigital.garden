---
{"dg-publish":true,"permalink":"/500-catalog-of-notes/513-web-dev/deno/deno-succinctly/"}
---

- # 1. Introducing Deno
    - These are some of the ways in which Deno improves on Node:
        - Is secure by default. Deno doesn’t allow programs to access your file system, network, or environment unless you explicitly give that program permission to do so.
        - Supports TypeScript out of the box. Of course, you can write Node applications in TypeScript too, but you need to install extra packages to do so—and keep them up to date.
        - Ships as a single executable file.
        - Includes built-in tools. Includes tools such as a dependency inspector (deno info) and a code formatter (deno fmt).
        - Includes standard modules. Deno has a set of audited standard modules that are guaranteed to work.
    - ## The V8 Runtime 
        - ![](local-asset://Geaux-Notes/Ls0GGB8Nse.png)
    - ## The Architecture and Internals
        - The main building blocks of Deno are Rust, Tokio, and V8:
            - Rust is a modern systems programming language developed by Mozilla, with a focus on high performance and safe concurrency. Rust shares a similar syntax with C++, but has memory safety features that don't rely on garbage collection. The initial choice for Deno was the Go programming language, but issues with garbage collection forced a switch to Rust.
            - Tokio is an "event-driven, non-blocking I/O platform for writing asynchronous applications with the Rust programming language. At a high level, it provides a few major components: Tools for working with asynchronous tasks, including synchronization primitives and channels and timeouts, delays, and intervals." (Description taken from [Tokio documentation](https://docs.rs/tokio/1.5.0/tokio/).)
            - V8, as we have already learned, is Google's open-source JavaScript engine, written in C++, and which features in the Chrome web browser.
        - ![](local-asset://Geaux-Notes/gxXzB_OeET.png)
        - You can consider programs written in TypeScript or JavaScript as being Deno’s front end. If you create a TypeScript (.ts) file and submit it to Deno, then Deno will first compile it to JavaScript and then submit it to V8. If you give it a JavaScript (.js) file, it will skip the compilation step. Anything you do in TypeScript or JavaScript is considered “unprivileged,” in that it doesn’t have access to the network, file system, or anything else outside of Deno’s sandbox, so it is secure by default.
        - Anything V8 needs to do outside of this unprivileged environment needs to be submitted to Deno’s Rust back end. For example, if you want to access files, send emails, create servers, set timeouts, and so on, all that fun stuff needs to be handled by Rust. The communication between the unprivileged side (JavaScript/TypeScript) and the privileged side (Rust) is managed by a set of JavaScript bindings for Rust called Rusty_v8.
        - JavaScript is a single-threaded application, which is fine for a single browser instance, but totally inadequate for server applications that need to respond to requests from multiple clients simultaneously. For that we need asynchronous I/O running in an event loop.
        - The event loop is provided by **tokio**
            - The event loop:
                - Is an endless loop that waits for tasks, executes them, and then sleeps until it receives more tasks.
                - Executes tasks from the event queue starting from the oldest first, but only when the call stack is empty—that is, there is no ongoing task.
                - Uses callbacks and promises to signify the completion status of the task.
        - 
# 2. URL Shortener
- Another time

# 3. Deno Static Site Generator
- 