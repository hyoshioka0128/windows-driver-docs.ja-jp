---
title: 記憶域クラス ドライバーの Dispatch ルーチン
description: 記憶域クラス ドライバーの Dispatch ルーチン
ms.assetid: 99713661-5e99-4110-b369-afc084a2aaef
keywords:
- ディスパッチ ルーチン WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f373ea646c63871ead67c04930fd79e659064d5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339051"
---
# <a name="storage-class-drivers-dispatch-routines"></a>記憶域クラス ドライバーの Dispatch ルーチン


## <span id="ddk_storage_class_drivers_dispatch_routines_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_DISPATCH_ROUTINES_KG"></span>


クラス ドライバー [ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)と[ **DispatchClose** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンがないデバイスに固有の要件をある通常します。 ほとんどのストレージ クラス ドライバーが中間のドライバーです。そのディスパッチ ルーチンは状態のみを返す\_成功するより高度なドライバーと、間接的には、ユーザー モード アプリケーションが I/O のデバイスを開くし、その後、デバイスを閉じるように特定のデバイス オブジェクトが存在することを示します。

クラス ドライバー [ **DispatchDeviceControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)と[ **DispatchInternalDeviceControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンは、常駐である必要がありますことはできませんが、。ページング可能なまたはドライバーのページング可能なイメージ] セクションの一部にすることです。 によって、特定の要求の IOCTL、ディスパッチ ルーチンがこのような可能性があります。 ページングされたルーチンを呼び出すか (これにより、実行中のスレッドをブロックする)、同期または通知オブジェクトからの呼び出しを待機がディスパッチ ルーチンは、不明な IOCTL を通じて渡すことがである必要があります。ディスパッチで\_レベル。

ストレージ クラス ドライバーが必要、 [ **DispatchPnP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)日常的なを開始する要求の停止、およびデバイスを削除要求または応答を他の PnP デバイスがページング パス上の通知などです。 PnP 開始要求の処理について詳しくは、次を参照してください。 [、記憶域クラス ドライバーの PnP 開始を処理](handling-pnp-start-in-a-storage-class-driver.md)します。 PnP 他の要求の処理について詳しくは、次を参照してください。[記憶域周辺機器への PnP の要求を処理](handling-pnp-requests-to-storage-peripherals.md)します。

ストレージ クラス ドライバーが必要、 [ **DispatchPower** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンのデバイスの電源状態を設定するための要求。 詳細については、次を参照してください。[記憶域周辺機器に電力の要求を処理](handling-power-requests-to-storage-peripherals.md)します。

ストレージ クラス ドライバーが必要、 [ **DispatchShutdown** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンと、場合によって、 [ **DispatchFlushBuffers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンの場合、デバイスそのデバイスは、によって内部的には、データをキャッシュする HBA バスに接続する場合がありますまたはファイル システムは、クラス ドライバー上に重ねられる場合は、内部的には、データはキャッシュします。 データの整合性を維持するには、システムがシャット ダウンにこのようなキャッシュ デバイスにフラッシュする必要があります。

参照してください[書き込みディスパッチ ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff566407)ディスパッチ ルーチンの一般的な要件の詳細について。

 

 




