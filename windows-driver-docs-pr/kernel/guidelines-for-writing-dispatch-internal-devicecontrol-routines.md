---
title: Dispatch(Internal)DeviceControl ルーチンの記述に関するガイドライン
description: Dispatch(Internal)DeviceControl ルーチンの記述に関するガイドライン
ms.assetid: e64ab28e-2904-41c2-a262-405bc129b9bb
keywords:
- ディスパッチルーチン WDK カーネル、DispatchDeviceControl ルーチン
- ディスパッチルーチン WDK カーネル、DispatchInternalDeviceControl ルーチン
- DispatchDeviceControl ルーチン
- DispatchInternalDeviceControl ルーチン
- IRP_MJ_DEVICE_CONTROL i/o 関数のコード
- IRP_MJ_INTERNAL_DEVICE_CONTROL i/o 関数のコード
- 内部デバイス制御ディスパッチルーチン WDK カーネル
- デバイス制御ディスパッチルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f05993e9bad112784cbf27352986328fde22fc96
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836677"
---
# <a name="guidelines-for-writing-dispatchinternaldevicecontrol-routines"></a>Dispatch(Internal)DeviceControl ルーチンの記述に関するガイドライン





[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)または[*DispatchInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンを記述するときは、次の点に注意してください。

少なくとも、より高いレベルのドライバーでは、irp 内の独自の i/o スタックの場所から、\_CONTROL または[**irp\_MJ\_内部\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)に対する[ **\_デバイスのパラメーター\_MJ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)をコピーする必要があります。次に下位レベルのドライバーの i/o スタックの場所に移動します。 次に、それ以降のドライバーのデバイスオブジェクトと IRP へのポインターを指定して[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出す必要があります。

上位レベルのドライバーは、 **IoCallDriver**によって返された状態値を伝達するか、または、ドライバーを同期的に処理する要求の制御を返すときに返される IRP の i/o status ブロックで設定する必要があります。

基になるデバイスドライバーは、その代わりにこれらの要求のサブセットを完了する密接に結合されたクラスドライバーがない限り、デバイス制御要求を処理する必要があります。 通常、デバイスドライバーの*DispatchDeviceControl*ルーチンは、各 IRP の i/o スタックの場所で**DeviceIoControl コード**を有効にすることで、これらの要求の処理を開始します。

下位レベルのデバイスドライバーでは、要求と共に渡されたパラメーターを確認し、パラメーターが無効な場合は、適切なエラーで IRP を失敗させる必要があります。 これらの要求に対するパラメーターの有効性を確認するための最も一般的なチェックは、次のような形式です。

```cpp
    if (Irp->Parameters.DeviceIoControl.InputBufferLength < 
            (sizeof(IOCTL_SPECIFIC_STRUCTURE))) { 
        status = STATUS_XXX;
```

または
```cpp
    if (Irp->Parameters.DeviceIoControl.OutputBufferLength < 
            (sizeof(IOCTL_SPECIFIC_STRUCTURE))) { 
        status = STATUS_XXX; 
```

状態の値が設定されている状態\_バッファー\_\_が小さすぎるか、状態\_無効な\_パラメーターです。
すべてのデバイスドライバーの*DispatchDeviceControl*または*DispatchInternalDeviceControl*ルーチンは、i/o 状態ブロックに適切な NTSTATUS 値を設定し、その**値を設定して、認識されていない i/o 制御コードの受信を処理する必要があります。情報**フィールドをゼロにし、IO の優先*順位*を持つ IRP を完了すると\_\_インクリメントされません。

デバイスドライバーハンドルの特定の i/o 制御コードには、同じ種類のデバイスに対して、デバイスの種類に固有のシステム定義の i/o 制御コードを含める必要があります。 各種類のデバイスのシステム要件および対応する (Windows SDK) ヘッダーファイルに関する詳細については、Windows Driver Kit (WDK) のデバイス固有のセクションを参照してください。それぞれがプレフィックス*ntdd*で始まり、これらの i/o 制御コード用のシステム定義の構造体。

密接に結合されたクラス/ポートドライバーペアのクラスドライバーは、基になるポートドライバーに渡すことなく、デバイス制御要求のサブセットを処理および完了できます。 ただし、このようなクラスドライバーは、デバイスの状態の変更を必要とするすべての有効なデバイス制御要求と、デバイスに関する揮発性情報 (現在のボーレート、ボリューム、またはビデオモードなど) を返す必要があるすべてのデバイス制御要求に渡す必要があります。

 

 




