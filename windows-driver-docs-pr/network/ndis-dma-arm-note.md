---
title: ARM/ARM64 プロセッサでの NDIS DMA の使用を防ぐために注意してください
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4712128bba51a6bc1c12586b40b49a0b7a86849a
ms.sourcegitcommit: 724404f7baf0f7f9a8bd3fd3eaf41c09f45a9e60
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445871"
---
# 

> [!CAUTION]
> ARM および ARM64 プロセッサの場合、NDIS ドライバーライターは NDIS スキャッター/Gather DMA ではなく WDF DMA または WDM DMA を使用することを強くお勧めします。 
>
> WDF DMA の詳細については、「 [KMDF ドライバーでの Dma 操作の処理](../wdf/handling-dma-operations-in-kmdf-drivers.md)」を参照してください。
>
> WDM DMA の詳細については、「[ドライバーの入出力の管理](../kernel/managing-input-output-for-drivers.md)」の dma 関連の子トピックを参照してください。
