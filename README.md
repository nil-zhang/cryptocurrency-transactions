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

## zcash transaction

## conclusion
