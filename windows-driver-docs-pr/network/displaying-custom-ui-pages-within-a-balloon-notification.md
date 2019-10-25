---
title: バルーン通知内のカスタム UI ページの表示
description: バルーン通知内のカスタム UI ページの表示
ms.assetid: 5ed2ba59-88ae-4379-b729-1d741b30a7a0
keywords:
- カスタム UI WDK ネイティブ 802.11 IHV UI 拡張 DLL、バルーン通知
- バルーン通知 (WDK)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 803ccebf89d0561505336b8bc7aee294923d7a2f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838136"
---
# <a name="displaying-custom-ui-pages-within-a-balloon-notification"></a>バルーン通知内のカスタム UI ページの表示




 

ネイティブ 802.11 IHV 拡張 DLL が[**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)を呼び出してカスタムユーザーインターフェイス (UI) を表示する場合、ワイヤレス LAN (WLAN) アダプターがワイヤレスに接続している場合、オペレーティングシステムはクリック可能なバルーン通知を使用して ui を表示します。ネットワーク. この状況では、カスタム UI の要求がバルーン通知として表示されます。

-   ネイティブ 802.11 IHV 拡張 DLL が[**Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)を呼び出して、関連付け後の操作を正常に完了します。

-   オペレーティングシステムが、WLAN 接続をリセットするために DLL の[*Dot11ExtIhvAdapterReset*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset) IHV ハンドラー関数を呼び出す前。

ネイティブ 802.11 IHV 拡張 DLL がカスタム UI の表示を要求する方法の詳細については、「[カスタム ui の表示](requesting-the-display-of-a-custom-ui.md)の要求」を参照してください。

カスタム UI 要求をバルーン通知として処理する場合、オペレーティングシステムは次の処理を実行します。

1.  ネイティブ 802.11 IHV 拡張 DLL の[*Dot11ExtIhvIsUIRequestPending*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_is_ui_request_pending) ihv ハンドラー関数を呼び出して、UI 要求がまだ保留中かどうかを確認します。 オペレーティングシステムは、ネイティブ 802.11 IHV 拡張 DLL によって[**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)に渡されるグローバル一意識別子 (GUID) を使用して、UI 要求を指定します。

2.  指定された UI 要求に対して[*Dot11ExtIhvIsUIRequestPending*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_is_ui_request_pending)が**TRUE**を返した場合、オペレーティングシステムはネイティブ 802.11 IHV UI 拡張 DLL の[**IDot11ExtUI:: GetDot11ExtUIBalloonText**](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff553771(v=vs.85))メソッドを呼び出します。 このメソッドを使用すると、DLL は、バルーン通知内に表示されるローカライズされたテキストを含む文字列バッファーを返します。

3.  ローカライズされたテキストを含むバルーン通知を表示します。

4.  エンドユーザーがバルーン通知をクリックすると、オペレーティングシステムは、要求された**IWizardExtension** COM インターフェイスでサポートされているカスタム UI を起動します。 [**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)を呼び出すと、802.11 ネイティブ 802.11 Ihv UI 拡張 dll 内で**IWizardExtension**実装のクラス識別子 (CLSID) が指定されます。

    オペレーティングシステムが**IWizardExtension:: AddPages**メソッドを呼び出すと、ネイティブ 802.11 IHV UI 拡張 DLL は、カスタム UI ページを表す propsheet ページ構造体のハンドルの配列を返します。

    **IWizardExtension** com インターフェイスの詳細については、「 [IWizardExtension com インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56607)」を参照してください。 PROPSHEET のページ構造の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

5.  **Iwizardsite** COM インターフェイスを使用して、ネイティブ 802.11 IHV UI 拡張 DLL によって指定された ui ページを移動します。 このインターフェイスの詳細については、「 [Iwizardsite COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56608)」を参照してください。

カスタム UI が表示されている間、ネイティブ 802.11 IHV UI 拡張 DLL は[IPROPERTYBAG COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56610)を使用して、コンテキスト固有のデータを読み書きできます。 このプロセスの詳細については、「[プロファイルとコンテキストデータへのアクセス](accessing-profile-and-context-data.md)」を参照してください。 カスタム UI の表示が完了すると、ネイティブ 802.11 IHV UI 拡張 DLL は、 **WlanSendUIResponse**を呼び出すことによって、ユーザーが入力した応答データをネイティブ 802.11 IHV 拡張 dll に返すことができます。 DLL は、UI 要求の GUID と、応答データを格納するバッファーへのポインターを渡します。

ネイティブ 802.11 IHV UI 拡張機能 DLLcalls **WlanSendUIResponse**を呼び出すと、オペレーティングシステムはネイティブ 802.11 IHV 拡張 DLL の[*Dot11ExtIhvProcessUIResponse*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_process_ui_response) ihv ハンドラー関数を呼び出して、カスタム UI の応答データを転送します。

**WlanSendUIResponse** API の詳細については、Windows SDK のドキュメントを参照してください。

 

 





