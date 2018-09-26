# cryptocurrency-transactions

## Bitcoin transaction

比特币交易的本质是包含交易参与者之间价值转移相关信息的数据结构。可以将比特币交易理解成纸质支票有助于理解其工作原理。

一笔比特币交易大小一般为为300-400Bytes。通过验证的交易会在秒级时间内扩散到网络中所有的节点。异常交易所能到达的节点不会超过一个。

比特币交易的基本单位是未经使用的交易输出，简称UTXO。比特币可以被分割成表示八位小数的“聪”，UTXO可以是一“聪”的任意倍，但UTXO一旦被创建出来就是不能被再次分割的。

一笔比特币交易通过使用所有者的签名来解锁UTXO，并通过使用新的所有者的比特币地址来锁定并创建UTXO。

给某人发送比特币实际上是创造新的UTXO，注册到那个人的地址，并且能被他用于新的支付。

UTXO被每个全节点在存储于本地内存数据库 — “UTXO池”，新的交易从UTXO池中消耗一个或多个输出。

交易输出包含一定量的比特币（聪）和一个锁定脚本。锁定脚本会把输出锁在一个特定的比特币地址上，从而把一定数量的比特币所有权转移到新的所有者上。
交易输入是指向UTXO的指针。若想支付UTXO，一个交易的输入也需要包含一个解锁脚本，用来满足UTXO的支付条件。解锁脚本通常是一个签名，用来证明对于在锁定脚本中的比特币地址拥有所有权。

交易费基于交易的尺寸，用KBytes来计算，而不是基于比特币的价值。最小交易费被固定在0.0001BTC/KBytes。交易费没有特定的字段表示，而是通过所有输入的总和，以及所有输出的总和之间的差值来表示。

比特币交易脚本是一种逆波兰表示法的基于栈的执行语言。该语言没有循环和大部分流控制，是非图灵完备的；但脚本的复杂性有限，也保证了交易可执行次数的可预见性，增加了脚本的安全性。

## Ethereum transaction

## EOS transaction

## Monero transaction

## zcash transaction
