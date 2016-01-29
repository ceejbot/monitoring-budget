Monitoring on a budget

I was at a metrics & monitoring conference last year, because that's become my passion since starting at npm. While standing in line for lunch at the conference, I overheard a conversation behind me. One person said to another, "we have a team working on keeping our metrics database up."

"Wow!," I thought. "I also have a team running that same database! That team is about 1% of one person, *me*."

On a typical Tuesday, the npm registry serves about 150 million packages to Javascript developers running `npm install`. It'll handle peak loads of 10K requests/second even on a slow day. It generates about 200G of log data a day. This is notable use, well past what a typical startup company sees. But the registry team at npm is only four people, and we don't have a lot of money to spend on external services that couldn't handle all that data even if we could afford them.

So how do we know the npm registry is up and running? How do we get visibility on our maze of microservices and databases? We use chewing gum, baling wire, and a lot of open source tools, including our very own metrics system, `Numbat`.

I'm going to tell you all about Numbat, how we use it, and how you can steal code and ideas from us to monitor your own web services on the cheap. Because if you don't have metrics, you have *no idea* what your services are doing.
