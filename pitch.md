# Monitoring on a budget

## elevator pitch

Trendy microservices! Traditional monoliths! You have services backing your web sites. What are they doing? How often are they doing it? Do you have visibility into your systems? What does that mean? Why does it matter? How can you get it? How can you get visibility into your systems when you've got a tight budget? Here's how the npm registry does it.

## description

On a typical Tuesday, the npm registry serves about 150 million packages to Javascript developers running `npm install`. It'll handle peak loads of 10K requests/second even on a slow day. It generates about 200G of log data a day. This is notable use, well past what a typical startup company sees. But the registry team at npm is only four people, and we don't have a lot of money to spend on external services that couldn't handle all that data even if we could afford them.

So how do we know the npm registry is up and running? How do we get visibility on our maze of microservices and databases? What's the next step beyond using PingDom or a service like it to figure out if your service is up? What should you do if you want to ask questions about the performance of a complicated maze of services? How do you get those pretty graphs and dashboards that look like mission control for a space launch without a whole team working on it?

At npm we've experimented with a lot of open-source tools, selected the ones that helped us most, and written a collection of other open-source tools to bring them all together. I'm going to tell you all about the Numbat-Powered Metrics system, how we use it, and how it does not *just* pretty graphs but also application-aware monitoring, all in javascript! You can borrow code and ideas from us to monitor your own web services on the cheap. Because if you don't have metrics, you have *no idea* what your services are doing.

## bio

CJ, known to her friends as "ceej", has been on the Internet making mistakes since 1987. She has somehow survived to enjoy writing software even more than she did back then, and she suspects she might have learned some useful things about how to do it during that time. Her current position as VP of Engineering at npm, Inc, is her favorite job ever. She gets to run the npm registry and the amazing tiny team that keeps the packages flowing.

Her favorite member of One Direction is Brian Eno.

## why me

Metrics and monitoring are my new obsession now that I'm responsible for the npm package registry. I was at a metrics & monitoring conference last year to learn how big companies do it and steal some tips. While standing in line for lunch at the conference, I overheard a conversation behind me. One person said to another, "we have a team working on keeping our metrics database up."

"Wow!," I thought. "I also have a team running that same database! That team is about 1% of one person, *me*."
