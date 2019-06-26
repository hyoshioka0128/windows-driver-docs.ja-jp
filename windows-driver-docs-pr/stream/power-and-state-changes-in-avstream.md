---
title: AVStream の電源と状態の変更
description: AVStream の電源と状態の変更
ms.assetid: f62f4306-97c0-40fe-89ec-d08eb18988c9
keywords:
- AVStream WDK、電源と状態の変化
- 電源の変更、WDK AVStream
- 状態の変更、WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e253c29111f582a92db828895e048c881b6dfbd7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369556"
---
# <a name="power-and-state-changes-in-avstream"></a>AVStream の電源と状態の変更


AVStream を受信すると、 [ **IRP\_MN\_設定\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)要求、ミニドライバーの呼び出す[ *AVStrMiniDeviceSetPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksdevicesetpower)コールバック ルーチンを 1 つ、ミニドライバーが指定されている場合。

AVStream がのセット要求を受信すると、 [ **KSPROPERTY\_接続\_状態**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-state)プロパティ、ミニドライバーの呼び出す[ *AVStrMiniPinSetDeviceState* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspinsetdevicestate)コールバック ルーチンを 1 つ、ミニドライバーが指定されている場合。

AVStream ミニドライバーを呼び出すことができます、システムは、スリープ状態から再開、 *AVStrMiniPinSetDeviceState*と*AVStrMiniDeviceSetPower*想定されている順序の逆の順序でコールバック ルーチン。 たとえば、 *AVStrMiniPinSetDeviceState*を呼び出すことは*beforeAVStrMiniDeviceSetPower*します。

その結果、ドライバー*コールバックが予想される注文のような逆操作を処理する準備をする必要があります*します。

この逆の操作は、システムがスリープ状態に電源オフ時に行われません。 下の電源でこれら 2 つのコールバック ルーチンは、常に想定されている順序で発生します。 たとえば、 *AVStrMiniPinSetDeviceState*する前に必ず呼び出される*AVStrMiniDeviceSetPower*します。

この逆転が発生した場合、シーケンス全体がようになります。

最初に、シーケンスの電源が発生します。

1.  *AVStrMiniPinSetDeviceState*からデバイスの状態を変更する要求を使用して呼び出した**KSSTATE\_実行**KSSTATE に\_一時停止します。

2.  *AVStrMiniDeviceSetPower* D0 から/D3 D2 に電源状態を変更する要求では呼び出されます。

3.  この時点で、システムがスリープ状態です。

4.  次に、電源投入シーケンスが発生します。

5.  *AVStrMiniDeviceSetPower*  /D3 D2 から D0 に電源状態を変更する要求では呼び出されます。

6.  *AVStrMiniPinSetDeviceState*からデバイスの状態を変更する要求を使用して呼び出した**KSSTATE\_一時停止**KSSTATE に\_を実行します。

このシナリオでは、手順 5. と 6. は、想定されている順序とは反対で手順を示します。

さらに、アプリケーションをストリーミングし、システムが電源オフ シーケンスを開始、実行しているキャプチャ グラフは一時停止状態で配置常に。 グラフが既に停止されている場合は、停止したままです。

 

 




