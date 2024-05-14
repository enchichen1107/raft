# Raft

## Verification

```go
go test -timeout 60s -race -count 1 ./...
```
![Alt text](./img/result.png?raw=true "test result")

## For Students of the NTHU CS5426 Distributed System Course

In the final project, you are asked to implement the Raft consensus algorithm, also a replicated state machine protocol, as the [paper](https://raft.github.io/raft.pdf) described and learn to:

- Use Go to implement the Raft module and learn to use Go to develop a concurrent, distributed applications.
- Use gRPC to communicate between services.
- The first version of your Raft implementation may be buggy. Learn to develop and debug in a large distributed applications. Be careful about deadlock and data race condition. Most of you bugs can be found by logging all the variables and states.
- Learn to design and write tests to verify your implementation.

The implementation will be divided into 2 parts: leader election, log replication.

## Future Work

There are many other works can be done to improve the Raft we designed, the following are some:

1. Log compaction: It is not practical for a long-running Raft server to store the complete logs forever. Instead, store a snapshot of the state from time. So Raft can discards log entries that precede the snapshot.
2. The paper mentioned that **"if AppendEntries fails because of log inconsistency: decrement nextIndex and retry"**. In the implementation, `nextEntry` decrease by 1 at once, it may need to retry too many times if the replication lag is huge. By adding more information to the `AppendEntries` RPC's response, can you find a way to know how much should `nextEntry` decrease if log inconsistency occur?
