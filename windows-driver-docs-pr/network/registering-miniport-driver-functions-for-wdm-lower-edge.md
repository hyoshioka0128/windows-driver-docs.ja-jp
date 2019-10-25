---
title: WDM の下端用のミニポート ドライバー関数の登録
description: WDM の下端用のミニポート ドライバー関数の登録
ms.assetid: 68048d36-d57c-4ad9-a15e-92b1d7866d4a
keywords:
- NDIS-WDM ミニポートドライバー WDK ネットワーク, 関数の登録
- NDIS-WDM ミニポートドライバー WDK ネットワーク、エントリポイント関数
- NDIS ミニポートドライバー WDK ネットワーク、エントリポイント関数の下端
- WDM 低エッジ WDK ネットワーク、エントリポイント関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d527fcea109fed9f1d1c39c13f64347e6938091b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842076"
---
# <a name="registering-miniport-driver-functions-for-wdm-lower-edge"></a>WDM の下端用のミニポート ドライバー関数の登録





WDM の下端があるミニポートドライバーは、 **driverentry**ルーチンで[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)関数を呼び出して、特定のエントリポイント関数を NDIS ライブラリに登録する必要があります。 これらのエントリポイント関数は、ミニポートドライバーの上端を構成し、「[ミニポートドライバーの初期化](initializing-a-miniport-driver.md)」で説明されています。 ただし、特定のエントリポイント関数を設定するために、WDM が低いミニポートドライバーは必要ありません。 たとえば、次のエントリポイント関数は、次の理由により設定されていません。

-   [*Miniportinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)、 [*MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)、 [*MiniportEnableInterruptEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_enable_interrupt)、および[*MiniportDisableInterruptEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_disable_interrupt)

    ミニポートドライバーは、物理ネットワークインターフェイスカード (NIC) からの割り込みを受信しないため、これらのエントリポイントルーチンは必要ありません。 特定のバスのドライバーは、ミニポートドライバーを対象とするバスにパケットが到着すると、割り込みを受信します。 次に、バスドライバーがミニポートドライバーに通知します。

-   [*MiniportSharedMemoryAllocateComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_allocate_shared_mem_complete)

    ミニポートドライバーでは共有メモリが割り当てられないため、入力ポイントルーチンの完了ルーチンが指定されていません。

-   [*MiniportCheckForHangEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_check_for_hang)

    ミニポートドライバーは、送信とタイムアウトの要求に基づいて、ミニポートインスタンスが応答を停止したかどうかを判断するために NDIS に依存します。そのため、このルーチンは通常必要ありません。

 

 





