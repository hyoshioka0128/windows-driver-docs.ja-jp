---
title: WDM 下端のミニポート ドライバー関数を登録します。
description: WDM 下端のミニポート ドライバー関数を登録します。
ms.assetid: 68048d36-d57c-4ad9-a15e-92b1d7866d4a
keywords:
- 関数の登録、NDIS WDM ミニポート ドライバー WDK ネットワーク
- NDIS WDM ミニポート ドライバー WDK ネットワー キング、エントリ ポイント関数
- 下端の NDIS ミニポート ドライバー WDK ネットワー キング、エントリ ポイント関数
- WDM 低い edge WDK ネットワー キング、エントリ ポイント関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2096d9945108bdf0fd1b18516da51bd2972af0c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531422"
---
# <a name="registering-miniport-driver-functions-for-wdm-lower-edge"></a>WDM 下端のミニポート ドライバー関数を登録します。





WDM 下端のミニポート ドライバーを呼び出す必要があります、 [ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)関数でその**DriverEntry**ルーチンは特定のエントリ ポイントを登録するにはNDIS ライブラリを使用した機能です。 これらのエントリ ポイント関数は、ミニポート ドライバーの上端を作成し、記載されて[ミニポート ドライバーの初期化](initializing-a-miniport-driver.md)します。 ただし、WDM 下端のミニポート ドライバーでは、特定のエントリ ポイント関数を設定する必要はありません。 たとえば、次のエントリ ポイント関数が設定されていない次の理由。

-   [*MiniportInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff559395)、 [ *MiniportInterruptDPC*](https://msdn.microsoft.com/library/windows/hardware/ff559398)、 [ *MiniportEnableInterruptEx*](https://msdn.microsoft.com/library/windows/hardware/ff559380)と[ *MiniportDisableInterruptEx*](https://msdn.microsoft.com/library/windows/hardware/ff559375)

    ミニポート ドライバーは、物理ネットワーク インターフェイス カード (NIC) からの割り込みを受信せず、これらのルーチンのエントリ ポイントは必要ありません。 特定のバスのドライバーは、ミニポート ドライバーには、バス上のパケットが到着したときに、割り込みを受信します。 バス ドライバーは、ミニポート ドライバーを通知します。

-   [*MiniportSharedMemoryAllocateComplete*](https://msdn.microsoft.com/library/windows/hardware/ff559446)

    ミニポート ドライバーが共有メモリを割り当てられなかったため完了エントリ ポイントのルーチンが指定されていません。

-   [*MiniportCheckForHangEx*](https://msdn.microsoft.com/library/windows/hardware/ff559346)

    そのミニポート インスタンスが停止した場合、応答して送信に基づいており、要求では、このルーチンを通常不要をそのタイムアウトを決定する NDIS ミニポート ドライバーが利用できます。

 

 





