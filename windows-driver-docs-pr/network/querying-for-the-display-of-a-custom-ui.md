---
title: カスタム UI の表示のクエリ
description: カスタム UI の表示のクエリ
ms.assetid: 89f39281-db97-4cbe-8753-43ab30d840c8
keywords:
- カスタム UI WDK ネイティブ 802.11 IHV UI 拡張機能の DLL、クエリを実行します。
- カスタムの UI 画面のクエリを実行します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50e7a1dfdf975e1b3ea54b48ac87c2fc7f336d8a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385433"
---
# <a name="querying-for-the-display-of-a-custom-ui"></a>カスタム UI の表示のクエリ




 

オペレーティング システムでは、DLL に表示するカスタム UI があるかどうかを判断するネイティブの 802.11 IHV 拡張機能の DLL を照会できます。 ワイヤレス LAN (WLAN) アダプターが WLAN のネットワーク接続プロセス内で次のフェーズのいずれかに移行するたびに、オペレーティング システムは、DLL を照会します。

<a href="" id="pre-association-------"></a>**前の関連付け**   
IHV 拡張 DLL の前に、接続フェーズでは、関連付け前の操作を開始します。 前の関連付け操作の詳細については、次を参照してください。[関連付け前操作](pre-association-operations.md)します。

<a href="" id="post-association-------"></a>**後の関連付け**   
IHV 拡張 DLL の後に、接続フェーズでは、後の関連付け操作を完了します。 詳細については、後の関連付け操作は、次を参照してください。[後関連付け操作](post-association-operations.md)します。

オペレーティング システム DLL を呼び出すネイティブ 802.11 IHV 拡張機能の[ *Dot11ExtIhvQueryUIRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_query_ui_request) IHV ハンドラーは、カスタム UI を表示できるかどうかをクエリする関数。 オペレーティング システムが使用して、接続プロセスの現在のフェーズを通過、 *connectionPhase*パラメーター。 かどうかには、カスタムの UI を表示する必要があります、DLL を返します、 [ **DOT11EXT\_IHV\_UI\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request) p 構造*pIhvUIRequest*パラメーター。

を通じて、 [ **DOT11EXT\_IHV\_UI\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request)構造、802.11 IHV 拡張機能のネイティブ DLL を次のデータをカスタム UI を指定します。

-   ユーザー セッション識別子 (ID)、特定のユーザー コンテキストを識別するために使用されます。

-   グローバル一意識別 ID (GUID)、UI の特定の要求を識別します。

-   クラス ID (CLSID) **IWizardExtension** 802.11 IHV UI 拡張機能のネイティブ DLL に実装される COM インターフェイスです。 CLSID は、DLL でサポートされている特定のカスタム UI を要求に使用されます。

    詳細については、 **IWizardExtension** COM インターフェイスを参照してください[IWizardExtension COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56607)します。

-   独立系ハードウェア ベンダー (IHV) によって定義され、指定した処理されている独自の形式でデータを格納しているバッファー **IWizardExtension** COM インターフェイスです。 たとえば、バッファーには、カスタム UI 内で表示される既定値が含まれます。

カスタムの UI が標準のネットワーク接続 UI 内のウィザード ページのセットとして表示されます。 このプロセスの詳細については、次を参照してください。[内、ネットワーク接続ウィザードでカスタム UI ページを表示する](displaying-custom-ui-pages-within-the-network-connection-wizard.md)します。

 

 





