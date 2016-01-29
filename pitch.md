# Monitoring on a budget

## elevator pitch

Trendy microservices, all over the place zooming data around. What are they doing? How often are they doing it? You need metrics & monitoring to get the visibility into your systems that you need, and if you're like me, you can't afford to spend a lot to have them. Here's how npm does it.

## description

I was at a metrics & monitoring conference last year, because npm registry metrics are my obsession now that I run the registry. While standing in line for lunch at the conference, I overheard a conversation behind me. One person said to another, "we have a team working on keeping our metrics database up."

"Wow!," I thought. "I also have a team running that same database! That team is about 1% of one person, *me*."
On a typical Tuesday, the npm registry serves about 150 million packages to Javascript developers running `npm install`. It'll handle peak loads of 10K requests/second even on a slow day. It generates about 200G of log data a day. This is notable use, well past what a typical startup company sees. But the registry team at npm is only four people, and we don't have a lot of money to spend on external services that couldn't handle all that data even if we could afford them.

So how do we know the npm registry is up and running? How do we get visibility on our maze of microservices and databases? We use chewing gum, baling wire, and a lot of open source tools, including our very own metrics system, `numbat`.

I'm going to tell you all about `numbat`, how we use it, and how it does not *just* pretty graphs but also application-aware monitoring, all in javascript! You can borrow code and ideas from us to monitor your own web services on the cheap. Because if you don't have metrics, you have *no idea* what your services are doing.

## bio

CJ, known to her friends as "ceej", has been on the Internet making mistakes since 1987. She has somehow survived to enjoy writing software even more than she did back then, and she suspects she might have learned some useful things about how to do it during that time. Her current position as VP of Engineering at npm, Inc, is her favorite job ever. She gets to run the npm registry and the amazing tiny team that keeps the packages flowing.

Her favorite member of One Direction is Brian Eno.
