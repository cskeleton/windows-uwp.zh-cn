---
author: WilliamsJason
title: 设备门户控制器 API 参考
description: 了解如何获取附加物理控制器的数量，并将其以编程方式关闭。
ms.author: wdg-dev-content
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 292c9c29149b56b9be4255215e97e703278d8abf
ms.sourcegitcommit: c104b653601d9b81cfc8bb6032ca434cff8fe9b1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2018
ms.locfileid: "1921222"
---
# <a name="controller-api-reference"></a>控制器 API 参考   
通过使用此 REST API，可以获取附加物理控制器的数量并将其关闭。

## <a name="determine-the-number-of-attached-physical-controllers"></a>确定附加物理控制器的数量

**请求**

可以使用以下请求检查设备上附加的物理控制器的数量。

方法      | 请求 URI
:------     | :-----
获取 | /ext/remoteinput/controllers
<br />
**URI 参数**

- 无

**请求标头**

- 无

**请求正文**   

- 无

**响应**   

- JSON 数字属性 ConnectedControllerCount，指定附加物理控制器的数量。

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
200 | 成功
4XX | 错误代码
5XX | 错误代码

## <a name="disconnect-all-physical-controllers-on-the-devkit"></a>断开开发工具包上所有物理控制器的连接

**请求**

可以使用以下请求断开设备上所有物理控制器的连接。

方法      | 请求 URI
:------     | :-----
删除 | /ext/remoteinput/controllers
<br />
**URI 参数**

- 无

**请求标头**

- 无

**请求正文**   

- 无

**响应**   

- 无 

**状态代码**

此 API 具有以下预期状态代码。

HTTP 状态代码      | 说明
:------     | :-----
204 | 断开控制器的请求已成功。
4XX | 错误代码
5XX | 错误代码

<br />
**可用设备系列**

* Windows Xbox