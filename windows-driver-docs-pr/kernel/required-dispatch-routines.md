---
title: 必須のディスパッチ ルーチン
description: 必須のディスパッチ ルーチン
ms.assetid: 9b760ac7-7f31-47ad-bf84-7d79c6b24ebd
keywords:
- ディスパッチルーチン WDK カーネル、必須
- 必要なディスパッチルーチン WDK カーネル
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.openlocfilehash: eb42ff5bb4a781c129f61f8ee85b1ed72e319215
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836469"
---
# <a name="required-dispatch-routines"></a>必須のディスパッチ ルーチン

ほとんどのドライバーは、次の*ディスパッチ*ルーチンを処理する必要があります。

-   [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_pnp**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)は、pnp デバイス認識、ハードウェア構成、またはリソース割り当てに関連する要求を示します。 通常、このような要求は、PnP マネージャーまたは密接に結合された上位レベルのドライバーからデバイスドライバーに送信されます。

-   [*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)は、デバイスまたはシステムの電源状態に関する要求を示します。 このような要求は、電源マネージャーまたは密接に結合された上位レベルのドライバーのいずれかによってデバイスドライバーに送信されます。

-   [*DispatchCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)は、ユーザーモードで保護されたサブシステム (アプリケーションまたはサブシステム固有のドライバーに代わって) が、ターゲットデバイスオブジェクトに関連付けられているファイルオブジェクトのハンドルを要求したかどうかを示します。上位レベルのドライバーは、デバイスオブジェクトをターゲットデバイスオブジェクトに接続または接続しています。

-   [*DispatchClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_CLOSE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)は、ターゲットデバイスオブジェクトに関連付けられていたファイルオブジェクトの最後のハンドルが閉じられ、解放されたことを示します。 すべての i/o 要求が完了または取り消されたため、ファイルオブジェクトポインターへの未処理の参照はありません。

-   [*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)は、基になる物理デバイスからシステムにデータを転送するための i/o 要求を示します。

-   [*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_WRITE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)は、システムから基になる物理デバイスにデータを転送する i/o 要求を示します。

-   [*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)は、デバイスの種類に固有の操作を指定する、システム定義のデバイスタイプ固有の i/o 制御コードを含む要求を示します。 上位レベルのドライバーは、これらの Irp を基になるデバイスドライバーに渡します。通常は、デバイスにアクセスして要求を処理します。

-   [*DispatchInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)は、ほとんどの場合、特にプライベートに定義されたドライバー固有のドライバーにより、デバイスドライバーに要求が送信されることを示します。デバイスタイプ固有またはデバイス固有の操作を要求しているデバイスタイプ固有またはデバイス固有の i/o 制御コード。

    特定の SCSI ドライバー、キーボードまたはマウスデバイスドライバー、システムによって提供されるドライバーと相互運用可能なパラレルドライバーなど、システムによって定義された内部デバイス i/o 制御要求を処理するために必要なのは、特定の種類のドライバーのみです。

-   [*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_SYSTEM\_CONTROL**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)を使用して、ドライバーに対する WMI 要求を指定します。 WMI の詳細については、「 [Windows Management Instrumentation](implementing-wmi.md)」を参照してください。

ドライバーが提供する必要があるディスパッチルーチンは、基になる物理デバイスの種類と機能によって異なります。 ドライバーが処理する必要がある IRP 主要関数コードに関するデバイスタイプ固有の情報については、Windows Driver Kit (WDK) のデバイスタイプに固有のドキュメントを参照してください。

 

 




