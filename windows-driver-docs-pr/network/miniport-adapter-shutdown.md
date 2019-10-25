---
title: ミニポート アダプターのシャットダウン
description: ミニポート アダプターのシャットダウン
ms.assetid: 57d964f1-03c7-4b54-9d04-1d187c96e052
keywords:
- ミニポートアダプター WDK ネットワーク、シャットダウン
- の WDK ネットワーク、シャットダウン
- MiniportShutdownEx
- ミニポートドライバー WDK ネットワーク、システムのシャットダウン
- NDIS ミニポートドライバー WDK、システムのシャットダウン
- WDK ネットワークのシャットダウン
- システムシャットダウンの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7810384dded49b781e8c57fae65087d075a8a59e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844248"
---
# <a name="miniport-adapter-shutdown"></a>ミニポート アダプターのシャットダウン





ミニポートドライバーの初期化中に、NDIS ミニポートドライバーが[*Miniportshutdownex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)関数を登録する必要があります。

システムがシャットダウンされると、NDIS は NDIS ミニポートドライバーの[*Miniportshutdownex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)関数を呼び出します。 *Miniportshutdownex*は、ハードウェアを既知の状態に復元します。

NDIS が[*Miniportshutdownex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)に渡された*shutdownaction*パラメーターは、シャットダウンの理由をミニポートドライバーに通知します。

シャットダウンハンドラーは、ユーザー操作の結果として呼び出すことができます。この場合は、IRQL = パッシブ\_レベルで実行されます。 回復不能なシステムエラーの結果として呼び出すこともできます。その場合は、任意の IRQL で実行できます。

[*Miniportshutdownex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)は、 **Ndis * Xxx*** 関数を呼び出さないでください。 ミニポートドライバーは、i/o ポートの読み取りと書き込みを行う関数を呼び出したり、ハードウェアを既知の状態に戻すために DMA エンジンを無効にしたりすることができます。

[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)とは異なり、 [*miniportshutdownex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)では割り当てられたリソースを解放しないでください。 *Miniportshutdownex*は、NIC を停止するだけで済みます。

## <a name="related-topics"></a>関連トピック


[ミニポートドライバーのアダプターの状態](adapter-states-of-a-miniport-driver.md)

[ミニポートアダプターの停止](halting-a-miniport-adapter.md)

[ミニポートアダプターの状態と操作](miniport-adapter-states-and-operations.md)

[NDIS ミニポートドライバーを書き込んでいます](writing-ndis-miniport-drivers.md)

 

 






