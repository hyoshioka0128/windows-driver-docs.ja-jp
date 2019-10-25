---
title: デバイスが一時停止したときの着信 IRP の保留
description: デバイスが一時停止したときの着信 IRP の保留
ms.assetid: 4964e06b-f1b9-4421-89d1-ad79ce7d7307
keywords:
- 保持 (Irp を)
- Irp WDK PnP
- I/o 要求パケットの WDK PnP
- PnP デバイスの一時停止
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5dd8faaca80925c34f837175048b24c146b1921a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836485"
---
# <a name="holding-incoming-irps-when-a-device-is-paused"></a>デバイスが一時停止したときの着信 IRP の保留





デバイスのドライバーは、そのリソースが再分配されているときに、デバイスを一時停止する必要があります。 リソースの再調整中に、一部のドライバーは、Irp\_が完了したことを通知してデバイスを一時停止[ **\_クエリ\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)の要求を停止し、その他のドライバーが irp を受信するまでデバイスの一時停止を遅延[ **\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)要求を\_しています。 どちらの場合も、 **IRP\_\_が停止し\_デバイス**が成功すると、デバイスを一時停止する必要があります。

ドライバーは、デバイスで実行中のすべての Irp を完了し、デバイスへのアクセスを必要とする新しい Irp を開始しないようにする必要があります。

デバイスの一時停止中に Irp を保持するために、ドライバーは次のような手順を実装します。

1.  [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンで、デバイス拡張機能のフラグを定義します。これには、NEW\_要求を保留\_という名前が付けられます。 フラグをクリアします。

2.  Irp を保持するための FIFO キューを作成します。

    ドライバーが既に Irp をキューに登録している場合は、デバイスを一時停止する前に、ドライバーが未処理の要求を完了する必要があるため、同じキューを再利用できます。

    ドライバーがまだ IRP キューを持っていない場合は、 *AddDevice*ルーチンで作成する必要があります。 どのような種類のキューが作成されるかは、ドライバーがキューをフラッシュする方法によって異なります。 ドライバーは、インタロック、ダブルリンクリスト、および**Exinterlocked ロック*Xxx*リスト**ルーチンを使用する場合があります。

3.  **Irp\_完了\_クエリ\_\_デバイス**(または**IRP\_\_デバイスの停止**) を停止し、未処理の要求を完了し、保留\_新しい\_要求を設定します。誤り.

4.  デバイスにアクセスするディスパッチルーチン ( [*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)や[*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)など) で、[HOLD\_NEW\_REQUESTS] フラグが設定されているかどうかを確認します。 その場合、ドライバーは IRP を pending としてマークし、キューに入れる必要があります。

    ドライバーの*DispatchPnP*ルーチンは、それを保持するのではなく、PnP irp の処理を続行する必要があります。また、 [*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、引き続き電源 irp を処理する必要があります。

5.  *DispatchPnP*で、start または cancel-stop IRP に応答して、HOLD\_NEW\_REQUESTS フラグを解除し、irp を保持するキューで irp を開始します。

    これらの PnP Irp を処理するための最後の手順は、これらのアクションです。 たとえば、start IRP に応答する場合、ドライバーはまずデバイスを起動する操作を実行し、次に IRP を保持するキューで Irp を開始する必要があります。

    IRP を保持するキューからの Irp の処理でエラーが発生しても、開始または取り消しの Irp に対して返される状態には影響しません。

 

 




