---
title: "Layer2介绍"
date: 2023-01-06T14:46:35+08:00
draft: false
description: Layer2的产生和模型介绍
---

<!--more-->

在Web3领域，2022年最热的事一定是FTX的破产，但要说最2022年最热的技术，Layer2的发展可以排在很靠前的位置上。

我们用一点文字，简单的理解下Layer2的技术

## 什么是Layer2
Layer2并不是个很新的概念。在几年前，由于ETH的交易效能差，就衍生过很多解决方案，尝试去提高ETH的交易效能。

在了解Layer2之前，先了解几个基本概念。

### 区块链不可能三角

<div align=center>
	<img src="/img/blockchain-trilemma.png" width="512px"/>
</div>

这是著名的区块链不可能三角模型。这里暂且不讨论出处及这个模型的准确性，但这个模型非常真实的反映了当前区块链面对的困境。

无法在去中心化的基础上，同时提高效率和安全性。

### 交易成本

这是当前ETH的交易时间和费用

<div align=center>
	<img src="/img/etherscan-gas.png" width="512px"/><br>etherscan-gastracker
</div>

取中间的Average看，大概一笔交易费用在0.5美金，时间是3分钟。

相比较费用来说，ETH的交易性能是更大的瓶颈。当前的TPS差不多30/s左右。（2022年9月份升级POS后，ETH的交易TPS目标为1000/s, 实际还有很多要调整）

相比Paypal或者Visa，tps为千甚至万级别，相差甚远。

Layer2就是尝试解决交易能效的问题，也称为Layer1扩容。

### Layer2的交易模型

<div align=center>
	<img src="/img/Layer1.png" width="512px"/>
</div>

以ETH的交易模型为例。

<div align=center>
	<img src="/img/Layer2.png" width="512px"/>
</div>

在Layer2的交易中，主要变化的点，在于批量。原本一次校验和打包，只有一笔交易，通过Layer2的机制，可以合并多笔，从而让交易费用显著的降低。我们称之为对Layer1的扩容。

可以把批量的校验和打包等操作，想象为传统银行的清结算动作，假设一个银行内部在1分钟内，有100笔不同用户的转账交易，完全可以汇总在一起，做一次系统更新的动作，降低系统更新成本开销。

但这个动作，就带来很多问题。如中心化，可靠性，交易的真实性验证等。为此，不同的Layer2提供方也有各自不同的扩容方案。

## Layer2的扩容方案

Layer2的扩容方案有很多种，可以从l2beat.com上看到相关的数据统计

<div align=center>
	<img src="/img/Layer2_tvl.png" width="512px"/>
</div>

现在比较主流的方案，比较集中在Rollup上。当然，如果对Optimistic Chain和Validium模型感兴趣，也可以自行了解一下。

### Rollup
Rollup的一个特点，就是链下，通过合约脱离主链的存在。这种模式最大的问题就是如何保证链下交易的安全性。

这里也分为两种，Optimistic Rollups 和 ZK Rollups

### Optimistic Rollups
乐观归并，采用的是信任Layer2的交易，假设交易都是正确的，设定交易有效期，在有效期内，可以对不正确的交易提出质疑，则会对这一次归并的交易重新计算，同时对“有问题”的交易计算节点进行处罚。由于乐观的认为交易的可靠性，可以极大的保证交易效率，降低成本，但缺点也存在，假定交易是正确的，这里存在比较高的风险，如果出现有问题的交易，需要做撤回，重新发起等复杂的流程。

### ZK Rollups
零知识归并。与乐观归并相反，采用的对交易的不信任，所有交易都要通过验证。这保证了交易的安全性。

在现在的阶段上，ZK的验证还是有很高的的成本，这意味着相比Optimistic的模式有更高的费用。

### 方案对比
不过由于ZK的安全和信息保护价值，ZK的技术模型会有更多高的认可度，但流动性现在仍然在Otimistic上，截止本文发布，市场上前两名是 Arbitrum One和Optimism

## Layer2的问题
上述这些说明Layer2如何解决扩容的问题，再说一下问题。

### 问题1：Layer2并不开放，相互并不兼容
由于Layer2的机制，基本模型为合并计算，回归到Layer1上的写入，大都需要独立的L2账户体系，这些账户是无法通用，也就意味着资金无法轻易的从不同L2中间流转，依托Layer2的应用，选择兼容不同的Layer2基础设施，就跟同时兼容ETH和Solana一样艰难。

### 问题2：与ETH的主链扩容重复
随着ETH的升级，交易能效的提升，未来Layer2是否必要，仍然是个未知数。

当然，可见的几年内，还不能确定ETH的效能提升。Layer2上的应用也在显著的增加。短期还是非常看好Layer2.

## Layer2的前景

其实Layer2的前景就跟他的问题一样，如果ETH或者Layer2达到足够高效，那么有很多应用就会得到飞速发展。

当前Web3领域流行的DApp，基本上集中在DeFi和NFT上，这类产品比较显著的特征是低频，同时产生高价值。

当Layer2足够高校，很多高频低价值的应用就会迅速发展，比如GameFi，SocialFi等等。甚至Web3交易所，会对传统的Web2交易所有非常大的冲击。

2023年，在web3熊市的时候，仍然看好Layer2的发展，以及应用生态会进一步的增加。

## 引用

https://ethereum.org/zh/layer-2/
https://l2beat.com/scaling/tvl