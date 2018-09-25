---
title: GET (/users/{userId}/profile/settings/people/{userList})
assetID: f6553499-89e2-f21b-a00f-7e5437c045ff
permalink: en-us/docs/xboxlive/rest/uri-usersuseridprofilesettingspeopleuserlistget.html
author: KevinAsgari
description: " GET (/users/{userId}/profile/settings/people/{userList})"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: d57a6620115d5f009c054210a50548c3da7e47d5
ms.sourcegitcommit: 194ab5aa395226580753869c6b66fce88be83522
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "4153505"
---
# <a name="get-usersuseridprofilesettingspeopleuserlist"></a>GET (/users/{userId}/profile/settings/people/{userList})
获取用户的个人资料或支持用户，与人脉名字对象。 这些 Uri 的域是`profile.xboxlive.com`。
 
  * [备注](#ID4EV)
  * [URI 参数](#ID4EKB)
  * [查询字符串参数](#ID4EVB)
  * [需的请求标头](#ID4EQC)
  * [请求正文](#ID4E2D)
 
<a id="ID4EV"></a>

 
## <a name="remarks"></a>备注
 
**userList**和**Userid**是互斥的参数。 如果指定了这两或任何一个，你将得到**BadRequest** 。 **userList**是数组，以便在多个命名的列表是适用于请求方案未来篡改。 **Userid**构成 Xuid 十进制字符串-JSON 已损坏时序列化 64 位无符号的整数。 最后，Xbox One 中的设置将被命名为设置，使用正常的用户可读的名称，而不是 64 位无符号的整数或模糊的常量，如**XONLINE_PROFILE_ASDF**。
  
<a id="ID4EKB"></a>

 
## <a name="uri-parameters"></a>URI 参数
 
| 参数| 类型| 说明| 
| --- | --- | --- | 
| userId| 字符串| 可以是 xuid(12345)、 gt(myGamertag) 或 me。| 
| userList| 字符串| 若要获取设置的人员的命名的列表。 目前，用户是唯一支持的列表。| 
  
<a id="ID4EVB"></a>

 
## <a name="query-string-parameters"></a>查询字符串参数
 
| 参数| 类型| 说明| 
| --- | --- | --- | --- | --- | --- | 
| settings| 字符串| 设置名称的逗号分隔的列表。| 
  
<a id="ID4EQC"></a>

 
## <a name="required-request-headers"></a>需的请求标头
 
| 标头| 类型| 说明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| x xbl 协定版本| 32 位有符号整数| 值 = 2| 
| 内容类型| 字符串| 值 = <code>application/json</code>| 
  
<a id="ID4E2D"></a>

 
## <a name="request-body"></a>请求正文
 
<a id="ID4EBE"></a>

 
### <a name="sample-request"></a>示例请求
 

```cpp
GET /users/me/profile/settings/people/people?settings=GameDisplayName,GameDisplayPicRaw,Gamerscore,Gamertag
      
```

  
<a id="ID4EKE"></a>

  
 
<a id="ID4EME"></a>

 
##### <a name="response-body"></a>响应正文 
该响应是一个**ReadMultiSettingsResponseV2**对象。 假设调用用户有只有一个好友：
  

```cpp
{
      "profileUsers":[
         {
            "id":"2533274791381930",
            "settings":[
               {
                  "id":"GameDisplayName",
                  "value":"John Smith"
               },
               {
                  "id":"GameDisplayPicRaw",
                  "value":"http://images-eds.xboxlive.com/image?url=z951ykn43p4FqWbbFvR2Ec.8vbDhj8G2Xe7JngaTToBrrCmIEEXHC9UNrdJ6P7KIN0gxC2r1YECCd3mf2w1FDdmFCpSokJWa2z7xtVrlzOyVSc6pPRdWEXmYtpS2xE4F&format=png&w=64&h=64"
               },
               {
                  "id":"Gamerscore",
                  "value":"0"
               },
               {
                  "id":"Gamertag",
                  "value":"CracklierJewel9"
               }
            ]
         }
      ]
   }
         
```

   
<a id="ID4E3E"></a>

 
## <a name="see-also"></a>另请参阅
 
<a id="ID4E5E"></a>

 
##### <a name="parent"></a>Parent 的子磁盘） 

[/users/{userId}/profile/settings/people/{userList}?settings={settings}](uri-usersuseridprofilesettingspeopleuserlist.md)

 [Profile (JSON)](../../json/json-profile.md)

   