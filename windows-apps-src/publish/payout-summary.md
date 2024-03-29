---
Description: “付款摘要”会向你显示有关通过应用和加载项获得的收益的详细信息。 它还使你可以知道你将何时收到付款和收到多少付款。
title: 付款摘要
ms.assetid: F0D070BE-8267-4CC9-B0D2-085EBA74AC98
ms.date: 10/31/2018
ms.topic: article
keywords: windows 10, uwp, 付款摘要, 声明, 付款, 收益, 支出, 付款, 收入
ms.localizationpriority: medium
ms.openlocfilehash: 90238360ecc48beb974546dc5b49ac09c01407eb
ms.sourcegitcommit: 35a511c2b29ae3d5008612a5fc13d3eb6370d2d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2019
ms.locfileid: "67495733"
---
# <a name="payout-summary"></a>付款摘要

**付款摘要**显示有关已获得与 Microsoft money 的详细信息。 它还使你可以知道你将何时收到付款和收到多少付款。

如果在 Azure Marketplace 中销售产品，还将在**付款摘要**中看到成功付款信息。 有关 Azure Marketplace 付款的更多详细信息，请参阅 [Microsoft Azure 应用商店参与策略](https://go.microsoft.com/fwlink/p/?LinkId=722436)和 [Microsoft Azure 应用商店发布者协议](https://go.microsoft.com/fwlink/p/?LinkID=699560 )。

> [!NOTE]
> 为了适合进行付款，你将继续必须达到[付款阈值](payment-thresholds-methods-and-timeframes.md)的 50 美元。 有关付款阈值的详细信息请参阅此页并查看应用程序开发人员协议。

## <a name="access-the-payout-summary-pages"></a>访问付款摘要页

若要打开一个付款摘要页：

1. 在右上角选择钱图标。
2. 选择付款，事务历史记录，或导出数据。

## <a name="payments-page"></a>付款页面

此页上的总计表示所有在您所参与的程序。 可以按参与者 ID、 程序、 付款 ID 和 Earning 类型进行筛选。 以美元为单位给出了金额。 付费的值还会显示在为货币付费。

| 区域                   | 描述                                                                                  |
|------------------------|----------------------------------------------------------------------------------------------|
| 本年度的付款总额   | 为所有支付给你本年度，以美元为单位，所有应用程序。       |
| 下一步估计的付款 | 单找您的下一步付款 (即使还有一些其他即将推出)，以美元为单位。 |
| 最后一次付款           | 量 （以美元为单位）、 程序名称和程序的最近付款。           |
| 源的付款     | 付款，以美元为单位，表示由程序在过去的 12 个月的量。           |
| 付款               | 选择付费或挂起然后根据需要对进行排序。 有关其他详细信息的特定支付选择视图。 若要下载一份付款汇款语句，请选择下载。 请注意事务历史记录数据可能需要 24 小时才会出现，因此您可能不会立即看到相关联的收入。 |

若要导出的任何数据在此页上，选择导出，然后按照导出数据页上的方向。

## <a name="transaction-history-page"></a>事务历史记录页

此页显示所有您的个人收入，包括日期、 类型，并为每个获得。 可以选择要查看的时间段，还可以筛选按注册 ID、 程序、 付款 ID、 Earning 类型、 级别、 和状态。 为当前会计年度 (年 7 月 1 日-6 月 30 日) 和以前的两个会计年度中，会提供数据。

若要查看有关获得更多详细信息，请选择页面右侧的向下箭头。 这将显示级别、 收入金额和产品。 如果由于某种原因的任何此类数据不可用，但需要访问它，请联系[支持](https://developer.microsoft.com/en-us/windows/support)]。 如果获取是调整，并不是事务的结果，将不会显示产品字段。

若要导出的任何事务数据，此页上，选择导出，然后按照导出数据页上的方向。 从事务历史记录页导出的文件显示数据的货币事务，事务货币和以美元为单位中的收益中的付费的值付费为货币。

## <a name="payment-status"></a>付款状态

| 获取状态           | Reason                                                                                                                                      | 合作伙伴所需操作？                                   |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------|
| 未处理              | 获取是适合付款。 它将保持此状态冷却期激励计划的计划指南中的定义。 | 否                                                         |
| 即将推出                 | 付款处理付款之前挂起的内部评审生成顺序。                                                               | 否                                                         |
| 挂起的税务发票      | 税务发票不完整或无效。                                                                                                  | 你需要更新税务发票之前您可以支付 |
| 在查看被拒绝   | 在查看被拒绝付款。                                                                                                     | 请联系[Microsoft 支持部门](https://developer.microsoft.com/en-us/windows/support)有关详细信息                      |
| Failed                   | 付款失败，因为 Microsoft 系统错误。                                                                                         | 请联系[Microsoft 支持部门](https://developer.microsoft.com/en-us/windows/support)有关详细信息                      |
| 正在进行中              | 付款正在进行中。                                                                                                                 | 否                                                         |
| 不正确的付款        | 付款 recouping 正在进行中。                                                                                                       | 否                                                         |
| 发送                     | 付款已发送到你的银行。                                                                                                     | 否                                                         |
| 重新处理             | 付款遇到 Microsoft 系统错误，正在重新处理。                                                                  | 否                                                         |
| 反转                 | 付款已被你的银行撤消，并且将在下一个付款周期中再次发送。                                                     | 否                                                         |
| 已拒绝的税务发票     | 在查看被拒绝，税务发票。 税务发票评审完成之前，所有挂起的付款都将置于保持状态。                 | 请联系[Microsoft 支持部门](https://developer.microsoft.com/en-us/windows/support)有关详细信息                      |
| 待审批的税务发票 | 与要评审你的税务发票。 批准税务发票后，将发布您的付款。                                   | 否                                                         |
| 已拒绝                 | 你的银行拒绝付款。                                                                                                      | 有关详细信息，请联系银行。                             |

## <a name="export-data-page"></a>导出数据页

在此页上，以导出所需的数据按照的说明。

注意：

- 当您访问此页上从任一的付款或事务历史记录页上时，不携带您的筛选器。 你将需要重新学习这些导出数据页上。
- 导出数据页不会刷新自身。 您可能需要刷新页面手动，请参阅最新数据。
- 筛选器可能会导致无数据可用错误。 这可能意味着已保留三个月内，在选定时间段的默认值，然后选择从已超出该时间段获取的付款 ID。 展开时间段，然后重试。

## <a name="payment-download-export"></a>付款下载导出

此选项提供的付款接收对于给定的程序，关联的税务，银行和聚合信赖量的下载。 此报表用于很多合作伙伴中心程序，因此，某些列可能会针对一些不适用于您的报表。 下面被标记的那些列。

| 列名              | 描述                                                                                                                             |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| participantID            | 获取计划的认证的合作伙伴的主要标识                                                                           |
| participantIDType        | 通常程序 id 激励程序和卖方 ID 的存储程序                                                              |
| participantName          | 信赖的合作伙伴的名称                                                                                                             |
| programName              | 激励/存储程序名称                                                                                                            |
| 获得                   | 获得该程序/participantID 支付到货币量                                                                     |
| earnedUSD                | 获得的计划/参与者 ID，以美元为单位的数量                                                                                    |
| withheldTax              | 税务程序/participantID 支付到货币的款项中扣缴的量                                                             |
| salesTax                 | 程序/participantID 支付到货币销售税的总量                                                          |
| totalPayment             | 排除预缴税金和包括的程序/participantID 增值税 （如果适用） 的本地货币的总付款 |
| currencyCode             | 支付到货币代码                                                                                                                    |
| paymentMethod            | 用来支付合作伙伴 （电子银行转帐、 贷记） 的方法                                                              |
| paymentID                | 付款的唯一标识符。 此数字将通常显示在你银行对帐单。                                               |
| paymentStatus            | 付款状态                                                                                                                          |
| paymentStatusDescription | 付款状态的友好说明                                                                                                  |
| paymentDate              | 从 Microsoft 发送日期付款                                                                                                    |

## <a name="transaction-history-download-export"></a>事务历史记录下载导出

此选项提供每个信赖的行项，您看到在事务历史记录页中，获得类型、 日期、 关联的事务量、 客户、 产品和其他事务的详细信息适用于您的程序的下载。

| 列名                    | 描述                                                                                                                              |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| earningId                      | 每个拥有的唯一标识符                                                                                                       |
| participantId                  | 获取计划的认证的合作伙伴的主要标识                                                                            |
| participantIdType              | 卖方 ID                                                                                                                                |
| participantName                | 信赖的合作伙伴的名称                                                                                                              |
| partnerCountryCode             | 位置所在国家/地区的信赖的合作伙伴                                                                                                  |
| programName                    | 激励/存储程序名称                                                                                                             |
| transactionId                  | 事务的唯一标识符                                                                                                    |
| transactionCurrency            | 在其中发生原始客户交易的货币                                                                             |
| transactionDate                | 事务日期。 适用于其中许多事务参与一个获得的程序                                           |
| transactionExchangeRate        | 用于显示相应的美元金额的汇率日期                                                                             |
| transactionAmount              | 根据哪些获得生成的原始事务货币交易金额                                              |
| transactionAmountUSD           | 以美元为单位的事务量                                                                                                                |
| 级别                          | 指示拥有业务的规则                                                                                                  |
| earningRate                    | 应用于要生成获得的事务量的激励速率                                                                      |
| quantity                       | 根据计划而异。 指示事务程序计费的数量                                                            |
| earningType                    | 指示是否费用、 rebate、 coop、 销售等。                                                                                          |
| earningAmount                  | 获取原始事务货币量                                                                                      |
| earningAmountUSD               | 获取以美元为单位的数量                                                                                                                    |
| earningDate                    | 获得的日期                                                                                                                      |
| calculationDate                | 获取计算系统中的日期                                                                                            |
| earningExchangeRate            | 用于显示相应的美元金额的汇率                                                                                  |
| exchangeRateDate               | 用于计算 EarningAmount 美元汇率日期                                                                                   |
| claimId                        | 将始终为空白                                                                                                                     |
| paymentId                      | 付款的唯一标识符。 此数字是通常显示在你银行对帐单                                                 |
| paymentStatus                  | 付款状态                                                                                                                           |
| paymentStatusDescription       | 付款状态的友好说明                                                                                                   |
| customerId                     | 将始终为空白                                                                                                                     |
| customerName                   | 将始终为空白                                                                                                                     |
| partNumber                     | 将始终为空白                                                                                                                     |
| productName                    | 链接到事务的产品名称                                                                                                       |
| productId                      | 唯一产品标识符                                                                                                                |
| ParentProductID                | 唯一的父产品标识符。 请注意：如果没有用来交易的父产品，则父产品 ID = 产品 ID。 |
| parentProductName              | 父产品的名称。 请注意：如果没有用来交易的父产品，则父产品名称 = 产品名称。   |
| productType                    | 产品的类型（如应用、加载项、游戏等）                                                                                        |
| invoiceNumber                  | 将始终为空白                                                                                                                     |
| subscriptionId                 | 将始终为空白                                                                                                                     |
| subscriptionStartDate          | 将始终为空白                                                                                                                     |
| subscriptionEndDate            | 将始终为空白                                                                                                                     |
| resellerId                     | 将始终为空白                                                                                                                     |
| resellerName                   | 将始终为空白                                                                                                                     |
| distributorId                  | 将始终为空白                                                                                                                     |
| distributorName                | 将始终为空白                                                                                                                     |
| agreementNumber                | 将始终为空白                                                                                                                     |
| agreementStartDate             | 将始终为空白                                                                                                                     |
| agreementEndDate               | 将始终为空白                                                                                                                     |
| 工作负荷                       | 将始终为空白                                                                                                                     |
| transactionType                | 交易的类型（如购买、退款、冲销、拒付等）                                                               |
| localProviderSeller            | 本地提供程序/卖方的记录                                                                                                          |
| taxRemitted                    | 免除的税收额（销售税、使用税或 VAT/GST 税）。                                                                                   |
| taxRemitModel                  | 负责代缴税款（销售税、使用税或 VAT/GST 税）的一方。                                                                    |
| storeFee                       | 保留由 Microsoft 提供的应用程序或外接程序存储区中的费用为量。                                           |
| transactionPaymentMethod       | 客户用于交易的付款方式（如信用卡、移动运营商结算、PayPal 等）                                |
| tpan                           | 指示第三方 ad 网络                                                                                                     |
| purchaseTypeCode               | 将始终为空白                                                                                                                     |
| purchaseOrderType              | 将始终为空白                                                                                                                     |
| purchaseOrderCoverageStartDate | 将始终为空白                                                                                                                     |
| purchaseOrderCoverageEndDate   | 将始终为空白                                                                                                                     |
| externalReferenceId            | 将始终为空白                                                                                                                     |
| externalReferenceIdLabel       | 将始终为空白                                                                                                                     |

## <a name="payout-statement-download-export-legacy"></a>付款语句下载导出 （旧版）

旧的付款摘要页中在有限时间，付出比率语句将可供下载。 该报表包含以下字段。

> [!NOTE]
> 旧的事务历史记录具有名为对应于最新历史记录中的"收入"列的"保留"的列不同之处在于它不包括所有收益，状态 ="付款发送"。

| 字段名称              | 描述                                                                                                                                                             |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 收入来源          | 收入的来源，基于交易发生的位置（例如 Microsoft Store、Windows Phone 应用商店、Windows 应用商店 8、广告等）                  |
| 订单编码                | 唯一订单标识符。 此 ID 允许你通过各自的非购买交易（如退款、拒付等）标识购买交易。 两者将具有相同订单编码。 此外，在拆分付费（已针对单个购买使用了多种付款方式）时，它将允许你链接购买交易。 |
| 交易 ID          | 唯一交易标识符。                                                                                                                                          |
| 交易日期时间   | 进行交易的日期和时间 (UTC)。                                                                                                                       |
| 父产品 ID       | 唯一的父产品标识符。 请注意：如果没有用来交易的父产品，则父产品 ID = 产品 ID。                                |
| 产品 ID              | 唯一产品标识符。                                                                                                                                              |
| 父产品名称     | 父产品的名称。 请注意：如果没有用来交易的父产品，则父产品名称 = 产品名称。                                  |
| 产品名称            | 产品的名称。                                                                                                                                                    |
| 产品类型            | 产品的类型（如应用、加载项、游戏等）                                                                                                                       |
| 数量                | 当收入来源为适用于企业的 Microsoft Store 时，数量表示已购买的许可证数量。 对于所有其他收入来源，数量将始终为 1。 注意：即使当单笔交易因使用了两种不同的付款方式而拆分为两个明细项目时，每个明细项目都将显示数量为 1。 |
| 交易类型        | 交易的类型（如购买、退款、冲销、拒付等）                                                                                              |
| 付款方式          | 客户用于交易的付款方式（如信用卡、移动运营商结算、PayPal 等）                                                               |
| 国家/地区        | 进行交易的国家/地区。                                                                                                                          |
| 本地提供商/卖家 | 记录的本地提供商/卖家。                                                                                                                                        |
| 交易币种    | 交易的币种。                                                                                                                                            |
| 交易金额      | 交易的金额。                                                                                                                                              |
| 免除的税收            | 免除的税收额（销售税、使用税或 VAT/GST 税）。                                                                                                                  |
| 净收入            | 交易金额减去免除的税收。                                                                                                                                   |
| 应用商店费用               | 由 Microsoft 扣除的净收入百分比将用作支付在应用商店中提供应用或加载项的费用。                                                      |
| 应用收益            | 净收入减去应用商店费用。                                                                                                                                       |
| 扣缴的税款          | 所得税扣缴金额。 （未包括在“已保留”  的 .csv 文件中。）                                                                                                |
| 付款                 | 应用收益减去任何相应的所得税预缴（交易币种中所示的金额）。 （未包括在“已保留”  的 .csv 文件中。）                               |
| 外汇汇率                 | 用于将交易币种兑换为付款货币的外汇汇率。                                                                                         |
| 付款货币        | 付款时所使用的货币。                                                                                                                                       |
| 已兑换的付款       | 使用外汇汇率，将付款金额兑换为付款货币。                                                                                                         |
| 税款代缴模型         | 负责代缴税款（销售税、使用税或 VAT/GST 税）的一方。                                                                                                   |
| 资格日期时间   | 交易收益可用于付款的日期和时间 (UTC)。 在创建付款时，这包括资格日期时间早于付款创建日期的交易收益。 （仅包括在“已保留”  的 .csv 文件中。） |
| 费用                 | 显示“交易金额”列汇总的所有费用明细的细目。 （仅包括在 Azure Marketplace 中；不包括在“已保留”  的 .csv 文件中。） |
