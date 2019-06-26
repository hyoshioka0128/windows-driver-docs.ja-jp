---
title: プロトコル ドライバー リセット操作
description: プロトコル ドライバー リセット操作
ms.assetid: 862029e5-8c46-4889-80f5-15c463f228a3
keywords:
- プロトコル ドライバー WDK ネットワー キング、リセットの操作
- NDIS は、ドライバー WDK のプロトコル、リセット操作
- リセット操作の WDK NDIS プロトコル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1831e8b8c15033e75b092b686b2a5664d6f230a5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385449"
---
# <a name="protocol-driver-reset-operations"></a>プロトコル ドライバー リセット操作





プロトコル ドライバーには、NDIS 6.0 とそれ以降のバージョンのリセット操作を開始できません。

通常、基になるミニポート ドライバーは、NIC が送信または要求の操作中にタイムアウトしているために、NIC をリセットします。 この条件は、NDIS ミニポート ドライバーの呼び出す[ *MiniportCheckForHangEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_check_for_hang)後[ *MiniportResetEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)関数。 または、ミニポート ドライバーでは、NIC の受信の機能が決定されますが、機能しなくなります。

NDIS によってリセットが開始された場合と*MiniportResetEx*返します NDIS\_状態\_保留中、NDIS 呼び出し、 [ **ProtocolStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_status_ex)(または[**ProtocolCoStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_status_ex)) NDIS の状態での各バインド プロトコル ドライバー関数\_状態\_リセット\_を開始します。 ミニポート ドライバーを呼び出すと[ **NdisMResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismresetcomplete)、NDIS をもう一度呼び出す*ProtocolStatusEx*(または*ProtocolCoStatusEx*) で、NDIS のステータス\_状態\_リセット\_終了します。

プロトコル ドライバーには、未処理を送信する、基になるバインディングの NIC がリセットされるため、NIC をキャンセルできる可能性を処理する必要があります。 バインドされているプロトコル ドライバーに保留中のすべての送信要求がある場合は、NDIS は適切な状態で完了プロトコル ドライバーに送信を示します。 プロトコル ドライバーには、リセット操作が完了したら、NIC が再び動作可能になりますと仮定すると、送信要求を再送信する必要があります。

プロトコル ドライバーが NDIS の状態を受信すると\_状態\_リセット\_必要があります、開始。

-   まで送信可能である、ネットワーク データを保持*プロトコル (Co) の状態*受信、NDIS\_状態\_リセット\_終了の通知。

-   転送される任意の NDIS 呼び出しを行うことでネットワーク データを返すなどのリソースを返すへの呼び出しを除く、基になるミニポート ドライバーに[ **NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreturnnetbufferlists)します。

後*ProtocolStatusEx*(または*ProtocolCoStatusEx*)、NDIS を受け取る\_状態\_リセット\_エンドのメッセージ プロトコル ドライバーに送信を再開できますネットワークデータと OID を要求します。

 

 





