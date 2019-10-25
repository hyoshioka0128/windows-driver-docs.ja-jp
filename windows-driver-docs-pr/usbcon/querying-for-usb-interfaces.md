---
Description: USB クライアントドライバーは、i/o 要求パケット (IRP) メカニズムを使用する代わりに、バスドライバーインターフェイスへの参照を取得し、それを使用してバスドライバールーチンにアクセスできます。
title: バス ドライバー インターフェイスのクエリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d2551f404da196f7d007d5d71649823e1489b1f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824205"
---
# <a name="querying-for-bus-driver-interfaces"></a>バス ドライバー インターフェイスのクエリ


USB クライアントドライバーは、i/o 要求パケット (IRP) メカニズムを使用する代わりに、バスドライバーインターフェイスへの参照を取得し、それを使用してバスドライバールーチンにアクセスできます。




バスドライバーインターフェイスを使用すると、クライアントドライバーにいくつかの利点があります。

-   IRP を割り当てずに、インターフェイスのサービスを使用できます。

-   インターフェイスのルーチンは、発生した IRQL で呼び出すことができます。

Windows Vista USB では、クライアントドライバーは、自身が管理するデバイスのインターフェイスコレクションを定義する際に、 [Usb 共通クラスの汎用親ドライバー](usb-common-class-generic-parent-driver.md)を支援するインターフェイスを公開することができます。

バスドライバーインターフェイスを取得するには、クライアントドライバーが[**IRP\_\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)要求をバスドライバーに送信する必要があります。 クライアントドライバーで、次のようにします。

1.  次のスタックの場所で、型が IRP\_\_クエリ\_インターフェイスの IRP を作成します。
    ```cpp
    irpstack = IoGetNextIrpStackLocation(irp);
    irpstack->MajorFunction= IRP_MJ_PNP;
    irpstack->MinorFunction= IRP_MN_QUERY_INTERFACE;
    ```

2.  インターフェイスにメモリを割り当て、スタックポイントを新しいメモリに設定します。 たとえば、USB\_バス\_インターフェイスにメモリを割り当てる場合は[ **\_USBDI\_V0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbbusif/ns-usbbusif-_usb_bus_interface_usbdi_v0)インターフェイスを使用します。
    ```cpp
    irpstack->Parameters.QueryInterface.Interface = (USB_BUS_INTERFACE_USBDI_V0) newly allocated interface buffer;
    ```

3.  **InterfaceSpecificData**を NULL に設定します。
    ```cpp
    irpstack->Parameters.QueryInterface.InterfaceSpecificData = NULL;
    ```

4.  適切なインターフェイス GUID、インターフェイスのサイズ、およびインターフェイスのバージョンを使用して、IRP スタックを初期化します。
    ```cpp
    irpstack->Parameters.QueryInterface.InterfaceType = &USB_BUS_INTERFACE_USBDI_GUID;
    irpstack->Parameters.QueryInterface.Size = sizeof(USB_BUS_INTERFACE_USBDI_V0);
    irpstack->Parameters.QueryInterface.Version = USB_BUSIF_USBDI_VERSION_0;
    ntStatus = IoCallDriver(PDO that the client passes URBs to, irp);
    ```

5.  [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出して、クエリインターフェイスの IRP をスタックに渡します。
    ```cpp
    ntStatus = IoCallDriver(PDO that the client passes URBs to, irp);
    ```

USB インターフェイスの詳細については、「 [Usb クライアントドライバーのバスドライバーインターフェイスルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#usbdi)」を参照してください。

## <a name="related-topics"></a>関連トピック
[USB デバイス用の Windows クライアントドライバーの開発](usb-driver-development-guide.md)  



