---
title: 割り込みとの同期
description: 割り込みとの同期
ms.assetid: f201acfa-98e4-4373-ba63-b6c814810f99
keywords:
- WDK のネットワー キング、同期を中断します。
- NdisMSynchronizeWithInterruptEx
- 同期の WDK の割り込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb23cd578eea16a0e1ab99807cc44ef8088402ac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377952"
---
# <a name="synchronizing-with-interrupts"></a>割り込みとの同期





ミニポート ドライバーの場合、 [ *MiniportInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_isr)関数と他の NIC の登録や状態変数などのリソースを共有する*MiniportXxx*で実行される関数をIRQL を削減する*MiniportXxx*関数を呼び出す必要があります[ **NdisMSynchronizeWithInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsynchronizewithinterruptex)します。 この呼び出しにより、ミニポート ドライバーの[ *MiniportSynchronizeInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_synchronize_interrupt)関数同期とマルチプロセッサの安全な方法で共有リソースにアクセスします。

 

 





