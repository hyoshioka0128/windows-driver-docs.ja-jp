---
title: ネットワーク接続ウィザード内のカスタム UI ページの表示
description: ネットワーク接続ウィザード内のカスタム UI ページの表示
ms.assetid: 102f142a-91d1-4b55-a111-15a297c03e23
keywords:
- カスタム UI WDK ネイティブ 802.11 IHV UI 拡張機能の DLL、ネットワーク接続ウィザード
- ネットワーク接続ウィザード WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 449b78226a5b97742a35806fca07839daceb73db
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386559"
---
# <a name="displaying-custom-ui-pages-within-the-network-connection-wizard"></a>ネットワーク接続ウィザード内のカスタム UI ページの表示




 

802.11 IHV UI 拡張機能のネイティブ DLL でサポートされているカスタム ユーザー インターフェイス (UI) は、UI の要求がいずれかで行われたときに、オペレーティング システムのネットワーク接続ウィザード内で表示できます。

-   呼び出し[ **Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_ui_request)、ネイティブの 802.11 IHV 拡張機能の DLL によって行われました。 このプロセスの詳細については、次を参照してください。[カスタム UI の表示を要求する](requesting-the-display-of-a-custom-ui.md)します。

-   ネイティブ 802.11 IHV 拡張 DLL の呼び出し**Dot11ExtQueryUIRequest**オペレーティング システムによって行われた、IHV ハンドラー関数。 このプロセスの詳細については、次を参照してください。[カスタム UI を表示するためのクエリ](querying-for-the-display-of-a-custom-ui.md)します。

オペレーティング システムでは、ワイヤレス ネットワークに接続しようとして、ワイヤレス LAN (WLAN) アダプター場合に、ネットワーク接続ウィザード内でカスタムの UI が表示されます。 このような状況では、カスタム UI の要求が期間内のバルーン通知として表示されます。

-   オペレーティング システム DLL を呼び出すネイティブ 802.11 IHV 拡張機能の後に[ *Dot11ExtIhvPerformPreAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)ワイヤレス ネットワークの関連付け前の操作を開始する IHV ハンドラー関数。

-   ネイティブの 802.11 IHV 拡張 DLL の呼び出しの前に[ **Dot11ExtPostAssociateCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)後関連付け操作を正常に完了します。

ネットワークの接続ウィザード内でカスタム UI 要求を挿入するときに、オペレーティング システムは、次を行います。

1.  DLL を呼び出すネイティブ 802.11 IHV 拡張機能の[ *Dot11ExtIhvIsUIRequestPending* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_is_ui_request_pending) IHV ハンドラー関数 UI 要求がまだがかどうかを判断する保留中です。 オペレーティング システムに渡されるグローバル一意識別子 (GUID) を使用して UI 要求を指定する[ **Dot11ExtSendUIRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_ui_request) 802.11 IHV 拡張機能のネイティブ DLL でします。

2.  場合[ *Dot11ExtIhvIsUIRequestPending* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_is_ui_request_pending)返します**TRUE**オペレーティング システムを要求されたインスタンスの指定した UI 要求**IWizardExtension** COM インターフェイスと、ネットワーク接続ウィザードのフロー、現在の UI にバインドします。 呼び出し時に[ **Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_ui_request)、ネイティブの 802.11 IHV 拡張 DLL のクラス id (CLSID) を指定します、 **IWizardExtension**実装内のネイティブ 802.11 IHV UI 拡張 DLL。

    オペレーティング システムも呼び出して、 **IWizardExtension::AddPages**メソッドを使用する 802.11 IHV UI 拡張機能のネイティブ DLL がカスタム UI ページを表す PROPSHEETPAGE 構造体のハンドルの配列を返します。

    詳細については、 **IWizardExtension** COM インターフェイスを参照してください[IWizardExtension COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56607)します。

3.  を介してネイティブ 802.11 IHV UI 拡張 DLL で制御される UI ページ間を移動、 **IWizardSite** COM インターフェイスです。 このインターフェイスの詳細については、次を参照してください。 [IWizardSite COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56608)します。

802.11 IHV UI 拡張機能のネイティブ DLL の読み取りまたは書き込みをコンテキストに固有のデータ、カスタム UI が表示されている間、 [IPropertyBag COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56610)します。 このプロセスの詳細については、次を参照してください。[へのアクセス プロファイルとコンテキスト データ](accessing-profile-and-context-data.md)します。

802.11 IHV UI 拡張機能のネイティブ DLL が呼び出すことによって、802.11 IHV 拡張機能のネイティブ DLL にユーザーが入力した応答データを返すことができます、カスタム UI が表示されたら、 **WlanSendUIResponse**します。 DLL では、応答データを格納するバッファーへのポインターと同様に、UI 要求の GUID に渡します。

802.11 IHV UI 拡張機能のネイティブ DLL 後**WlanSendUIResponse**、オペレーティング システム DLL を呼び出すネイティブ 802.11 IHV 拡張機能の[ *Dot11ExtIhvProcessUIResponse* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_process_ui_response)カスタム UI の応答データを転送する IHV ハンドラー関数。

詳細については、 **WlanSendUIResponse** API、Microsoft Windows SDK のドキュメントを参照してください。

 

 





