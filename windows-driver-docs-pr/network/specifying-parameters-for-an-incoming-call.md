---
title: 着信呼び出しのパラメーターの指定
description: 着信呼び出しのパラメーターの指定
ms.assetid: f1436c05-f475-454c-b68f-e387821834d4
keywords:
- いる CoNDIS WAN ドライバー WDK、ネットワークの着信呼び出し
- WDK WAN、着信電話サービス
- いる CoNDIS TAPI WDK、ネットワークの着信呼び出し
- 音声の WDK networing、着信通話のストリーミング
- 着信呼び出しの WDK いる CoNDIS WAN
- WDK いる CoNDIS WAN の呼び出し
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32e80d8a27e3860d054c959d18cec9bfaac4f716
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383627"
---
# <a name="specifying-parameters-for-an-incoming-call"></a>着信呼び出しのパラメーターの指定





着信呼び出しを指定する際に**Ndis (M) CmDispatchIncomingCall**、コール マネージャーまたは音声のストリーミングをサポートする MCM で、次の値を指定する必要があります、 [ **CO\_の呼び出し\_MANAGER\_パラメーター** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545381(v=vs.85))構造体。

-   最大転送サイズの SDU (CallMgrParameters-&gt;Transmit.MaxSduSize)

-   最大受信 SDU サイズ (CallMgrParameters-&gt;Receive.MaxSduSize)

さらに、コール マネージャーや、MCM 指定してください、次の値の行で\_呼び出す\_情報構造体。

-   **ulMediaMode**

    このフィールドは LINEMEDIAMODE を含める必要があります\_TAPIMEDIAMODE にマップする、AUTOMATEDVOICE\_TAPI 3.0 でオーディオです。

-   **ulCallerIDFlags**

-   **ulCallerIDSize**

-   **ulCallerIDOffset**

-   **ulCallerIDNameSize**

-   **ulCallerIDNameOffset**

-   **ulCalledIDFlags**

-   **ulCalledIDSize**

-   **ulCalledIDOffset**

-   **ulCalledIDNameSize**

-   **ulCalledDNameOffset**

-   **ulCallerIDAddressType**

-   **ulCalledIDAddressType**

コール マネージャーまたは CO 以外、アドレス ファミリをサポートする MCM\_アドレス\_ファミリ\_TAPI\_プロキシを前の行を指定します\_呼び出す\_情報メンバーに応答する場合、[OID\_CO\_TAPI\_TRANSLATE\_NDIS\_CALLPARAMS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-translate-ndis-callparams)クエリ。

コール マネージャーまたは CO をサポートする、MCM\_アドレス\_ファミリ\_TAPI\_プロキシ ファミリは、上記の行を指定\_呼び出す\_情報メンバーのメディアに固有の部分に、CO\_呼び出す\_MANAGER\_パラメーター構造体を提供する**Ndis (M) CmDispatchIncomingCall**します。

行のメンバーの説明については\_呼び出す\_情報構造体を Microsoft Windows SDK ドキュメントで LINECALLINFO 構造体を参照してください。

 

 





