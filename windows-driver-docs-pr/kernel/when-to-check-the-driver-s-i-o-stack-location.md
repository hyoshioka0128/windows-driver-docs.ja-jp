---
title: ドライバーの I/O スタック位置を確認すべき場合
description: ドライバーの I/O スタック位置を確認すべき場合
ms.assetid: ca084221-7b07-4db0-a987-9dd8a66d169c
keywords:
- ディスパッチルーチン WDK カーネル、i/o スタックの場所
- I/o スタックの場所 WDK ディスパッチルーチン
- ドライバー i/o スタックの場所 WDK ディスパッチルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 123c684563f9ffc4dc55071110c3d15515a9614e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835745"
---
# <a name="when-to-check-the-drivers-io-stack-location"></a>ドライバーの I/O スタック位置を確認すべき場合





主要な i/o 関数のコードは、受信する各 IRP のドライバーの[i/o スタックの場所](i-o-stack-locations.md)に設定されます。

ドライバーのディスパッチルーチンは、次のいずれかの条件を満たす場合に、IRP に対してドライバーの i/o スタックの場所を調べて、どのような処理を行うかを決定する必要があります。

-   ディスパッチルーチンでは、複数の主要な i/o 関数コードが処理されます。

-   ディスパッチルーチンは、特定の主要な関数コードの一連のマイナー関数コードを処理する必要があります。 マイナー関数コードを持つ Irp には、 [**irp\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)と[**irp\_MJ\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)、および SCSI ポートドライバーとファイルシステムドライバーが処理する必要がある特定の irp が含まれます。

-   デバイスドライバーまたは密接に結合された上位レベルのドライバーのディスパッチルーチンは、 [**irp\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)または[**irp\_MJ\_内部\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)要求を処理します。これには、i/o 制御コードのセットが関連付けられています。

ドライバーの i/o スタックの場所へのポインターを取得するには、そのディスパッチルーチンが[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出します。

上位レベルのドライバーのディスパッチルーチンは、常に**Iogetシャー**ドを呼び出します。また、 [**Iogetnextiシャー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)ドの場所を呼び出して、次に小さいドライバーの i/o スタックの場所へのポインターを取得します。これは、 [irp がドライバースタックを通過](passing-irps-down-the-driver-stack.md)するときに、次の下位のドライバーに対して設定されます。

デバイスドライバーの[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンまたは[*DispatchInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチン (場合によっては、密接に結合されたクラスドライバー) は、各要求の**DeviceIoControl**にあるドライバーの i/o スタックの場所に設定されている i/o 制御コードを判断する必要があります。 I/o 制御コードは、ドライバーの i/o スタックの場所に含まれています。

ほとんどの場合、上位レベルのドライバーの*DispatchDeviceControl*または*DispatchInternalDeviceControl*ルーチンは、irp 内のスタック位置を設定した後に、 **irp\_MJ\_デバイス\_CONTROL**または**irp\_MJ\_内部\_デバイス\_** の制御要求を次の下位のドライバーに渡します。 ただし、scsi クラスドライバーは、特定の[Scsi ポートの i/o 制御コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を確認してから、これらの要求に渡す前に scsi ポートドライバーの i/o スタックの場所を正しく設定できるようにする必要があります。

 

 




