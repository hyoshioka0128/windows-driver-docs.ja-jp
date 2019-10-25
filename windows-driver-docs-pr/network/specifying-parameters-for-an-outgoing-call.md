---
title: 発信呼び出しのパラメーターの指定
description: 発信呼び出しのパラメーターの指定
ms.assetid: 6e11dcd7-33ae-4b9e-8609-1baccec691d5
keywords:
- CoNDIS WAN ドライバー WDK ネットワーク、発信呼び出し
- 電話 services WDK WAN、発信呼び出し
- CoNDIS TAPI WDK ネットワーク、発信呼び出し
- voice streaming WDK netて、発信呼び出し
- 送信呼び出し WDK CoNDIS
- WDK を呼び出す WAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5008ed9100247ddb6e342aa62580765d2a2a12ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841870"
---
# <a name="specifying-parameters-for-an-outgoing-call"></a>発信呼び出しのパラメーターの指定





発信通話を行うときは、音声ストリーミングをサポートする呼び出しマネージャーまたは MCM が、 [ **\_manager\_PARAMETERS 構造体の CO\_呼び出し**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545381(v=vs.85))で次の値を指定する必要があります。

-   最大転送 SDU サイズ (CallMgrParameters-&gt;送信. MaxSduSize)

-   最大受信 SDU サイズ (CallMgrParameters-&gt;Receive. MaxSduSize)

CO\_ADDRESS\_ファミリ以外のアドレスファミリをサポートする呼び出しマネージャーまたは MCM\_TAPI\_プロキシは、OID\_のクエリに応答して、TAPI 呼び出しパラメーターを NDIS 呼び出しパラメーターに変換するときに、これらの値を入力し[@no\_\_TAPI\_CALLPARAMS を変換](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-translate-tapi-callparams)します。

CO\_アドレス\_ファミリ\_TAPI\_プロキシファミリでサポートされている呼び出しマネージャーまたは MCM は、 [**ProtocolCmMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_make_call)のコンテキストでこれらの値を CO\_呼び出し\_MANAGER\_パラメーター構造に書き込みます。プロシージャ. *ProtocolCmMakeCall*関数に渡される sdu の最大サイズが正しくないことに注意してください。 *ProtocolCmMakeCall*関数は、正しい値を使用して誤った値を上書きする必要があります。

 

 





