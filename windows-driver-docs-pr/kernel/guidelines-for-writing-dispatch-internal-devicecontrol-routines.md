---
title: ディスパッチ (内部) デバイスのルーチンを記述するためのガイドライン
description: ディスパッチ (内部) デバイスのルーチンを記述するためのガイドライン
ms.assetid: e64ab28e-2904-41c2-a262-405bc129b9bb
keywords:
- ディスパッチ ルーチンの WDK カーネル、DispatchDeviceControl ルーチン
- ディスパッチ ルーチンの WDK カーネル、DispatchInternalDeviceControl ルーチン
- DispatchDeviceControl ルーチン
- DispatchInternalDeviceControl ルーチン
- IRP_MJ_DEVICE_CONTROL I/O 関数のコード
- IRP_MJ_INTERNAL_DEVICE_CONTROL I/O 関数のコード
- デバイスの内部コントロール ディスパッチ ルーチン WDK カーネル
- デバイス制御ディスパッチ ルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 588966e1a0767a9201345d00cf6205d833bd9e51
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537166"
---
# <a name="guidelines-for-writing-dispatchinternaldevicecontrol-routines"></a>ディスパッチ (内部) デバイスのルーチンを記述するためのガイドライン





書き込み時に、次の点を留意してください、 [ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)または[ *DispatchInternalDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

高度なドライバーには、少なくとものパラメーターをコピーする必要があります、 [ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)または[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766) IRP では、独自 I/O スタックの場所から、[次へ] の下位レベルのドライバーの I/O スタックの場所への要求。 呼び出す必要がありますし、 [**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)次の下位ドライバーのデバイス オブジェクトと IRP へのポインター。

高度なドライバーがによって返される状態値を反映する必要があります**保留**または下位のドライバーを同期的に処理する要求の制御が戻ったときに返される IRP の I/O の状態のブロックに設定します。

基になるデバイス ドライバーは、自身のためにこれらの要求のサブセットが完了すると密接に結合されたクラス ドライバーがない限り、デバイス制御要求を処理する必要があります。 デバイス ドライバーの*DispatchDeviceControl*ルーチンがオンにしてこれらの要求の処理を開始して、通常は、 **Parameters.DeviceIoControl.IoControlCode** I/O で各 IRP の場所をスタックします。

低レベル デバイス ドライバーには、パラメーターが渡される要求と、任意のパラメーターが有効でない場合は、該当するエラーにより IRP を失敗を確認する必要があります。 これらの要求にパラメーターの有効性の最も一般的なチェックでは、フォームがあります。

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

ステータス値のセットは、状態のいずれかで\_バッファー\_すぎます\_小規模または状態\_無効な\_パラメーター。
すべてのデバイス ドライバーの*DispatchDeviceControl*または*DispatchInternalDeviceControl*ルーチンが使用されたブロックを I/O の状態を設定して I/O 制御コードを認識できませんの受信を処理する必要があります、NTSTATUS 値の適切な設定をその**情報**フィールドをゼロにしてで IRP の完了を*PriorityBoost* IO の\_いいえ\_インクリメント。

デバイス ドライバーを処理する特定の I/O 制御コードは、デバイス固有の型、システム定義されている I/O 制御コードの同じ種類のデバイスを含める必要があります。 詳細については、デバイスと対応する (Windows SDK) のヘッダー ファイル、プレフィックスで始まるの種類ごとのシステム要件は Windows Driver Kit (WDK) のデバイスに固有のセクションを参照して*ntdd*のこれらの I/O 制御コードのシステム定義の構造体の宣言。

クラス/ポートに密接に結合されたドライバーの組のクラス ドライバーは処理し、デバイス制御要求のサブセットを基になるポート ドライバーに渡すことがなく完了できます。 ただし、このようなクラス ドライバーは、デバイス、および揮発性については、その現在のボー レート、ボリューム、またはビデオ モードなど、デバイスの戻り値を必要とする対象の状態の変更を必要とするすべての有効なデバイス制御要求に渡す必要があります。

 

 




