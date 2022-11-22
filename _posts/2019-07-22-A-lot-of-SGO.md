---
published: true
---
## SGO (stuff going on)

I've been interning at [SIXGEN](https://sixgen.io) for the past two months or so and things are going great.

The first few weeks, I was asked to research <a href="https://blog.cloudflare.com/esni/">Encrypted Server Name Indicator</a> and how it could be used in pentesting combined with C2 software. It was awesome to learn about, but way too new for my current skill level in C code and dissecting/understanding it. I did manage to take a [custom Openssl](https://github.com/sftcd/openssl) and convert it to a [byte array in Go](https://medium.com/dtoebe/embed-other-binaries-in-golang-binary-3f613314884c) and then compile. However, the byte array still relied on custom libraries that needed to be pre-installed so hit a dead end for now. Maybe once the protocol evolves or I learn C and then learn the openssl library, I'll revisit.

I was also sent to a [BlackBag Tech](https://www.blackbagtech.com/) course where I learned the tool for two days. Awesome deep dive into forensics.

More recently, I've been working on a Ruby on Rails project. I started out getting my feet wet with helping one of the other devs combine three models into one and create a hierarchical structure within the unified model. Good learning to get back into the feel for RoR. Then I took a ticket of my own.... Thinking it would be easy, I grabbed a PDF generation ticket. Googled PDF gems and landed on [Prawn](http://prawnpdf.org/api-docs/2.0/) which is fairly simple to use after reviewing the docs. 

Little did I know the PDF is generated from the central object in our app. The object touches almost everything in the database somehow. And the relationships aren't straight forward and the naming doesn't necessarily match up with what the customer uses... needless to say, I'm understanding the reason [DDD](https://en.wikipedia.org/wiki/Domain-driven_design") is so helpful. Luckily, this has really helped flesh out issues and flesh out my understanding of RoR and relational databases. It's also hammered home the usefulness of writing tests. You can't easily create a specifically formatted PDF all at once from a massive object. It's been a slow process of breaking down the parts and understanding each piece, then plugging that piece into the overarching shell to spit out something pretty.

As for my list, I finished reading about Kali but other things got waylaid in the move/new internship. Currently I'm focused on writing Pathfinder 2nd Edition rules in C#/.NET and beginning to study for [OSCP](https://www.offensive-security.com/information-security-certifications/oscp-offensive-security-certified-professional/").
