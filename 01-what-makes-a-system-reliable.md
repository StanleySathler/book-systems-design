# Chapter 1 — What Makes a System Reliable?

*Building systems that users can trust.*

Imagine you built an API that sends emails.

A user calls your API. You return `200 OK`.

But the email never gets sent.

Your API worked. Your server didn't crash. Your database is healthy.

**Yet your system failed.**

Reliability isn't just about keeping servers running. It's about making sure your system does what it promised to do.

## 1. The four pillars of reliability

There are four concepts worth understanding.

### Availability — Is it working?

Availability measures how often your system is operational and able to serve requests.

If your API is down for 10 minutes, it's unavailable during those 10 minutes.

**Approximate maximum downtime**

| Availability | Downtime per year |
|---|---:|
| 99% | 3.65 days |
| 99.9% | 8.76 hours |
| 99.99% | 52.6 minutes |
| 99.999% | 5.26 minutes |

More nines mean less room for downtime.

But availability alone doesn't guarantee that your system behaves correctly.

### Durability — Is the data safe?

Imagine your API accepts an email request and stores it in PostgreSQL.

A few seconds later, the server crashes.

When it comes back, the email request should still exist.

That's durability.

**Once your system promises that data is saved, it shouldn't lose it.**

### Fault tolerance — Can it survive failures?

Imagine you have three workers sending emails.

One crashes.

The other two continue processing jobs.

Your system survived a component failure without losing its core functionality.

That's fault tolerance.

A fault-tolerant system doesn't require every component to be healthy at all times.

### Reliability — Does it do what it promised?

Reliability is the bigger picture.

A reliable email API should:

- Accept valid requests.
- Keep accepted emails safe.
- Send them, or report when they cannot be sent.
- Avoid unintended duplicates.
- Recover from failures.

A system can be available but unreliable.

For example, an API that always returns `200 OK` but silently loses 5% of emails may have excellent HTTP availability and terrible reliability.

## 2. Reliability is a promise

Different systems make different promises.

A payment API might promise:

**"We won't charge you twice for the same payment."**

An inventory system might promise:

**"We won't sell more items than we have."**

An email API might promise:

**"Once we accept your email, we won't silently lose it."**

These promises shape your architecture.

If losing an email is unacceptable, storing it only in memory isn't enough.

If duplicate payments are unacceptable, retrying requests blindly isn't safe.

**You can't design reliability until you define what failure means.**

## 3. Reliability requires trade-offs

Suppose your database is unavailable.

Your email API has two options:

**Option A — Reject the request.**

Return `503 Service Unavailable`.

The user can retry later.

**Option B — Accept the request anyway.**

Return success and temporarily store the email in memory.

Option B improves short-term availability.

But if your server crashes, that email disappears.

For a system that promises not to lose accepted emails, Option A is safer.

Sometimes, **rejecting a request is more reliable than pretending it succeeded.**

## 4. How do we measure reliability?

Start with the promises you made.

For an email API, useful metrics include:

| Metric | What it tells you |
|---|---|
| API availability | Can users make requests? |
| Accepted-email loss rate | Are accepted emails disappearing? |
| Queue age | Are emails waiting too long? |
| Duplicate-send rate | Are customers receiving duplicates? |
| p99 latency | How slow are the slowest 1% of requests? |

Not all metrics are equally important.

A system with 99.99% API availability can still be unreliable if accepted emails frequently disappear.

Measure what users actually care about.

## 5. The most important lesson

Reliability isn't about preventing every failure.

That's impossible.

Servers crash. Networks disconnect. Databases become unavailable. Dependencies fail.

A reliable system expects these things to happen.

It knows how to respond, recover, and protect its promises.

**Remember:** A reliable system isn't one that never fails. It's one that handles failures without breaking its promises.

---

## Quick challenge

Your email API receives a request.

1. It saves the email in PostgreSQL.
2. It returns `200 OK`.
3. The server crashes before publishing the job to SQS.

The email exists in the database, but no worker knows about it.

**Is this system reliable? What would you change?**

*We'll revisit this scenario in Chapter 26: The Transactional Outbox.*
