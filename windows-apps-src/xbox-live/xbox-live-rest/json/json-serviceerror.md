---
title: ServiceError (JSON)
assetID: 81c43f6e-bfff-c4b5-d25c-eace22649f01
permalink: en-us/docs/xboxlive/rest/json-serviceerror.html
author: KevinAsgari
description: " ServiceError (JSON)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: 9f9f5cb3f4dc0565cafc073cea35e3e6e00d273f
ms.sourcegitcommit: 194ab5aa395226580753869c6b66fce88be83522
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "4147871"
---
# <a name="serviceerror-json"></a>ServiceError (JSON)
包含有关错误对服务调用失败时返回的信息。 
<a id="ID4EN"></a>

 
## <a name="serviceerror"></a>ServiceError
 
ServiceError 对象具有以下规范。
 
| 成员| 类型| 说明| 
| --- | --- | --- | 
| code| 32 位有符号整数 | 错误类型。 请参阅下表有关可能的值。 | 
| 源| 字符串 | 引发了错误的服务的名称。 例如，值为<code>ReputationFD</code>指示错误是在信誉服务。 | 
| description| 字符串| 错误的描述。 | 
 
<a id="ID4EBC"></a>

 
### <a name="error-codes"></a>错误代码
 
| 值| 说明| 
| --- | --- | --- | --- | --- | 
| 0| 成功无错误| 
| 4000| 提交与 POST 请求失败验证的请求正文的 JSON 文档无效。 请参阅描述字段的详细信息。 | 
| 4100| 用户不会不存在 XUID 请求 URI 中包含不表示 XBOX Live 上的有效用户。| 
| 4500| 未授权授权错误调用方进行执行请求的操作。| 
| 5000| 服务错误时出现的服务内部错误| 
| 5300| 服务不可用服务不可用。| 
   
<a id="ID4EQE"></a>

 
## <a name="sample-json-syntax"></a>JSON 语法示例
 

```json
{
    "code": 4000,
    "source": "ReputationFD",
    "description": "No targetXuid field was supplied in the request"
}
    
```

  
<a id="ID4EZE"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4E2E"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[JavaScript 对象表示法 (JSON) 对象参考](atoc-xboxlivews-reference-json.md)

   