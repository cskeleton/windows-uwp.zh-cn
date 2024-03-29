---
ms.assetid: b632a6cc-3503-4ab8-bfd1-dde731bd89ab
description: 本部分包括的主题介绍了适用于通用 Windows 平台 (UWP) 应用的 XAML 框架。
title: XAML 平台
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: e22a10e74a834daf4d256313f0e353a6829911c0
ms.sourcegitcommit: f0f933d5cf0be734373a7b03e338e65000cc3d80
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2019
ms.locfileid: "65984243"
---
# <a name="xaml-platform"></a>XAML 平台


本部分中的主题解释了普遍适用于你编写的任何应用的编程概念（假设你使用 C#、Microsoft Visual Basic 或 Visual C++ 组件扩展 (C++/CX) 作为编程语言并使用 XAML 进行 UI 定义）。 这包括基本的编程概念（例如使用属性和事件）以及如何在通用 Windows 平台 (UWP) 应用编程中应用这些概念。 通用 Windows 平台 (UWP) 通过添加依赖属性系统，扩展了 C#、Visual Basic 或 C++/CX 属性概念以及它们的值。 本部分中的主题还介绍了 UWP 所使用的 XAML 语言，并通过介绍一些基本方案和高级主题，说明了如何使用 XAML 定义 UWP 应用的 UI。

| 主题 | 描述 |
|-------|-------------|
| [XAML概述](xaml-overview.md) | 我们将向 Windows 运行时应用开发人员介绍 XAML 语言和 XAML 概念，并介绍在使用 XAML 创建 Windows 运行时应用时，在 XAML 中声明对象和设置属性的不同方式。 |
| [依赖属性概述](dependency-properties-overview.md) | 本主题介绍了在使用 C++、C# 或 Visual Basic 编写 Windows 运行时应用以及 UI 的 XAML 定义时可用的依赖属性系统。 |
| [自定义依赖属性](custom-dependency-properties.md) | 介绍如何为使用 C++、C# 或 Visual Basic 的 Windows 运行时应用定义和实现自定义依赖属性。 |
| [附加属性概述](attached-properties-overview.md) | 介绍 XAML 中的附加属性概念，并提供一些示例。 |
| [自定义附加属性](custom-attached-properties.md) | 介绍如何将一个 XAML 附加属性实现为依赖属性，以及如何定义让附加属性可用于 XAML 所必需的访问器约定。 |
| [事件和路由事件概述](events-and-routed-events-overview.md) | 我们将介绍在使用 C#、Visual Basic 或 C++/CX 作为编程语言并使用 XAML 进行 UI 定义时，针对 Windows 运行时应用的事件的编程概念。 你可以在 XAML 中的 UI 元素声明中为事件分配处理程序，或者在代码中添加处理程序。 Windows 运行时支持**路由事件**：借助此功能，某些输入事件和数据事件可由引发该事件的对象以外的对象来处理。 在定义控件模板或使用页面或版式容器时，路由事件十分有用。 |
|[桌面应用中的 UWP 控件（XAML 岛）](/windows/apps/desktop/modernize/xaml-islands)| 介绍如何使用 UWP XAML 控件增强 Windows 窗体、WPF 或 Win32 桌面应用程序的 UI。|
