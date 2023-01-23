# 比特币的数据结构
哈希指针 hash pointers

普通的指针，p 只是指向一个地址。哈希指针，除了地址，还要保存哈希值。

区块链是一个一个链表，那么区块链里面的指针是用哈希指针代替了普通的指针。最先出现的区块是 genesis block，最晚产生的区块是 most recent block。（注意，是最晚出现的区块，指向最先出现的区块）
1. 区块链结构性质，tamper-evident log 篡改证明记录
    1. 例子，如果有个人篡改了区块链中某一个 block 的记录，那么篡改之后，之后的区块就会被修改，以此类推，那么最终系统保存的哈希值，在验证的时候，会对不上。所以，我们哈希链表，只需要保存最晚生成的哈希值，就可以验证之后的哈希表是否被篡改。
2. merkle tree，和 binary tree 差不多。区别和链表与区块链的区别一样，是用哈希指针代替了，普通的指针，然后形成树结构。只不过方向也是反的，merkle tree 的底部是最新生成的，是叶子结点，往上指
    1. 最下面的是数据块，data blocks
    2. 非叶子结点都是哈希指针
    3. merkle tree 的用途，提供 merkle proof。比特币的结点，有全结点（block header，block body），轻结点（比如手机，钱包）。如果需要向轻结点证明，支付是否未完成，那么如何验证交易是否在区块链上？
    4. 首先，找到 merkle tree 的 data block 的位置，然后从该位置一直往上，到根结点的路径就是 merkle proof。
    5. merkle tree 可以代替区块链上的一个 block
    6. spv 是本地计算，H() 是向全结点请求，轻结点计算全节点发送的，相邻结点的哈希值，即可以证明了。
    7. proof of membership，proof of inclusion。也就是说，验证算法的复杂度。merkle proof 是 O(log(n))。如果要证明 proof of non-membership，那么就很难证明了，是 O(n)
    8. 如果，没有对叶结点对排序的前提的话，那么就一定是 O(n) 的顺序，如果排序好的，叫 sorted merkle tree，但是比特币中不要求排序，因为比特币中不太有 proof of non-membership 的情况
    9. 只要无环数据结构，都可以用哈希指针来代替普通指针。

