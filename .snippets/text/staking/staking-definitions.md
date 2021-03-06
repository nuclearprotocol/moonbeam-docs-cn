关于Moonbeam质押挖矿系统，我们需要了解以下重要参数：

 - **轮次（Round）**—— 质押行动被执行所需的固定区块数量。举例而言，新的委托将会在下个轮次开始时执行。当减少绑定数量或是撤销委托时，资金将会在一定轮次后退回
 - **候选收集人（Candidates）**—— 在获得足够质押量后进入收集人有效集，才有资格产生区块的节点运营商
 - **收集人（Collators）**—— 获选成为区块生产者的候选收集人。他们从收集用户的交易记录并为中继链提供状态转换证明以供验证
 - **委托人（Delegators）**—— 质押Token的Token持有者，为特定的候选收集人担保。任何持有超过最低数量且能够[自由支配](https://wiki.polkadot.network/docs/learn-accounts#balance-types)的Token的人皆能够成为委托人
 - **最低委托持有量（Minimum delegation per candidate）**——委托人要委托候选收集人所需的最低Token数量
 - **候选收集人的委托人限额（Maximum delegators per candidate）**——每个候选收集人能接受的最高可获得奖励的委托人数量（根据质押数量决定）
 - **最高委托量（Maximum delegations）**—— 委托人能够委托的最高候选收集人数量
 - **退出生效期（Exit delay）**——退出生效期为候选收集人或是委托人在提交减少质押数量、撤销质押或离开候选收集人集或委托人后执行动作所需等待的时间
 - **奖励分发延迟（Reward payout delay）**—— 在奖励自动分发至余额前所需等待的固定数量的轮次
 - **奖励池（Reward pool）**—— 为收集人和委托人所设计的年通胀比例
 - **收集人佣金（Collator commission）**—— 收集人初始获得质押奖励的固定比例，与奖励池无关
 - **委托人奖励（Delegator rewards）**—— 分配给所有合格委托人奖励的总和，根据质押的数量计算（[阅读更多](/learn/features/staking/#reward-distribution）
 - **惩罚（Slashing）**—— 避免收集人执行不当行为的机制，通常惩罚为扣除收集人和委托人一定占比的质押数量。目前暂无惩罚机制，但可通过治理改变。收集人生产区块后未获得中继链最终确定将不会获得奖励