---
title: WDM の下端用のミニポート ドライバー関数の登録
description: WDM の下端用のミニポート ドライバー関数の登録
ms.assetid: 68048d36-d57c-4ad9-a15e-92b1d7866d4a
keywords:
- 関数の登録、NDIS WDM ミニポート ドライバー WDK ネットワーク
- NDIS WDM ミニポート ドライバー WDK ネットワー キング、エントリ ポイント関数
- 下端の NDIS ミニポート ドライバー WDK ネットワー キング、エントリ ポイント関数
- WDM 低い edge WDK ネットワー キング、エントリ ポイント関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b2f528a190c9d38ec80db04d8748b5843bdbe17
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359159"
---
# <a name="registering-miniport-driver-functions-for-wdm-lower-edge"></a>WDM の下端用のミニポート ドライバー関数の登録





WDM 下端のミニポート ドライバーを呼び出す必要があります、 [ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)関数でその**DriverEntry**ルーチンは特定のエントリ ポイントを登録するにはNDIS ライブラリを使用した機能です。 これらのエントリ ポイント関数は、ミニポート ドライバーの上端を作成し、記載されて[ミニポート ドライバーの初期化](initializing-a-miniport-driver.md)します。 ただし、WDM 下端のミニポート ドライバーでは、特定のエントリ ポイント関数を設定する必要はありません。 たとえば、次のエントリ ポイント関数が設定されていない次の理由。

-   [*MiniportInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_isr)、 [ *MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_interrupt_dpc)、 [ *MiniportEnableInterruptEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_enable_interrupt)と[ *MiniportDisableInterruptEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_disable_interrupt)

    ミニポート ドライバーは、物理ネットワーク インターフェイス カード (NIC) からの割り込みを受信せず、これらのルーチンのエントリ ポイントは必要ありません。 特定のバスのドライバーは、ミニポート ドライバーには、バス上のパケットが到着したときに、割り込みを受信します。 バス ドライバーは、ミニポート ドライバーを通知します。

-   [*MiniportSharedMemoryAllocateComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_allocate_shared_mem_complete)

    ミニポート ドライバーが共有メモリを割り当てられなかったため完了エントリ ポイントのルーチンが指定されていません。

-   [*MiniportCheckForHangEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_check_for_hang)

    そのミニポート インスタンスが停止した場合、応答して送信に基づいており、要求では、このルーチンを通常不要をそのタイムアウトを決定する NDIS ミニポート ドライバーが利用できます。

 

 





