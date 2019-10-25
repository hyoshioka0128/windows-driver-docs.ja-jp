---
title: IRP ディスパッチ ルーチンの登録
description: IRP ディスパッチ ルーチンの登録
ms.assetid: 096f4bb7-2326-4e6c-b3db-a2d95ca4982b
keywords:
- IRP ディスパッチルーチンを登録しています
- ディスパッチルーチン WDK ファイルシステム
- IRP ディスパッチルーチン WDK ファイルシステム、登録
- Irp WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c48110d16e9bbba82555e9469e83c7c9e5c8225b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841004"
---
# <a name="registering-irp-dispatch-routines"></a>IRP ディスパッチ ルーチンの登録


## <span id="ddk_registering_irp_dispatch_routines_if"></span><span id="DDK_REGISTERING_IRP_DISPATCH_ROUTINES_IF"></span>


フィルタードライバーの[**Driverobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンの*driverobject*パラメーターは、フィルタードライバーの[**ドライバーオブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)へのポインターを提供します。 I/o 要求パケット (IRP) ディスパッチルーチンを登録するには、これらのルーチンのエントリポイントを driver オブジェクトの**MajorFunction**メンバーに格納する必要があります。 たとえば、"MyLegacyFilter" という架空のドライバーでは、ディスパッチルーチンのエントリポイントを次のように設定できます。

```cpp
for (i = 0; i <= IRP_MJ_MAXIMUM_FUNCTION; i++) {
    DriverObject->MajorFunction[i] = MyLegacyFilterDispatch;
}
DriverObject->MajorFunction[IRP_MJ_CREATE] = MyLegacyFilterCreate;
DriverObject->MajorFunction[IRP_MJ_CLOSE] = MyLegacyFilterClose;
DriverObject->MajorFunction[IRP_MJ_FILE_SYSTEM_CONTROL] = MyLegacyFilterFsControl;
```

上記**の for**ループでは、すべての IRP 主要な関数コードに既定のディスパッチルーチンが割り当てられていることに注意してください。 この割り当ては適切な方法です。これを行わないと、i/o マネージャーは不明な状態の IRP を完了し、既定ではデバイス\_要求\_無効\_ます。 このような要求は通常、ドライバースタックの下位にある別のドライバーを対象としているため、ファイルシステムフィルタードライバーは未知の Irp をこのように拒否することはできません。 このため、既定のディスパッチルーチンは、通常、次の下位レベルのドライバーに IRP を渡します。

 

 




