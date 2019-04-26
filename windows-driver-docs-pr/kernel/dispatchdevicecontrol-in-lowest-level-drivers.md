---
title: 最下位レベル ドライバーの DispatchDeviceControl
description: 最下位レベル ドライバーの DispatchDeviceControl
ms.assetid: 51caacd3-c9e0-450e-9060-f308ab46b5a0
keywords:
- ディスパッチ ルーチンの WDK カーネル、DispatchDeviceControl ルーチン
- ディスパッチ DispatchDeviceControl ルーチン
- IRP_MJ_DEVICE_CONTROL I/O 関数のコード
- デバイス制御ディスパッチ ルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e215dccc837f5b32a228ed6dd3b7762c37204260
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350034"
---
# <a name="dispatchdevicecontrol-in-lowest-level-drivers"></a>最下位レベル ドライバーの DispatchDeviceControl





[ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)要求すること、ドライバーがそのデバイスの状態を変更または情報を提供する最下位レベルのドライバーが必要ですについては、そのデバイスの状態。 ほとんどの種類のドライバーがさまざまな I/O 制御コードを処理するために必要なため、 [ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンが通常含まれて、**切り替える**ステートメント次のようなやや:

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

このコード フラグメントに示すよう、 *DispatchDeviceControl*ルーチンでは、パラメーターは、各 I/O コントロール サポート コードをドライバーする必要があります、場合によってこれらの I/O 制御コードのグループにでも確認します。

デバイス ドライバーの次の実装のガイドラインを考慮して*DispatchDeviceControl*ルーチン。

-   *DispatchDeviceControl* 」の説明に従って、有効期間、およびパラメーター エラーをすぐに完全な Irp のパラメーターを確認する必要があります[Irp の完了](completing-irps.md)します。

-   I/O 制御コードをグループ化、**ケース**ステートメント (実際) ときに有効なパラメーターのためのテストは経済性に優れたコードの保守とドライバーのパフォーマンスとサイズの面でします。 上記のコード フラグメントの内容を一般的な構造を使用する I/O 制御コードはこのような自然な候補を**ケース**グループ。

-   切り替え最初の i/o 制御コードを*DispatchDeviceControl*ルーチンが満たすことができる、完全な IRP パフォーマンスが向上、ドライバーが高速化の制御を返すためです。

-   操作も処理でドライバーのパフォーマンスを向上できる頻度を指定する I/O 制御コードの切り替え後で要求された**IRP\_MJ\_デバイス\_コントロール**要求。

-   パフォーマンス向上のため、すべての最下位レベルのデバイス ドライバーの*DispatchDeviceControl*ルーチンは IRP がドライバーの他のルーチンをキューに登録せず、可能なすべてのデバイス制御要求を満たす必要があります。

場合、 *DispatchDeviceControl*ルーチンは IRP を完了することができますを呼び出す必要が[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)で、 *PriorityBoost* IO の\_いいえ\_インクリメントします。 場合、 *DispatchDeviceControl*ルーチンがキューに IRP がさらに処理するため、呼び出す必要があります[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)状態を返すと\_保留します。

 

 




