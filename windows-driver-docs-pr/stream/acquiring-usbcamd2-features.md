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
ms.openlocfilehash: 7f034a961b20c35ef596688395fd7973b44c9237
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357186"
---
# <a name="acquiring-usbcamd2-features"></a>USBCAMD2 機能の取得


ポインターを取得する必要があります、 [ **USBCAMD\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff568605) USBCAMD2 の新機能を使用する前に構造体します。 ポインターを取得するためにビルドし、送信、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff551687)カメラ ミニドライバーからの要求[ **SRB\_初期化\_完了**](https://msdn.microsoft.com/library/windows/hardware/ff568182)ハンドラーで、 [ *AdapterReceivePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff554080)コールバック関数。 USBCAMD2 ミニドライバーのライブラリは、この IRP を処理し、型 USBCAMD の直接呼び出しインターフェイスを返します\_カメラ ミニドライバー インターフェイス。 インターフェイスは、基本的に関数ポインターのテーブルです。

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

 

 




