---
title: カスタム UI の表示の要求
description: カスタム UI の表示の要求
ms.assetid: 4b7366d9-e55a-4b24-b75f-a5f133b80ca7
keywords:
- カスタム UI WDK ネイティブ 802.11 IHV UI 拡張機能の DLL、表示を要求します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4a14426a8874e8630f128976d364b59ddf1d933
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349392"
---
# <a name="requesting-the-display-of-a-custom-ui"></a>カスタム UI の表示の要求




 

ネイティブの 802.11 IHV 拡張 DLL は、802.11 IHV UI 拡張機能のネイティブ DLL でのカスタム ユーザー インターフェイス (UI) の表示を要求できます。 たとえば、IHV 拡張機能の DLL にカスタム UI が表示されることを要求する可能性があります。

-   ワイヤレス LAN (WLAN) の関連付け操作中にさまざまな段階で、エンドユーザーに通知します。

-   エンドユーザーは、WLAN アダプターが WLAN のネットワークの関連付けを解除するときに通知します。

-   WLAN ネットワークへの認証の結果をエンドユーザーに通知します。

カスタム UI を起動またはネイティブの 802.11 IHV 拡張 DLL の呼び出し、通知を表示する[ **Dot11ExtSendUIRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff547567)へのポインターを渡すと、 [ **DOT11EXT\_IHV\_UI\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff547637)を通じて構造体、 *pIhvUIRequest*この関数のパラメーター。

を通じて、 [ **DOT11EXT\_IHV\_UI\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff547637)構造、802.11 IHV 拡張機能のネイティブ DLL を次のデータをカスタム UI を指定します。

-   ユーザー セッション識別子 (ID)、特定のユーザー コンテキストを識別するために使用されます。

-   グローバル一意識別 ID (GUID)、UI の特定の要求を識別します。

-   クラス ID (CLSID) **IWizardExtension** 802.11 IHV UI 拡張機能のネイティブ DLL に実装されている COM インターフェイスです。 CLSID は、DLL でサポートされている特定のカスタム UI を要求に使用されます。

    詳細については、 **IWizardExtension** COM インターフェイスを参照してください[IWizardExtension COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56607)します。

-   独立系ハードウェア ベンダー (IHV) によって定義され、指定した処理されている独自の形式でデータを格納するバッファー **IWizardExtension** COM インターフェイスです。 たとえば、バッファーには、カスタム UI 内で表示される既定値が含まれます。

ユーザーのセッション ID の WLAN 接続状態に応じて、カスタム UI 要求が、次のいずれかとして表示されます。

-   場合は、アダプターは、WLAN のネットワークに接続されているが、要求がクリック可能なバルーン通知を通じて UI が起動されるスタンドアロンとして表示されます。 このプロセスの詳細については、次を参照してください。[バルーン通知を表示する](displaying-custom-ui-pages-within-a-balloon-notification.md)します。

-   アダプターが WLAN ネットワークへの接続中にある場合は、要求が標準のネットワーク接続 UI 内のウィザード ページのセットとして表示されます。 このプロセスの詳細については、次を参照してください。[内、ネットワーク接続ウィザードでカスタム UI ページを表示する](displaying-custom-ui-pages-within-the-network-connection-wizard.md)します。

 

 





