---
title: リセット
description: リセット
ms.assetid: 5f37eca3-08b6-4bac-9d02-8a8ebd8c1904
keywords:
- 接続指向の NDIS WDK で、Nic をリセットします。
- いる CoNDIS WDK ネットワーク、Nic をリセットします。
- ネットワークの NIC の WDK をリセットします。
- WDK の Nic をリセットするネットワークを
- ネットワーク インターフェイス カードの WDK ネットワー キング、リセット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0eae45af00de256eda41a1984cf195b0bee2cb0b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379200"
---
# <a name="reset"></a>リセット





ミニポート ドライバーのまたは MCM ドライバーの NDIS を呼び出すことができます[ *MiniportResetEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset) NIC をリセットする機能

**注**  active であり、リセットする前に有効である AF、SAP、および VC のハンドルは、リセット後にアクティブで有効です。

 

次の図は、ミニポート ドライバーにリセット要求を発行したクライアントを示します。

![ミニポート ドライバーにリセット要求を発行したクライアントを示す図](images/cm-27.png)

次の図は、MCM のドライバーへのリセット要求を発行したクライアントを示します。

![mcm ドライバーへのリセット要求を発行したクライアントを示す図](images/fig1-26.png)

NDIS がプロトコルを呼び出すことによってバインドされている各プロトコルを通知する、基になる接続指向のドライバーでは、NIC をリセットは、するときに[ **ProtocolCoStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_status_ex) NDIS で関数を\_の状態\_リセット\_を開始します。

NDIS は受け入れませんプロトコルによる送信し、ミニポート ドライバーまたは MCM ドライバーへの要求中、ミニポート ドライバーのまたは MCM ドライバーの NIC をリセットしています。 リセットは、進行中は、プロトコルのドライバーをミニポート ドライバーにパケットを送信する必要がありますしない[ **NdisCoSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscosendnetbufferlists) ミニポートドライバーの情報を要求または[ **NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)します。

*MiniportResetEx* NIC をリセットするために必要なすべてのデバイスに依存するアクションを実行します。 *MiniportResetEx*同期的に完了できるかを呼び出して非同期的に実行できます[ **NdisMResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismresetcomplete):

-   NDIS が各バインドのプロトコルを呼び出し、リセットが同期的に完了すると、 *ProtocolCoStatusEx* NDIS で関数を\_状態\_リセット\_終了します。

-   NDIS が各バインドのプロトコルを呼び出し、リセットが非同期的に完了すると、 *ProtocolCoStatusEx* NDIS で関数を\_状態\_リセット\_終了します。

 

 





