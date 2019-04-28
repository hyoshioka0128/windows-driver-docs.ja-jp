---
Description: I/O 要求パケット (IRP) メカニズムを使用する代わりに USB クライアント ドライバーは、バス ドライバー インターフェイスへの参照を取得し、バス ドライバーのルーチンへのアクセスに使用できます。
title: バス ドライバー インターフェイスのクエリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc0af9d081017db8cb0c3346f27bf9933d274f70
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378856"
---
# <a name="querying-for-bus-driver-interfaces"></a>バス ドライバー インターフェイスのクエリ


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

USB の詳細についてを参照してくださいをインターフェイスの[USB クライアント ドライバー、バス ドライバー インターフェイス ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#usbdi)します。

## <a name="related-topics"></a>関連トピック
[USB デバイスの Windows クライアント ドライバーの開発](usb-driver-development-guide.md)  



