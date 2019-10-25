---
title: NDIS ミニポートドライバーの割り込みを処理する
description: NIC または別のデバイスが割り込みを生成するときに NDIS ミニポートドライバーが使用する呼び出しについて説明します。
ms.assetid: 75dc3676-f88f-4d86-8c77-02f48083de71
keywords:
- WDK ネットワークの割り込み、処理
- MiniportInterrupt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8eeb72aa046212076e9e92f9762dbf47429aa163
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842616"
---
# <a name="handling-interrupts-for-ndis-miniport-drivers"></a>NDIS ミニポートドライバーの割り込みを処理する





NDIS は、NIC、またはその割り込みを共有する別のデバイスが割り込みを生成するときに、 [*Miniportinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)関数を呼び出します。

基になる NIC で割り込みが生成されなかった場合、 *Miniportinterrupt*は直ちに**FALSE**を返す必要があります。 それ以外の場合は、割り込みを処理した後に**TRUE**を返します。

ミニポートドライバーは、 *Miniportinterrupt*関数でできるだけ少ない作業を行う必要があります。 I/o 操作を[*MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)関数に遅延させる必要があります。 NDIS は、割り込みの遅延処理を完了するために*MiniportInterruptDPC*を呼び出します。

*Miniportinterrupt*が返された後に追加の dpc をキューに追加するために、ミニポートドライバーは、 *Miniportinterrupt*関数の[**targetprocessors**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismqueuedpc)パラメーターのビットを設定します。 *Miniportinterrupt*または*MiniportInterruptDPC*から追加の dpc を要求するには、ミニポートドライバーが**NdisMQueueDpc**関数を呼び出します。

ミニポートドライバーは**NdisMQueueDpc**を呼び出して、他のプロセッサに対する追加の DPC 呼び出しを要求できます。

 

 





