---
Description: Instead of using the I/O Request Packet (IRP) mechanism, a USB client driver can get a reference to a bus driver interface and use it to access bus driver routines.
title: バス ドライバー インターフェイスの照会
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17449c4945716f83b336ea2e4d74acc1485ab166
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549803"
---
# <a name="querying-for-bus-driver-interfaces"></a>バス ドライバー インターフェイスの照会


I/O 要求パケット (IRP) メカニズムを使用する代わりに USB クライアント ドライバーは、バス ドライバー インターフェイスへの参照を取得し、バス ドライバーのルーチンへのアクセスに使用できます。




クライアント ドライバーにいくつかの利点は、バス ドライバー インターフェイスを使用します。

-   IRP を割り当てずに、インターフェイスのサービスを使用できます。

-   発生した IRQL でインターフェイスのルーチンを呼び出すことができます。

Windows Vista の USB クライアント ドライバー自体は公開できますを支援するためのインターフェイス、[共通クラス ジェネリック親ドライバーを USB](usb-common-class-generic-parent-driver.md)で、管理対象デバイスのインターフェイスのコレクションを定義します。

クライアント ドライバーを送信する必要があります、バス ドライバー インターフェイスを取得する、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff551687)バス ドライバーに要求します。 クライアントは、ドライバー。

1.  作成型 IRP の IRP\_MN\_クエリ\_スタックの次の場所でインターフェイス。
    ```cpp
    irpstack = IoGetNextIrpStackLocation(irp);
    irpstack->MajorFunction= IRP_MJ_PNP;
    irpstack->MinorFunction= IRP_MN_QUERY_INTERFACE;
    ```

2.  インターフェイスのメモリの割り当てし、新しいメモリを指して、スタックを作成します。 メモリを割り当てる例については、 [ **USB\_BUS\_インターフェイス\_USBDI\_V0** ](https://msdn.microsoft.com/library/windows/hardware/ff539210)インターフェイス。
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

5.  呼び出す[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)を下位のスタックのクエリ インターフェイス IRP を渡します。
    ```cpp
    ntStatus = IoCallDriver(PDO that the client passes URBs to, irp);
    ```

USB の詳細についてを参照してくださいをインターフェイスの[USB クライアント ドライバー、バス ドライバー インターフェイス ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff540134#usbdi)します。

## <a name="related-topics"></a>関連トピック
[USB デバイスの Windows クライアント ドライバーの開発](usb-driver-development-guide.md)  



