---
title: "缓冲区平铺"
description: "一个缓冲区资源分为多个 64KB 的磁贴，如果最后一个磁贴的大小不是 64KB 的倍数，其中会有一些空白空间。"
ms.assetid: 577DC6B0-F373-4748-AD80-2784C597C366
keywords:
- "缓冲区平铺"
author: PeterTurcan
ms.author: pettur
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
translationtype: Human Translation
ms.sourcegitcommit: c6b64cff1bbebc8ba69bc6e03d34b69f85e798fc
ms.openlocfilehash: 2382974de7146f4ba64c2422a01c4d3d297a8977
ms.lasthandoff: 02/07/2017

---

# <a name="buffer-tiling"></a>缓冲区平铺


一个[缓冲器](introduction-to-buffers.md)资源分为多个 64KB 的磁贴，如果最后一个磁贴的大小不是 64KB 的倍数，其中会有一些空白空间。

结构化的缓冲区对要平铺的步幅不能有约束。 但在第一时间将其平铺会牺牲使用 [**StructuredBuffers**](https://msdn.microsoft.com/library/windows/desktop/ff471514) 时可能的硬件性能优化。

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>相关主题


[流式资源区域的平铺方式](how-a-streaming-resource-s-area-is-tiled.md)

 

 




