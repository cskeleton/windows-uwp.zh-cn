---
author: stevewhims
description: C + + /winrt 提供函数和节省大量时间和精力当你想要实现和/或传递集合的基类。
title: 集合通过 C + + WinRT
ms.author: stwhi
ms.date: 08/24/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10，uwp，标准，c + +，cpp，winrt，投影集合
ms.localizationpriority: medium
ms.openlocfilehash: 5495649a6b7fad633e24e244aa3f6efbcc05e441
ms.sourcegitcommit: 7efffcc715a4be26f0cf7f7e249653d8c356319b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "3118067"
---
# <a name="collections-with-cwinrtwindowsuwpcpp-and-winrt-apisintro-to-using-cpp-with-winrt"></a>使用集合[C + + WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt)

> [!NOTE]
> **与在商业发行之前可能会进行实质性修改的预发布产品相关的一些信息。 Microsoft 对于此处提供的信息不作任何明示或默示的担保。**

在内部，Windows 运行时集合有很多复杂移动部件。 但当你想要将集合对象传递给 Windows 运行时函数，或实现你自己的集合属性和集合类型，有函数和基本类在 C + + /winrt 来支持你。 这些功能的复杂性退出或在双手，并采用时间和精力保存你的大量的开销。

> [!IMPORTANT]
> 如果你安装了[Windows 10 SDK 预览版 17661](https://www.microsoft.com/software-download/windowsinsiderpreviewSDK)，可用或更高版本可以在本主题中所述的功能。

[**IVector**](/uwp/api/windows.foundation.collections.ivector_t_)是实现的元素的任何随机访问集合的 Windows 运行时接口。 如果你要自行实现**IVector** ，还需要实现[**IIterable**](/uwp/api/windows.foundation.collections.iiterable_t_)、 [**IVectorView**](/uwp/api/windows.foundation.collections.ivectorview_t_)和[**IIterator**](/uwp/api/windows.foundation.collections.iiterator_t_)。 即使你*需要*自定义集合类型，有大量工作。 但是，如果你已将**std:: vector** （或**std:: map**或**std::unordered_map**） 中的数据，并且你希望将，传递给 Windows 运行时 API，然后你想要避免尽可能进行工作，该级别。 和避免它*是*可能的因为 C + + WinRT 将帮助你有效地和轻松地创建集合。

## <a name="helper-functions-for-collections"></a>对于集合的帮助程序函数

### <a name="general-purpose-collection-empty"></a>常规用途的集合空

若要检索实现通用集合的类型的新对象，你可以调用[**winrt::single_threaded_vector**](/uwp/cpp-ref-for-winrt/single-threaded-vector)函数模板。 作为[**IVector**](/uwp/api/windows.foundation.collections.ivector_t_)，返回的对象，它通过其调用返回的对象的函数和属性的接口。

```cppwinrt
...
#include <winrt/Windows.Foundation.Collections.h>
#include <iostream>
using namespace winrt;
...
int main()
{
    init_apartment();

    Windows::Foundation::Collections::IVector<int> coll{ winrt::single_threaded_vector<int>() };
    coll.Append(1);
    coll.Append(2);
    coll.Append(3);

    for (auto const& el : coll)
    {
        std::cout << el << std::endl;
    }

    Windows::Foundation::Collections::IVectorView<int> view{ coll.GetView() };
}
```

你可以看到在上面的代码示例中，创建集合后可以追加元素，循环访问它们，并通常将该对象，就像你可能已从 API 收到任何 Windows 运行时集合对象。 如果你需要对集合的不可变的视图，然后你可以调用[**IVector::GetView**](/uwp/api/windows.foundation.collections.ivector-1.getview)，所示。 如上所示的模式&mdash;的创建和使用集合&mdash;适用于你想要将数据传入，或获取数据，API 的简单方案。

### <a name="general-purpose-collection-primed-from-data"></a>常规用途的集合，从数据 primed

你还可以避免对你可以在上面的代码示例中看到的**追加**调用的开销。 你可能已具有源数据中，或者你可能想要填充之前创建的 Windows 运行时集合对象。 操作方法如下。

```cppwinrt
auto coll1{ winrt::single_threaded_vector<int>({ 1,2,3 }) };

std::vector<int> values{ 1,2,3 };
auto coll2{ winrt::single_threaded_vector<int>(std::move(values)) };

for (auto const& el : coll2)
{
    std::cout << el << std::endl;
}
```

你可以传递一个包含到**winrt::single_threaded_vector**，数据的临时对象与`coll1`上面。 也可以移动 （假设你将不会访问它再次） **std:: vector**到函数。 在这两种情况下，你在传递到函数的*rvalue* 。 这样可以让编译器有效，并避免复制数据。 如果你想要了解有关*rvalues*的详细信息，请参阅[值的分类，并且对它们的引用](cpp-value-categories.md)。

如果你想要将 XAML 项目控件绑定到集合，然后就可以。 但请注意，若要正确设置[**ItemsControl.ItemsSource**](/uwp/api/windows.ui.xaml.controls.itemscontrol.itemssource)属性，你需要将其设置为类型**IVector** **IInspectable** （或互操作性类型，如[**IBindableObservableVector**](/uwp/api/windows.ui.xaml.interop.ibindableobservablevector)） 的值。 下面是一个代码示例，生成的集合类型适合绑定，并将元素追加到它。

```cppwinrt
auto bookSkus{ winrt::single_threaded_vector<Windows::Foundation::IInspectable>() };
bookSkus.Append(make<Bookstore::implementation::BookSku>(L"Moby Dick"));
```

上面*可以*集合可绑定到 XAML 项目控件;但集合不是可供观察。

### <a name="observable-collection"></a>可观测集合

若要检索实现*可观测*集合的类型的新对象，请使用任何元素类型调用[**winrt::single_threaded_observable_vector**](/uwp/cpp-ref-for-winrt/single-threaded-observable-vector)函数模板。 但若要使一个可观测集合适合绑定到 XAML 项目控件，用作**IInspectable**元素类型。

作为[**IObservableVector**](/uwp/api/windows.foundation.collections.iobservablevector_t_)，返回的对象，它通过其你 （或绑定到该控件） 调用返回的对象的函数和属性的接口。

```cppwinrt
auto bookSkus{ winrt::single_threaded_observable_vector<Windows::Foundation::IInspectable>() };
```

有关详细信息和代码示例，有关绑定你的用户界面 (UI) 控件到一个可观测集合，请参阅[XAML 项目控件; 绑定到 C + + /winrt 集合](binding-collection.md)。

### <a name="associative-collection-map"></a>关联的集合 （映射）

有关联的集合的目前我们所看到的两个功能的版本。

- [**Winrt::single_threaded_map**](/uwp/cpp-ref-for-winrt/single-threaded-map)函数模板返回为[**IMap**](/uwp/api/windows.foundation.collections.imap_k_v_)关联非可观测集合。
- [**Winrt::single_threaded_observable_map**](/uwp/cpp-ref-for-winrt/single-threaded-observable-map)函数模板返回为[**IObservableMap**](/uwp/api/windows.foundation.collections.iobservablemap_k_v_)关联可观测集合。

（可选） 可以通过将传递给该函数的类型**std:: map**或**std::unordered_map** *rvalue*优化数据与这些集合。

```cppwinrt
auto coll1{
    winrt::single_threaded_map<winrt::hstring, int>(std::map<winrt::hstring, int>{
        { L"AliceBlue", 0xfff0f8ff }, { L"AntiqueWhite", 0xfffaebd7 }
    })
};

std::map<winrt::hstring, int> values{
    { L"AliceBlue", 0xfff0f8ff }, { L"AntiqueWhite", 0xfffaebd7 }
};
auto coll2{ winrt::single_threaded_map<winrt::hstring, int>(std::move(values)) };
```

### <a name="single-threaded"></a>单线程

"单线程"的这些函数的名称中指示他们不提供任何并发&mdash;换言之，它们不是线程安全。 提及的线程的无关而言，因为从这些函数返回的对象是所有敏捷 (请参阅[敏捷对象在 C + + WinRT](agile-objects.md))。 只是对象的单线程。 如果你只是想要在应用程序二进制接口 (ABI) 传递数据的一种方法或其他完全合适。

## <a name="base-classes-for-collections"></a>对于集合的基类

如果要为完整的灵活性，实现你自己的自定义集合，然后你将想要避免执行此操作的方法。 例如，这是一个自定义的矢量视图将如下所示*不借助 C + + /winrt 的基类*。

```cppwinrt
...
using namespace winrt;
using namespace Windows::Foundation::Collections;
...
struct MyVectorView :
    implements<MyVectorView, IVectorView<float>, IIterable<float>>
{
    // IVectorView
    float GetAt(uint32_t const) { ... };
    uint32_t GetMany(uint32_t, winrt::array_view<float>) const { ... };
    bool IndexOf(float, uint32_t&) { ... };
    uint32_t Size() { ... };

    // IIterable
    IIterator<float> First() const { ... };
};
...
IVectorView<float> view{ winrt::make<MyVectorView>() };
```

相反，它是更易于[**winrt::vector_view_base**](/uwp/cpp-ref-for-winrt/vector-view-base)结构模板中，从派生自定义的矢量视图和只实现**get_container**函数来公开容器保存你的数据。

```cppwinrt
struct MyVectorView2 :
    implements<MyVectorView2, IVectorView<float>, IIterable<float>>,
    winrt::vector_view_base<MyVectorView2, float>
{
    auto& get_container() const noexcept
    {
        return m_values;
    }

private:
    std::vector<float> m_values{ 0.1f, 0.2f, 0.3f };
};
```

返回**get_container**容器必须提供的**开始**和**结束**接口该**winrt::vector_view_base**预期。 如上面的示例中所示， **std:: vector**提供的。 但是，则可以返回满足相同合约，包括你自己的自定义容器的任何容器。

```cppwinrt
struct MyVectorView3 :
    implements<MyVectorView3, IVectorView<float>, IIterable<float>>,
    winrt::vector_view_base<MyVectorView3, float>
{
    auto get_container() const noexcept
    {
        struct container
        {
            float const* const first;
            float const* const last;

            auto begin() const noexcept
            {
                return first;
            }

            auto end() const noexcept
            {
                return last;
            }
        };

        return container{ m_values.data(), m_values.data() + m_values.size() };
    }

private:
    std::array<float, 3> m_values{ 0.2f, 0.3f, 0.4f };
};
```

以下是基本的类的 C + + /winrt 提供可帮助你实现自定义的集合。

### [<a name="winrtvectorviewbase"></a>winrt::vector_view_base](/uwp/cpp-ref-for-winrt/vector-view-base)

请参阅上面的代码示例。

### [<a name="winrtvectorbase"></a>winrt::vector_base](/uwp/cpp-ref-for-winrt/vector-base)

```cppwinrt
struct MyVector :
    implements<MyVector, IVector<float>, IVectorView<float>, IIterable<float>>,
    winrt::vector_base<MyVector, float>
{
    auto& get_container() const noexcept
    {
        return m_values;
    }

    auto& get_container() noexcept
    {
        return m_values;
    }

private:
    std::vector<float> m_values{ 0.1f, 0.2f, 0.3f };
};
```

### [<a name="winrtobservablevectorbase"></a>winrt::observable_vector_base](/uwp/cpp-ref-for-winrt/observable-vector-base)

```cppwinrt
struct MyObservableVector :
    implements<MyObservableVector, IObservableVector<float>, IVector<float>, IVectorView<float>, IIterable<float>>,
    winrt::observable_vector_base<MyObservableVector, float>
{
    auto& get_container() const noexcept
    {
        return m_values;
    }

    auto& get_container() noexcept
    {
        return m_values;
    }

private:
    std::vector<float> m_values{ 0.1f, 0.2f, 0.3f };
};
```

### [<a name="winrtmapviewbase"></a>winrt::map_view_base](/uwp/cpp-ref-for-winrt/map-view-base)

```cppwinrt
struct MyMapView :
    implements<MyMapView, IMapView<winrt::hstring, int>, IIterable<IKeyValuePair<winrt::hstring, int>>>,
    winrt::map_view_base<MyMapView, winrt::hstring, int>
{
    auto& get_container() const noexcept
    {
        return m_values;
    }

private:
    std::map<winrt::hstring, int> m_values{
        { L"AliceBlue", 0xfff0f8ff }, { L"AntiqueWhite", 0xfffaebd7 }
    };
};
```

### [<a name="winrtmapbase"></a>winrt::map_base](/uwp/cpp-ref-for-winrt/map-base)

```cppwinrt
struct MyMap :
    implements<MyMap, IMap<winrt::hstring, int>, IMapView<winrt::hstring, int>, IIterable<IKeyValuePair<winrt::hstring, int>>>,
    winrt::map_base<MyMap, winrt::hstring, int>
{
    auto& get_container() const noexcept
    {
        return m_values;
    }

    auto& get_container() noexcept
    {
        return m_values;
    }

private:
    std::map<winrt::hstring, int> m_values{
        { L"AliceBlue", 0xfff0f8ff }, { L"AntiqueWhite", 0xfffaebd7 }
    };
};
```

### [<a name="winrtobservablemapbase"></a>winrt::observable_map_base](/uwp/cpp-ref-for-winrt/observable-map-base)

```cppwinrt
struct MyObservableMap :
    implements<MyObservableMap, IObservableMap<winrt::hstring, int>, IMap<winrt::hstring, int>, IMapView<winrt::hstring, int>, IIterable<IKeyValuePair<winrt::hstring, int>>>,
    winrt::observable_map_base<MyObservableMap, winrt::hstring, int>
{
    auto& get_container() const noexcept
    {
        return m_values;
    }

    auto& get_container() noexcept
    {
        return m_values;
    }

private:
    std::map<winrt::hstring, int> m_values{
        { L"AliceBlue", 0xfff0f8ff }, { L"AntiqueWhite", 0xfffaebd7 }
    };
};
```

## <a name="important-apis"></a>重要的 API
* [ItemsControl.ItemsSource](/uwp/api/windows.ui.xaml.controls.itemscontrol.itemssource)
* [IObservableVector](/uwp/api/windows.foundation.collections.iobservablevector_t_)
* [IVector](/uwp/api/windows.foundation.collections.ivector_t_)
* [winrt::map_base](/uwp/cpp-ref-for-winrt/map-base)
* [winrt::map_view_base](/uwp/cpp-ref-for-winrt/map-view-base)
* [winrt::observable_map_base](/uwp/cpp-ref-for-winrt/observable-map-base)
* [winrt::observable_vector_base](/uwp/cpp-ref-for-winrt/observable-vector-base)
* [winrt::single_threaded_observable_map](/uwp/cpp-ref-for-winrt/single-threaded-observable-map)
* [winrt::single_threaded_map](/uwp/cpp-ref-for-winrt/single-threaded-map)
* [winrt::single_threaded_observable_vector](/uwp/cpp-ref-for-winrt/single-threaded-observable-vector)
* [winrt::single_threaded_vector](/uwp/cpp-ref-for-winrt/single-threaded-vector)
* [winrt::vector_base](/uwp/cpp-ref-for-winrt/vector-base)
* [winrt::vector_view_base](/uwp/cpp-ref-for-winrt/vector-view-base)

## <a name="related-topics"></a>相关主题
* [值的分类，并且对它们的引用](cpp-value-categories.md)
* [XAML 项目控件；绑定到 C++/WinRT 集合](binding-collection.md)