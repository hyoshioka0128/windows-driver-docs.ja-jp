---
title: NDIS 6.20 が動作の側のスロットルを受信します。
description: NDIS 6.20 が動作の側のスロットルを受信します。
ms.assetid: dc8d0f32-37ee-4383-864d-7d814d37c3c8
keywords:
- NDIS 6.20 WDK、受信側のスロットル
- 受信側のスロットル (RST) WDK NDIS 6.20 が動作
- RST WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f753335a06a4592e407b92503803623a664d7a0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559473"
---
# <a name="receive-side-throttle-in-ndis-620"></a>NDIS 6.20 が動作の側のスロットルを受信します。





NDIS 6.20 が動作には、マルチ メディア アプリケーションでメディアの再生中に中断の可能性を減らすため、受信側のスロットル (RST) の機能強化が導入されています。 RST のサポートは、NDIS 6.20 が動作し、以降のドライバーの必須です。

場合は、NDIS ドライバーに費やすディスパッチ遅延プロシージャ呼び出し (DPC) の IRQ レベルで時間がかかりすぎる、マルチ メディア アプリケーションのスレッドのスケジューリングの待機時間が増加し、メディアの再生中に中断が発生する可能性があります。 メディアの再生を NDIS 6.20 が動作し、後でドライバーを高めるためには、NDIS は受信 DPC のミニポート ドライバーを示すパケットの数を制御できます。

## <a name="related-topics"></a>関連トピック


[*MiniportInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff559395)

[*MiniportInterruptDPC*](https://msdn.microsoft.com/library/windows/hardware/ff559398)

[*MiniportMessageInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff559407)

[*MiniportMessageInterruptDPC*](https://msdn.microsoft.com/library/windows/hardware/ff559411)

[**NDIS\_受信\_スロットル\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff567241)

[**NdisMQueueDpcEx**](https://msdn.microsoft.com/library/windows/hardware/ff563640)

 

 






