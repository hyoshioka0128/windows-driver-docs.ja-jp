---
title: バッテリ ミニクラス ドライバーの Unload ルーチン
description: バッテリ ミニクラス ドライバーの Unload ルーチン
ms.assetid: f0acbf94-95d1-4a9d-aafd-1f868c5560cc
keywords:
- バッテリ miniclass ドライバー WDK、ルーチン
- ルーチンをアンロードします。
- デバイスの確認をアンロードします。
- デバイスのアンロード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 540aeff00daf0ac359b19a2fc7be4e075620b4f1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335071"
---
# <a name="unload-routine-of-a-battery-miniclass-driver"></a>バッテリ ミニクラス ドライバーの Unload ルーチン


## <span id="ddk_unload_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_UNLOAD_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


*アンロード*バッテリ miniclass ドライバーのルーチンで、ドライバーのデバイスが削除されたすべてのことと、miniclass ドライバーが割り当てられているリソースを解放します。

*アンロード*ルーチンが、すべてのデバイスが削除され、いない場合は、残りのデバイスごとに次の操作のことを確認する必要があります最初。

1.  呼び出す[ **BatteryClassUnload** ](https://msdn.microsoft.com/library/windows/hardware/ff536271) miniclass ドライバーには、デバイスがアンロード中クラス ドライバーに通知します。

2.  ドライバーのインターフェイスを使用して、ACPI ドライバーなどの下位のドライバーからデバイスの通知を無効にします。

3.  デバイスのデバイス オブジェクトを呼び出すことによって削除[ **IoDeleteDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549083)、次のようにします。

    ```cpp
        IoDeleteDevice (NewBatt->DeviceObject);
    ```

Miniclass ドライバーのすべてのデバイスが読み込まれた後は、*アンロード*ルーチンが miniclass ドライバーによって割り当てられているリソースを解放する必要があります。

Miniclass ドライバーの*アンロード*ルーチンは、すべてのドライバーのデバイスが削除された後、いつでも呼び出すことができます。 PnP マネージャー呼び出し、*アンロード*IRQL でシステムのスレッドのコンテキストで日常的なパッシブ =\_レベル。

 

 




