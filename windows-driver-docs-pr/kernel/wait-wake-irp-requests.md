---
title: 待機/ウェイク IRP 要求
description: 待機/ウェイク IRP 要求
ms.assetid: c67d6dcb-f4a9-4df0-abb8-9d84fc44ec40
keywords:
- 送信待機/ウェイク Irp
- ウェイク アップ信号には、WDK のカーネルが有効になっています。
- Irp WDK の電源管理のウェイク/待機を送信します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c08b0f0a7a51accbccadec3e05ba797777acf418
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358135"
---
# <a name="waitwake-irp-requests"></a>待機/ウェイク IRP 要求





送信する、 [ **IRP\_MN\_待機\_WAKE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)、ドライバーを呼び出す[ **PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp)、PDO のターゲットへのポインター、システム電源の状態、およびコールバック ルーチンへのポインター (その他のパラメーター) の間で渡すことです。

システムの電源状態では、この IRP がシステムを wake 最小電源の状態を指定します。 等しいかそれよりもさらに電源を値として使用することがあります、 [ **SystemWake** ](systemwake.md)状態で、 [**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)構造体。 たとえば、ドライバーに渡します**PowerSystemSleeping2**の IRP で、関連付けられている IRP の S0、S1、S2 の状態から復帰するシステム可能性があります。 システムがこのような場合は、S0 と s2 の場合サポートする必要があります (範囲の最高と最低の搭載状態) が必要な S1 をサポートしていません。

待機/ウェイク IRP を要求するすべてのドライバーを指定する必要があります、[コールバック ルーチン](wait-wake-callback-routines.md)、他のすべてのドライバーは IRP を完了した後に呼び出されます。 このルーチンで、ドライバーが、そのデバイスを動作状態に戻るに必要なことすべてを実行できます。

応答で**PoRequestPowerIrp**、電源マネージャーの割り当てコードを少しで累乗 IRP **IRP\_MN\_待機\_WAKE**デバイスの上部に送信しますPDO のターゲットのスタック。 呼び出し元には、IRP をキャンセルする必要がある場合に後で使用できる割り当て済みの IRP にポインターが返されます。

エラーが発生しなかった場合**PoRequestPowerIrp**ステータスを返します\_保留します。 この状態は、IRP が正常に送信され、完了待ちの状態を意味します。

待機/ウェイク IRP では、システムまたはデバイスの電源の状態は変更されません。 デバイスのウェイク アップ シグナルだけができます。 IRP が保留外部からの信号は、システムまたはデバイスがスリープ解除するまでです。

 

 




