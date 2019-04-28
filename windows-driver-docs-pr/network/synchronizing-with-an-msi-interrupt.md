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
ms.openlocfilehash: 8a8ed85eac6e133b6a9da0962c5f03f078eaa28a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362540"
---
# <a name="synchronizing-with-an-msi-interrupt"></a>MSI 割り込みとの同期





ミニポート ドライバーの場合、 [ *MiniportMessageInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff559407)関数と他のネットワーク インターフェイス カード (NIC) の登録や状態変数などのリソースを共有する*MiniportXxx* 、もう一方に下位の IRQL で実行される関数を*MiniportXxx*関数を呼び出す必要があります、 [ **NdisMSynchronizeWithInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563681)関数。 この呼び出しにより、ミニポート ドライバーの[ **MiniportSynchronizeMessageInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/ff559455)関数同期とマルチプロセッサの安全な方法で共有リソースにアクセスします。

 

 





