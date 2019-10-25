---
title: カスタム UI の表示の要求
description: カスタム UI の表示の要求
ms.assetid: 4b7366d9-e55a-4b24-b75f-a5f133b80ca7
keywords:
- カスタム UI WDK ネイティブ 802.11 IHV UI 拡張 DLL、要求 (表示を)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a114e9b14d67c642506b1b9270da34e1039db49d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842032"
---
# <a name="requesting-the-display-of-a-custom-ui"></a>カスタム UI の表示の要求




 

ネイティブ 802.11 IHV 拡張 DLL では、ネイティブ 802.11 IHV UI 拡張 DLL を使用してカスタムユーザーインターフェイス (UI) の表示を要求できます。 たとえば、IHV 拡張 DLL は、次のようにカスタム UI を表示するように要求できます。

-   ワイヤレス LAN (WLAN) の関連付け操作中にさまざまな段階でエンドユーザーに通知します。

-   Wlan アダプターが WLAN ネットワークとの関連付けが解除されたときに、エンドユーザーに通知します。

-   エンドユーザーに、認証の結果を WLAN ネットワークに通知します。

カスタム UI を起動するか、通知を表示するには、ネイティブ 802.11 IHV 拡張 DLL が[**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)を呼び出し、 [**DOT11EXT\_ihv\_UI\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request)構造へのポインターを*pihvuirequest*を介して渡します。この関数のパラメーター。

ネイティブ 802.11 IHV 拡張 DLL では、 [**DOT11EXT\_IHV\_UI\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request)構造を使用して、次のデータを使用してカスタム UI を指定します。

-   ユーザーセッション識別子 (ID)。特定のユーザーコンテキストを識別するために使用されます。

-   特定の UI 要求を識別するグローバル一意識別子 (GUID)。

-   ネイティブ 802.11 IHV UI 拡張 DLL 内に実装されている**IWizardExtension** COM インターフェイスのクラス ID (CLSID)。 CLSID は、DLL によってサポートされる特定のカスタム UI を要求するために使用されます。

    **IWizardExtension** com インターフェイスの詳細については、「 [IWizardExtension com インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56607)」を参照してください。

-   独立系ハードウェアベンダー (IHV) によって定義され、指定された**IWizardExtension** COM インターフェイスによって処理される専用の形式のデータを格納するバッファー。 たとえば、バッファーには、カスタム UI 内に表示される既定値を含めることができます。

ユーザーセッション ID の WLAN 接続状態に応じて、カスタム UI 要求は次のいずれかとして表示されます。

-   アダプターが WLAN ネットワークに接続されている場合は、クリック可能なバルーン通知によって起動されるスタンドアロン UI として要求が表示されます。 このプロセスの詳細については、「[バルーン通知の表示](displaying-custom-ui-pages-within-a-balloon-notification.md)」を参照してください。

-   アダプターが WLAN ネットワークに接続している場合、要求は標準のネットワーク接続 UI 内の一連のウィザードページとして表示されます。 このプロセスの詳細については、「[ネットワーク接続ウィザードでカスタム UI ページを表示する](displaying-custom-ui-pages-within-the-network-connection-wizard.md)」を参照してください。

 

 





