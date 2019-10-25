---
title: 中間ドライバー リセット操作
description: 中間ドライバー リセット操作
ms.assetid: 473dce77-4636-40da-ac38-cda1676eba3f
keywords:
- 中間ドライバー WDK ネットワーク、リセット操作
- NDIS 中間ドライバー WDK、リセット操作
- 中間ドライバーのリセット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7bb893e24577f879b3f2e1a62fc84cc7d6b119b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844179"
---
# <a name="intermediate-driver-reset-operations"></a>中間ドライバー リセット操作





基になる NIC がリセットされるため、基になるドライバーへのバインドに対する未処理の送信が削除される状況を処理するために、中間ドライバーを準備する必要があります。

基になるドライバーは通常、NIC をリセットします。これは、NDIS がキューに置かれた送信または NIC にバインドされた要求をタイムアウトしたときにミニポートドライバーの[*Miniportresetex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)関数を呼び出します。 基になる NIC がリセットされた場合、NDIS は、バインドされた各プロトコルの[**protocolstatusex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex)(または[**protocolcostatusex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_status_ex)) 関数を呼び出します。また、ndis\_status の状態を持つ中間ドライバーを呼び出し\_開始\_リセットします。 ミニポートドライバーがリセットを完了すると、NDIS は*Protocolstatusex*(または*protocolcostatusex*) を再度呼び出して、ndis\_STATUS の状態\_リセット\_終了します。

NIC がリセットされると、バインドされた中間ドライバーに、その NIC に保留中の送信ネットワークデータがある場合は、NDIS によってそれらのネットワークデータが適切な状態で中間ドライバーに戻されます。 リセットが完了すると、中間ドライバーはこれらのネットワークデータを再送信する必要があります。

中間ドライバーが NDIS\_STATUS の状態を受信し\_リセット\_開始すると、次のようになります。

-   *Protocolstatusex*または*PROTOCOLCOSTATUSEX*が NDIS\_の状態を受信するまで、送信可能なネットワークデータを保持し\_終了通知をリセット\_ます。

-   *Protocolstatusex*(または*protocolcostatusex*) が NDIS\_の状態を受信してから、\_の終了通知\_リセットするまで、受信したすべてのネットワークデータを次の上位のドライバーに対して保持します。

-   進行中の操作と NIC の状態について、保持している内部状態をクリーンアップします。

*Protocolstatusex*(または*protocolcostatusex*) が NDIS\_STATUS を受信し\_\_をリセットした後、中間ドライバーはネットワークデータの送信を再開し、要求を行い、上位レベルのドライバーを示すことができます。

中間ドライバーには、 [*Miniportresetex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)関数が用意されていません。

 

 





