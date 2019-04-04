---
title: カスタム UI を表示するためのクエリ
description: カスタム UI を表示するためのクエリ
ms.assetid: 89f39281-db97-4cbe-8753-43ab30d840c8
keywords:
- カスタム UI WDK ネイティブ 802.11 IHV UI 拡張機能の DLL、クエリを実行します。
- カスタムの UI 画面のクエリを実行します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f359fb087120412a9bbdd99fc6ed99cfb39d51b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550108"
---
# <a name="querying-for-the-display-of-a-custom-ui"></a>カスタム UI を表示するためのクエリ




 

オペレーティング システムでは、DLL に表示するカスタム UI があるかどうかを判断するネイティブの 802.11 IHV 拡張機能の DLL を照会できます。 ワイヤレス LAN (WLAN) アダプターが WLAN のネットワーク接続プロセス内で次のフェーズのいずれかに移行するたびに、オペレーティング システムは、DLL を照会します。

<a href="" id="pre-association-------"></a>**前の関連付け**   
IHV 拡張 DLL の前に、接続フェーズでは、関連付け前の操作を開始します。 前の関連付け操作の詳細については、[関連付け前操作](pre-association-operations.md)を参照してください。

<a href="" id="post-association-------"></a>**後の関連付け**   
IHV 拡張 DLL の後に、接続フェーズでは、後の関連付け操作を完了します。 詳細については、後の関連付け操作は、[後関連付け操作](post-association-operations.md)を参照してください。

オペレーティング システム DLL を呼び出すネイティブ 802.11 IHV 拡張機能の[ *Dot11ExtIhvQueryUIRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff547507) IHV ハンドラーは、カスタム UI を表示できるかどうかをクエリする関数。 オペレーティング システムが使用して、接続プロセスの現在のフェーズを通過、 *connectionPhase*パラメーター。 かどうかには、カスタムの UI を表示する必要があります、DLL を返します、 [ **DOT11EXT\_IHV\_UI\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff547637) p 構造*pIhvUIRequest*パラメーター。

を通じて、 [ **DOT11EXT\_IHV\_UI\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff547637)構造、802.11 IHV 拡張機能のネイティブ DLL を次のデータをカスタム UI を指定します。

-   ユーザー セッション識別子 (ID)、特定のユーザー コンテキストを識別するために使用されます。

-   グローバル一意識別 ID (GUID)、UI の特定の要求を識別します。

-   クラス ID (CLSID) **IWizardExtension** 802.11 IHV UI 拡張機能のネイティブ DLL に実装される COM インターフェイスです。 CLSID は、DLL でサポートされている特定のカスタム UI を要求に使用されます。

    詳細については、 **IWizardExtension** COM インターフェイスを参照してください[IWizardExtension COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56607)します。

-   独立系ハードウェア ベンダー (IHV) によって定義され、指定した処理されている独自の形式でデータを格納しているバッファー **IWizardExtension** COM インターフェイスです。 たとえば、バッファーには、カスタム UI 内で表示される既定値が含まれます。

カスタムの UI が標準のネットワーク接続 UI 内のウィザード ページのセットとして表示されます。 このプロセスの詳細については、[内、ネットワーク接続ウィザードでカスタム UI ページを表示する](displaying-custom-ui-pages-within-the-network-connection-wizard.md)を参照してください。

 

 





