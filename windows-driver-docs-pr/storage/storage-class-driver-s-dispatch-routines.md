---
title: 記憶域クラス ドライバーの Dispatch ルーチン
description: 記憶域クラス ドライバーの Dispatch ルーチン
ms.assetid: 99713661-5e99-4110-b369-afc084a2aaef
keywords:
- ディスパッチルーチン WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f97249cbe3499cde4a7bfc26ebfe5de2f59e976
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845088"
---
# <a name="storage-class-drivers-dispatch-routines"></a>記憶域クラス ドライバーの Dispatch ルーチン


## <span id="ddk_storage_class_drivers_dispatch_routines_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_DISPATCH_ROUTINES_KG"></span>


クラスドライバーの[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンと[**DispatchClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンには、通常、デバイス固有の要件はありません。 ほとんどのストレージクラスドライバーは、中間ドライバーです。ディスパッチルーチンは、特定のデバイスオブジェクトが存在することを示す状態\_成功だけを返します。これにより、上位レベルのドライバーと間接的にユーザーモードアプリケーションが i/o のデバイスを開き、その後でデバイスを閉じることができます。

クラスドライバーの[**DispatchDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンと[**DispatchInternalDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンが常駐している必要があります。つまり、これらはページング可能ではなく、ドライバーのページング可能なイメージセクションの一部でもありません。 このようなディスパッチルーチンは、特定の要求の IOCTL に応じて、ページングされたルーチンを呼び出したり、同期または通知オブジェクトからの呼び出し (その結果、実行中のスレッドをブロックする) を待機したりすることがありますが、ディスパッチルーチンは、によって不明な IOCTL を渡すことができる必要があります。ディスパッチ\_レベル。

ストレージクラスドライバーは、デバイスを開始、停止、および削除するための[**DispatchPnP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンと、デバイスがページングパスにあるという通知などの他の PnP 要求に応答する必要があります。 PnP 開始要求の処理の詳細については、「[ストレージクラスドライバーでの Pnp 開始の処理](handling-pnp-start-in-a-storage-class-driver.md)」を参照してください。 その他の PnP 要求の処理の詳細については、「[ストレージ周辺機器への Pnp 要求の処理](handling-pnp-requests-to-storage-peripherals.md)」を参照してください。

また、ストレージクラスドライバーには、デバイスの電源状態を設定するように要求するための[**DispatchPower**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンも必要です。 詳細については、「[ストレージ周辺機器への電源要求の処理](handling-power-requests-to-storage-peripherals.md)」を参照してください。

ストレージクラスドライバーには、 [**DispatchShutdown**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンと、デバイスが内部でデータをキャッシュしている場合は[**DispatchFlushBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンが必要です。データを内部的にキャッシュする HBA によってデバイスがバスに接続されている場合、またはファイルシステムの場合は、は、クラスドライバーの上に階層化されています。 データの整合性を維持するには、システムをシャットダウンする前に、このようなキャッシュをデバイスにフラッシュする必要があります。

ディスパッチルーチンの一般的な要件の詳細については、「[ディスパッチルーチンの記述](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines)」も参照してください。

 

 




