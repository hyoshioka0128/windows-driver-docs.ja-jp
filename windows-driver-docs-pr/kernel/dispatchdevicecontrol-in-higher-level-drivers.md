---
title: 上位レベルのドライバーでの DispatchDeviceControl
description: 上位レベルのドライバーでの DispatchDeviceControl
ms.assetid: baff49c4-8764-4b65-84f4-ce5e10d51ed2
keywords:
- ディスパッチルーチン WDK カーネル、DispatchDeviceControl ルーチン
- ディスパッチ DispatchDeviceControl ルーチン
- IRP_MJ_DEVICE_CONTROL i/o 関数のコード
- デバイス制御ディスパッチルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: af07f82fd6aed65b7797824ffff006f4de07af3a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838731"
---
# <a name="dispatchdevicecontrol-in-higher-level-drivers"></a>上位レベルのドライバーでの DispatchDeviceControl





通常、上位レベルのドライバーの[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、次の下位レベルのドライバーの i/o スタックの場所を設定し、IRP を[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)に渡します。 *DispatchDeviceControl*ルーチンは、ほとんどの場合、入力 IRP のパラメーターの有効性をチェックします。これは、基になるデバイスドライバーに、各デバイスタイプ固有 i/o 制御要求の処理方法についてのより適切な情報があると見なされるためです。

この一般的な規則の例外として、クラス/ポートドライバーペアのクラスドライバーの*DispatchDeviceControl*ルーチンが考えられます。 ペアリングされたクラス/ポートドライバーでのデバイス制御要求の処理の詳細については、[クラス/ポートドライバーでのディスパッチ (内部) DeviceControl](dispatch-internal-devicecontrol-in-class-port-drivers.md)に関する説明を参照してください。

特定のデバイスドライバーに密接に関連付けられていない新しい上位レベルのドライバーは、単に次の下位レベルのドライバーの[i/o スタックの場所](i-o-stack-locations.md)を設定し、 [**IRP\_MJ\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求に渡す必要があります。処理を続行します。

通常、デバイス制御要求は同期的に処理されます。 つまり、上位レベルのドライバーの*DispatchDeviceControl*ルーチンは、次のようにシステムに制御を返すことがよくあります。

```cpp
        :    : 
    return IoCallDriver(DeviceObject->NextDeviceObject, Irp);
```

ただし、下位のドライバーがそのような要求について\_保留状態を返す可能性がある場合、上位レベルのドライバーでは上記の手法を使用できません。 その場合、高レベルのドライバーは[**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出して[*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを登録する必要があります。 *Iocompletion*ルーチンが呼び出されると、i/o 状態ブロックを確認して、IRP がまだ保留中かどうかを確認できます。 そうである場合、 *Iocompletion*ルーチンは、要求を再試行するか、 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出す前に[**IOMARKIRPP終了**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出して、状態\_PENDING を返します。 上位レベルのドライバーは、最初にその IRP に対して**Iomarkirppending**を呼び出していない限り、状態\_保留中の irp を完了することはできません。

基になるデバイスドライバーが、要求を完了する前にデバイスから転送されるデータを大量に処理する必要がある場合、上位レベルのドライバーがこのようなデバイス制御要求を非同期に処理する可能性があります。 つまり、高いレベルのドライバーが[**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出して*iocompletion*ルーチンを登録し、その IRP を下位のドライバーに渡して、独自の*DispatchDeviceControl*ルーチンから制御を返す場合があります。

システムで定義されているほとんどすべての i/o 制御コードでは、基になるデバイスドライバーで転送できるデータの量は限られています。通常、ページ\_サイズよりもはるかに小さくなります。 一般的なルールとして、上位レベルのドライバーでは、これらの要求を同期的に処理する必要があります。これは、下位のドライバーが制御を迅速に返すためです。 つまり、上位レベルのドライバーの*Iocompletion*ルーチンを呼び出すことによるオーバーヘッドによって、この短い間隔でドライバーが実行できるその他の IRP 処理については補正されません。

基になるデバイスドライバーの[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)で irp を割り当てる上位レベルのドライバーは、これらのデバイス制御要求を同期的に処理できます。 上位レベルのドライバーは、オプションのイベントオブジェクトが**IoBuildDeviceIoControlRequest**に渡され、ドライバーによって割り当てられる IRP に関連付けられるのを待機できます。

 

 




