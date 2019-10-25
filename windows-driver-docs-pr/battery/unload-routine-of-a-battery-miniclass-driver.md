---
title: バッテリ ミニクラス ドライバーの Unload ルーチン
description: バッテリ ミニクラス ドライバーの Unload ルーチン
ms.assetid: f0acbf94-95d1-4a9d-aafd-1f868c5560cc
keywords:
- バッテリ miniclass ドライバー WDK、ルーチン
- アンロードルーチン
- デバイスのアンロードの検証
- デバイスのアンロード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 945739174fad68a6eb11307b5808696156006d6c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832211"
---
# <a name="unload-routine-of-a-battery-miniclass-driver"></a>バッテリ ミニクラス ドライバーの Unload ルーチン


## <span id="ddk_unload_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_UNLOAD_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


バッテリ miniclass ドライバーの*Unload*ルーチンにより、すべてのドライバーのデバイスが削除され、miniclass ドライバーが割り当てたすべてのリソースが解放されます。

*Unload*ルーチンは、まず、すべてのデバイスが削除されていることを確認し、存在しない場合は、残りのデバイスごとに次の手順を実行します。

1.  [**BatteryClassUnload**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassunload)を呼び出して、miniclass ドライバーによってデバイスがアンロードされていることをクラスドライバーに通知します。

2.  そのドライバーのインターフェイスを使用して、ACPI ドライバーなど、下位のドライバーからのデバイス通知を無効にします。

3.  次のように[**Iodeletedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)を呼び出して、デバイスのデバイスオブジェクトを削除します。

    ```cpp
        IoDeleteDevice (NewBatt->DeviceObject);
    ```

すべての miniclass ドライバーのデバイスがアンロードされた後、*アンロード*ルーチンは、miniclass ドライバーによって割り当てられたすべてのリソースを解放します。

Miniclass ドライバーの*Unload*ルーチンは、すべてのドライバーのデバイスが削除された後でいつでも呼び出すことができます。 PnP マネージャーは、IRQL = パッシブ\_レベルでシステムスレッドのコンテキストで*アンロード*ルーチンを呼び出します。

 

 




