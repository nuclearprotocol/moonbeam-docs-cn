---
title: XC-20和跨链资产
description: 了解如何使用资产预编译访问Moonbeam上跨链代币的ERC-20接口并与之交互。
---

# XC-20和跨链资产

![Cross-Chain Assets Precompiled Contracts Banner](/images/builders/xcm/xc20/overview/xc20-banner.png)

## 概览 {: #introduction } 

[跨共识信息格式（XCM）](https://wiki.polkadot.network/docs/learn-crosschain){target=_blank}定义了两条互操作的区块链之间传递信息的方式。此格式为Moonbeam/Moonriver与中继链或是其他波卡/Kusama生态内平行链之间打开了传递信息和资产的大门。

Substrate资产原生具有可互操作性。然而，开发者需要使用Substrate API与其交互。而这使开发者的体验感降低，尤其是来自以太坊生态的开发者。因此，为了协助开发者上手波卡和Kusama提供的原生互操作性，Moonbeam引入了XC-20概念。

XC-20为Moonbeam上独特的资产类别，其结合了Substrate资产的优点（原生可互操作性）但又使开发者能够通过预编译合约（以太坊API）使用熟悉的[ERC-20接口](https://github.com/PureStake/moonbeam/blob/master/precompiles/assets-erc20/ERC20.sol){target=_blank}与之交互。除此之外，开发者能够使用常用以太坊开发框架或dApp集成XC-20资产。

![Moonbeam XC-20 XCM Integration With Polkadot](/images/builders/xcm/overview/overview-4.png)

XC-20资产使用`xc`作为其名称的前缀与其他资产类别进行区分。举例而言，波卡上的DOT在Moonbeam上的相应资产将会是 _xcDOT_，Kusama上的KSM在Moonriver上的相应资产将会是 _xcKSM_。请注意，XC-20预编译合约并不支持跨链资产转移，但可以使其尽可能接近标准的ERC-20接口。XC-20的跨链转移是通过[X-Tokens Pallet](/builders/xcm/xc20/xtokens/)完成的。

XC-20类别的资产需要在使用前进行注册和与生态系统中的其他资产联结，这可以通过提案的形式以白名单流程进行。如果您对在测试网上测试XCM功能有兴趣，请通过[Discord Server](https://discord.gg/PfpUATX){target=_blank}与我们联系。更多关于XCM的信息，您也可以在文档页面的[XCM概览](/builders/xcm/overview/){target=_blank}页面查看。

## 现有XC-20资产 {: #current-xc20-assets}

现有可用XC-20资产列表如下：

=== "Moonbeam"
    |   起源   |  符号  |                                                              XC-20地址                                                              |
    |:--------:|:------:|:-----------------------------------------------------------------------------------------------------------------------------------:|
    | Polkadot | xcDOT  | [0xFfFFfFff1FcaCBd218EDc0EbA20Fc2308C778080](https://moonscan.io/address/0xFfFFfFff1FcaCBd218EDc0EbA20Fc2308C778080){target=_blank} |
    |  Acala   | xcaUSD | [0xfFfFFFFF52C56A9257bB97f4B2b6F7B2D624ecda](https://moonscan.io/address/0xfFfFFFFF52C56A9257bB97f4B2b6F7B2D624ecda){target=_blank} |
    |  Acala   | xcACA  | [0xffffFFffa922Fef94566104a6e5A35a4fCDDAA9f](https://moonscan.io/address/0xffffFFffa922Fef94566104a6e5A35a4fCDDAA9f){target=_blank} |

     _*您可以在[Polkadot.js的Assets页](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fwss.api.moonbeam.network#/assets){target=_blank}查看每个资产ID_

=== "Moonriver"
    |   起源    |  符号  |                                                                   XC-20地址                                                                   |
    |:---------:|:------:|:---------------------------------------------------------------------------------------------------------------------------------------------:|
    |  Kusama   | xcKSM  | [0xFfFFfFff1FcaCBd218EDc0EbA20Fc2308C778080](https://moonriver.moonscan.io/address/0xffffffff1fcacbd218edc0eba20fc2308c778080){target=_blank} |
    |  Bifrost  | xcBNC  | [0xFFfFFfFFF075423be54811EcB478e911F22dDe7D](https://moonriver.moonscan.io/address/0xFFfFFfFFF075423be54811EcB478e911F22dDe7D){target=_blank} |
    |  Karura   | xcKAR  | [0xFfFFFFfF08220AD2E6e157f26eD8bD22A336A0A5](https://moonriver.moonscan.io/address/0xFfFFFFfF08220AD2E6e157f26eD8bD22A336A0A5){target=_blank} |
    |  Karura   | xcaUSD | [0xFfFffFFfa1B026a00FbAA67c86D5d1d5BF8D8228](https://moonriver.moonscan.io/address/0xFfFffFFfa1B026a00FbAA67c86D5d1d5BF8D8228){target=_blank} |
    | Kintsugi  | xcKINT | [0xfffFFFFF83F4f317d3cbF6EC6250AeC3697b3fF2](https://moonriver.moonscan.io/address/0xfffFFFFF83F4f317d3cbF6EC6250AeC3697b3fF2){target=_blank} |
    | Kintsugi  | xckBTC | [0xFFFfFfFfF6E528AD57184579beeE00c5d5e646F0](https://moonriver.moonscan.io/address/0xFFFfFfFfF6E528AD57184579beeE00c5d5e646F0){target=_blank} |
    | Statemine | xcRMRK | [0xffffffFF893264794d9d57E1E0E21E0042aF5A0A](https://moonriver.moonscan.io/address/0xffffffFF893264794d9d57E1E0E21E0042aF5A0A){target=_blank} |
    | Statemine | xcUSDT | [0xFFFFFFfFea09FB06d082fd1275CD48b191cbCD1d](https://moonriver.moonscan.io/address/0xFFFFFFfFea09FB06d082fd1275CD48b191cbCD1d){target=_blank} |

     _*您可以在[Polkadot.js的Assets页](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fwss.api.moonriver.moonbeam.network#/assets){target=_blank}查看每个资产ID_

=== "Moonbase Alpha"
    |          起源           |  符号   |                                                                  XC-20地址                                                                   |
    |:-----------------------:|:-------:|:--------------------------------------------------------------------------------------------------------------------------------------------:|
    |  Relay Chain Alphanet   | xcUNIT  | [0xFfFFfFff1FcaCBd218EDc0EbA20Fc2308C778080](https://moonbase.moonscan.io/address/0xFfFFfFff1FcaCBd218EDc0EbA20Fc2308C778080){target=_blank} |
    |    Basilisk Alphanet    |  xcBSX  | [0xFFfFfFfF4d0Ff56d0097BBd14920eaC488540BFA](https://moonbase.moonscan.io/address/0xFFfFfFfF4d0Ff56d0097BBd14920eaC488540BFA){target=_blank} |
    |    Bifrost Alphanet     |  xcBNC  | [0xFffFFFfF1FAE104Dc4C134306bCA8e2E1990aCfd](https://moonbase.moonscan.io/address/0xFffFFFfF1FAE104Dc4C134306bCA8e2E1990aCfd){target=_blank} |
    |    Calamari Alphanet    |  xcKMA  | [0xFFffFffFA083189f870640b141ae1E882c2b5bad](https://moonbase.moonscan.io/address/0xFFffFffFA083189f870640b141ae1E882c2b5bad){target=_blank} |
    |  Crust/Shadow Alphanet  |  xcCSM  | [0xffFfFFFf519811215E05eFA24830Eebe9c43aCD7](https://moonbase.moonscan.io/address/0xffFfFFFf519811215E05eFA24830Eebe9c43aCD7){target=_blank} |
    |     Karura Alphanet     |  xcKAR  | [0xFfFFFFfF08220AD2E6e157f26eD8bD22A336A0A5](https://moonbase.moonscan.io/address/0xFfFFFFfF08220AD2E6e157f26eD8bD22A336A0A5){target=_blank} |
    |     Karura Alphanet     | xckUSD  | [0xFfFffFFfa1B026a00FbAA67c86D5d1d5BF8D8228](https://moonbase.moonscan.io/address/0xFfFffFFfa1B026a00FbAA67c86D5d1d5BF8D8228){target=_blank} |
    |     Khala Alphanet      |  xcPHA  | [0xffFfFFff8E6b63d9e447B6d4C45BDA8AF9dc9603](https://moonbase.moonscan.io/address/0xffFfFFff8E6b63d9e447B6d4C45BDA8AF9dc9603){target=_blank} |
    |    Kintsugi Alphanet    | xcKINT  | [0xFFFfffff27C019790DFBEE7cB70F5996671B2882](https://moonbase.moonscan.io/address/0xFFFfffff27C019790DFBEE7cB70F5996671B2882){target=_blank} |
    |    Kintsugi Alphanet    | xckBTC  | [0xFffFfFff5C2Ec77818D0863088929C1106635d26](https://moonbase.moonscan.io/address/0xFffFfFff5C2Ec77818D0863088929C1106635d26){target=_blank} |
    |    Litentry Alphanet    |  xcLIT  | [0xfffFFfFF31103d490325BB0a8E40eF62e2F614C0](https://moonbase.moonscan.io/address/0xfffFFfFF31103d490325BB0a8E40eF62e2F614C0){target=_blank} |
    | Parallel Heiko Alphanet |  xcHKO  | [0xffffffFF394054BCDa1902B6A6436840435655a3](https://moonbase.moonscan.io/address/0xffffffFF394054BCDa1902B6A6436840435655a3){target=_blank} |
    |   Statemine Alphanet    | xcMRMRK | [0xFFffffFfd2aaD7f60626608Fa4a5d34768F7892d](https://moonbase.moonscan.io/address/0xFFffffFfd2aaD7f60626608Fa4a5d34768F7892d){target=_blank} |
    

     _*您可以在[Polkadot.js的Assets页](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fwss.api.moonbase.moonbeam.network#/assets){target=_blank}查看每个资产ID_

本教程将会带您了解如何使用Polkadot.js Apps检索Moonbase Alpha测试网上可用的XC-20资产并计算其预编译地址。除此之外，您还将学会如何使用Remix与XC-20预编译合约交互。

## XC-20与ERC-20 {: #xc-20-vs-erc-20 }

尽管XC-20和ERC-20有很多相似之处，但仍让需要注意两者之间的差异。

首先，XC-20是基于Substrate的资产，因此，它们也受到治理等Substrate功能的直接影响。此外，通过 Substrate API完成的XC-20交易不会在基于EVM的区块浏览器中可见，例如[Moonscan](https://moonscan.io){target=_blank}。只有通过以太坊API完成的交易才能通过此类浏览器看到。

尽管如此，XC-20可以通过ERC-20接口进行交互，因此它们具有可以从Substrate和Ethereum API交互的特性。这为开发者在使用这类资产时提供了更大的灵活性，并允许与基于EVM的智能合约（如DEX、借贷平台等）无缝集成。

## 跨链资产的检索列表 {: #list-xchain-assets }

获取Moonbase Alpha测试网上目前可用的XC-20资产列表，请导向至[Polkadot.js Apps](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fwss.api.moonbase.moonbeam.network#/explorer)并确认您已连接至Moonbase Alpha。接着，点击**Developer**标签并在下拉菜单中选取**Chain State**。随后，您可以遵循以下步骤查看可用的XC-20资产：

1. 在**selected state query**下拉菜单中选择**assets**

2. 选择**asset**函数

3. 关闭**include option**滑块

4. 点击**+**按钮传送检索指令

![Fetch list of cross-chain assets](/images/builders/xcm/xc20/overview/xc20-1.png)

检索结果将会以asset ID和其相关信息的形式显现，包含所有Moonbase Alpha上已注册的XC-20资产。

## 检索跨链资产元数据 {: #x-chain-assets-metadata }

为了获得特定XC-20资产的详细信息（如名称、标志和multi-location等），您可以使用**metadata**函数以获得元数据：

1. 在**selected state query**下拉菜单中选择**assets**

2. 选择**metadata**函数

3. 开启**include option**滑块

4. 输入先前在**asset**函数获得的asset ID。请注意，如果您复制和粘贴的asset ID有任何标点符号，这些标点符号会被自动移除且有可能连带移除数字本身。请确认数字与asset ID完全相同。在本示例中，您可以使用asset ID：`42259045809535163221576417993425387648`

5. 点击**+**按钮传送检索指令

![Get asset metadata](/images/builders/xcm/xc20/overview/xc20-2.png)

您将会获得元数据的结果，您可以查看与VUNIT XC-20资产的相关asset ID。

## 计算预编译地址 {: #calculate-xc20-address }

现在您已经检索可用XC-20资产的列表，在您通过预编译与其交互之前，您需要从asset ID获取预编译地址。

XC-20预编译地址可以使用以下公式进行计算：

```
address = "0xFFF..." + DecimalToHex(AssetId)
```

根据以上的计算，第一步是获得asset ID的u128表达方式，并将其转换为十六进制数值（hex value）。您可以使用您的搜寻引擎查询适当的转换工具。举例而言，资产ID `42259045809535163221576417993425387648`的十六进制数值（hex value）为`1FCACBD218EDC0EBA20FC2308C778080`。

由于以太坊地址长度为40个字符，您将会需要在十六进制数值（hex value）前置入`F`s直到这个地址拥有40个字符。

由于先前十六位进制（hex value）已被计算为32个字符，所以在十六位进制值（hex value）加入8个`F`s将能使其成为40个字符的地址以使其能够与XC-20预编译交互。在本示例中，完整地址为`0xFFFFFFFF1FCACBD218EDC0EBA20FC2308C778080`。

资产预编译的代码将仅会处在`0xFFFFFFFF00000000000000000000000000000000`和`0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF`之间。

现在您已获得XC-20资产的预编译地址，您可以在Remix使用此地址与任何XC-20资产和ERC-20资产交互。

## ERC-20接口 {: #the-erc20-interface }

Moonbeam上的[ERC20.sol](https://github.com/PureStake/moonbeam/blob/master/precompiles/assets-erc20/ERC20.sol)接口跟随智能合约中Token的标准API接口，[EIP-20 Token Standard](https://eips.ethereum.org/EIPS/eip-20) 。此标准定义了一个Token合约必须实现与应用程序互操作所需的函数和动作。

--8<-- 'text/erc20-interface/erc20-interface.md'

## 查看先决条件 {: #checking-prerequisites } 

通过XC-20预编译获得XC-20资产的使用和转移，您将需要：

- [安装MetaMask并连接至Moonbase Alpha测试网](/tokens/connect/metamask/){target=_blank}
- 在Moonbase Alpha上创建或是拥有两个账户/builders/get-started/networks/moonbase/#get-tokens/){target=_blank}
- 至少其中一个账户拥有足够的`DEV` Token。您可以通过Moonbase Alpha[任务中心](/builders/get-started/networks/moonbase/#get-tokens/)获得Token以进行测试

## 使用Remix与预编译合约交互 {: #interact-with-the-precompile-using-remix }

您可以使用[Remix](https://remix.ethereum.org/){target=_blank}与XC-20预编译交互，首先您需要将ERC-20接口加入Remix：

1. 获得[ERC20.sol](https://github.com/PureStake/moonbeam/blob/master/precompiles/assets-erc20/ERC20.sol){target=_blank}的复制文档

2. 将文档内容复制并粘贴至名为**IERC20.sol**的Remix文档

![Load the interface in Remix](/images/builders/xcm/xc20/overview/xc20-3.png)

### 编译合约 {: #compile-the-contract }

当您成功在Remix读取ERC-20接口后，您将需要编译：

1. 点击（从上至下的）第二个**Compile**标签

2. 编译**IERC20.sol**文档

![Compiling IERC20.sol](/images/builders/xcm/xc20/overview/xc20-4.png)

当接口已成功被编译后，您将会在**Compile**标签旁看到绿色的打勾符号。

### 访问合约 {: #access-the-contract }

您将使用获得的XC-20预编译地址访问接口，而非部署ERC-20预编译合约：

1. 在Remix内的**Compile**标签下点击**Deploy and Run**标签。请注意，预编译合约已经被部署

2. 确保已在**Environment**下拉菜单中选择**Injected Web3**。当您已经选择**Injected Web3**，MetaMask将会跳出弹窗要求将您的账户连接至Remix

3. 确认**Account**下显示的为正确账户

4. 确认已在**Contract**下拉菜单中选择**IERC20 - IERC20.sol**。由于此为预编译合约，您不需要部署任何代码。同时，我们将会在**At Address**区域内显示预编译地址

5. 提供在[Calculate Precompile Address](#calculate-precompile-address)部分计算得到的XC-20预编译地址`0xFFFFFFFF1FCACBD218EDC0EBA20FC2308C778080`，并点击**At Address**

![Access the address](/images/builders/xcm/xc20/overview/xc20-5.png)

!!! 注意事项
    如果您希望确保运行顺利，您可以使用您的搜寻引擎查询校验工具以校验您的XC-20预编译地址。当地址校验成功，您可以将其用在**At Address**字段中。

XC-20的**IERC20**预编译将会在**Deployed Contracts**列表下显示。现在您可以使用任何ERC-20函数以获得XC-20的信息或是转移XC-20。

![Interact with the precompile functions](/images/builders/xcm/xc20/overview/xc20-6.png)

如果您想更深入学习每个函数，您可以查看[ERC-20预编译教程](/builders/build/canonical-contracts/precompiles/erc20/){target=_blank}并加以修改来适用XC-20预编译交互。