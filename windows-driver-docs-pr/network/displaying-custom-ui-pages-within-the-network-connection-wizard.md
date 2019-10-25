---
title: ネットワーク接続ウィザード内のカスタム UI ページの表示
description: ネットワーク接続ウィザード内のカスタム UI ページの表示
ms.assetid: 102f142a-91d1-4b55-a111-15a297c03e23
keywords:
- カスタム UI WDK ネイティブ 802.11 IHV UI Extensions DLL、ネットワーク接続ウィザード
- ネットワーク接続ウィザード WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97c9f3e183fdfb1f356625d978b6c787d5e20478
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834826"
---
# <a name="displaying-custom-ui-pages-within-the-network-connection-wizard"></a>ネットワーク接続ウィザード内のカスタム UI ページの表示




 

ネイティブ 802.11 IHV UI 拡張 DLL でサポートされているカスタムユーザーインターフェイス (UI) は、次のいずれかの方法で UI の要求が行われたときに、オペレーティングシステムのネットワーク接続ウィザード内に表示されます。

-   ネイティブ 802.11 IHV Extensions DLL によって作成された[**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)の呼び出し。 このプロセスの詳細については、「[カスタム UI の表示の要求](requesting-the-display-of-a-custom-ui.md)」を参照してください。

-   オペレーティングシステムによって作成された、ネイティブ 802.11 IHV Extensions DLL の**Dot11ExtQueryUIRequest** ihv ハンドラー関数の呼び出し。 このプロセスの詳細については、「[カスタム UI の表示のクエリ](querying-for-the-display-of-a-custom-ui.md)」を参照してください。

ワイヤレス LAN (WLAN) アダプターがワイヤレスネットワークに接続しようとしている場合、オペレーティングシステムは、ネットワーク接続ウィザード内にカスタム UI を表示します。 この場合、カスタム UI の要求は、次の期間内にバルーン通知として表示されます。

-   オペレーティングシステムがネイティブ 802.11 IHV Extensions DLL の[*Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate) ihv ハンドラー関数を呼び出して、ワイヤレスネットワークとの関連付け前の操作を開始した後。

-   ネイティブ 802.11 IHV 拡張 DLL が[**Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)を呼び出してから、関連付け後の操作を正常に完了する前。

ネットワーク接続ウィザードでカスタム UI 要求を挿入すると、オペレーティングシステムは次の処理を実行します。

1.  ネイティブ 802.11 IHV 拡張 DLL の[*Dot11ExtIhvIsUIRequestPending*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_is_ui_request_pending) ihv ハンドラー関数を呼び出して、UI 要求がまだ保留中かどうかを確認します。 オペレーティングシステムは、ネイティブ 802.11 IHV 拡張 DLL によって[**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)に渡されるグローバル一意識別子 (GUID) を使用して、UI 要求を指定します。

2.  指定された UI 要求に対して[*Dot11ExtIhvIsUIRequestPending*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_is_ui_request_pending)が**TRUE**を返した場合、オペレーティングシステムは、要求された**IWizardExtension** COM インターフェイスをインスタンス化し、ネットワーク接続ウィザードの現在の UI フローにバインドします。 [**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)を呼び出すと、802.11 ネイティブ 802.11 Ihv UI 拡張 dll 内で**IWizardExtension**実装のクラス識別子 (CLSID) が指定されます。

    また、オペレーティングシステムは**IWizardExtension:: AddPages**メソッドも呼び出します。このメソッドは、ネイティブ 802.11 IHV UI 拡張 DLL が、カスタム UI ページを表す propsheet ページ構造体のハンドルの配列を返します。

    **IWizardExtension** com インターフェイスの詳細については、「 [IWizardExtension com インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56607)」を参照してください。

3.  **Iwizardsite** COM インターフェイスを使用して、ネイティブ 802.11 IHV UI 拡張 DLL によって制御される ui ページを移動します。 このインターフェイスの詳細については、「 [Iwizardsite COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56608)」を参照してください。

カスタム UI が表示されている間、ネイティブ 802.11 IHV UI 拡張 DLL は[IPROPERTYBAG COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56610)を使用して、コンテキスト固有のデータを読み書きできます。 このプロセスの詳細については、「[プロファイルとコンテキストデータへのアクセス](accessing-profile-and-context-data.md)」を参照してください。

カスタム UI が表示された後、ネイティブ 802.11 IHV UI 拡張 DLL は、 **WlanSendUIResponse**を呼び出すことによって、ユーザーが入力した応答データをネイティブ 802.11 IHV 拡張 dll に返すことができます。 DLL は、UI 要求の GUID と、応答データを格納しているバッファーへのポインターを渡します。

ネイティブ 802.11 IHV UI 拡張 DLL が**WlanSendUIResponse**を呼び出すと、オペレーティングシステムはネイティブ 802.11 IHV Extension Dll の[*Dot11ExtIhvProcessUIResponse*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_process_ui_response) ihv ハンドラ関数を呼び出して、カスタム UI の応答データを転送します。

**WlanSendUIResponse** API の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

 





