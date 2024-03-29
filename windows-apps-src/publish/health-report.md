---
Description: 在合作伙伴中心的运行状况报告，可以获取与相关的性能和质量的应用，包括故障和无响应事件的数据。
title: 运行状况报告
ms.assetid: 4F671543-1E91-4E59-88A3-638E3E64539A
ms.date: 10/31/2018
ms.topic: article
keywords: Windows 10, uwp, 运行状况, 崩溃, 无响应事件, 应用运行状况康, 运行状况数据, 堆栈跟踪, cab 文件, 失败, 故障, pdb, 符号
ms.localizationpriority: medium
ms.openlocfilehash: 3c9e58cae32bc5303222deecab2cc470e0b68b71
ms.sourcegitcommit: fca0132794ec187e90b2ebdad862f22d9f6c0db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "63790834"
---
# <a name="health-report"></a>运行状况报告

**运行状况**中的报表[合作伙伴中心](https://partner.microsoft.com/dashboard)使您可以与相关的性能和质量的应用，包括故障和无响应事件的数据。 可以在合作伙伴中心，查看此数据或[将报告下载](download-analytic-reports.md)要脱机查看。 如果适用，可以查看堆栈跟踪和/或 CAB 文件以便进一步调试。

或者，也可以使用 [Microsoft Store 分析 REST API](../monetize/access-analytics-data-using-windows-store-services.md) 以编程方式检索数据。


## <a name="apply-filters"></a>应用筛选器

在页面顶部附近，可以选择希望显示数据的时间段。 默认选择是 **72H**（72 小时），但可以改选 **30D** 以显示最近 30 天的数据。 请注意在你的本地时间区域中显示数据**72 小时**视图和为 utc **30 D**视图。

还可以展开**筛选器**，以按照程序包类型、市场和/或设备类型筛选该页面上的所有数据。

-   **包版本**:默认设置是**所有**。 如果应用包含多个程序包，可以在此处选择一个特定程序包。
-   **市场**:默认筛选器是**所有市场**，但可以限制到一个或多个市场的数据。
-   **设备类型**:默认设置是**所有**，但您可以选择显示只有一个特定设备类型的数据。 请注意，**其他**类别包括制造商/型号被识别，但无法将其加入此筛选器中显示的其中一个预定义类别的设备。 对于这些设备，可以在**故障详细信息**报告的**故障日志**部分查看设备型号。  
-   **OS 版本**:默认值是**所有操作系统版本**，但你可以选择某一特定 OS 版本。
-   **OS 发行版本**:默认值是**所有 OS 都发行版本**，但你可以选择特定版本的所选**OS 版本**。
-   **沙盒**:默认值是**零售**，但对于使用多个开发沙盒 （如 Xbox Live 与集成的游戏） 的产品，你可以选择其中一个此处。 （如果你的产品不使用沙盒，此筛选器将仅显示**零售**且不适用。）
-   **体系结构**:默认值是**所有体系结构**，但你可以选择特定系统体系结构类型。 仅当选择 **30D** 时此筛选器才可用。
-   **PRAID**:默认设置是**所有**，但如果创建你的应用程序包时，您可以定义多个包相对应用程序 Id (PRAIDs)，您可以选择显示仅与一个 PRAID 相关的数据。 如果你未定义多个 PRAID，将不会显示此筛选器。

下面列出的所有图表中的信息将反映所选的日期范围和任何筛选器。 某些部分还允许应用其他筛选器。


## <a name="failure-hits"></a>故障发生

**故障发生**图显示在所选时段内，客户在使用应用时每日遇到的崩溃和事件数量。 应用所遇到的每种事件将受到单独跟踪：崩溃、挂起、JavaScript 异常和内存故障。

当**30 D**所选时间段内，可能会看到圆形标记。 这些表示显著增加或减少我们认为您将想要了解给定值中。 日期显示圆圈表示在其中我们检测到的显著增加或减少相比前的一周的星期结束。 若要查看有关更改的内容的更多详细信息，请悬停在圆。  

> [!TIP]
> 您可以查看在过去的 30 天的重大更改与相关的更多见解[Insights 报告](insights-report.md)。

## <a name="failure-hits-by-market"></a>按市场的故障发生

**按市场的故障发生**图按市场显示所选时段内的崩溃和事件总数。

可以在可视**地图**窗体中查看此数据，或切换设置以在**表格**窗体中查看。 “表格”窗体一次显示五个市场，并且按字母顺序或用户会话最大/最小次数排序。 还可以下载数据，以便一起查看所有市场的信息。


## <a name="package-version"></a>程序包版本

**程序包版本**图按程序包显示所选时段内的崩溃和事件总数。 默认情况下，我们按发生数从高到低的顺序显示程序包版本。 可以通过切换此图的“发生”列中的箭头颠倒此顺序。

## <a name="failures"></a>故障

**故障**图按故障名称显示在选定时段内的崩溃和事件总数。 每个故障名称由四个部分组成：一个或多个问题类、异常/错误检查代码、发生故障的图像/驱动程序的名称和相关的函数名称。 默认情况下，我们按发生数从高到低的顺序显示故障。 可以通过切换此图的“发生”列中的箭头颠倒此顺序。 对于每个故障，还会显示其所占故障总数的百分比。

> [!TIP]
> 有时，你可能会在此部分看到**未知**的条目。 尽管我们尽最大努力也会发生此情况，我们无法收集一个或多个故障的完整详细信息，它们将全部被分组在**未知**下。 多数情况下，发生这种情况是由于存储限制，但也可能是由于设备的隐私设置、网络连接问题、部分/失败故障转储以及其他因素。
>
> 如果你在故障名称中看到有 **!unknown**，这意味着符号不存在，因此我们无法识别故障名称。 请务必在程序包中加入符号以获取准确的故障分析。 请参阅[配置应用包](../packaging/packaging-uwp-apps.md#configure-an-app-package)。 相反，包含 **!unknown_error_in_** 和 **!unknown_function** 的故障名称则意味着我们由于各种其他原因无法收集完整的详细信息。

若要显示特定故障的**故障详细信息**报告，请选择相应的故障名称。 如果包含了符号文件，**故障详细信息**报告将包括过去一个月的故障发生数、列出发生详细信息（日期、程序包版本、设备类型、设备型号、操作系统版本）的故障日志以及指向堆栈跟踪和/或 CAB 文件的链接（如可用）。

> [!TIP]
> 仅当故障发生在使用 Windows 预览体验成员版本的计算机中时 CAB 文件才将可用，因此并非所有故障都将包含 CAB 下载选项。 若要显示具有 CAB 文件的故障，请选择**失败下载**部分筛选器中。 此外可以单击**链接**中的标头**失败日志**对结果进行排序，因此故障包括 CAB 文件出现在列表顶部。

上**失败详细信息**页上，还可以看到**堆栈普及程度**图表，其中显示了参与失败，按百分比，排序的前堆栈和**设备配置 (30 D)** 图表中，提供有关遇到的失败的设备的配置详细信息。 


## <a name="crash-free-sessions-and-devices-30d"></a>无故障会话和设备 (30 D)

**无故障会话和设备**图表显示的设备或没有在过去的 30 天内遇到崩溃的用户会话的百分比。 此信息可帮助你了解如何广泛应用崩溃影响你的用户。 例如，应用可能具有一天中的 10,000 崩溃。 如果受影响的 90%的设备，然后将可能的分类为关键和采取措施来立即修复此错误。 但是，如果仅表示 5%的设备使用您的应用程序，可能是较低优先级。

此图表就有两个选项卡：
- **无故障设备**:显示没有在每一天 （在过去的 30 天内） 遇到故障的唯一设备的百分比。
- **会话无故障**:显示没有在每一天 （在过去的 30 天内） 遇到故障的唯一用户会话的百分比。


 

 
