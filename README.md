# cryptocurrency-transactions

## Bitcoin transaction

比特币交易的本质是包含交易参与者之间价值转移相关信息的数据结构。可以将比特币交易理解成纸质支票有助于理解其工作原理。

一笔比特币交易大小一般为为300-400Bytes。通过验证的交易会在秒级时间内扩散到网络中所有的节点。异常交易所能到达的节点不会超过一个。

![image](https://github.com/nil-zhang/cryptocurrency-transactions/blob/master/images/bitcoin-tx-overview-spending.svg)

比特币交易的基本单位是未经使用的交易输出，简称UTXO。比特币可以被分割成表示八位小数的“聪”，UTXO可以是一“聪”的任意倍，但UTXO一旦被创建出来就是不能被再次分割的。

一笔比特币交易通过使用所有者的签名来解锁UTXO，并通过使用新的所有者的比特币地址来锁定并创建UTXO。

给某人发送比特币实际上是创造新的UTXO，注册到那个人的地址，并且能被他用于新的支付。

UTXO被每个全节点在存储于本地内存数据库 — “UTXO池”，新的交易从UTXO池中消耗一个或多个输出。

![image](https://github.com/nil-zhang/cryptocurrency-transactions/blob/master/images/bitcoin-transaction-propagation.svg)

交易输出包含一定量的比特币（聪）和一个锁定脚本。锁定脚本会把输出锁在一个特定的比特币地址上，从而把一定数量的比特币所有权转移到新的所有者上。
交易输入是指向UTXO的指针。若想支付UTXO，一个交易的输入也需要包含一个解锁脚本，用来满足UTXO的支付条件。解锁脚本通常是一个签名，用来证明对于在锁定脚本中的比特币地址拥有所有权。

交易费基于交易的尺寸，用KBytes来计算，而不是基于比特币的价值。最小交易费被固定在0.0001BTC/KBytes。交易费没有特定的字段表示，而是通过所有输入的总和，以及所有输出的总和之间的差值来表示。

比特币交易脚本是一种逆波兰表示法的基于栈的执行语言。该语言没有循环和大部分流控制，是非图灵完备的；但脚本的复杂性有限，也保证了交易可执行次数的可预见性，增加了脚本的安全性。

![image](https://github.com/nil-zhang/cryptocurrency-transactions/blob/master/images/bitcoin_transaction_chain.png)

## Ethereum transaction

Ethereum 在 transaction 层面和 Bitcoin 最大的区别是 Ethereum 是 Account 模型（Bitcoin 是没有 Account 的）。在 Ethereum 中有两种类型的 Account，一种是被私钥控制的 Account，它没有任何的代码，与 Bitcoin 地址基本有完全相同的功能，能够向网络中发送已签名的 transaction；另一种是被 smart contract 控制的 Account，能够在每一次收到消息时，执行保存在 contract_code 中的代码，所有的 smart contract 在网络中都能够响应其他账户的请求和消息并提供一些服务。

![image](https://github.com/nil-zhang/cryptocurrency-transactions/blob/master/images/ethereum_transaction.png)

Account 模型是一种非常容易理解的区块链应用模型，它与我们生活中的账户模型非常相似，只是为了保证账户的安全，使用了签名以及 nonce 的机制阻止恶意的攻击。这种基于 Account 模型的应用包含了一个包含所有账户余额的全局状态，在进行转账时，需要由节点对账户的余额进行验证，判断当前账户是否有足够的 Ether 进行转账。

![image](https://github.com/nil-zhang/cryptocurrency-transactions/blob/master/images/ethereum_state_transition.png)

## EOS transaction

## Monero transaction

Monero 使用三项关键技术实现了区块链的交易隐私保护：隐秘地址 (stealth address)、环签名 (ring signature)、环签名机密交易 (Ring CT)。但 transaction 还是基于标准的 Bitcoin UTXO 模型。当 Monero 中的发起者构造一笔交易时，首先从区块链系统所记录的历史交易中，找寻到与自己想要使用的 output 同等面值的其它 output (属于其它公钥)来构成一个环签名，并通过这种方式来达到发送者隐私保护。

在以前的比特币系统中，节点会将输入引用的输出从 UTXO 集合中移走，从而保证 output 只被花费一次，但是在门罗币系统中是通过 Key Image 来实现的。Key Image := x Hp(P) ，其中 x 是私钥，P 是公钥，即 P = x G。即相同的 P 导致会产生相同的 Key Image。所以门罗币系统中的节点会维护一个已见到过的所有 Key Image 集合，如果一笔交易的 Key Image 出现在该集合中，则被认为是无效的。
![image](https://github.com/nil-zhang/cryptocurrency-transactions/blob/master/images/cryptnote_transaction.png)

Menero 典型的交易过程如下：

Bob决定支付一笔输出，其被发送到一次性公钥。他需要Extra (1), TxOutNumber (2) 以及其账号私钥(3)来恢复其一次性私钥(4)。
当发送一笔交易给Carol时，Bob随机生成其Extra值(5)。Bob使用Extra (6), TxOutNumber (7) 和Carol的账号公钥(8.) 来得到其输出公钥(9)。
面对其他钥匙(10)，Bob在输入值中隐藏了其对应输出的链接。为了避免双重支付，他还打包了产生于一次性私钥(11)的钥匙图像。
最后，Bob使用他的一次性私钥(12), 所有的公钥 (13) 和钥匙图像 (14)对这次交易进行了签名。他在交易的最后进行了环签名(15)。
![image](https://github.com/nil-zhang/cryptocurrency-transactions/blob/master/images/cryptonote_transaction.png)

## zcash transaction

在Zcash中，想发送一笔私密交易款项，支付方不能直接向收款方证明，因为区块链网络是透明的。只能以匿名的方式，但是这样收款方就不知道是谁发的。支付方想要向收款方证明，就需要在支付同时带上一定能间接证明自己身份且不会被他人认出的信息，比如一段经过加密的字符串。这时只要支付方提供查看密钥给收款方，收款方解密后就可知道交易信息。支付方可以自主决定将查看密钥给谁，因此，他可以让很多人都知道这笔交易，也可以不让任何人知道，实现绝对的私密。

![image](https://github.com/nil-zhang/cryptocurrency-transactions/blob/master/images/zcash-transaction.png)

## comparison of transaction 

|  cryptocurrency     | Bitcoin     | Ethereum    | EOS     | Monero     | zcash    |
| ---------- | :-----------:  | :-----------: | ---------- | :-----------:  | :-----------: |
|      |      |      |     |      |      |
|      |      |      |     |      |      |
|      |      |      |     |      |      |
|      |      |      |     |      |      |
|      |      |      |     |      |      |
|      |      |      |     |      |      |
|      |      |      |     |      |      |
|      |      |      |     |      |      |
|      |      |      |     |      |      |

