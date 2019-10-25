---
title: NDIS 6.20 の受信側スロットル
description: NDIS 6.20 の受信側スロットル
ms.assetid: dc8d0f32-37ee-4383-864d-7d814d37c3c8
keywords:
- NDIS 6.20 WDK、受信側スロットル
- 受信側スロットル (RST) WDK NDIS 6.20
- RST WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6287e1f7c4a87d542feacf7878098c834b365884
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844857"
---
# <a name="receive-side-throttle-in-ndis-620"></a>NDIS 6.20 の受信側スロットル





NDIS 6.20 では、マルチメディアアプリケーションでのメディアの再生中に中断される可能性を減らすために、受信側スロットル (RST) の機能強化が導入されています。 NDIS 6.20 以降のドライバーでは、RST のサポートは必須です。

NDIS ドライバーが遅延プロシージャ呼び出し (DPC) でディスパッチ IRQ レベルでの時間を過剰に費やした場合、マルチメディアアプリケーションスレッドのスケジュール待機時間が長くなり、メディアの再生中に中断が発生する可能性があります。 Ndis 6.20 以降のドライバーでメディアの再生を向上させるために、NDIS では、受信 DPC でミニポートドライバーが示すパケットの数を制御できます。

## <a name="related-topics"></a>関連トピック


[*MiniportInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)

[*MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)

[*MiniportMessageInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt)

[*MiniportMessageInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt_dpc)

[**NDIS\_受信\_スロットル\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_throttle_parameters)

[**NdisMQueueDpcEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismqueuedpcex)

 

 






