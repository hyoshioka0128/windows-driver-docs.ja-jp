---
title: ARM または ARM64 プロセッサ上で NDIS DMA の使用を防ぐために注意してください。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bacadff06277b9cfb4816cdde57c0653775ea863
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539865"
---
> [!CAUTION]
> ARM および ARM64 のプロセッサでは、NDIS ドライバー作成者が NDIS スキャッター/ギャザー DMA ではなく、WDF DMA または WDM DMA を使用することを強くお勧めします。 
>
> WDF DMA の詳細については、[KMDF ドライバーで DMA 操作を処理](../wdf/handling-dma-operations-in-kmdf-drivers.md)を参照してください。
>
> WDM DMA の詳細については、の子の DMA に関連するトピックを参照して[ドライバーの入力/出力を管理する](../kernel/managing-input-output-for-drivers.md)します。
