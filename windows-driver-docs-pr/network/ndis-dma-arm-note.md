---
title: ARM/ARM64 プロセッサでの NDIS DMA の使用を防ぐために注意してください
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 32310496340d59aa8696625e9535743de516a24e
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75297192"
---
# <a name="note-to-discourage-ndis-dma-use-on-armarm64-processors"></a>ARM/ARM64 プロセッサでの NDIS DMA の使用を防ぐために注意してください

> [!CAUTION]
> ARM および ARM64 プロセッサの場合、NDIS ドライバーライターは NDIS スキャッター/Gather DMA ではなく WDF DMA または WDM DMA を使用することを強くお勧めします。
>
> WDF DMA の詳細については、「 [KMDF ドライバーでの Dma 操作の処理](../wdf/handling-dma-operations-in-kmdf-drivers.md)」を参照してください。
>
> WDM DMA の詳細については、「[ドライバーの入出力の管理](../kernel/managing-input-output-for-drivers.md)」の dma 関連の子トピックを参照してください。
