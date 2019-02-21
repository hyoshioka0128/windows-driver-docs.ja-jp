---
title: NDIS VMQ のライブ マイグレーションのサポート
description: NDIS VMQ のライブ マイグレーションのサポート
ms.assetid: 6872594a-35f8-4fbf-b764-22b286fb940c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48e61e6bfa1e72abd3cc25effeee6841e96f1820
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529488"
---
# <a name="ndis-vmq-live-migration-support"></a>NDIS VMQ のライブ マイグレーションのサポート





ライブ マイグレーションをサポートするためには、任意の命令で、または保留中の I/O 境界一時仮想マシン (VM) を停止できます。 つまり、VM では、保留中の受信要求が完了しない可能性があります。 そのため、ネットワークの仮想サービス プロバイダー (VSP) を返しますすべて受信パケットの VM は返されませんでしたを基になるネットワーク アダプターにします。

**注**  で、HYPER-V 子パーティションは、VM でとも呼ばれます。

 

別のホスト、VM が再起動されると、ネットワーク、新しいホスト上の VSP では、再開の VM が返され、それらミニポート ドライバーで新しいで基になるまで渡しませんの受信パケット処理します。 移行が完了したら後、は、VM に関連付けられている受信キューが解放され、別の VM の再利用できます。

**注**  新しいネットワーク アダプターで VMQ がサポートされない可能性があります。

 

NDIS ミニポート ドライバー、VMQ を解放するための要求の受信キューに、次の手順に従います。

1.  ネットワーク アダプターには、キューを DMA 停止状態を入力する必要があります、受信キューに関連付けられている受信バッファーへのデータの DMA 転送が停止します。 ネットワーク アダプターは、受信したときにおそらく DMA アクティビティを停止、 [OID\_受信\_フィルター\_オフ\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569785) OID 要求を受信側の最後のフィルターの設定をクリアするにはキューです。

2.  ミニポート ドライバーが生成されます、 [ **NDIS\_状態\_受信\_キュー\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567417)状態を示す値を**QueueState**のメンバー、 [ **NDIS\_受信\_キュー\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567214)構造体を設定**NdisReceiveQueueOperationalStateDmaStopped** NDIS DMA 転送が停止していることを通知します。

3.  ミニポート ドライバーは、指定された受信パケット、ミニポート ドライバーに返されるキューのすべての待機します。

4.  ミニポート ドライバーのネットワーク アダプターの受信を呼び出して、キューに関連付けられているバッファーが割り当てられているすべての共有メモリを解放する[ **NdisFreeSharedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff562601)します。

5.  ミニポート ドライバーが完了すると、 [OID\_受信\_フィルター\_FREE\_キュー](https://msdn.microsoft.com/library/windows/hardware/ff569789) OID 要求を受信キューを解放します。

キューの状態の詳細については、次を参照してください。 [NDIS VM キュー状態](ndis-virtual-machine-queue-states.md)します。

 

 





