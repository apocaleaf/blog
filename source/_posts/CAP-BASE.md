---
title: 'CAP and BASE Theorem'
date: 2023-11-04 05:47:13
excerpt: 'CAP and BASE Theorem'
categories: 分布式系统
tags: [分布式系统, 数据一致性]
---

# CAP
## Definition
In [theoretical computer science](https://en.wikipedia.org/wiki/Theoretical_computer_science), the CAP theorem, also named Brewer's theorem after computer scientist [Eric Brewer](https://en.wikipedia.org/wiki/Eric_Brewer_(scientist)), states that any [distributed data store](https://en.wikipedia.org/wiki/Distributed_data_store) can provide only [two of the following three](https://en.wikipedia.org/wiki/Trilemma) guarantees:[[1]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-Gilbert_Lynch-1)[[2]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-2)[[3]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-3)
[Consistency](https://en.wikipedia.org/wiki/Consistency_model)
Every read receives the most recent write or an error.
[Availability](https://en.wikipedia.org/wiki/Availability)
Every request receives a (non-error) response, without the guarantee that it contains the most recent write.
[Partition tolerance](https://en.wikipedia.org/wiki/Network_partitioning)
The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes.
When a [network partition](https://en.wikipedia.org/wiki/Network_partition) failure happens, it must be decided whether to do one of the following:

- cancel the operation and thus decrease the availability but ensure consistency
- proceed with the operation and thus provide availability but risk inconsistency.

[![image.png](https://cdn.nlark.com/yuque/0/2023/png/38373106/1698518185421-e55f0b31-6c77-4057-b5c0-33f08d2429d8.png#averageHue=%23d7e4b9&clientId=ucc119fa9-213c-4&from=paste&id=u33e5dcb9&originHeight=219&originWidth=220&originalType=url&ratio=1&rotation=0&showTitle=false&size=25893&status=done&style=none&taskId=ub22a2ee4-0555-4b31-96ed-9d0e0fa8082&title=)](https://en.wikipedia.org/wiki/File:CAP_Theorem_Venn_Diagram.png)
CAP Theorem Venn Diagram
Thus, if there is a network partition, one has to choose between consistency or availability. Note that consistency as defined in the CAP theorem is quite different from the consistency guaranteed in [ACID](https://en.wikipedia.org/wiki/ACID) [database transactions](https://en.wikipedia.org/wiki/Database_transaction).[[4]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-4)
## Explanation
No distributed system is safe from network failures, thus network partitioning generally has to be tolerated.[[5]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-5)[[6]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-6) In the presence of a partition, one is then left with two options: consistency or [availability](https://en.wikipedia.org/wiki/Availability). When choosing consistency over availability, the system will return an error or a time out if particular information cannot be guaranteed to be up to date due to network partitioning. When choosing availability over consistency, the system will always process the query and try to return the most recent available version of the information, even if it cannot guarantee it is up to date due to network partitioning.
In the absence of a partition, both availability and consistency can be satisfied.[[7]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-paclec-7)
Database systems designed with traditional [ACID](https://en.wikipedia.org/wiki/ACID) guarantees in mind such as [RDBMS](https://en.wikipedia.org/wiki/Relational_database_management_system) choose [consistency](https://en.wikipedia.org/wiki/Consistency_(database_systems)) over availability, whereas systems designed around the [BASE](https://en.wikipedia.org/wiki/Eventual_consistency) philosophy, common in the [NoSQL](https://en.wikipedia.org/wiki/NoSQL) movement for example, choose availability over consistency.[[8]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-Brewer2012-8)
## History
According to [University of California, Berkeley](https://en.wikipedia.org/wiki/University_of_California,_Berkeley) computer scientist [Eric Brewer](https://en.wikipedia.org/wiki/Eric_Brewer_(scientist)), the theorem first appeared in autumn 1998.[[8]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-Brewer2012-8) It was published as the CAP principle in 1999[[9]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-Brewer1999-9) and presented as a [conjecture](https://en.wikipedia.org/wiki/Conjecture) by Brewer at the 2000 [Symposium on Principles of Distributed Computing](https://en.wikipedia.org/wiki/Symposium_on_Principles_of_Distributed_Computing) (PODC).[[10]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-Brewer2000-10) In 2002, [Seth Gilbert](https://en.wikipedia.org/w/index.php?title=Seth_Gilbert&action=edit&redlink=1) and [Nancy Lynch](https://en.wikipedia.org/wiki/Nancy_Lynch) of [MIT](https://en.wikipedia.org/wiki/MIT) published a formal proof of Brewer's conjecture, rendering it a [theorem](https://en.wikipedia.org/wiki/Theorem).[[1]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-Gilbert_Lynch-1)
In 2012, Brewer clarified some of his positions, including why the often-used "two out of three" concept can be somewhat misleading because system designers only need to sacrifice consistency or availability in the presence of partitions; partition management and recovery techniques exist. Brewer also noted the different definition of consistency used in the CAP theorem relative to the definition used in [ACID](https://en.wikipedia.org/wiki/ACID).[[8]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-Brewer2012-8)[[11]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-:0-11)
A similar theorem stating the trade-off between consistency and availability in distributed systems was published by Birman and Friedman in 1996.[[12]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-12) Birman and Friedman's result restricted this lower bound to non-commuting operations.
The [PACELC theorem](https://en.wikipedia.org/wiki/PACELC_theorem), introduced in 2010,[[7]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-paclec-7) builds on CAP by stating that even in the absence of partitioning, there is another trade-off between latency and consistency. PACELC means, if partition (P) happens, the trade-off is between availability (A) and consistency (C); Else (E), the trade-off is between latency (L) and consistency (C).
