---
title: ネットワークの接続ウィザード内のカスタム UI ページを表示します。
description: ネットワークの接続ウィザード内のカスタム UI ページを表示します。
ms.assetid: 102f142a-91d1-4b55-a111-15a297c03e23
keywords:
- カスタム UI WDK ネイティブ 802.11 IHV UI 拡張機能の DLL、ネットワーク接続ウィザード
- ネットワーク接続ウィザード WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71b3a0d2d8c408567fe0b734dbc49f1178a5f3db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536769"
---
# <a name="displaying-custom-ui-pages-within-the-network-connection-wizard"></a>ネットワークの接続ウィザード内のカスタム UI ページを表示します。




 

802.11 IHV UI 拡張機能のネイティブ DLL でサポートされているカスタム ユーザー インターフェイス (UI) は、UI の要求がいずれかで行われたときに、オペレーティング システムのネットワーク接続ウィザード内で表示できます。

-   呼び出し[ **Dot11ExtSendUIRequest**](https://msdn.microsoft.com/library/windows/hardware/ff547567)、ネイティブの 802.11 IHV 拡張機能の DLL によって行われました。 このプロセスの詳細については、次を参照してください。[カスタム UI の表示を要求する](requesting-the-display-of-a-custom-ui.md)します。

-   ネイティブ 802.11 IHV 拡張 DLL の呼び出し**Dot11ExtQueryUIRequest**オペレーティング システムによって行われた、IHV ハンドラー関数。 このプロセスの詳細については、次を参照してください。[カスタム UI を表示するためのクエリ](querying-for-the-display-of-a-custom-ui.md)します。

オペレーティング システムでは、ワイヤレス ネットワークに接続しようとして、ワイヤレス LAN (WLAN) アダプター場合に、ネットワーク接続ウィザード内でカスタムの UI が表示されます。 このような状況では、カスタム UI の要求が期間内のバルーン通知として表示されます。

-   オペレーティング システム DLL を呼び出すネイティブ 802.11 IHV 拡張機能の後に[ *Dot11ExtIhvPerformPreAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547499)ワイヤレス ネットワークの関連付け前の操作を開始する IHV ハンドラー関数。

-   ネイティブの 802.11 IHV 拡張 DLL の呼び出しの前に[ **Dot11ExtPostAssociateCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff547530)後関連付け操作を正常に完了します。

ネットワークの接続ウィザード内でカスタム UI 要求を挿入するときに、オペレーティング システムは、次を行います。

1.  DLL を呼び出すネイティブ 802.11 IHV 拡張機能の[ *Dot11ExtIhvIsUIRequestPending* ](https://msdn.microsoft.com/library/windows/hardware/ff547479) IHV ハンドラー関数 UI 要求がまだがかどうかを判断する保留中です。 オペレーティング システムに渡されるグローバル一意識別子 (GUID) を使用して UI 要求を指定する[ **Dot11ExtSendUIRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff547567) 802.11 IHV 拡張機能のネイティブ DLL でします。

2.  場合[ *Dot11ExtIhvIsUIRequestPending* ](https://msdn.microsoft.com/library/windows/hardware/ff547479)返します**TRUE**オペレーティング システムを要求されたインスタンスの指定した UI 要求**IWizardExtension** COM インターフェイスと、ネットワーク接続ウィザードのフロー、現在の UI にバインドします。 呼び出し時に[ **Dot11ExtSendUIRequest**](https://msdn.microsoft.com/library/windows/hardware/ff547567)、ネイティブの 802.11 IHV 拡張 DLL のクラス id (CLSID) を指定します、 **IWizardExtension**実装内のネイティブ 802.11 IHV UI 拡張 DLL。

    オペレーティング システムも呼び出して、 **IWizardExtension::AddPages**メソッドを使用する 802.11 IHV UI 拡張機能のネイティブ DLL がカスタム UI ページを表す PROPSHEETPAGE 構造体のハンドルの配列を返します。

    詳細については、 **IWizardExtension** COM インターフェイスを参照してください[IWizardExtension COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56607)します。

3.  を介してネイティブ 802.11 IHV UI 拡張 DLL で制御される UI ページ間を移動、 **IWizardSite** COM インターフェイスです。 このインターフェイスの詳細については、次を参照してください。 [IWizardSite COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56608)します。

802.11 IHV UI 拡張機能のネイティブ DLL の読み取りまたは書き込みをコンテキストに固有のデータ、カスタム UI が表示されている間、 [IPropertyBag COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56610)します。 このプロセスの詳細については、次を参照してください。[へのアクセス プロファイルとコンテキスト データ](accessing-profile-and-context-data.md)します。

802.11 IHV UI 拡張機能のネイティブ DLL が呼び出すことによって、802.11 IHV 拡張機能のネイティブ DLL にユーザーが入力した応答データを返すことができます、カスタム UI が表示されたら、 **WlanSendUIResponse**します。 DLL では、応答データを格納するバッファーへのポインターと同様に、UI 要求の GUID に渡します。

802.11 IHV UI 拡張機能のネイティブ DLL 後**WlanSendUIResponse**、オペレーティング システム DLL を呼び出すネイティブ 802.11 IHV 拡張機能の[ *Dot11ExtIhvProcessUIResponse* ](https://msdn.microsoft.com/library/windows/hardware/ff547504)カスタム UI の応答データを転送する IHV ハンドラー関数。

詳細については、 **WlanSendUIResponse** API、Microsoft Windows SDK のドキュメントを参照してください。

 

 





