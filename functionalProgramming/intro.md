# Functional Programming

```java
int increment(int cnt) {
    return cnt+1;
}
```

不依赖于外部的数据，而且也不改变外部数据的值，返回一个新的值。

## 三大特性

- immutable data
- first class functions
- tail call, tail recursion

## Techniques

- map & reduce
- pipeline
- recursing
- currying
    + 把函数当成变量来用，关注于描述问题而不是怎么实现
- higher order function

## Advantages

- parallelization
- lazy evaluation
- determinism

### map & reduce

```python
name_len = map(len, ['hao', 'chen', 'coolshell'])
print(name_len)
```

Others:

- filter
- find
- all
- any


