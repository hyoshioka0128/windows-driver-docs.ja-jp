---
title: プロファイルとコンテキスト データへのアクセス
description: プロファイルとコンテキスト データへのアクセス
ms.assetid: 88463b20-e61b-4258-b5ff-9b6880c1d0f6
keywords:
- カスタム UI WDK ネイティブ 802.11 IHV UI 拡張機能の DLL、プロファイル データ
- カスタム UI WDK ネイティブ 802.11 IHV UI 拡張機能の DLL、コンテキスト データ
- コンテキスト データ WDK ネットワーク
- プロファイル データの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 926dfd62e3405a376a7148da77ff0549dbab8c14
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384426"
---
# <a name="accessing-profile-and-context-data"></a>プロファイルとコンテキスト データへのアクセス




 

802.11 IHV UI 拡張機能のネイティブ DLL でサポートされているカスタム ユーザー インターフェイス (UI) は、いずれかで表示できます。

-   呼び出し[ **Dot11ExtSendUIRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_ui_request) 802.11 IHV 拡張機能のネイティブ DLL によって行われました。 このプロセスの詳細については、次を参照してください。[カスタム UI の表示を要求する](requesting-the-display-of-a-custom-ui.md)します。

-   ネイティブ 802.11 IHV 拡張 DLL の呼び出し*Dot11ExtQueryUIRequest*オペレーティング システムによって行われた IHV ハンドラー関数。 このプロセスの詳細については、次を参照してください。[カスタム UI を表示するためのクエリ](querying-for-the-display-of-a-custom-ui.md)します。

バルーン通知またはオペレーティング システムのネットワーク接続ウィザードを通じて UI 要求が表示するかどうかに関係なく、802.11 IHV UI 拡張機能のネイティブの DLL は、次のデータにアクセスできます。

<a href="" id="network-connection-profile-data"></a>**ネットワーク接続のプロファイル データ**  
カスタム UI は、ネットワークの接続ウィザード内に表示される、802.11 IHV UI 拡張機能のネイティブ DLL は、現在のネットワーク接続プロファイルの IHV で定義された部分にアクセスできます。 このデータは境界付けられた XML フラグメントとして書式設定、 &lt;IHV&gt; &lt;/IHV&gt; XML タグ。 これらのタグ内の XML データは、IHV の実装に固有し、オペレーティング システムに対して非透過的です。

プロファイル データへのアクセスは、**読み取り**と**書き込み**のメソッド、 [IPropertyBag COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56610)という名前のプロパティの**IHV\_プロファイル\_データ**します。

<a href="" id="context-data"></a>**コンテキスト データ**  
ネイティブの 802.11 IHV 拡張機能の DLL によってカスタム UI を指定します、 [ **DOT11EXT\_IHV\_UI\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request)構造体は、両方の引数として渡される、[ **Dot11ExtSendUIRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_ui_request)と[ *Dot11ExtIhvQueryUIRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_query_ui_request)関数。 DOT11EXT 内\_IHV\_UI\_、IHV が提供できる要求の構造 (を通じて、 **pvUIRequest**メンバー) にカスタム UI 固有のコンテキスト データ。 通常、IHV は、カスタム UI の既定の設定では、このデータを書式設定します。

プロファイル データへのアクセスは、**読み取り**と**書き込み**のメソッド、 [IPropertyBag COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56610)という名前のプロパティの**IHV\_通知\_データ**します。

802.11 IHV UI 拡張機能のネイティブ DLL にアクセスする、 [IPropertyBag COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56610)を通じて、 *IUnknown*によって返されるポインター、 [ **IObjectWithSite::SetSite** ](https://docs.microsoft.com/windows/desktop/api/ocidl/nf-ocidl-iobjectwithsite-setsite)メソッド。 詳細については、次を参照してください。 [ **IObjectWithSite**](https://docs.microsoft.com/windows/desktop/api/ocidl/nn-ocidl-iobjectwithsite)します。

IPropertyBag COM インターフェイスの代わりに、802.11 IHV UI 拡張機能のネイティブ DLL にアクセスできる、 **IHV\_プロファイル\_データ**と**IHV\_通知\_データ**プロパティを通じて、 [ **GetProp** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-getpropa) Win32 関数。 このような状況で次の例に示すように、DLL は、親ウィンドウのハンドルを使用する必要があります。

```C++
LPWSTR lpszBuffer = (LPWSTR) GetProp(GetParent(hwndDlg), L"IHV_PROFILE_DATA");
```

 

 





