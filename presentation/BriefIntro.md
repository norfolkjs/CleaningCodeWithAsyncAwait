---
title: Cleaning Up Code with Async Await
separator: <!--s-->
verticalSeparator: <!--v-->
theme: solarized
revealOptions:
    transition: 'fade'
---
# Async/Await
## January 2018 @ Norfolk.js
## Stanley ZHeng
<!-- ![](https://www.businessprocessincubator.com/wp-content/uploads/2016/02/www.imaworldwide.comhubfsimagesThe-Biggest-How-To-Post-Ever-369a5b9b18f757c0e189169b5a4b9092774637ab-1.png) -->
<!--s-->
## We all like JavaScript
<!--v-->
## JavaScript is Asyncronous
<!--v-->
## Asyncronous code is hard
<!--v-->
## I want my brain to work less

<!--s-->

## Node 6 

<section>
    <pre><code data-trim data-noescape>
    <mark>FROM node:6</mark>

    # if you're doing anything beyond your local machine, please pin this to a specific version at https://hub.docker.com/_/node/
    FROM node:6

    RUN mkdir -p /opt/app

    # default to port 3000
    ARG API_PORT=3000
    ENV API_PORT $API_PORT
    EXPOSE $API_PORT

    # check every 30s to ensure this service returns HTTP 200
    # HEALTHCHECK CMD curl -fs http://localhost:$PORT/healthz || exit 1

    </pre></code>
</section>


<!--v-->

## Node 8

<section>
    <pre><code data-trim data-noescape>
    <mark>FROM node:8</mark>

    # if you're doing anything beyond your local machine, please pin this to a specific version at https://hub.docker.com/_/node/
    FROM node:6

    RUN mkdir -p /opt/app

    # default to port 3000
    ARG API_PORT=3000
    ENV API_PORT $API_PORT
    EXPOSE $API_PORT

    # check every 30s to ensure this service returns HTTP 200
    # HEALTHCHECK CMD curl -fs http://localhost:$PORT/healthz || exit 1

    </pre></code>
</section>
<!--v-->

![](https://media.giphy.com/media/qUDenOaWmXImQ/giphy.gif)
<!--v-->
![](https://media.giphy.com/media/vebdBlWcL2g5G/giphy.gif)

<!--v-->
![](https://media.giphy.com/media/3oKIPrCu48s5KfzV7i/giphy.gif)
<!--s-->



## Node 8 LTS
    - Node.js API (N-API) 
    - V8 5.8
    - Buffer Improvements
    - Async/Await (7.5+)
    - NPM 5
    - Better Promise API
    - HTTP/2

<!--v-->
# adds two keywords 
## async
## await

<!--v-->
# What is async/await?
<!--v-->
![mpj](images/mpj.png)

"Async/Await keywords allows us to pause the execution of functions  and this in turn writes asynchronous code that reads like synchronous code."
 \-  MPJ, FunFunFunction

<!--v-->
## Example
```javascript
async function foo () {
    const p1 = await bar()
    const p2 = await baz("World", 2000)
    return await p1 + p2 + await Promise.resolve('!');
}

function bar () {
    return new Promise((resolve)=>setTimeout(
        function(){resolve("Hello ")}, 500))
}

function baz(str, interval) {
    return new Promise((resolve)=>setTimeout(
        function(){resolve(str)}, interval))	
}




(async function main() {
        console.log(await foo())
})()

```
[http://jsbin.com/nufumiz/edit?js,console](http://jsbin.com/nufumiz/edit?js,console)


<!--v-->
## Evaluate it in an IIFE 
``` javascript
(async function main() {
        console.log(await foo())
})()
# > "Hello World!"
```

<!--s--> 
## notes of async await
- you can't await a non-top level function 
- if you await something that doesn't return you'll block your application run
- Async await is learned from C# (2012) and probably in your other favorite language

<!--s--> 
References
- https://www.youtube.com/watch?v=568g8hxJJp4
- Building Iterators https://github.com/getify/You-Dont-Know-JS/blob/master/async%20%26%20performance/ch4.md#promise-aware-generator-runner
- Iterators https://medium.freecodecamp.org/demystifying-es6-iterables-iterators-4bdd0b084082
Credit 
- Made with https://github.com/webpro/reveal-md