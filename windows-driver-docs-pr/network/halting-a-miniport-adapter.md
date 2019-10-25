---
title: ミニポート アダプターの停止
description: ミニポート アダプターの停止
ms.assetid: fd57a2b1-593d-412b-96b5-eabd3ea392e0
keywords:
- ミニポートアダプター WDK ネットワーク、停止
- WDK ネットワークのアダプター、停止
- 状態 WDK ネットワークを停止しました
- ミニ Porthaltex
- アダプターの停止
- アダプターの停止
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d1fdc20b86ab07647f51dcf88baec49042a0d6d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840483"
---
# <a name="halting-a-miniport-adapter"></a>ミニポート アダプターの停止





NDIS は、アダプターがシステムから削除されたときにリソースの割り当てを解除し、ハードウェアを停止するために、NDIS ミニポートドライバーの[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を呼び出します。 NDIS は、ドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数が正常に復帰した後に、 *Miniporthaltex*を呼び出すことができます。 *MiniportInitializeEx*の詳細については、「[ミニポートアダプターの初期化](initializing-a-miniport-adapter.md)」を参照してください。

[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)は、デバイスに割り当てられたドライバーのリソースを解放する必要があります。 ドライバーは、最初にリソースを割り当てた**Ndis<em>Xxx</em>** 関数の reciprocals を呼び出す必要があります。 一般的なルールとして、 *Miniporthaltex*関数は、初期化中に使用された逆順で、相互**Ndis<em>Xxx</em>** 関数を呼び出す必要があります。

アダプターが割り込みを生成した場合、ミニポートドライバーの[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数は、 *Miniporthaltex*が割り込みを無効にするまで、ドライバーの[*miniportinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)関数によって割り込まれる可能性があります。

未処理の OID 要求または送信要求がある場合、NDIS は[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)を呼び出しません。 Ndis は*Miniporthaltex*を呼び出した後、影響を受けるデバイスに対してそれ以上の要求を送信しません。

[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)が戻ると、ミニポートドライバーが停止状態になります。

## <a name="related-topics"></a>関連トピック


[ミニポートドライバーのアダプターの状態](adapter-states-of-a-miniport-driver.md)

[ミニポートアダプターの状態と操作](miniport-adapter-states-and-operations.md)

[ミニポートドライバー停止ハンドラー](halt-handler.md)

[NDIS ミニポートドライバーを書き込んでいます](writing-ndis-miniport-drivers.md)

 

 






