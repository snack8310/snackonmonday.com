---
title: "Layer2介绍"
date: 2023-01-06T14:46:35+08:00
draft: true
description: Layer2的概念介绍
---

<!--more-->

在Web3领域，2022年最热的事一定是FTX的破产，但要说最2022年最热的技术，Layer2的发展可以排在很靠前的位置上。

我们用一点文字，简单的理解下Layer2的技术

## 什么是Layer2
Layer2并不是个很新的概念。在了解Layer2之前，先了解几个基本概念。

### 区块链不可能三角
去中心化
规模
安全

### 交易成本

时间 && 费用

现状

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

## Layer2的前景
高价低频：DeFI
低价高频：GameFi，SocialFi，DeFi对Web2的交易所


## Layer2的问题
Layer2相互不兼容，
L1的交易，需要在L2有账户体系

### 竞争性
ZK Rollup现在看技术上有优势
但流动性现在仍然在Otimistic上，截止本文发布，市场上前两名是 Arbitrum One和Optimism

## 引用

https://ethereum.org/zh/layer-2/
https://l2beat.com/scaling/tvl