# Binary Indexed Tree

First used for data compression. Now it's often used for storing frequencies and
manipulating cumulative frequency tables.

## problem to attack

We have n boxes, possible queries are

1. add marble to box `i`
2. sum marbles from box `k` to bok `l`

The naive solution has time complexity `O(1)` for query 1 and `O(n)` for query 2.
Suppose make `m` queries, the worse case time complexity `O(m * n)`.

1. Using `RMQ`, can solve it with worsr case time complexity `O(mlogn)`
2. Using `BIT`, also `O(mlogn)`, but eaiser to code and less memory space


