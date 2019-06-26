---
title: NDIS 6.20 の受信側スロットル
description: NDIS 6.20 の受信側スロットル
ms.assetid: dc8d0f32-37ee-4383-864d-7d814d37c3c8
keywords:
- NDIS 6.20 WDK、受信側のスロットル
- 受信側のスロットル (RST) WDK NDIS 6.20 が動作
- RST WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30a8e167454faf586344151b63fadfa5179ef2d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373326"
---
# <a name="receive-side-throttle-in-ndis-620"></a>NDIS 6.20 の受信側スロットル





NDIS 6.20 が動作には、マルチ メディア アプリケーションでメディアの再生中に中断の可能性を減らすため、受信側のスロットル (RST) の機能強化が導入されています。 RST のサポートは、NDIS 6.20 が動作し、以降のドライバーの必須です。

場合は、NDIS ドライバーに費やすディスパッチ遅延プロシージャ呼び出し (DPC) の IRQ レベルで時間がかかりすぎる、マルチ メディア アプリケーションのスレッドのスケジューリングの待機時間が増加し、メディアの再生中に中断が発生する可能性があります。 メディアの再生を NDIS 6.20 が動作し、後でドライバーを高めるためには、NDIS は受信 DPC のミニポート ドライバーを示すパケットの数を制御できます。

## <a name="related-topics"></a>関連トピック


[*MiniportInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_isr)

[*MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_interrupt_dpc)

[*MiniportMessageInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_message_interrupt)

[*MiniportMessageInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_message_interrupt_dpc)

[**NDIS\_受信\_スロットル\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_receive_throttle_parameters)

[**NdisMQueueDpcEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismqueuedpcex)

 

 






