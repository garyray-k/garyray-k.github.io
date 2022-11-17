---
published: false
---
## 20190218 - Blazor, CORS, and JS

I've been stalling a lot in building this front end for the API, but just wanted to muse a bit about what I've learned recently. I went through the 'Practical Javascript' @ [watchandcode.com](https://watchandcode.com) and learned a bit about JS. There's a lot more to it though. Really seems daunting but I suppose that's because I've never done it.

On a long drive home I listened to a .NET Rocks podcast about Blazor and that got me thinking that I could just write the front end using Blazor and skip learning more JS. Not sure if that's the best idea but it's an idea for now.

This all led me to asking around int he Operation Code Slack channel about doing dev on a web-page. One thing led to another and I don't know anything about making a web page. yet. Regardless of that, I did get some clarification on somethign within my API that I was clueless on. CORS. I learned that it basically tells a browser when to enable using data from a certain API. So if I tell my API to app.UseCors() but .WithOrigins("http://foo.com") then the browser will know to only use my API's data when working with foo.com