---
title: 記憶域フィルター ドライバーの I/O 要求サポート
description: 記憶域フィルター ドライバーの I/O 要求サポート
ms.assetid: 2899bf91-584f-47fe-9d5c-3feb07b8707e
keywords:
- ストレージフィルタードライバー WDK、i/o 要求のサポート
- フィルタードライバー WDK storage、i/o 要求のサポート
- SFD WDK storage、i/o 要求のサポート
- Irp WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5675573b90e6872fb899c3996d46b72ff14069fb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844467"
---
# <a name="storage-filter-drivers-support-of-io-requests"></a>記憶域フィルター ドライバーの I/O 要求サポート


## <span id="ddk_storage_filter_driver_s_support_of_i_o_requests_kg"></span><span id="DDK_STORAGE_FILTER_DRIVER_S_SUPPORT_OF_I_O_REQUESTS_KG"></span>


上位レベルのストレージフィルタードライバー (SFD) は、ユーザーアプリケーションと上位レベルのドライバーから Irp をインターセプトし、必要に応じて、次の下位のドライバー (ストレージクラスドライバーまたは他のフィルタードライバー) に渡す前に必要に応じて変更します。 このような SFD は、非標準の形式でデバイスとの間で送受信されるデータの変換や、 [**IRP\_MJ\_デバイスへの応答としてのデバイスのプログラミングなど、特別な処理を必要とする要求に対してデバイス固有のサポートを提供し\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求。

低レベルの SFD は、記憶域クラスドライバーによって発行された SRBs や Irp を監視し、必要に応じて、次の下位のドライバー (ストレージポートドライバーまたは他のフィルタードライバー) に渡す前に、それらを変更します。

上位レベルと下位レベルの SFDs の両方で、より低いドライバーで、特別な処理を必要としないすべての i/o 要求を処理できます。

ストレージクラスドライバーと同様に、SFD には、すべての上位レベルのカーネルモードドライバーに共通の次の要件があります。

-   I/o マネージャーや上位レベルのドライバーが適切な i/o 操作のために Irp を送信できる*ディスパッチ*ルーチンのセットを提供する必要があります。 SFD は、その種類のデバイスのストレージクラスドライバーと同じ IRP\_MJ\_XXX のセットをサポートしている必要があります。

-   [**IRP\_MJ\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求では、その物理デバイスが処理できるクラスドライバーでサポートされている i/o 制御コードの数をサポートする必要があります。また、可能であれば、ドライバーの残りの i/o 制御コードのサポートをエミュレートします。

-   PnP と電源 Irp を処理するために[*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチン、 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチン、[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチン、および*ディスパッチ*ルーチンが必要です。また、 [*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)など、他の標準の上位レベルのドライバールーチンを使用することもできます。必要に応じてルーチン。

-   PnP、電源管理、およびシステム制御の Irp を処理するためのルールに従っている必要があります。

デバイスに特別な機能がある場合、SFD は、システムに必要なデバイスタイプ固有の i/o 制御コードのセットに加えて、 [**IRP\_MJ\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求に対して、システムが必要とする一連の i/o 制御コードをサポートできます。

 

 




