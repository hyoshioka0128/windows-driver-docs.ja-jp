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
ms.openlocfilehash: a9a5d26255b8ec8a9ee8863376cf0a1b5a05d031
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716940"
---
# <a name="halting-a-miniport-adapter"></a>ミニポート アダプターの停止





NDIS 呼び出し NDIS ミニポート ドライバーの[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)アダプターが、システムから削除されるリソースの割り当てを解除して、ハードウェアを停止する関数。 NDIS を呼び出すことができます*MiniportHaltEx*ドライバーの後に[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数が正常に返されます。 詳細については*MiniportInitializeEx*を参照してください[ミニポート アダプターの初期化](initializing-a-miniport-adapter.md)します。

[*MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)ドライバーがデバイスに割り当てられたリソースを解放する必要があります。 ドライバーの逆数を呼び出す必要があります、 **Ndis<em>Xxx</em>** 関数が、最初に割り当てられたリソース。 一般的な規則として、 *MiniportHaltEx*関数が、相互に呼び出す必要があります**Ndis<em>Xxx</em>** 初期化中に使用する逆の順序で関数。

アダプターの割り込み、ミニポート ドライバーの生成かどうか[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)関数は、ドライバーのによって割り込まれることができます[ *MiniportInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_isr)行われるまで*MiniportHaltEx*割り込みを無効にします。

NDIS は呼び出しません[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt) OID が要求または要求を送信する未処理がある場合。 NDIS NDIS 呼び出しの後に、影響を受けるデバイスのそれ以降の要求送信しない*MiniportHaltEx*します。

後[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt) 、ミニポート ドライバーが中止状態を返します。

## <a name="related-topics"></a>関連トピック


[ミニポート ドライバーのアダプターの状態](adapter-states-of-a-miniport-driver.md)

[ミニポート アダプタの状態と操作](miniport-adapter-states-and-operations.md)

[ミニポート ドライバー Halt ハンドラー](halt-handler.md)

[書き込みの NDIS ミニポート ドライバー](writing-ndis-miniport-drivers.md)

 

 






