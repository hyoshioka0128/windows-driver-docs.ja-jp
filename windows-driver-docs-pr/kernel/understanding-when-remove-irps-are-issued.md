---
title: 削除の Irp が発行された場合の理解
description: 削除の Irp が発行された場合の理解
ms.assetid: e92e30ce-ca0d-4f00-b54a-778bafba15b3
keywords:
- Irp の削除 WDK PnP
- Irp WDK PnP
- I/o 要求パケットの WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f609a1974aebb13763d488a80dfe7c05ac36bf3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838379"
---
# <a name="understanding-when-remove-irps-are-issued"></a>削除の Irp が発行された場合の理解





次の図は、デバイスのドライバーの削除に関連する一般的な一連の Irp を示しています。

![一般的な remove irp 遷移を示す図](images/rem-irps.png)

次の注意事項は、前の図の丸で囲まれた数値に対応しています。

1.  クエリの削除

    PnP マネージャーは、 [**IRP\_の\_クエリを発行\_\_デバイスを削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)して、マシンを中断せずにデバイスを削除できるかどうかを確認します。 また、この IRP は、ユーザーがデバイスの2000ドライバーを更新するように要求した場合に、デバイスマネージャーがデバイスを無効にした場合にも送信されます。 (Windows 98/Me では、PnP マネージャーは、このような状況で停止 Irp を送信します。詳細については、「[デバイスの停止](stopping-a-device.md)」を参照してください。)

    デバイススタック内のすべてのドライバーが正常な状態\_返された場合、ドライバーはデバイスを削除保留中の状態にします。 この状態では、ドライバーは、デバイスが削除されないようにする操作を開始することはできません。

    この "クリーンな" 削除の場合、PnP マネージャーは、削除 IRP を送信する前に、クエリ削除の IRP を送信します。 「驚く」削除の詳細については、手順 5. を参照してください。

    上の図には示されていませんが、バスドライバーは、開始されていないデバイスの **\_デバイスを削除\_** ために、IRP\_を実行\_クエリを受信する可能性があります。 これは、ユーザーが物理的にコンピューター上に存在していても無効になっているデバイスを動的に削除するように要求した場合に発生する可能性があります。

2.  成功したクエリの削除

    PnP マネージャーは、デバイスのドライバーを削除するために、 [ **\_デバイス\_削除する IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)を発行します。

    ドライバーは、この要求を正常に完了する必要があります。 デバイスのドライバーは、必要なクリーンアップを実行し、デバイススタックからデタッチし、FDO およびすべてのフィルター DOs を削除します。 親バスドライバーは、ユーザーがコンピューターから物理的にデバイスを削除するまで PDO を保持します。

    ドライバーが Irp を受信し、削除 IRP の前に[ **\_デバイスを停止\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)場合があることに注意してください。ただし、これは必須ではありません。 Windows 2000 以降では、 **IRP\_\_停止\_デバイス**は、リソースの再調整のためにデバイスを一時停止するためにのみ使用されます。削除の手順ではありません。 デバイスの停止中にユーザーがデバイスのハードウェアを削除した場合、PnP マネージャーは stop IRP の後のある時点で削除の IRP を送信しますが、停止は削除の前提条件ではありません。

3.  デバイスの Reenumerate

    ドライバーによってデバイスオブジェクトが削除された後にデバイスが再列挙された場合、PnP マネージャーはドライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンを呼び出し、\_デバイスを起動してデバイスを復元するために、 [**IRP\_完了\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)発行します。 ( [PnP の観点からデバイスの状態](state-transitions-for-pnp-devices.md#ddk-state-transitions-for-pnp-devices-kg)も参照してください)。

4.  クエリの削除を取り消す

    PnP マネージャーは、 [**IRP\_を実行\_キャンセル\_\_デバイスを削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device)して、クエリ削除要求をキャンセルします。

    IRP\_に応答して **\_キャンセル\_\_デバイスを削除**すると、ドライバーはデバイスを開始状態に戻します。

5.  突然の削除 (windows 2000 以降のバージョンの Windows)

    Windows 2000 以降のシステムでは、ユーザーが unplugs または Eject ハードウェアプログラムを使用せずにコンピューターからデバイスを削除した場合、PnP マネージャーは、予期しない[ **\_irp\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)irp を\_送信します。

    このような場合は、ドライバーが事前の警告を受信しないため、"驚かれる" 削除と呼ばれます。

    **Irp\_削除**irp に応答すると、デバイスのドライバーは未処理の i/o をすべて失敗とし、デバイスによって使用されているハードウェアリソースを解放します。\_\_します。 ドライバーは、デバイスが存在しないため、そのデバイスにアクセスしようとするコンポーネントがないことを確認する必要があります。

    すべてのドライバーは、 **irp\_** を処理する必要があります。 IRP\_削除 irp\_処理し、状態を [成功]\_[状態] に設定する必要があります。

    **IRP\_\_驚く\_の削除**を取り消すことはできません。

6.  突然削除した後に削除する (Windows 2000 以降のバージョンの Windows)

    デバイスに対して開いているハンドルがすべて閉じられると、PnP マネージャーは、デバイスのドライバーに\_デバイスの要求を[**削除\_、IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)を送信します。 各ドライバーは、デバイススタックからデタッチされ、そのデバイスオブジェクトを削除します。

7.  突然の削除 (Windows 98/Me)

    Windows 98/Me では、警告を表示せずにデバイスを削除した場合、ドライバーが[**IRP\_\_突然\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)されることはありません。 PnP マネージャーは、 **\_デバイス\_削除する IRP\_** のみを送信します。 WDM ドライバーには、\_予期しない**irp\_\_** を処理するコードが含まれ\_ている必要があります。これには、 **\_デバイス**(突然の削除のための Windows 2000 およびそれ以降の動作) と IRP の\_が削除されます。 **\_デバイスを削除**しても、前に削除された\_IRP (Windows 98/Me 動作) は不要です。\_

8.  失敗した開始後に削除する (Windows 2000 以降)

    デバイス用のドライバーの1つが **\_デバイスを起動\_、irp\_** 失敗した場合、PnP マネージャーは、デバイススタックへの\_デバイスの要求を**削除\_、\_irp**を送信します。 このように remove IRP を使用すると、デバイスのすべてのドライバーに、デバイスが正常に開始されなかったことが通知されます。 Irp\_に応答して **\_デバイスの irp\_削除**すると、デバイスのドライバーによって開始操作が元に戻され (start IRP が成功した場合)、その*AddDevice*操作が元に戻されます。 PnP マネージャーは、このようなデバイスを "失敗した開始" としてマークします。

    この動作は、Windows 2000 以降のプラットフォームにのみ適用されます。 Windows 98/Me では、PnP マネージャーは、障害が発生した場合に応答して **\_デバイスの\_を停止**して、IRP\_を送信します。

PnP デバイス用のドライバーは、通常の remove IRP 遷移を示す図に示されているものよりも多くの状況で、 **irp\_\_\_** を実行します。 たとえば、ユーザーが PC カードをコンピューターに挿入し、デバイスを起動する前に削除することができます。 この場合、PnP マネージャーは、ドライバーの*AddDevice*ルーチンが呼び出された後、 **irp\_\_を実行**する前に、デバイスの要求\_開始する前に、突然削除される irp を発行します。 PnP デバイスのドライバーは、ドライバーの*AddDevice*ルーチンが呼び出された後、いつでも削除 irp を処理できるように準備する必要があります。

 

 




