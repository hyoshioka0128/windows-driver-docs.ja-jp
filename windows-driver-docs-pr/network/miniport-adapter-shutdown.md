---
title: ミニポート アダプターのシャットダウン
description: ミニポート アダプターのシャットダウン
ms.assetid: 57d964f1-03c7-4b54-9d04-1d187c96e052
keywords:
- ミニポート アダプタの WDK ネットワー キング、シャット ダウン
- アダプターの WDK ネットワー キング、シャット ダウン
- MiniportShutdownEx
- ミニポート ドライバー WDK ネットワー キング、システムのシャット ダウン
- NDIS ミニポート ドライバー WDK、システムのシャット ダウン
- シャット ダウンの WDK ネットワーク
- システム シャット ダウンの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aefc5819670a99448f6eb1d5e125dad6b6b3492a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571869"
---
# <a name="miniport-adapter-shutdown"></a>ミニポート アダプターのシャットダウン





NDIS ミニポート ドライバーを登録する必要があります、 [ *MiniportShutdownEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559449)ミニポート ドライバーの初期化中に機能します。

NDIS 呼び出し NDIS ミニポート ドライバーの[ *MiniportShutdownEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559449)システムがシャット ダウン時に機能します。 *MiniportShutdownEx*ハードウェアを既知の状態に復元します。

*ShutdownAction* NDIS に渡されるパラメーター [ *MiniportShutdownEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559449)シャット ダウンの理由のミニポート ドライバーに通知します。

シャット ダウン ハンドラーを呼び出すことが、ユーザー操作の結果としての IRQL で実行する場合、= パッシブ\_レベル。 回復不能なシステム エラーの結果として呼び出すこともできます、この場合、IRQL で実行できます。

[*MiniportShutdownEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559449)なしで呼び出す必要があります**Ndis * Xxx*** 関数。 ミニポート ドライバーでは、読み取りと書き込み I/O ポートまたは既知の状態にハードウェアを返却する DMA エンジンを無効にする関数を呼び出すことができます。

異なり[ *MiniportHaltEx*](https://msdn.microsoft.com/library/windows/hardware/ff559388)、 [ *MiniportShutdownEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559449)割り当てられたリソースを解放する必要があります。 *MiniportShutdownEx* NIC を停止する必要があります

## <a name="related-topics"></a>関連トピック


[ミニポート ドライバーのアダプターの状態](adapter-states-of-a-miniport-driver.md)

[ミニポート アダプターを停止します。](halting-a-miniport-adapter.md)

[ミニポート アダプタの状態と操作](miniport-adapter-states-and-operations.md)

[書き込みの NDIS ミニポート ドライバー](writing-ndis-miniport-drivers.md)

 

 






