---
title: IRP の削除が発行される場合の概要
description: IRP の削除が発行される場合の概要
ms.assetid: e92e30ce-ca0d-4f00-b54a-778bafba15b3
keywords:
- Irp WDK PnP の削除します。
- WDK PnP Irp
- I/O 要求パケット PnP WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac338558a121e5d9fb176bb395ba96a20a31fc92
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382936"
---
# <a name="understanding-when-remove-irps-are-issued"></a>IRP の削除が発行される場合の概要





次の図では、デバイスのドライバーを削除する Irp の一般的なシーケンスを示します。

![一般的なを示す図 irp の遷移を削除します。](images/rem-irps.png)

次のノートは、前の図の丸の番号に対応しています。

1.  クエリを削除します。

    PnP マネージャーの問題、 [ **IRP\_MN\_クエリ\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)マシンを停止することがなくデバイスを削除できるかどうかを確認します。 ユーザーがデバイス マネージャーは、デバイスを無効にされた場合、デバイスと (Windows 2000 以降) のドライバーの更新を要求すると、この IRP も送信します。 (Windows 98 で PnP マネージャーとは、送信/Irp を停止するこのような状況では、参照してください[デバイスを停止する](stopping-a-device.md)詳細についてはします)。

    デバイス スタックのすべてのドライバーが状態を返す場合\_成功すると、ドライバーが、デバイス、削除保留中状態にします。 この状態で、ドライバーは、デバイスが削除されないようにするすべての操作を開始する必要がありますできません。

    この場合は「クリーン」削除 PnP マネージャーは、削除 IRP を送信する前にクエリの削除 IRP を送信します。 手順 5「突然」削除の説明を参照してください。

    上の図では表示されません、バス ドライバーが表示される可能性があります、 **IRP\_MN\_クエリ\_削除\_デバイス**が開始されていないデバイス。 これは、ユーザーの要求を動的にコンピューターに物理的に存在するが、無効にするデバイスを削除する場合に発生することができます。

2.  成功したクエリの後に削除します。

    PnP マネージャーの問題、 [ **IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)デバイスのドライバーを削除します。

    ドライバーは、この要求に成功する必要があります。 デバイスのドライバー、必要なクリーンアップを実行、デバイス スタックからデタッチして、および削除、FDO いずれかの DOs をフィルター処理します。 親のバス ドライバーは、ユーザーがマシンからのデバイスを物理的に削除するまで、PDO を保持します。

    ドライバーが表示される可能性があります、 [ **IRP\_MN\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)を削除する前に、IRP は必要ありません。 Windows 2000 以降、 **IRP\_MN\_停止\_デバイス**にのみ使用、デバイスの負荷を分散リソースを一時停止は、削除に向けての第一歩です。 デバイスの停止中に、ユーザーは、デバイスのハードウェアを削除した場合は、PnP マネージャー IRP、停止後にいくつかの時点で削除 IRP を送信しますが、停止を削除するための前提条件ではありません。

3.  デバイスを再列挙します。

    PnP マネージャーがドライバーを呼び出す場合は、デバイスは、ドライバーがそれらのデバイス オブジェクトを削除後に再度列挙は、 [ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチンで、問題、 [ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)にデバイスを再開します。 (また、 [PnP の観点からデバイスの状態](state-transitions-for-pnp-devices.md#ddk-state-transitions-for-pnp-devices-kg)図)。

4.  クエリの削除を取り消す

    PnP マネージャーの問題、 [ **IRP\_MN\_キャンセル\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device)クエリの削除要求を取り消します。

    応答、 **IRP\_MN\_キャンセル\_削除\_デバイス**ドライバーは、デバイスを開始状態に戻します。

5.  驚きの削除 (Windows 2000 および Windows の以降のバージョン)

    Windows 2000 およびそれ以降のシステムでは、上から切り離し、マシンからのデバイスを取り外しますプログラムを使用せず、ユーザーの場合、PnP マネージャー送信、 [ **IRP\_MN\_突然\_の削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal) IRP します。

    ドライバーは、高度な警告も表示されませんので、このケースでは「突然」の取り外しを呼び出しています。

    応答、 **IRP\_MN\_突然\_削除**IRP、デバイスのドライバーが未処理の I/O は失敗し、デバイスで使用されるハードウェア リソースを解放します。 ドライバーは存在しないため、デバイスにアクセスするコンポーネントが試みるしないことを確認してください。

    すべてのドライバーを処理する必要があります、 **IRP\_MN\_突然\_削除**IRP の状態を状態を設定する必要があります\_成功します。

    **IRP\_MN\_突然\_削除**はキャンセルできません。

6.  驚くべきこと (Windows 2000 および Windows の以降のバージョン) を削除した後で削除します。

    PnP マネージャーが送信するデバイスへのすべての開いているハンドルが閉じている場合、 [ **IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)デバイスのドライバーを要求します。 各ドライバーでは、デバイス スタックからデタッチし、そのデバイス オブジェクトを削除します。

7.  驚きの削除 (Windows 98/Me)

    Windows 98 で、ドライバーを受信しません/、 [ **IRP\_MN\_突然\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)警告なしで、デバイスが削除されたとき。 PnP マネージャーでのみ送信、 **IRP\_MN\_削除\_デバイス**します。 WDM ドライバーは、両方を処理するコードをいる必要があります、 **IRP\_MN\_突然\_削除**続けて、 **IRP\_MN\_削除\_デバイス** (Windows 2000 とのそれ以降の動作は、突然の削除)、 **IRP\_MN\_削除\_デバイス**ことがなく、突然削除 IRP (Windows 98/Me動作)。

8.  失敗した開始 (Windows 2000 以降) の後に削除します。

    デバイスのドライバーのいずれかが失敗した場合、 **IRP\_MN\_開始\_デバイス**、PnP マネージャーに送信、 **IRP\_MN\_削除\_デバイス**デバイス スタックを要求します。 このような削除 IRP により、デバイスが正常に開始しないことに、デバイスのすべてのドライバーが通知されます。 応答、 **IRP\_MN\_削除\_デバイス**IRP、デバイスのドライバーを元に戻す、開始操作 (開始 IRP が成功した) 場合を元に戻すと、 *AddDevice*操作。 PnP マネージャーによって、このようなデバイスとして、「開始できませんでした」

    この動作は、Windows 2000 以降のプラットフォームのみに適用されます。 Windows 98 で PnP マネージャーに送信する、/、 **IRP\_MN\_停止\_デバイス**失敗した開始に応答します。

PnP デバイスのドライバーを受信できる、 **IRP\_MN\_突然\_削除**IRP の遷移を削除する一般的な方法を示す図で示したものよりも多くの状況でします。 たとえば、ユーザーは、PC カードをコンピューターに挿入し、デバイスが開始される前に削除します。 ドライバーの後、PnP マネージャーが突然削除 IRP を発行する場合、 *AddDevice*ルーチンは、呼び出されたが、発行する前に、 **IRP\_MN\_開始\_デバイス**要求。 ドライバーの PnP デバイスを処理するために準備する必要があります削除 Irp ドライバーの後にいつでも*AddDevice*ルーチンが呼び出されます。

 

 




