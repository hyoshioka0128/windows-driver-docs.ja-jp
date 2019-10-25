---
title: プロパティ ページ プラグイン
description: プロパティ ページ プラグイン
ms.assetid: cf5f5861-1670-413c-9c42-c1b6eb6d719a
keywords:
- カーネルストリーミングプロキシ WDK AVStream、プロパティページ
- プロパティページ WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6c536c42576e6ae25a6c6b8d7ebf9506bd61f0f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823730"
---
# <a name="property-page-plug-in"></a>プロパティ ページ プラグイン


KS プロキシのプラグインとしてプロパティページを記述することにより、デバイスプロパティにユーザーインターフェイスを提供できます。 このトピックでは、このようなプラグインを作成する方法について説明します。 まず、「 [KS プロキシプラグインの登録](registering-ks-proxy-plug-ins.md)」の説明に従ってオブジェクトを登録します。

次に、フィルターのファクトリテンプレートを宣言します。 ファクトリテンプレートは、クラスC++ファクトリの情報を格納するクラスです。

DLL 内で、DLL 内のフィルターまたは COM コンポーネントごとに1つずつ、 [CFactoryTemplate](https://go.microsoft.com/fwlink/p/?linkid=106450)オブジェクトのグローバル配列を宣言します。 プロパティページが1つしかない場合は、配列内にオブジェクトを1つだけ作成します。

各オブジェクトについて、クラス識別子 (CLSID) の GUID を生成し、宣言にエントリを指定します。

配列は、g\_Templates という名前にする必要があります。

```cpp
CFactoryTemplate g_Templates[] =
{
    {
        L"My Property Page",
        &CLSID_MyPropPage),
        CMyPropPage::CreateInstance,
        NULL,
        NULL
    },
};
```

プロパティページは[cbasepropertypage](https://go.microsoft.com/fwlink/p/?linkid=106449)クラスから派生する必要があり、 **cbasepropertypage**のいくつかのメソッドをオーバーライドする必要があります。

```cpp
class CMyPropPage: public CBasePropertyPage
{
public:
    // creation routine returns ptr to new prop pg as a CUnknown
    static CUnknown* CreateInstance( LPUNKNOWN piOuterUnknown, HRESULT* phResult );

    // overridden methods:
    HRESULT OnConnect( IUnknown *punk);
    HRESULT OnDisconnect();
    HRESULT OnApplyChanges();
    HRESULT OnActivate();
    HRESULT OnDeactivate();
    INT_PTR OnReceiveMessage( HWND hWnd, UINT uMsg, WPARAM wParam, LPARAM lParam );
private:
    CMyPropPage ( LPUNKNOWN piOuterUnknown );
};
```

プロパティページを初期化するために、ホスティングプロパティシートは[IPropertyPage:: Set ite](https://go.microsoft.com/fwlink/p/?linkid=106442)を呼び出します。 この呼び出しは、プラグインの**OnConnect**メソッドの呼び出しになります。 この呼び出しの時点では、プロパティページはフィルターに接続されていますが、プロパティページはまだ表示されていません。

**OnConnect**への呼び出しで指定されるパラメーターは KS プロキシへのインターフェイスであり、 **IKsPropertySet**へのポインターに対してクエリを実行できます。 その後、 [**IKsPropertySet:: Get**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-ikspropertyset-get)と[**IKsPropertySet:: Set**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dsound/nf-dsound-ikspropertyset-set)を呼び出して、ドライバーの公開されたプロパティを操作できます。

また、 **CreateInstance**メソッドも指定する必要があります。 システムは、プロパティページのメソッドを呼び出して、プロパティページのインスタンスを作成します。 このメソッドは、クラスのコンストラクターを呼び出してインスタンス化する必要があります。

コンストラクターは、外側の不明なインターフェイス (この場合は KS プロキシ) へのポインターを受け取ります。

プロパティページの**OnDisconnect**メソッドは、プロパティページが関連オブジェクトを解放する必要があるときに呼び出されます。 このコールバックでは、 **Release**メソッドを呼び出すことによって、インターフェイスへのポインターの参照カウントを KS プロキシにデクリメントする必要があります。

 

 




