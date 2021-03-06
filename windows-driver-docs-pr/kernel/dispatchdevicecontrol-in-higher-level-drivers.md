---
title: 上位レベル ドライバーの DispatchDeviceControl
description: 上位レベル ドライバーの DispatchDeviceControl
ms.assetid: baff49c4-8764-4b65-84f4-ce5e10d51ed2
keywords:
- ディスパッチ ルーチンの WDK カーネル、DispatchDeviceControl ルーチン
- ディスパッチ DispatchDeviceControl ルーチン
- IRP_MJ_DEVICE_CONTROL I/O 関数のコード
- デバイス制御ディスパッチ ルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09dba5e0df1b6fe6906cd9aee278edea2234cd96
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385257"
---
# <a name="dispatchdevicecontrol-in-higher-level-drivers"></a>上位レベル ドライバーの DispatchDeviceControl





通常、 [ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)より高度なドライバーのルーチンは、単に下位レベルの次のドライバーの I/O スタックの場所を設定し、上で、IRP を渡します[ **保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)します。 *DispatchDeviceControl*ルーチンは、基になるデバイス ドライバーは各デバイスの種類に固有の I/O 制御を処理する方法についてより詳細な情報があると見なされますので、ほとんど IRP の入力パラメーターの有効性をチェック要求。

この一般的な規則をする可能性のある例外は、 *DispatchDeviceControl*クラス/ポート ドライバー 1 組のクラス ドライバーで日常的な。 クラス/ポートのペアになっているドライバーでのデバイス制御要求の処理の詳細については、次を参照してください。[クラス/ポート ドライバーにディスパッチ (内部) デバイス](dispatch-internal-devicecontrol-in-class-port-drivers.md)します。

特定のデバイス ドライバーに密接に関連付けられていない任意の新しい高度なドライバーを設定する必要があります、 [I/O スタックの場所](i-o-stack-locations.md)、下位レベルの次のドライバーとパス、 [ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)さらに処理するために要求します。

デバイスの管理要求が同期処理される通常します。 つまりより高度なドライバーの*DispatchDeviceControl*ルーチン頻繁に返せる制御システムに次のようにします。

```cpp
        :    : 
    return IoCallDriver(DeviceObject->NextDeviceObject, Irp);
```

ただしより高度なドライバー場合は使用できません前述のテクニックを下位のドライバーは、状態を返す可能性があります\_このような要求を保留します。 その場合より高度なドライバーを呼び出す必要があります[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)を登録する、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチン。 ときに、 *IoCompletion*ルーチンを呼び出すと、IRP がまだがかどうかを判断する I/O のステータスのブロックを確認できる保留中です。 その場合、 *IoCompletion*ルーチンが要求を再試行しますか、または、場合によっては、 [ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)を呼び出す前に[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)ステータスを返す\_保留します。 高度なドライバーは IRP の状態を完了できません必要があります\_PENDING と呼ばれることがない限り**IoMarkIrpPending**その IRP の最初。

場合は、基になるデバイス ドライバーが要求を完了する前に、デバイスから転送されるデータ量を処理する必要がありますしより高度なドライバー可能性がありますこのようなデバイス制御要求は非同期で処理します。 つまりより高度なドライバーが呼び出す可能性があります[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)を登録する、 *IoCompletion*ルーチンは、下位のドライバーに IRP を渡すしから制御を返す独自*DispatchDeviceControl*ルーチン。

ほぼすべてのシステム定義されている I/O 制御コードは、少量のデータ、通常は大幅に下回るページのみを転送する基になるデバイス ドライバーを必要と\_量。 一般的な規則としてより高度なドライバーが要求を処理これら同期的に、上記のコード フラグメントで示すように下位のドライバー制御を返すようにすばやくためです。 高度なドライバーの呼び出しのオーバーヘッドは、 *IoCompletion*ルーチンがすべて追加 IRP がドライバーの処理が完了できる、このような短い間隔での補償されません。

高度なドライバーの Irp によって割り当てられる[ **IoBuildDeviceIoControlRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)基になるデバイスのドライバー要求を処理できるこれらデバイス制御に同期的にします。 渡される省略可能なイベント オブジェクトの上位レベルのドライバーが待機できる**IoBuildDeviceIoControlRequest** IRP がドライバーに割り当てられたに関連付けられているとします。

 

 




