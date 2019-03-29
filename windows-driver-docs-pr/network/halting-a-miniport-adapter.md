---
title: ミニポート アダプターの停止
description: ミニポート アダプターの停止
ms.assetid: fd57a2b1-593d-412b-96b5-eabd3ea392e0
keywords:
- ミニポート アダプタ WDK ネットワークは、停止します。
- アダプター WDK ネットワー キング、停止します。
- 停止状態の WDK ネットワーク
- MiniportHaltEx
- アダプターの停止
- アダプターの停止
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73f267239759d55483fb078efab3ff264501468b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574100"
---
# <a name="halting-a-miniport-adapter"></a>ミニポート アダプターの停止





NDIS 呼び出し NDIS ミニポート ドライバーの[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)アダプターが、システムから削除されるリソースの割り当てを解除して、ハードウェアを停止する関数。 NDIS を呼び出すことができます*MiniportHaltEx*ドライバーの後に[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数が正常に返されます。 詳細については*MiniportInitializeEx*を参照してください[ミニポート アダプターの初期化](initializing-a-miniport-adapter.md)します。

[*MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)ドライバーがデバイスに割り当てられたリソースを解放する必要があります。 ドライバーの逆数を呼び出す必要があります、 **Ndis * Xxx*** いる、最初に割り当てられたリソースの関数。 一般的な規則として、 *MiniportHaltEx*関数が、相互に呼び出す必要があります**Ndis * Xxx*** 関数の初期化中に使用される逆の順序。

アダプターの割り込み、ミニポート ドライバーの生成かどうか[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)関数は、ドライバーのによって割り込まれることができます[ *MiniportInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff559395)行われるまで*MiniportHaltEx*割り込みを無効にします。

NDIS は呼び出しません[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388) OID が要求または要求を送信する未処理がある場合。 NDIS NDIS 呼び出しの後に、影響を受けるデバイスのそれ以降の要求送信しない*MiniportHaltEx*します。

後[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388) 、ミニポート ドライバーが中止状態を返します。

## <a name="related-topics"></a>関連トピック


[ミニポート ドライバーのアダプターの状態](adapter-states-of-a-miniport-driver.md)

[ミニポート アダプタの状態と操作](miniport-adapter-states-and-operations.md)

[ミニポート ドライバー Halt ハンドラー](halt-handler.md)

[書き込みの NDIS ミニポート ドライバー](writing-ndis-miniport-drivers.md)

 

 






