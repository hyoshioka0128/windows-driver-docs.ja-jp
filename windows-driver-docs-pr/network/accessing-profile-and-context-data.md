---
title: プロファイルとコンテキスト データへのアクセス
description: プロファイルとコンテキスト データへのアクセス
ms.assetid: 88463b20-e61b-4258-b5ff-9b6880c1d0f6
keywords:
- カスタム UI WDK ネイティブ 802.11 IHV UI 拡張 DLL、プロファイルデータ
- カスタム UI WDK ネイティブ 802.11 IHV UI 拡張 DLL、コンテキストデータ
- コンテキストデータ WDK ネットワーク
- プロファイルデータ WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4ca9eb2324f763f721a9f4881aaeff7540f2909
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835401"
---
# <a name="accessing-profile-and-context-data"></a>プロファイルとコンテキスト データへのアクセス




 

ネイティブ 802.11 IHV UI 拡張 DLL でサポートされているカスタムユーザーインターフェイス (UI) は、次のいずれかを使用して表示できます。

-   ネイティブ 802.11 IHV 拡張 DLL によって作成された[**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)の呼び出し。 このプロセスの詳細については、「[カスタム UI の表示の要求](requesting-the-display-of-a-custom-ui.md)」を参照してください。

-   オペレーティングシステムによって作成されたネイティブ 802.11 IHV Extensions DLL の*Dot11ExtQueryUIRequest* ihv ハンドラー関数の呼び出し。 このプロセスの詳細については、「[カスタム UI の表示のクエリ](querying-for-the-display-of-a-custom-ui.md)」を参照してください。

バルーン通知またはオペレーティングシステムのネットワーク接続ウィザードのいずれかを使用して UI 要求を表示するかどうかに関係なく、ネイティブ 802.11 IHV UI 拡張 DLL は次のデータにアクセスできます。

<a href="" id="network-connection-profile-data"></a>**ネットワーク接続プロファイルデータ**  
ネットワーク接続ウィザード内にカスタム UI が表示されている場合、ネイティブ 802.11 IHV UI 拡張 DLL は、現在のネットワーク接続プロファイルの IHV 定義の部分にアクセスできます。 このデータは、&lt;IHV&gt; &lt;/ihv&gt; XML タグによって制限された XML フラグメントとして書式設定されます。 これらのタグ内の XML データは、IHV の実装に固有であり、オペレーティングシステムに対して非透過的です。

プロファイルデータへのアクセスは、 **IHV\_profile\_data**という名前のプロパティの[IPropertyBag COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56610)の**読み取り**および**書き込み**メソッドを介して行われます。

<a href="" id="context-data"></a>**コンテキストデータ**  
ネイティブ 802.11 IHV 拡張 DLL では、 [**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)と[*Dot11ExtIhvQueryUIRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_query_ui_request)の両方で引数として渡される[**DOT11EXT\_IHV\_UI\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request)構造を使用して、カスタム ui を指定します。関数. IHV は、DOT11EXT\_IHV\_UI\_要求構造体内で、カスタム UI に固有のコンテキストデータを使用して ( **Pvuirequest**メンバーを介して) 提供できます。 通常、IHV は、このデータをカスタム UI の既定の設定でフォーマットします。

プロファイルデータへのアクセスは、 **IHV\_NOTIFICATION\_data**という名前のプロパティの[IPropertyBag COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56610)の**読み取り**および**書き込み**メソッドを介して行われます。

ネイティブ 802.11 IHV UI 拡張 DLL は、 [**IObjectWithSite:: SetSite**](https://docs.microsoft.com/windows/desktop/api/ocidl/nf-ocidl-iobjectwithsite-setsite)メソッドを介して返される*IUnknown*ポインターを介して[IPropertyBag COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56610)にアクセスします。 詳細については、「 [**IObjectWithSite**](https://docs.microsoft.com/windows/desktop/api/ocidl/nn-ocidl-iobjectwithsite)」を参照してください。

IPropertyBag COM インターフェイスの代替手段として、ネイティブ 802.11 IHV UI 拡張 DLL は、 [**Getprop**](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-getpropa) Win32 を使用して、 **ihv\_プロファイル\_データ**および**ihv\_通知\_データ**プロパティにアクセスできます。プロシージャ. このような場合は、次の例に示すように、DLL で親ウィンドウのハンドルを使用する必要があります。

```C++
LPWSTR lpszBuffer = (LPWSTR) GetProp(GetParent(hwndDlg), L"IHV_PROFILE_DATA");
```

 

 





