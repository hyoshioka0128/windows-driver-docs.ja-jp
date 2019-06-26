---
title: バルーン通知内のカスタム UI ページの表示
description: バルーン通知内のカスタム UI ページの表示
ms.assetid: 5ed2ba59-88ae-4379-b729-1d741b30a7a0
keywords:
- カスタム UI WDK ネイティブ 802.11 IHV UI 拡張機能の DLL、バルーン通知
- バルーン通知 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 208e131c18a2a59d7cdcf2c4e2d3e3778ebff1ce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386563"
---
# <a name="displaying-custom-ui-pages-within-a-balloon-notification"></a>バルーン通知内のカスタム UI ページの表示




 

ネイティブの 802.11 IHV 拡張 DLL を呼び出す場合[ **Dot11ExtSendUIRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_ui_request)カスタム ユーザー インターフェイス (UI) を表示するには、オペレーティング システム UI が表示されます、クリック可能なバルーン通知による場合、ワイヤレス LAN (WLAN) アダプターが、ワイヤレス ネットワークに接続します。 このような状況では、カスタム UI の要求はバルーン通知として表示されます。

-   ネイティブの 802.11 IHV 拡張 DLL の後に呼び出す[ **Dot11ExtPostAssociateCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)後関連付け操作を正常に完了します。

-   オペレーティング システムの呼び出し、DLL の前に[ *Dot11ExtIhvAdapterReset* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_adapter_reset) WLAN 接続をリセットする IHV ハンドラー関数。

ネイティブの 802.11 IHV 拡張 DLL がカスタム UI の表示を要求する方法の詳細については、次を参照してください。[カスタム UI の表示を要求する](requesting-the-display-of-a-custom-ui.md)します。

バルーン通知としてカスタム UI 要求を処理するときにオペレーティング システムは、次のこと。

1.  DLL を呼び出すネイティブ 802.11 IHV 拡張機能の[ *Dot11ExtIhvIsUIRequestPending* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_is_ui_request_pending) IHV ハンドラー関数 UI 要求がまだがかどうかを判断する保留中です。 オペレーティング システムに渡されるグローバル一意識別子 (GUID) を使用して UI 要求を指定する[ **Dot11ExtSendUIRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_ui_request) 802.11 IHV 拡張機能のネイティブ DLL でします。

2.  場合[ *Dot11ExtIhvIsUIRequestPending* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_is_ui_request_pending)返します**TRUE** UI の指定された要求のオペレーティング システムは DLL を呼び出すネイティブ 802.11 IHV UI 拡張機能の[**IDot11ExtUI::GetDot11ExtUIBalloonText** ](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff553771(v=vs.85))メソッド。 このメソッドは、DLL は、バルーン通知内に表示するローカライズされたテキストを格納する文字列バッファーを返します。

3.  ローカライズされたテキストが含まれたバルーン通知が表示されます。

4.  オペレーティング システムがサポートされているカスタム UI を起動する場合は、エンドユーザーには、バルーン通知がクリックすると、によって、要求された**IWizardExtension** COM インターフェイスです。 呼び出し時に[ **Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_ui_request)、ネイティブの 802.11 IHV 拡張 DLL のクラス id (CLSID) を指定します、 **IWizardExtension**実装内のネイティブ 802.11 IHV UI 拡張 DLL。

    オペレーティング システムを呼び出すと、 **IWizardExtension::AddPages**メソッド、802.11 IHV UI 拡張機能のネイティブ DLL は、カスタム UI ページを表す PROPSHEETPAGE 構造体のハンドルの配列を返します。

    詳細については、 **IWizardExtension** COM インターフェイスを参照してください[IWizardExtension COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56607)します。 PROPSHEETPAGE 構造の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

5.  を介してネイティブ 802.11 IHV UI 拡張 DLL で指定した UI のページ間を移動**IWizardSite** COM インターフェイスです。 このインターフェイスの詳細については、次を参照してください。 [IWizardSite COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56608)します。

802.11 IHV UI 拡張機能のネイティブ DLL の読み取りまたは書き込みをコンテキストに固有のデータ、カスタム UI が表示されている間、 [IPropertyBag COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56610)します。 このプロセスの詳細については、次を参照してください。[へのアクセス プロファイルとコンテキスト データ](accessing-profile-and-context-data.md)します。 802.11 IHV UI 拡張機能のネイティブ DLL が呼び出すことによって、802.11 IHV 拡張機能のネイティブ DLL にユーザーが入力した応答データを返すことができます、カスタム UI の表示が完了すると、 **WlanSendUIResponse**します。 DLL は、応答データが含まれているバッファーへのポインターと同様に、UI 要求の GUID で渡します。

802.11 IHV UI 拡張機能のネイティブ DLLcalls 後**WlanSendUIResponse**、オペレーティング システムは DLL を呼び出すネイティブ 802.11 IHV 拡張機能の[ *Dot11ExtIhvProcessUIResponse* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_process_ui_response)カスタム UI の応答データを転送する IHV ハンドラー関数。

詳細については、 **WlanSendUIResponse** API、Windows SDK のドキュメントを参照してください。

 

 





