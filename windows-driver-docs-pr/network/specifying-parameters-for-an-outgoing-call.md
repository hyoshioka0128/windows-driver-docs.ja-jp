---
title: 発信呼び出しのパラメーターの指定
description: 発信呼び出しのパラメーターの指定
ms.assetid: 6e11dcd7-33ae-4b9e-8609-1baccec691d5
keywords:
- 発信呼び出しいる CoNDIS WAN のドライバー WDK ネットワーク
- 発信呼び出し WDK WAN、電話サービス
- いる CoNDIS TAPI WDK ネットワー キング、発信呼び出し
- 音声の WDK networing、発信呼び出しをストリーミングします。
- WDK いる CoNDIS WAN の呼び出しを送信
- WDK いる CoNDIS WAN の呼び出し
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18128c857ec0d5837d054385692141edf0da662f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383625"
---
# <a name="specifying-parameters-for-an-outgoing-call"></a>発信呼び出しのパラメーターの指定





発信通話をコール マネージャーまたは音声のストリーミングをサポートする MCM を実行してでは、次の値を指定する必要があるときに、 [ **CO\_呼び出す\_MANAGER\_パラメーター** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545381(v=vs.85))構造体。

-   最大転送サイズの SDU (CallMgrParameters-&gt;Transmit.MaxSduSize)

-   最大受信 SDU サイズ (CallMgrParameters-&gt;Receive.MaxSduSize)

コール マネージャーまたは CO 以外、アドレス ファミリをサポートする MCM\_アドレス\_ファミリ\_TAPI\_NDIS 変換 TAPI 呼び出しのパラメーターのクエリに対する応答のパラメーターを呼び出すときにプロキシをこれらの値に設定[OID\_CO\_TAPI\_TRANSLATE\_TAPI\_CALLPARAMS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-translate-tapi-callparams)します。

コール マネージャーまたは CO をサポートする MCM\_アドレス\_ファミリ\_TAPI\_プロキシ ファミリでは、これらの値を CO に書き込みます\_呼び出す\_MANAGER\_パラメーター構造体、コンテキストの[ **ProtocolCmMakeCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cm_make_call)関数。 渡される SDU の最大サイズに注意してください、 *ProtocolCmMakeCall*関数が正しくありません。 *ProtocolCmMakeCall*関数は、正しい値に不適切な値を上書きする必要があります。

 

 





