---
title: デバイスが一時停止したときの着信 IRP の保留
description: デバイスが一時停止したときの着信 IRP の保留
ms.assetid: 4964e06b-f1b9-4421-89d1-ad79ce7d7307
keywords:
- Irp を保持します。
- WDK PnP Irp
- I/O 要求パケット PnP WDK
- PnP デバイスの一時停止
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f18513365c36fbb0c26811af5930ab1025bc6b6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363434"
---
# <a name="holding-incoming-irps-when-a-device-is-paused"></a>デバイスが一時停止したときの着信 IRP の保留





デバイスのドライバーでは、そのリソースが調整されている場合、デバイスを一時停止する必要があります。 リソースが再調整中に一部のドライバーは、デバイスへの応答を一時停止、 [ **IRP\_MN\_クエリ\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)要求およびその他ドライバーの遅延を受け取るまで、デバイスの一時停止、 [ **IRP\_MN\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)要求。 どちらの場合、デバイスがある必要がありますと一時停止、 **IRP\_MN\_停止\_デバイス**が成功するとします。

ドライバーは、デバイス上で進行中の任意の Irp を完了し、デバイスへのアクセスを必要とする新しい Irp を開始しない必要があります。

デバイスが一時停止中に Irp を保持するには、ドライバーは、次の手順を実装します。

1.  その[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチン、保留中のような名前で、デバイスの拡張機能のフラグを定義する\_新規\_要求。 フラグをオフにします。

2.  Irp を保持するため、FIFO キューを作成します。

    場合は、ドライバーは Irp を既にキューでは、ドライバーがデバイスを一時停止する前に、未処理の要求を完了に必要なために、同じキューが再利用できます。

    1 つで、作成する必要がありますドライバーにまだ、IRP キューがない場合、 *AddDevice*ルーチン。 キューの種類を作成、ドライバーが、キューをフラッシュする方法によって異なります。 ドライバーは、インタロックされた、二重にリンクされたリストを使用して可能性があります、 **ExInterlocked*Xxx*一覧**ルーチン。

3.  その*DispatchPnP*のコードを**IRP\_MN\_クエリ\_停止\_デバイス**(または**IRP\_MN\_停止\_デバイス**)、未処理の要求を完了し、保留の設定、\_新規\_要求フラグ。

4.  などのデバイスにアクセスするディスパッチ ルーチンで[ *DispatchWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)または[ *DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)、確認するかどうか保留\_新規\_要求フラグを設定します。 そうである場合、ドライバーは IRP の保留をマークし、再生待ちにする必要があります。

    ドライバーの*DispatchPnP*ルーチンがそれを保持するのではなく、PnP Irp の処理を続行する必要があります、 [ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンは、電源 Irp の処理を続行する必要があります。

5.  *DispatchPnP*、開始とキャンセル停止 IRP に対して保留を解除\_新規\_要求フラグし、IRP を保持するキューで、Irp を起動します。

    これらのアクションは、これらの PnP Irp を処理するための最後の手順では可能性があります。 など開始 IRP への応答、ドライバーは、デバイスを開始する操作を実行する必要がありますまずとし、Irp IRP を保持するキューで開始できます。

    IRP を保持するキューから Irp の処理中のエラーでは、開始やキャンセル停止 Irp の返される状態は影響しません。

 

 




