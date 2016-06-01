# [fit] monitoring
# [fit] on a budget

---

![left](images/bumper2_nasa_big.jpg)
# [fit] C J Silverio
## [fit] vp of engineering, ![](images/npm.png)

## [fit] @ceejbot

^ How many of you have ever used npm to install something? How many of you use it daily? Yeah, that's a lot of you.

---  

# [fit] big numbers
# [fit] \(and some small ones)

---

# [fit] 205 million packages Tuesday
# [fit] 1 billion over the week

^ 205 million packages were downloaded on Tuesday. We're at 1 billion over the last week, and Monday was a US holiday.

----

# [fit] that's respectable
# [fit] that's starting to scale

^ That's starting to scale! Surely, CJ, you have a big team!

---

# [fit] npm is 25 people
# [fit] 4 of them are the registry team

^ We have 25 people now. When we started, it was 14 million / day with 5 people. Total. Most companies with services this large got there slowly and have staff to match. Not npm. We're a hobby project gone viral-- kaboom! If you're a javascript programmer, you're probably using us. Monitorama story.

---

# [fit] success is often
# [fit] a catastrophe

---

# [fit] solve problems on a
# [fit] shoestring budget

^ True story: I was at monitorama and (story here)

---

# [fit] keep the registry up so
# [fit] you never think about it

---

# [fit] 2 questions:
# [fit] is the registry up?
# [fit] how well is it performing?

---

# [fit] is the registry up?
# [fit] monitoring

---

# [fit] how well is it performing?
# [fit] metrics

---

# [fit] monitoring

---

# [fit] nagios
# [fit] state of the art in free

^ Trigger warning for web developers for the image I'm about to show.

---

![](images/nagios.png)

^ This is awful information design. The depressing thing is it works.

---

# [fit] It's okay. We never look at it.
# [fit] It just triggers Pager Duty.

^ Breathe.

---

# [fit] monitoring == pull
# [fit] ask questions that you
# [fit] know the right answers for

---

### [fit] Is this host up?
### [fit] Is this cert about to expire?
### [fit] Is the DB replication keeping up?

---

# [fit] if you get the wrong answer
# [fit] somebody gets paged

---

# [fit] nagios's virtue:
# [fit] custom checks

^ is couchdb replicating? are our CDN's error rates low? Are we getting too many issues on our public issue tracker?

---

# [fit] self-healing checks
# [fit] automate the fix if you can!

^ Hot budget tip! Don't involve a human.

---

# [fit] monitoring == unit tests

^ It's an engineering ratchet: you prevent yourself from having that bug again. After every production incident, we add monitoring.

---

# [fit] monitoring tells you what
# [fit] it doesn't tell you why

^ For that you need...

---

# [fit] metrics

^ Metrics.

---

# [fit] Q: What's a metric?

---

### [fit] Q: What's a metric?
### [fit] A: A name + a value + a time.

---

## kinds of metrics

- counter: it happened __N__ times
- gauge: it's __Y__-sized right now
- rate: it's happening __N__ times per second
- timing: it took __X__ milliseconds to do

---

# [fit] metrics == push
# [fit] the service tells you numbers

---

# [fit] emit from a service
# [fit] store in timeseries db
# [fit] query & graph

---

# [fit] the usual stack
# [fit] statsd ➜ graphite ➜ grafana

^ State of the art in free

---

![](images/grafana_dashboard_ex1.png)

^ This is grafana.

---

# [fit] I didn't like the
# [fit] state of the art

^ I am fussy.

---

* statsd is unconfigurable & uses UDP
* graphite is [wincing gif]
* grafana is aces though!

---

# [fit] Q: Why not send metrics over UDP?
## [fit] A: You care about receiving them.

^ How about when your system is stressed?

---

# [fit] for-pay services can do better
# [fit] but I can't afford them

---

# [fit] monitoring 400 processes right now
# [fit] 12+ GB of log data a day

^ For-pay services charge by volume, and volume is what the registry has.

---

# [fit] interlude:
# [fit] when *should* you pay?

---

# [fit] convert the £$€ cost
# [fit] into engineer hours/month

^ Realistically, to get the same results, how much time would you have to spend to get the results from that service? Are you okay with the half-decent version you get doing it yourself? Are you ready to devote an engineer?

---

## numbat was born

### "How hard can it be?" I said.

^ I wrote a manifesto with block diagrams and things. It was very blue-sky.

---

![fit](images/processing_metrics.png)

^ Weirdly this is pretty much what I ended up building.

---

## https://github.com/numbat-metrics

---

# [fit] npm's stack
# [fit] numbat ➜ influxdb ➜  grafana

---

![](images/Numbat_Full_Standing.jpg)

^ We have a thing about cute Australian marsupials at npm. Don't ask me why.

---

```js
var Emitter = require('numbat-emitter');

var emitter = new Emitter({
    uri: 'tcp://localhost:3333',
    app: 'www',
});

process.emit('metric', { name: 'httpd.latency', value: 30 });
process.emit('metric', { name: 'disk.used.percent', value: 36 });
process.emit('metric', { name: 'heartbeat' });
```

^ Every service npm runs in production has one of these.

---

It's so easy to emit a metric
any time something interesting happens
that we just do it

---

Every host has a collector.
The collector sends metrics to many destinations.
One of them is influxdb.
Grafana then draws pretty charts.

---

# [fit] 4000 metrics/sec
# [fit] from the registry

---

![fit](images/user-acl-two-response-codes.png)

^ See some spikes? We flushed a cache last night!

---

![](images/user-acl-two-more.jpg)

^ These are not just pretty graphs! These four charts show a problem with a service we'd just started sending traffic to. Latencies shot up!

---

![](images/grafana-four-charts.jpg)

^ The answer is here, in this second screenshot from the same page of graphics. The number queries used to answer handle that route was too high-- needed a redesign behind the scenes. Which we did. We spotted a db problem before we had it. Yay metrics!

---

# [fit] metrics ➜ alerts

^ We've got a metrics analyzer yelling at very low latency into a slack channel when certain metrics go out of bounds.

---

# [fit] Is a server handling traffic?
# [fit] Is latency higher than normal?
# [fit] Is your error rate higher than usual?

^  Your metrics know, and can yell if you vary from it.

---

# [fit] anomaly detection
# [fit] the real state of the art

^ Humans are really good at this: we are walking pattern detection engines. You looked at that chart and saw a pattern & a violation of the pattern, and you asked a question about it.

---

# [fit] numbat's stretch goal
# [fit] \(the framework is there)

^ Big companies like Twitter & Netflix have teams bigger than my entire registry team working on this, and there are some


---

# [fit] what: monitoring
# [fit] yes/no questions

---

# [fit] why: metrics
# [fit] data changing over time

---

# [fit] next: anomaly detection
# [fit] predictions & trends

---

# [fit] Don't guess.
# [fit] Get data.

---

# [fit] `npm install -g npm@latest`
# [fit] @ceejbot on all the things
