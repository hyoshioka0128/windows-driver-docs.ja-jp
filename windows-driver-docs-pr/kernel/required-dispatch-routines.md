---
title: 必須のディスパッチ ルーチン
description: 必須のディスパッチ ルーチン
ms.assetid: 9b760ac7-7f31-47ad-bf84-7d79c6b24ebd
keywords:
- 必要なディスパッチ ルーチン WDK カーネル
- 必要なディスパッチ ルーチン WDK カーネル
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.openlocfilehash: e3dc9f6943eeb0cc4369009413e289abdaa86ed3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324504"
---
# <a name="required-dispatch-routines"></a>必須のディスパッチ ルーチン

ほとんどのドライバーは、次を処理する必要があります*ディスパッチ*ルーチン。

-   [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_PNP** ](https://msdn.microsoft.com/library/windows/hardware/ff550772) PnP デバイスの認識機能、ハードウェア構成、またはリソースの割り当てに関連する要求を示します。 通常、このような要求は PnP マネージャーと密接に結合されたより高度なドライバーからのデバイス ドライバーに送信されます。

-   [*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784)デバイスまたはシステムの電源の状態に関連する要求を示します。 このような要求は、電源マネージャーまたは密接に結合されたより高度なドライバーのいずれかによって、デバイス ドライバーに送信されます。

-   [*DispatchCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff550729)ユーザー モードの保護されたサブシステムをするかを示します可能性がありますに代わって、アプリケーションまたはサブシステムに固有のドライバーが要求されたとき、ハンドルをファイル オブジェクトに関連付けられているため、ターゲット デバイス オブジェクト、またはより高度なドライバーが接続またはターゲットのデバイス オブジェクトにそのデバイス オブジェクトをアタッチします。

-   [*DispatchClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_閉じる**](https://msdn.microsoft.com/library/windows/hardware/ff550720)ターゲットがされたファイル オブジェクトの最後のハンドルに関連付けられていることを示すデバイス オブジェクトを閉じるし、リリースします。 すべての I/O 要求を完了またはキャンセル、ファイル オブジェクト ポインターへの未解決の参照がないのでされました。

-   [*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794)基になる物理デバイスから、システムにデータを転送する I/O 要求を示します。

-   [*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff550819)システムからデータを基になる物理デバイスに転送する I/O 要求を示します。

-   [*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)デバイスの種類に固有の操作を指定する、システム定義のデバイス固有の種類 I/O 制御コードを含む要求を示します。 高度なドライバーは、通常はデバイスにアクセスして、要求を処理する、基になるデバイス ドライバーにこれらの Irp を渡します。

-   [*DispatchInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)で通常は、密接に結合されたより高度なドライバーからほとんどの場合、デバイス ドライバーに送信要求を示します、プライベート定義されている、ドライバー固有とデバイス固有の種類またはデバイス固有 I/O コントロール コード デバイス固有の種類またはデバイスに固有の操作を要求します。

    ドライバーの特定の種類のみでは、特定の SCSI ドライバー、キーボードまたはマウス デバイス ドライバーでは、システムから提供されたドライバーと相互運用可能な並列ドライバーなど、システム定義の内部デバイス I/O コントロール要求を処理する必要があります。

-   [*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_システム\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550813)ドライバーへの WMI 要求を指定するために使用します。 WMI の詳細については、次を参照してください。 [Windows Management Instrumentation](implementing-wmi.md)します。

ドライバーを提供する必要があるディスパッチ ルーチンは、型および基になる物理デバイスの機能によって異なります。 デバイス固有の種類のドライバーを処理する必要があります IRP 主な機能のコードについては、デバイスの種類の特定のドキュメントで Windows Driver Kit (WDK) を参照してください。

 

 




