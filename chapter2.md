# chapter 2
密码学原理

比特币中，主要用到了密码学中的两个功能。密码学中的哈希函数被称为 cryptographic hash function，有两个重要性质：
1. collision resistance
    1. 如果 x 不等于 y，但是 H(x) = H(y)，则被称为哈希碰撞
    2. 如果有 256 位的哈希值，则是 $2^256$，按鸽笼原理，则一定会出现碰撞。
    3. 所以哈希碰撞一定会发生，只是看当前函数的碰撞的概率
    4. collision resistance 用处：某一个信息 m，H(m) 是信息摘要，digest，查看篡改情况
    5. 上传文件之前，存一个 hash，下载之后存一个 hash，对比hash来看看是否一致
    6. md5曾经是一个很流行的哈希函数，但是现在已经知道人为的如何制造哈希碰撞
2. hiding 
    1. 是指哈希函数的计算过程是单向不可逆的，给定 x 可以得到 H(x)，反之不行
    2. sealed envelope
    3. puzzle friendly
    4. 工作量证明，proof of work，找到符合要求的length了，是没有捷径的
    5. 挖矿难，验证很容易

sha-256：secure hash algorithm，是满足上述的若干性质的哈希算法

创建账户：(public key, private key)。非堆成加密体系，asymmetric encryption algorithm。创建之后，就拥有了账户
1. 加密是用公钥，解密用私钥（加密和解密都是用的同一个人的，是接收方的）。公钥是不用保密，私钥是要保密的。私钥只需要保存本地就可以。这就解决了，对称加密体系中的问题。
2. 比特币加密系统，公钥 = 账户，私钥 = 密码。

