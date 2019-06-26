---
Description: I/O 要求パケット (IRP) メカニズムを使用する代わりに USB クライアント ドライバーは、バス ドライバー インターフェイスへの参照を取得し、バス ドライバーのルーチンへのアクセスに使用できます。
title: バス ドライバー インターフェイスのクエリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 906c726b2f0c2f56faef43a9dbd13bc435df805f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358361"
---
# <a name="querying-for-bus-driver-interfaces"></a>バス ドライバー インターフェイスのクエリ


I/O 要求パケット (IRP) メカニズムを使用する代わりに USB クライアント ドライバーは、バス ドライバー インターフェイスへの参照を取得し、バス ドライバーのルーチンへのアクセスに使用できます。




クライアント ドライバーにいくつかの利点は、バス ドライバー インターフェイスを使用します。

-   IRP を割り当てずに、インターフェイスのサービスを使用できます。

-   発生した IRQL でインターフェイスのルーチンを呼び出すことができます。

Windows Vista の USB クライアント ドライバー自体は公開できますを支援するためのインターフェイス、[共通クラス ジェネリック親ドライバーを USB](usb-common-class-generic-parent-driver.md)で、管理対象デバイスのインターフェイスのコレクションを定義します。

クライアント ドライバーを送信する必要があります、バス ドライバー インターフェイスを取得する、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)バス ドライバーに要求します。 クライアントは、ドライバー。

1.  作成型 IRP の IRP\_MN\_クエリ\_スタックの次の場所でインターフェイス。
    ```cpp
    irpstack = IoGetNextIrpStackLocation(irp);
    irpstack->MajorFunction= IRP_MJ_PNP;
    irpstack->MinorFunction= IRP_MN_QUERY_INTERFACE;
    ```

2.  インターフェイスのメモリの割り当てし、新しいメモリを指して、スタックを作成します。 メモリを割り当てる例については、 [ **USB\_BUS\_インターフェイス\_USBDI\_V0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbbusif/ns-usbbusif-_usb_bus_interface_usbdi_v0)インターフェイス。
    ```cpp
    irpstack->Parameters.QueryInterface.Interface = (USB_BUS_INTERFACE_USBDI_V0) newly allocated interface buffer;
    ```

3.  設定**InterfaceSpecificData**を NULL にします。
    ```cpp
    irpstack->Parameters.QueryInterface.InterfaceSpecificData = NULL;
    ```

4.  適切なインターフェイスの GUID を持つ IRP スタック、インターフェイスのサイズと、インターフェイスのバージョンを初期化します。
    ```cpp
    irpstack->Parameters.QueryInterface.InterfaceType = &USB_BUS_INTERFACE_USBDI_GUID;
    irpstack->Parameters.QueryInterface.Size = sizeof(USB_BUS_INTERFACE_USBDI_V0);
    irpstack->Parameters.QueryInterface.Version = USB_BUSIF_USBDI_VERSION_0;
    ntStatus = IoCallDriver(PDO that the client passes URBs to, irp);
    ```

5.  呼び出す[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)を下位のスタックのクエリ インターフェイス IRP を渡します。
    ```cpp
    ntStatus = IoCallDriver(PDO that the client passes URBs to, irp);
    ```

USB の詳細についてを参照してくださいをインターフェイスの[USB クライアント ドライバー、バス ドライバー インターフェイス ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#usbdi)します。

## <a name="related-topics"></a>関連トピック
[USB デバイスの Windows クライアント ドライバーの開発](usb-driver-development-guide.md)  



