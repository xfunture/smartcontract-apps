# 快速了解 Compound

## 超额抵押贷款(over-collateralized loan)

目前区块链上的去中心化借贷为了保证偿还资金，大多为超额抵押贷款。用户需要抵押比借出资产价值更高的资产，才能获得借贷服务。从这个角度来说，目前的去中心化借贷的平台，与其说是提供借贷服务，更像是在提供金融杠杆服务。目前除了闪电贷，没有其他成熟的无抵押贷款模式。

## 聚合借贷

不同于一对一的抵押借贷，目前绝大多数的去中心化借贷平台都提供聚合借贷服务。只要是平台支持的资产，都可以抵押多种资产从而借贷另外的多种资产，方便了用户的操作。

## 标的资产(Underlying Token)

为了防止有人利用低流动性的资产套取高流动性的资产，去中心化借贷平台都只允许经过审核的高流动性资产作为标的资产进行借贷操作。

## cToken

cToken 是用户在 Compound 上存入资产的凭证，每一种标的资产都有对应的一种 cToken，凭此可以换回质押资产的本金和收益。

## 兑换率(Exchange Rate)

兑换率是 cToken 与标的资产的兑换比例，兑换率会随着时间和利率的变化而不断上涨，持有 cToken 就等于不断生息，所以也叫生息代币。

## 抵押因子(Collateral Factor)

每种标的资产都有一个抵押因子，代表用户抵押的资产价值对应可得到的借款的比率。假如用户存入了 1 个 ETH 并开启作为抵押品，当时的 ETH 价值为 2000 USD，抵押因子为 0.75。则可借额度为1 * 2000 * 0.75 = 1500 USD，可最多借出价值 1500 USD 的其他资产。

## 利率模型(Interest Rate Model)

- 基准年利率(baseRatePerYear)

当质押资产的资金使用率为 0 时，最低的年化利率。

- 直线型

在该模型下，资产的利率会随着资金使用率升高而线性增长（利率 = 基准年利率 + 资金使用率 * 增长率）

- 拐点型

在该模型下，资产利率的增长会分为两段，前面一段增长率较低，后面一段增长率较高。目前Compound 使用这一种利率模型，以资金使用率 80% 为拐点。

## 储备金率(Reserve Factor)

为了防止挤兑，需要有一定比率的储备金支持平时用户的存取款业务。这部分资产不计入资金使用率之内，因此不会被借出。

## 资金使用率(Utilization Rate)

资金使用率是指除了资产储备金外，其他所有资产的资金使用率。这一部分资金的存在决定了存款利率会比借款利率低。

## 清算(Liquidation)

如果资产价格波动导致抵押 `各资产的价值 * 各质押因子` 之和低于借款价值，那么借贷平台就会允许清算者对这部分资产进行清算。为了激励清算者，借贷平台会允许支付一部分的费用给清算者，而这当然是由被清算的用户来承担的。因此保持借贷平衡不触及平台的清算线，是非常重要的。

## 价格预言机(Price Oracle)

为了获取标的资产的实时价格，需要价格预言机对各大交易平台的资产价格进行记录。如果价格预言机记录了错误的价格，将会导致巨大的资产风险。
