# How to save user password

## Beginner

将明文密码做**one-way** hash然后save。

单向哈希有两个特性：

1. 从同一个密码进行单向哈希，得到的总是唯一确定的摘要
2. 计算速度快。随着技术进步，尤其是显卡在高性能计算中的普及，一秒钟能够完成数十
亿次单向哈希计算

Attacker可以将所有常用密码组合进行one-way hash，然后得到一个组合，与数据库中的摘
要进行对比就可以获得密码，叫做**rainbow table**

- lookup tables
- reverse lookup tables
- rainbow tables

## intermediate

### Salted Hash

We can prevent these attacks by randomizing each hash, so that when the same
password is hashed twice, the hashes are not the same.

We can randomize the hashes by appending or prepending a random string, call `salt`.
To check if a password is correct, we need the salt, so it is usually stored in
the user account database along with the hash.

#### safety

The salt does not need to be secret. Just by randomizing the hashes, lookup
tables, reverse lookup tables, and rainbow tables become ineffective. An
attacker won't know in advance what the salt will be, so they can't pre-compute
a lookup table or rainbow table.

#### Wrong usage

- salt reuse
- short salt
- Double Hashing & Wacky Hash Functions

### right-way

#### The basic

Salt should be generated using a Cryptographically Secure Pseudo-Random Number Generator (CSPRNG). 

To Store a Password

1. Generate a long random salt using a CSPRNG.
2. Prepend the salt to the password and hash it with a standard cryptographic hash function such as SHA256.
3. Save both the salt and the hash in the user's database record.

To Validate a Password

1. Retrieve the user's salt and hash from the database.
2. Prepend the salt to the given password and hash it using the same hash function.
3. Compare the hash of the given password with the hash from the database. If they match, the password is correct. Otherwise, the password is incorrect.

#### In web application, always hash on the server.

#### Making Password Cracking Harder: slow hash functions

`Key stretching`

这类方案有一个特点，算法中都有个因子，用于指明计算密码摘要所需要的资源和时间，也就是计算强度。计算强度越大，攻击者建立rainbow table越困难，以至于不可继续。

The idea is to make the hash function very slow, so that even with a fast GPU
or custom hardware, dictionary and brute-force attacks are too slow to be
worthwhile. The goal is to make the hash function slow enough to impede attacks,
but still fast enough to not cause a noticeable delay for the user.

Use a standard algorithm like [PBKDF2](http://en.wikipedia.org/wiki/PBKDF2) or
[bcrypt](http://en.wikipedia.org/wiki/Bcrypt).

### Impossible-to-crack Hashes: Keyed Hashes and Password Hashing Hardware

## History

首先让我们来看看不同的技术出现的时间： 

- 明文存储：有史以来 
- hash 存储：20世纪70年代早期 
- 加盐 hash：20世纪70年代晚期 
- bit/key stretching： bcrypt 2002， scrypt 2009， PBKDF2 2009 

## References

- [如何安全地存储密码](chrome-extension://klbibkeccnjlkjkiokjodocebajanakg/suspended.html#uri=http://blog.jianguoyun.com/?p=438)
- [hashing-security](https://crackstation.net/hashing-security.htm)
- [hash, salt及更多](http://www.oschina.net/question/28_57478?fromerr=VIo1n1ny)
- [加盐密码hash，如何正确使用](http://blog.jobbole.com/61872/)
- [各种语言的方案](http://www.freebuf.com/articles/web/96473.html)
