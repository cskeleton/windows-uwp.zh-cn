---
author: stevewhims
Description: "MakePri.exe 是可用于创建和转储 PRI 文件的命令行工具。 它作为 MSBuild 的一部分集成到 Microsoft Visual Studio 中，但它可用来手动或使用自定义生成系统创建包。"
title: "使用 MakePri.exe 手动编译资源"
template: detail.hbs
ms.author: stwhi
ms.date: 10/23/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: "windows 10, uwp, 资源, 图像, 资产, MRT, 限定符"
localizationpriority: medium
ms.openlocfilehash: 16d2a270a69497bc66f7b17109bc28b062f14b5e
ms.sourcegitcommit: d0c93d734639bd31f264424ae5b6fead903a951d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2017
---
<link rel="stylesheet" href="https://az835927.vo.msecnd.net/sites/uwp/Resources/css/custom.css">

# <a name="compile-resources-manually-with-makepriexe"></a>使用 MakePri.exe 手动编译资源

MakePri.exe 是可用于创建和转储 PRI 文件的命令行工具。 它作为 MSBuild 的一部分集成到 Microsoft Visual Studio 中，但它可用来手动或使用自定义生成系统创建包。

## <a name="makepriexe-command-line-options"></a>MakePri.exe 命令行选项

MakePri.exe 具有命令集 `createconfig`、`dump`、`new`、`resourcepack` 和 `versioned`。 有关其使用的详细信息，请参阅 [MakePri.exe 命令行选项](makepri-exe-command-options.md)。

## <a name="makepriexe-configuration"></a>MakePri.exe 配置

PRI XML 配置文件指示如何索引哪些资源。 配置 XML 的架构在 [MakePri.exe 配置](makepri-exe-configuration.md)中进行了描述。

## <a name="format-specific-indexers"></a>特定格式索引器

MakePri.exe 通常与 `new`、`versioned` 和 `resourcepack` 选项一起使用。 在这些情况下，它索引源文件以生成资源索引。 MakePri.exe 使用各种单独的索引器读取不同的源资源文件或资源容器。 最简单的索引器是文件夹索引器，它索引文件夹内容中的 `.jpg` 或 `.png` 图像等资源。 有关详细信息，请参阅 [MakePri.exe 特定格式索引器](makepri-exe-format-specific-indexers.md)。

## <a name="makepriexe-warnings-and-error-messages"></a>MakePri.exe 警告和错误消息

```
Resources found for language(s) '<language(s)>' but no resources found for default language(s): '<language(s)>'. Change the default language or qualify resources with the default language.
```

当 MakePri.exe 或 MSBuild 发现似乎使用语言限定符进行标记的指定名称资源的文件或字符串资源，但没有找到默认语言的候选项时，会显示上述警告。 在文件和文件夹中使用限定符的过程在[定制语言、比例和其他限定符的资源](tailor-resources-lang-scale-contrast.md)中进行了描述。 一个文件或文件夹中可能包含某种语言名称，但没有发现为完全匹配的默认语言限定的资源。 例如，如果项目使用“en-US”作为默认语言且具有名称为“de/logo.png”的文件，但没有任何文件使用默认语言“en-US”进行标记，就会显示此警告。 为了消除此警告，文件或字符串资源应使用默认语言进行限定，或者应更改默认语言。 若要更改默认语言，在 Visual Studio 中打开你的解决方案，并打开 `Package.appxmanifest`。 在应用程序选项卡上，确认已设置相应的默认语言（如“en”或“en-US”）。

```
No default or neutral resource given for '<resource identifier>'. The application may throw an exception for certain user configurations when retrieving the resources.
```

当 MakePri.exe 或 MSBuild 发现似乎使用语言限定符进行标记的文件或资源具有不清晰的资源时，会显示上述警告。 具有限定符，但不保证在运行时会返回该资源限定符的特定候选资源。 如果无法找到作为默认设置或将始终与用户的上下文匹配的特定语言、周围地区或其他限定符的候选资源，将显示此警告。 在运行时，对于特定的用户配置，如用户的语言首选项或主位置（**设置** > **时间和语言** > **区域和语言**），用于检索资源的 API 可能会引发意外的异常。 为了消除此警报，应该提供默认资源，例如项目的默认语言或全局家乡区域 (homeregion-001)。

## <a name="using-makepriexe-in-a-build-system"></a>在生成系统中使用 MakePri.exe

生成系统应使用 MakePri.exe `new`、`versioned` 或 `resourcepack` 命令，具体取决于正在生成的项目类型。 创建新的 PRI 文件的生成系统应使用 `new` 命令。 必须通过迭代确保内部偏移兼容性的生成系统可以使用 `versioned` 命令。 以下构建系统应使用 `resourcepack` 命令：必须创建一个 PRI 文件，该文件中包含其他的资源变体，而且需要验证以确保不为该变体添加任何新资源。

需要显式控制被编入索引的源文件的生成系统可以使用 ResFiles 索引器替代索引文件夹。 生成系统还可以使用具有不同[特定格式索引器](makepri-exe-format-specific-indexers.md)的多个索引传递生成单个 PRI 文件。

生成系统还可以使用 PRI 特定格式索引器将预生成的 PRI 文件添加到来自其他组件（如类库、程序集、SDK 和 DLL）的包的 PRI。

为其他组件、类库、程序集、DLL 和 SDK 生成 PRI 文件时，应使用 **initialPath** 配置确保组件资源具有自己的子资源地图，且不与其所在的应用相冲突。

## <a name="related-topics"></a>相关主题

* [MakePri.exe 命令行选项](makepri-exe-command-options.md)
* [MakePri.exe 配置](makepri-exe-configuration.md)
* [MakePri.exe 特定格式索引器](makepri-exe-format-specific-indexers.md)
* [定制语言、比例和其他限定符的资源](tailor-resources-lang-scale-contrast.md)