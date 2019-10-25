---
title: 最下位レベル ドライバーの DispatchDeviceControl
description: 最下位レベル ドライバーの DispatchDeviceControl
ms.assetid: 51caacd3-c9e0-450e-9060-f308ab46b5a0
keywords:
- ディスパッチルーチン WDK カーネル、DispatchDeviceControl ルーチン
- ディスパッチ DispatchDeviceControl ルーチン
- IRP_MJ_DEVICE_CONTROL i/o 関数のコード
- デバイス制御ディスパッチルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6a872bc8549c12482f4089dd09855ad609b8c42
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836865"
---
# <a name="dispatchdevicecontrol-in-lowest-level-drivers"></a>最下位レベル ドライバーの DispatchDeviceControl





最小レベルのドライバーに対する制御要求である[**IRP\_MJ\_デバイス\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)は、ドライバーがデバイスの状態を変更するか、デバイスの状態に関する情報を提供する必要があります。 多くの種類のドライバーは多数の i/o 制御コードを処理する必要があるため、 [*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンには通常、次のような**switch**ステートメントが含まれています。

```cpp
    :    : 
switch (irpSp->Parameters.DeviceIoControl.IoControlCode)
{ 
    case IOCTL_DeviceType_XXX: 
    case IOCTL_DeviceType_YYY: 
        if (irpSp->Parameters.DeviceIoControl.InputBufferLength < 
                (sizeof(IOCTL_XXXYYY_STRUCTURE)))
        { 
            status = STATUS_BUFFER_TOO_SMALL; 
            break; 
        } else { 
            IoMarkIrpPending(Irp); 
     :    : // pass IRP on for further processing 
    case ... 
     :    :
```

このコードフラグメントに示すように、 *DispatchDeviceControl*ルーチンは、ドライバーがサポートする必要がある i/o 制御コード (場合によっては、これらの i/o 制御コードのグループ) でもパラメーターをチェックします。

デバイスドライバーの*DispatchDeviceControl*ルーチンには、次の実装ガイドラインを考慮してください。

-   *DispatchDeviceControl*は、「 [irp の完了](completing-irps.md)」で説明されているように、パラメーターの有効性を確認し、パラメーターエラーを含む irp をすぐに完了する必要があります。

-   有効なパラメーターをテストするときに、 **case**ステートメントの i/o 制御コードをグループ化することは、ドライバーのパフォーマンス、サイズ、コードのメンテナンスにおいて経済的です。 前のコードフラグメントに示すように、一般的な構造を使用する i/o 制御コードは、このような**ケース**グループの自然候補です。

-   *DispatchDeviceControl*ルーチンが満たす i/o 制御コードを最初に切り替えて IRP を完了すると、ドライバーは制御を速く返すことができるため、パフォーマンスが向上します。

-   要求の頻度が低い操作を指定する i/o 制御コードで後から切り替えると、 **IRP\_MJ\_デバイス\_制御**要求を処理するときのドライバーのパフォーマンスが向上します。

-   パフォーマンスを向上させるために、すべての最下位レベルのデバイスドライバーの*DispatchDeviceControl*ルーチンは、IRP を他のドライバールーチンにキューすることなく、可能なすべてのデバイス制御要求を満たしている必要があります。

DispatchDeviceControl ルーチンが IRP を完了できる場合は、 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して、\_\_IO の優先*順位*をにする必要があります。 後続の処理のために*DispatchDeviceControl*ルーチンが IRP をキューに追加する必要がある場合は、 [**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)と戻りステータス\_PENDING を呼び出す必要があります。

 

 




