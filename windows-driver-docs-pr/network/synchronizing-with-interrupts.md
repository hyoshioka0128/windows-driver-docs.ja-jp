---
title: 割り込みとの同期
description: 割り込みとの同期
ms.assetid: f201acfa-98e4-4373-ba63-b6c814810f99
keywords:
- WDK ネットワークの割り込み、同期
- NdisMSynchronizeWithInterruptEx
- WDK 割り込みの同期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1112beabeee0241c590cf4a2ced87effc5022e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841784"
---
# <a name="synchronizing-with-interrupts"></a>割り込みとの同期





ミニポートドライバーの[*Miniportinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)関数が、NIC レジスタや状態変数などのリソースを、低い IRQL で実行される別の*miniportinterrupt*関数と共有している場合、その*miniportinterrupt*関数はを呼び出す[**必要があります。NdisMSynchronizeWithInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsynchronizewithinterruptex)。 この呼び出しにより、ミニポートドライバーの[*MiniportSynchronizeInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_synchronize_interrupt)関数が、同期されたマルチプロセッサセーフな方法で共有リソースにアクセスできるようになります。

 

 





