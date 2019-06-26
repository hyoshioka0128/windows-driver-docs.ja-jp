---
title: MSI 割り込みとの同期
description: MSI 割り込みとの同期
ms.assetid: 61745a93-79dc-49ac-9ace-3ecb647b7b9a
keywords:
- MSI X WDK ネットワーク、割り込みを同期します。
- メッセージ シグナル割り込み WDK ネットワー キング、割り込みを同期します。
- Msi WDK ネットワー キング、割り込みを同期します。
- WDK のネットワー キング、同期を中断します。
- WDK の MSI X の同期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd290096f040f4bffeb35d961fe574dc6024dfca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377958"
---
# <a name="synchronizing-with-an-msi-interrupt"></a>MSI 割り込みとの同期





ミニポート ドライバーの場合、 [ *MiniportMessageInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_message_interrupt)関数と他のネットワーク インターフェイス カード (NIC) の登録や状態変数などのリソースを共有する*MiniportXxx* 、もう一方に下位の IRQL で実行される関数を*MiniportXxx*関数を呼び出す必要があります、 [ **NdisMSynchronizeWithInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsynchronizewithinterruptex)関数。 この呼び出しにより、ミニポート ドライバーの[ **MiniportSynchronizeMessageInterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_synchronize_interrupt)関数同期とマルチプロセッサの安全な方法で共有リソースにアクセスします。

 

 





