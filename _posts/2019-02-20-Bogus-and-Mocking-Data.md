---
published: false
---
Today my first child is 10 months old! But you're not here for that. Let's talk Bogus</p>

I was going to manually go in and hand-jam a bunch of test SQL data for use while testing and demoing. But then I stumbled upon Bogus. Which is a lovely C# library for creating all kinds of random data but with intent. For instance, you can have it generate Lorem Ipsum sentences or sentence, a username, an email, pick from a list, etc. etc. I'm really happy to have found this.

I did have to do some weird stuff in Program.cs because I'm calling two additional functions to populate the data. The intent is to comment out or remove those two lines before sending this thing out into the wild.