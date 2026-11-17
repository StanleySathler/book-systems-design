# System Design: Building Systems That Don't Break

*A practical guide to scalable, resilient, and fault-tolerant systems.*

## Part 1 — The Foundations

*Understand what makes systems fail.*

1. **What Makes a System Reliable?** — Reliability, availability, durability, and fault tolerance.
2. **Everything Fails** — Networks, databases, workers, and dependencies.
3. **Latency vs. Throughput** — Fast responses don't mean high capacity.
4. **The Bottleneck Problem** — Your system is only as fast as its slowest part.
5. **Horizontal vs. Vertical Scaling** — More machines or bigger machines?
6. **Stateless vs. Stateful Services** — Why state makes scaling harder.
7. **Consistency vs. Availability** — What happens during network partitions?

## Part 2 — Handling Failures

*Failures are inevitable. Data loss doesn't have to be.*

8. **Timeouts** — Never wait forever.
9. **Retries** — When trying again helps, and when it hurts.
10. **Exponential Backoff & Jitter** — Retry without overwhelming the system.
11. **Idempotency** — Make repeated requests safe.
12. **Circuit Breakers** — Stop calling broken dependencies.
13. **Fallbacks** — What to do when your primary service fails.
14. **Graceful Degradation** — Keep the important features working.
15. **Bulkheads** — Prevent one failure from taking everything down.
16. **Dead Letter Queues** — What to do with jobs that keep failing.
17. **Reconciliation** — Repair inconsistencies after failures.

## Part 3 — Data & Consistency

*Keep your data correct, even under concurrency.*

18. **Database Transactions** — All or nothing.
19. **Race Conditions** — Two requests, one shared resource.
20. **Optimistic vs. Pessimistic Locking** — Prevent conflicting updates.
21. **Isolation Levels** — What transactions can see.
22. **Unique Constraints** — Let the database enforce correctness.
23. **Replication** — Copies improve availability, but create challenges.
24. **Replication Lag** — Why a successful write might not be visible.
25. **Sharding & Partitioning** — When one database isn't enough.
26. **The Transactional Outbox** — Save data and publish events reliably.
27. **Sagas** — Transactions across multiple services.
28. **Schema Migrations Without Downtime** — Change production safely.

## Part 4 — Queues & Background Jobs

*Move work out of the request path.*

29. **Synchronous vs. Asynchronous Processing** — When to wait and when to queue.
30. **Message Brokers vs. Database Queues** — SQS, Kafka, Redis, or PostgreSQL?
31. **Delivery Guarantees** — At-most-once, at-least-once, and exactly-once.
32. **Workers & Concurrency** — Process more jobs without creating chaos.
33. **Visibility Timeouts & Leases** — Recover jobs from dead workers.
34. **Duplicate Messages** — Why consumers must be idempotent.
35. **Message Ordering** — When order matters.
36. **Poison Messages** — One bad job shouldn't block everyone.
37. **Queue Backlogs** — What happens when jobs arrive faster than they finish.

## Part 5 — Scaling & Traffic Control

*Survive more traffic without falling apart.*

38. **Load Balancing** — Distribute requests across servers.
39. **Caching** — Reduce repeated work.
40. **Cache Invalidation** — The hard part of caching.
41. **Cache Stampedes** — When everyone requests the same missing data.
42. **Rate Limiting** — Protect systems from excessive requests.
43. **Token Bucket vs. Leaky Bucket** — Different ways to control traffic.
44. **Distributed Rate Limiting** — Enforce limits across many servers.
45. **Backpressure** — Slow producers when consumers can't keep up.
46. **Load Shedding** — Reject work to protect the system.
47. **Priority Queues & Fairness** — Serve important work without starving others.
48. **Hot Partitions** — When traffic isn't distributed evenly.
49. **Autoscaling** — Add capacity before it's too late.

## Part 6 — Observability & Operations

*Know something is broken before customers tell you.*

50. **Metrics, Logs & Traces** — Three ways to understand your system.
51. **SLIs, SLOs & SLAs** — Define what reliable actually means.
52. **Percentiles: p50, p95, p99** — Why averages lie.
53. **Health Checks** — Is the service alive or actually working?
54. **Alerting** — Wake someone up only when necessary.
55. **Error Budgets** — Balance shipping features with reliability.
56. **Incident Response** — What to do when production breaks.
57. **Postmortems** — Learn from failures without blaming people.
58. **Chaos Engineering** — Break things intentionally.
59. **Capacity Planning** — Know your limits before reaching them.

## Part 7 — Putting Everything Together

*Build real systems, then deliberately break them.*

60. **Design a Reliable Email API** — Queues, retries, idempotency, providers.
61. **Design a Payment System** — Prevent duplicate charges and lost payments.
62. **Design an Inventory Reservation System** — Handle concurrent purchases.
63. **Design a Webhook Delivery System** — Retry safely and handle slow consumers.
64. **Design a Notification System** — Millions of events, multiple channels.
65. **Design a Distributed Job Scheduler** — Run jobs reliably across machines.
66. **Design a Large-Scale Data Migration** — Move millions of records without downtime.
67. **Design a Multi-Region Service** — Survive a regional outage.
