---
title: NDIS ミニポート ドライバーの割り込みを処理
description: NDIS ミニポート ドライバーと NIC を使用すること、または別のデバイスには、割り込みが生成されます呼び出しについて説明します
ms.assetid: 75dc3676-f88f-4d86-8c77-02f48083de71
keywords:
- WDK ネットワーク、処理を中断します。
- MiniportInterrupt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0dc90a92505324ac6800c8ed3a7186153667f45
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379824"
---
# <a name="handling-interrupts-for-ndis-miniport-drivers"></a>NDIS ミニポート ドライバーの割り込みを処理





NDIS 呼び出し、 [ *MiniportInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_isr) NIC、または、NIC と、割り込みを共有する別のデバイスは、割り込みを生成するときに機能します。

*MiniportInterrupt*返す必要があります**FALSE**場合は、直ちに、基になる NIC は、割り込みを生成できませんでした。 返しますそれ以外の場合、 **TRUE**割り込みを処理した後。

ミニポート ドライバーで可能な限り少量の作業を行う必要があります、 *MiniportInterrupt*関数。 I/O 操作を延期する必要があります、 [ *MiniportInterruptDPC* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_interrupt_dpc)関数。 NDIS 呼び出し*MiniportInterruptDPC*割り込みの遅延処理の完了にします。

後に追加の Dpc キューに入れ*MiniportInterrupt* 、ミニポート ドライバーのビットのセットを返します、 [ **TargetProcessors** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismqueuedpc)のパラメーター、 *MiniportInterrupt*関数。 要求から追加 Dpc *MiniportInterrupt*または*MiniportInterruptDPC*、ミニポート ドライバーの呼び出し、 **NdisMQueueDpc**関数。

呼び出すことができます、ミニポート ドライバー **NdisMQueueDpc**追加 DPC が他のプロセッサの呼び出しを要求します。

 

 





