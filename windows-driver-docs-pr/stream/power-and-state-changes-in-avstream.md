---
title: AVStream の電源と状態の変更
description: AVStream の電源と状態の変更
ms.assetid: f62f4306-97c0-40fe-89ec-d08eb18988c9
keywords:
- AVStream WDK、パワーおよび状態の変更
- パワー変更 WDK、AVStream
- 状態変更 WDK、AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18dcf6a7fdc63dd4bf308137c8da7bd17f77ebb8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842622"
---
# <a name="power-and-state-changes-in-avstream"></a>AVStream の電源と状態の変更


AVStream は[ **\_電源要求\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)された IRP\_を受け取ると、ミニドライバーの[*Avstrminidevicesetpower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksdevicesetpower) callback ルーチンを呼び出します (ミニドライバーが指定されている場合)。

AVStream は、 [**Ksk プロパティ\_CONNECTION\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-state)プロパティの set 要求を受け取ると、ミニドライバーの[*Avstrminipinsetdevicestate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdevicestate)コールバックルーチンを呼び出します (ミニドライバーが指定されている場合)。

システムがスリープ状態から復帰すると、AVStream は、予期された順序とは逆にミニドライバーの*Avstrminipinsetdevicestate*および*avstrminidevicesetdevicecallback*ルーチンを呼び出すことができます。 たとえば、 *Avstrminipinsetdevicestate*を*Beforeavstrminidevicesetpower*と呼び出すことができます。

そのため、*予想されるコールバック順序の逆の処理を行うに*は、ドライバーを準備する必要があります。

この反転は、システムがスリープ状態になっている場合には発生しません。 電源が切断されると、これら2つのコールバックルーチンは常に予想される順序で発生します。 たとえば、 *Avstrminipinsetdevicestate*は*Avstrminidevicesetpower*の前に常に呼び出されます。

この反転が発生した場合、シーケンス全体は次のようになります。

まず、電源のダウンシーケンスが発生します。

1.  *Avstrminipinsetdevicestate*は、デバイスの状態を**KSK 状態**から ksk に変更するための要求を使用して呼び出され、\_一時停止\_ます。

2.  *Avstrminidevicesetpower*は、電源状態を D0 から D2/D3 に変更する要求で呼び出されます。

3.  この時点で、システムはスリープ状態です。

4.  次に、電源シーケンスが発生します。

5.  *Avstrminidevicesetpower*は、D2/D3 から D0 に電源状態を変更する要求で呼び出されます。

6.  *Avstrminipinsetdevicestate*は、デバイスの状態を ksk から変更するための要求を使用して呼び出され、\_実行されるように **\_** ます。

このシナリオでは、手順 5. と 6. は、予想される順序とは逆の手順です。

また、アプリケーションがストリーミングされ、システムが電源ダウンシーケンスを開始すると、実行中のキャプチャグラフは常に一時停止状態になります。 グラフが既に停止している場合は、停止したままになります。

 

 




