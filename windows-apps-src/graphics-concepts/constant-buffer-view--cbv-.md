---
title: "常量缓冲区视图 (CBV)"
description: "常量缓冲区包含着色器常量数据。 其优点在于数据持续存在，并且可由任意 GPU 着色器访问，直到需要更改数据。"
ms.assetid: 99AEC6B0-A43B-4B61-8C3A-ECC8DE1B69A7
keywords:
- "常量缓冲区视图 (CBV)"
author: PeterTurcan
ms.author: pettur
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
translationtype: Human Translation
ms.sourcegitcommit: c6b64cff1bbebc8ba69bc6e03d34b69f85e798fc
ms.openlocfilehash: 84d97f1d03c396ba379ad0a83bb094c09b769924
ms.lasthandoff: 02/07/2017

---

# <a name="constant-buffer-view-cbv"></a>常量缓冲区视图 (CBV)


常量缓冲区包含着色器常量数据。 其优点在于数据持续存在，并且可由任意 GPU 着色器访问，直到需要更改数据。

常量缓冲区的典型数据是世界、投影和视图矩阵，它们在绘制一帧的整个过程中保持恒定。

常量缓冲区布局应匹配 HLSL 布局（请参考[常量变量的封装规则](https://msdn.microsoft.com/library/windows/desktop/bb509632.aspx)）。

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>相关主题


[视图](views.md)

 

 




