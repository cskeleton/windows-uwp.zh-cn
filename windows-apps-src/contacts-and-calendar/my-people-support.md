---
title: "为应用程序添加“我的人脉”支持"
description: "介绍如何为应用程序添加“我的人脉”支持，以及如何固定和取消固定联系人"
author: mukin
ms.author: mukin
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: "windows 10，uwp"
ms.openlocfilehash: 61f73fd2fc0d14d0d1d478d67763c9b0e252cd36
ms.sourcegitcommit: ec18e10f750f3f59fbca2f6a41bf1892072c3692
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2017
---
# <a name="adding-my-people-support-to-an-application"></a>为应用程序添加“我的人脉”支持

> [!IMPORTANT]
> **预发行版 | 需要秋季创意者更新**：你必须以 [Insider SDK 16225](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewSDK) 为目标，并且运行[预览体验成员版本 16226](https://blogs.windows.com/windowsexperience/2017/06/21/announcing-windows-10-insider-preview-build-16226-pc/) 或更高版本，才能使用“我的人脉”API。

利用“我的人脉”功能，用户可以从应用程序中将联系人直接固定到其任务栏，从而创建一个可通过多种方式与之进行交互的新联系人对象。 本文介绍如何为此功能添加支持，以允许用户直接从应用固定联系人。 固定联系人后，可以使用新型用户交互，如[“我的人脉”共享](my-people-sharing.md)和[通知](my-people-notifications.md)。

![“我的人脉”聊天](images/my-people-chat.png)

## <a name="requirements"></a>要求

+ Windows 10 和 Microsoft Visual Studio 2017。 有关安装详细信息，请参阅[设置 Visual Studio](https://docs.microsoft.com/en-us/windows/uwp/get-started/get-set-up)。
+ C# 或类似面向对象的编程语言的基础知识。 若要开始使用 C#，请参阅[创建“Hello, world”应用](https://docs.microsoft.com/en-us/windows/uwp/get-started/create-a-hello-world-app-xaml-universal)。

## <a name="overview"></a>概述

你需要执行以下三项操作以使应用程序能够使用“我的人脉”功能：

1. [声明对应用程序清单中的 shareTarget 激活合约提供支持。](https://docs.microsoft.com/en-us/windows/uwp/contacts-and-calendar/my-people-sharing#declaring-support-for-the-share-contract)
2. [为用户可与之共用应用的联系人添加注释。](https://docs.microsoft.com/en-us/windows/uwp/contacts-and-calendar/my-people-sharing#annotating-contacts)
3.  支持同时运行应用程序的多个实例。 用户必须能够与完整版本的应用程序进行交互，并且可以同时在联系人面板中使用该应用程序。  他们甚至可以同时在多个联系人面板中使用该应用程序。  为了对此提供支持，应用程序需要能够同时运行多个视图。 若要了解如何执行此操作，请参阅文章[“显示应用的多个视图”](https://docs.microsoft.com/en-us/windows/uwp/layout/show-multiple-views)。

完成此操作后，应用程序将显示在已注释联系人的联系人面板中。

## <a name="declaring-support-for-the-contract"></a>声明对合约提供支持

若要声明对“我的人脉”合约提供支持，请在 Visual Studio 中打开应用程序。 从**解决方案资源管理器**中，右键单击 **Package.appxmanifest** 并选择**打开方式**。 从菜单中，选择 **XML (文本)编辑器**，然后单击**确定**。 对清单进行以下更改：

**之前**

```xml
<Package
  xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10">

    <Applications>
        <Application Id="MyApp"
          Executable="$targetnametoken$.exe"
          EntryPoint="My.App">
        </Application>
    </Applications>

```

**之后**

```xml
<Package
  xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:uap4="http://schemas.microsoft.com/appx/manifest/uap/windows10/4">

    <Applications>
        <Application Id="MyApp"
          Executable="$targetnametoken$.exe"
          EntryPoint="My.App">
          <Extensions>
            <uap4:Extension Category="windows.contactPanel" />
          </Extensions>
        </Application>
    </Applications>

```

添加此内容后，现在可以通过 **windows.ContactPanel** 合约启动你的应用程序，这样，你可以与联系人面板进行交互。

## <a name="annotating-contacts"></a>为联系人添加注释

若要允许应用程序中的联系人通过“我的人脉”窗格出现在任务栏中，你需要将联系人写入 Windows 联系人存储中。  若要了解如何编写联系人，请参阅[联系人卡片示例](https://github.com/Microsoft/Windows-universal-samples/tree/6370138b150ca8a34ff86de376ab6408c5587f5d/Samples/ContactCardIntegration)。

你的应用程序还必须为每个联系人编写注释。 注释是应用程序中与联系人相关联的一些数据。 注释必须包含与 **ProviderProperties** 成员中所需视图相对应的可激活的类，并且声明对 **ContactProfile** 操作提供支持。

你可以在应用运行过程中随时为联系人添加注释，但通常，在将联系人添加到 Windows 联系人存储后，你应该立即为联系人添加注释。

```Csharp
if (ApiInformation.IsApiContractPresent("Windows.Foundation.UniversalApiContract", 5))
{
    // Create a new contact annotation
    ContactAnnotation annotation = new ContactAnnotation();
    annotation.ContactId = myContact.Id;

    // Add appId and contact panel support to the annotation
    String appId = "MyApp_vqvv5s4y3scbg!App";
    annotation.ProviderProperties.Add("ContactPanelAppID", appId);
    annotation.SupportedOperations = ContactAnnotationOperations::ContactProfile;

    // Save annotation to contact annotation list
    // Windows.ApplicationModel.Contacts.ContactAnnotationList 
    await contactAnnotationList.TrySaveAnnotationAsync(annotation));
}
```

“appId”是后跟“!” 和可激活的类 ID 的包系列名称。 若要查找包系列名称，请使用默认编辑器打开 **Package.appxmanifest**，并在“打包”选项卡中查找。 在此，“应用”是与应用程序启动视图相对应的可激活类。

## <a name="allow-contacts-to-invite-new-potential-users"></a>允许联系人邀请新的潜在用户

默认情况下，你的应用程序将仅显示在你已明确为其添加注释的联系人的联系人面板中。  这是为了避免与无法通过应用与之进行交互的联系人相混淆。  如果你想要为应用程序无法识别的联系人显示应用程序（例如，为了邀请用户将该联系人添加到其帐户中），则可以将以下内容添加到清单中：

**之前**

```Csharp
<Applications>
    <Application Id="MyApp"
      Executable="$targetnametoken$.exe"
      EntryPoint="My.App">
      <Extensions>
        <uap4:Extension Category="windows.contactPanel" />
      </Extensions>
    </Application>
</Applications>
```

**之后**

```Csharp
<Applications>
    <Application Id="MyApp"
      Executable="$targetnametoken$.exe"
      EntryPoint="My.App">
      <Extensions>
        <uap4:Extension Category="windows.contactPanel">
            <uap4:ContactPanel SupportsUnknownContacts="true" />
        </uap4:Extension>
      </Extensions>
    </Application>
</Applications>
```

通过进行此更改，你的应用程序将在用户已固定的所有联系人的联系人面板中显示为可用选项。  使用联系人面板合约激活应用程序后，你应该查看联系人是否是应用程序所识别的联系人。  如果不是，则应该显示应用的新用户体验。

![“我的人脉”联系人面板](images/my-people.png)

## <a name="support-for-email-apps"></a>对电子邮件应用的支持

如果你正在编写电子邮件应用，则无需为每个联系人手动添加注释。  如果你声明对联系人窗格和 mailto: 协议提供支持，则将针对具有电子邮件地址的用户自动显示你的应用程序。

## <a name="running-in-the-contact-panel"></a>在联系人面板中运行

现在，对于部分或所有用户，你的应用程序将出现在联系人面板中，你需要使用联系人面板合约来处理激活。

```Csharp
override protected void OnActivated(IActivatedEventArgs e)
{
    if (e.Kind == ActivationKind.ContactPanel)
    {
        // Create a Frame to act as the navigation context and navigate to the first page
        var rootFrame = new Frame();

        // Place the frame in the current Window
        Window.Current.Content = rootFrame;

        // Navigate to the page that shows the Contact UI.
        rootFrame.Navigate(typeof(ContactPage), e);

        // Ensure the current window is active
        Window.Current.Activate();
    }
}
```

使用此合约激活应用程序后，它将收到 [ContactPanelActivatedEventArgs 对象](https://docs.microsoft.com/en-us/uwp/api/windows.applicationmodel.activation.contactpanelactivatedeventargs)。  这包含应用程序启动时尝试与之进行交互的联系人的 ID，以及 [ContactPanel](https://docs.microsoft.com/en-us/uwp/api/windows.applicationmodel.contacts.contactpanel) 对象。 你应该保留对此 ContactPanel 对象的引用，这样，你将可以与面板进行交互。

ContactPanel 对象有应用程序应该侦听的两个事件：
+ 当用户调用了要求在其自己的窗口中启动完整应用程序的 UI 元素后，将会发送 **LaunchFullAppRequested** 事件。  你的应用程序负责自行启动并传递所有必需的上下文。  但是，你可以根据喜好自由地执行此操作（例如，通过协议启动）。
+ 当你的应用程序即将关闭时会发送 **Closing** 事件，并允许你保存任何上下文。

ContactPanel 对象还允许你设置联系人面板标题的背景颜色（如果未设置，它将默认为系统主题），并且允许以编程方式关闭联系人面板。



## <a name="the-pinnedcontactmanager-class"></a>PinnedContactManager 类

[PinnedContactManager](https://docs.microsoft.com/en-us/uwp/api/windows.applicationmodel.contacts.pinnedcontactmanager) 用于管理将哪些联系人固定到任务栏。 利用此类，你可以固定和取消固定联系人、确定是否固定了联系人，并确定当前运行应用程序的系统是否支持在特定图面上进行固定。

你可以使用 **GetDefault** 方法检索 PinnedContactManager 对象：

```Csharp
PinnedContactManager pinnedContactManager = PinnedContactManager.GetDefault();
```

## <a name="pinning-and-unpinning-contacts"></a>固定和取消固定联系人
你现在可以使用刚创建的 PinnedContactManager 固定和取消固定联系人。 **RequestPinContactAsync** 和 **RequestUnpinContactAsync** 方法向用户提供确认对话框，因此必须从应用程序单线程单元（ASTA 或 UI）线程中调用它们。

```Csharp
async void PinContact (Contact contact)
{
    await pinnedContactManager.RequestPinContactAsync(contact,
                                                      PinnedContactSurface.Taskbar);
}

async void UnpinContact (Contact contact)
{
    await pinnedContactManager.RequestUnpinContactAsync(contact,
                                                        PinnedContactSurface.Taskbar);
}
```

你还可以同时固定多个联系人：

```Csharp
async Task PinMultipleContacts(Contact[] contacts)
{
    await pinnedContactManager.RequestPinContactsAsync(
        contacts, PinnedContactSurface.Taskbar);
}
```

> [!Note]
> 目前，无法通过批处理操作来取消固定联系人。

**注意：** 

## <a name="see-also"></a>另请参阅
+ [“我的人脉”共享](my-people-sharing.md)
+ [“我的人脉”通知](my-people-notifications.md)
+ [联系人卡片示例](https://github.com/Microsoft/Windows-universal-samples/tree/6370138b150ca8a34ff86de376ab6408c5587f5d/Samples/ContactCardIntegration)
+ [PinnedContactManager 类文档](https://docs.microsoft.com/en-us/uwp/api/windows.applicationmodel.contacts.pinnedcontactmanager)