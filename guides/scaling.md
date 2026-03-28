---
title: Scaling
description: Running Yosoi at scale with queues, observability, and distributed storage.
---

*Full documentation coming soon.*

Yosoi is designed to scale beyond a single machine. The integrations below are planned or in progress:

| Integration | Role |
|-------------|------|
| **Redis**<sup>[△](#ref-1)</sup> | Distributed selector cache and job state |
| **RabbitMQ**<sup>[○](#ref-2)</sup> | URL queue and worker coordination |
| **Prefect**<sup>[◑](#ref-3)</sup> | Workflow orchestration and scheduling |
| **Langfuse**<sup>[◇](#ref-4)</sup> | LLM observability and prompt tracing |
| **Persistence** | Durable result storage across runs |
| **Turso**<sup>[★](#ref-5)</sup> | Embedded distributed SQLite for selector snapshots |

More integrations TBD.

## References

<a id="ref-1"></a>△ **Redis**. Redis Ltd. *In-memory data structure store used as a database, cache, and message broker.* https://redis.io/docs/

<a id="ref-2"></a>○ **RabbitMQ**. Broadcom. *Open-source message broker supporting multiple messaging protocols.* https://www.rabbitmq.com/docs/

<a id="ref-3"></a>◑ **Prefect**. Prefect Technologies. *Workflow orchestration platform for data and ML pipelines.* https://docs.prefect.io/

<a id="ref-4"></a>◇ **Langfuse**. Langfuse. *Open-source LLM observability, tracing, and analytics platform.* https://langfuse.com/docs

<a id="ref-5"></a>★ **Turso**. ChiselStrike. *Embedded distributed SQLite built on libSQL.* https://docs.turso.tech/
