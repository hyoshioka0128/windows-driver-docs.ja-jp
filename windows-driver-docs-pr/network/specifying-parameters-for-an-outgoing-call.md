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
ms.openlocfilehash: a9c9241270952e78641b56526fe967350695b8cd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388123"
---
# <a name="specifying-parameters-for-an-outgoing-call"></a>発信呼び出しのパラメーターの指定





発信通話をコール マネージャーまたは音声のストリーミングをサポートする MCM を実行してでは、次の値を指定する必要があるときに、 [ **CO\_呼び出す\_MANAGER\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff545381)構造体。

-   最大転送サイズの SDU (CallMgrParameters-&gt;Transmit.MaxSduSize)

-   最大受信 SDU サイズ (CallMgrParameters-&gt;Receive.MaxSduSize)

コール マネージャーまたは CO 以外、アドレス ファミリをサポートする MCM\_アドレス\_ファミリ\_TAPI\_NDIS 変換 TAPI 呼び出しのパラメーターのクエリに対する応答のパラメーターを呼び出すときにプロキシをこれらの値に設定[OID\_CO\_TAPI\_TRANSLATE\_TAPI\_CALLPARAMS](https://msdn.microsoft.com/library/windows/hardware/ff569100)します。

コール マネージャーまたは CO をサポートする MCM\_アドレス\_ファミリ\_TAPI\_プロキシ ファミリでは、これらの値を CO に書き込みます\_呼び出す\_MANAGER\_パラメーター構造体、コンテキストの[ **ProtocolCmMakeCall** ](https://msdn.microsoft.com/library/windows/hardware/ff570246)関数。 渡される SDU の最大サイズに注意してください、 *ProtocolCmMakeCall*関数が正しくありません。 *ProtocolCmMakeCall*関数は、正しい値に不適切な値を上書きする必要があります。

 

 





