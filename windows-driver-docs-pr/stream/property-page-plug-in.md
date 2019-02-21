---
title: プラグインのプロパティ ページ
description: プラグインのプロパティ ページ
ms.assetid: cf5f5861-1670-413c-9c42-c1b6eb6d719a
keywords:
- カーネル ストリーミング プロキシ WDK AVStream、プロパティ ページ
- WDK AVStream プロパティ ページ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca2464ee8b40dfb68b434d02b0f09d2f1ef60666
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537338"
---
# <a name="property-page-plug-in"></a>プラグインのプロパティ ページ


KS プロキシ用のプラグインとしてのプロパティ ページを記述することで、デバイスのプロパティへのユーザー インターフェイスを行うことができます。 このトピックでは、このようなプラグインを作成する方法について説明します。 」の説明に従って、オブジェクトを最初に、登録[KS プロキシの登録にプラグイン](registering-ks-proxy-plug-ins.md)します。

次に、フィルターの工場出荷時のテンプレートを宣言します。 工場出荷時のテンプレートは、クラス ファクトリに関する情報を含む C++ クラスです。

DLL の宣言のグローバル配列[CFactoryTemplate](https://go.microsoft.com/fwlink/p/?linkid=106450)オブジェクト、フィルターまたは DLL で COM コンポーネントごとに 1 つ。 1 つのプロパティ ページのみの場合は、配列の 1 つのオブジェクトを作成します。

オブジェクトごとに、クラス id (CLSID) の GUID を生成し、宣言内のエントリを提供します。

配列は、g 名前必要があります\_テンプレート。

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

プロパティ ページがクラスから派生する必要があります[CBasePropertyPage](https://go.microsoft.com/fwlink/p/?linkid=106449)いくつかのメソッドのオーバーライドと**CBasePropertyPage**:

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

ホストのプロパティ シートの呼び出し、プロパティ ページを初期化する[IPropertyPage::SetPageSite](https://go.microsoft.com/fwlink/p/?linkid=106442)します。 この呼び出しの結果、プラグインの呼び出しで**OnConnect**メソッド。 この呼び出しの時に、プロパティ ページが、フィルターに接続されたが、プロパティ ページが表示されていません。

呼び出しで指定されたパラメーター **OnConnect**インターフェイスへのポインターを照会することができますし、KS プロキシは、 **IKsPropertySet**します。 呼び出して[ **IKsPropertySet::Get** ](https://msdn.microsoft.com/library/windows/hardware/ff560719)と[ **IKsPropertySet::Set** ](https://msdn.microsoft.com/library/windows/hardware/ff560721)ドライバーの公開されているプロパティを操作します。

指定することも必要があります、 **CreateInstance**メソッド。 システムでは、プロパティ ページのインスタンスを作成するプロパティ ページのメソッドを呼び出します。 このメソッドは、インスタンス化するクラスのコンス トラクターを呼び出す必要があります。

コンス トラクターは、KS プロキシをここでは外部の不明なインターフェイスへのポインターを受け取ります。

プロパティ ページの**OnDisconnect**メソッドが呼び出されますプロパティ ページが関連付けられているオブジェクトを解放する必要があります。 このコールバックは、呼び出すことによって KS プロキシへのインターフェイスへのポインターの参照カウントをデクリメントする必要があります、**リリース**メソッド。

 

 




