---
title: USBCAMD2 機能の取得
description: USBCAMD2 機能の取得
ms.assetid: 39db38a8-8279-4c61-9010-cc6d4767efc2
keywords:
- Windows 2000 カーネルストリーミングモデル WDK、USBCAMD2 ミニドライバーライブラリ
- ストリーミングモデル WDK Windows 2000 カーネル、USBCAMD2 ミニドライバーライブラリ
- カーネルストリーミングモデル WDK、USBCAMD2 ミニドライバーライブラリ
- USBCAMD2 機能 WDK Windows 2000 カーネルストリーミング
- USB ベースのストリーミングカメラの WDK USBCAMD2
- カメラ WDK USBCAMD2
- IRP_MN_QUERY_INTERFACE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 919fb3ebe55b60bab3677ab48601fbad458396e3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843368"
---
# <a name="acquiring-usbcamd2-features"></a>USBCAMD2 機能の取得


新しい USBCAMD2 機能を使用する前に、 [**USBCAMD\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/ns-usbcamdi-usbcamd_interface)構造へのポインターを取得する必要があります。 ポインターを取得するには、 [*Adapterreceivepacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-padapter_receive_packet_routine)コールバックで、\_ミニドライバーの[**SRB 初期化\_完全な**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-initialization-complete)ハンドラーから[ **\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)要求を作成して\_送信します。プロシージャ. USBCAMD2 ミニドライバーライブラリは、この IRP を処理し、カメラミニドライバーに USBCAMD\_インターフェイス型の直接呼び出しインターフェイスを返します。 インターフェイスは、基本的には関数ポインターのテーブルです。

次のコードは、カメラミニドライバーから\_クエリ\_インターフェイス要求の IRP\_を作成して送信する方法を示しています。

```cpp
KeInitializeEvent(&Event, NotificationEvent, FALSE);
Irp = IoBuildSynchronousFsdRequest(
    IRP_MJ_PNP,
    pDeviceObject,
    NULL,
    0,
    NULL,
    &Event,
    &IoStatusBlock);

if (NULL != Irp)
{
    Irp->RequestorMode = KernelMode;
    IrpStackNext = IoGetNextIrpStackLocation(Irp);
    //
    // Create an interface query out of the Irp.
    //
    IrpStackNext->MinorFunction = IRP_MN_QUERY_INTERFACE;
    IrpStackNext->Parameters.QueryInterface.InterfaceType = (GUID*)&GUID_USBCAMD_INTERFACE;
    IrpStackNext->Parameters.QueryInterface.Size = sizeof(*pUsbcamdInterface);
    IrpStackNext->Parameters.QueryInterface.Version = USBCAMD_VERSION_200;
    IrpStackNext->Parameters.QueryInterface.Interface = (PINTERFACE)pUsbcamdInterface;
    IrpStackNext->Parameters.QueryInterface.InterfaceSpecificData = NULL;
    Status = IoCallDriver(pDeviceObject, Irp);
    if (STATUS_PENDING == Status)
    {
        //
        // This  waits using KernelMode so that the stack, and therefore the
        // event on that stack, is not paged out.
        //
        KeWaitForSingleObject(&Event, Executive, KernelMode, FALSE, NULL);
        Status = IoStatusBlock.Status;
    }

}
else
{
    Status = STATUS_INSUFFICIENT_RESOURCES;
}
```

 

 




