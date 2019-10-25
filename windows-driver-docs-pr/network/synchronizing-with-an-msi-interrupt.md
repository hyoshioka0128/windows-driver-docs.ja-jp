---
title: MSI 割り込みとの同期
description: MSI 割り込みとの同期
ms.assetid: 61745a93-79dc-49ac-9ace-3ecb647b7b9a
keywords:
- MSI-X WDK ネットワーク, 割り込みの同期
- メッセージシグナル割り込み、WDK ネットワーク、割り込みの同期
- Msi WDK ネットワーク, 割り込みの同期
- WDK ネットワークの割り込み、同期
- 同期 WDK MSI-X
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: edfd8ab179f6ca60e18aedb4aa6b369224308e33
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841786"
---
# <a name="synchronizing-with-an-msi-interrupt"></a>MSI 割り込みとの同期





ミニポートドライバーの[*Miniportmessageinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt)関数が、ネットワークインターフェイスカード (NIC) レジスタや状態変数などのリソースを、低い IRQL で実行される別の*miniportxxx*関数と共に共有している場合、その他の*miniportxxx*関数は[**NdisMSynchronizeWithInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsynchronizewithinterruptex)関数を呼び出す必要があります。 この呼び出しにより、ミニポートドライバーの[**MiniportSynchronizeMessageInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_synchronize_interrupt)関数が、同期されたマルチプロセッサセーフな方法で共有リソースにアクセスできるようになります。

 

 





