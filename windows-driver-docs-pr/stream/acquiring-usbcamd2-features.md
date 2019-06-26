---
title: USBCAMD2 機能の取得
description: USBCAMD2 機能の取得
ms.assetid: 39db38a8-8279-4c61-9010-cc6d4767efc2
keywords:
- Windows 2000 カーネル ストリーミング モデル WDK、USBCAMD2 ミニドライバー ライブラリ
- ストリーミング モデル WDK Windows 2000 カーネル、USBCAMD2 ミニドライバー ライブラリ
- カーネル ストリーミング モデルの WDK、USBCAMD2 ミニドライバー ライブラリ
- WDK Windows 2000 のカーネル ストリーミング USBCAMD2 を機能します。
- USB ベースのストリーミング カメラ WDK USBCAMD2
- カメラ WDK USBCAMD2
- IRP_MN_QUERY_INTERFACE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b6db0717e2266aa112513bc6e9b9f63064935d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386779"
---
# <a name="acquiring-usbcamd2-features"></a>USBCAMD2 機能の取得


ポインターを取得する必要があります、 [ **USBCAMD\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/ns-usbcamdi-usbcamd_interface) USBCAMD2 の新機能を使用する前に構造体します。 ポインターを取得するためにビルドし、送信、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)カメラ ミニドライバーからの要求[ **SRB\_初期化\_完了**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-initialization-complete)ハンドラーで、 [ *AdapterReceivePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-padapter_receive_packet_routine)コールバック関数。 USBCAMD2 ミニドライバーのライブラリは、この IRP を処理し、型 USBCAMD の直接呼び出しインターフェイスを返します\_カメラ ミニドライバー インターフェイス。 インターフェイスは、基本的に関数ポインターのテーブルです。

次のコードをビルドし、IRP を送信する方法を示して\_MN\_クエリ\_カメラ ミニドライバーからインターフェイスの要求。

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

 

 




