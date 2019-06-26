---
title: IRP ディスパッチ ルーチンの登録
description: IRP ディスパッチ ルーチンの登録
ms.assetid: 096f4bb7-2326-4e6c-b3db-a2d95ca4982b
keywords:
- IRP ディスパッチ ルーチンを登録します。
- ディスパッチ ルーチン WDK ファイル システム
- IRP ディスパッチ ルーチン WDK ファイル システムを登録します。
- Irp WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cf6e99cbd6bc861cb64b272e5026145e8272fdc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385131"
---
# <a name="registering-irp-dispatch-routines"></a>IRP ディスパッチ ルーチンの登録


## <span id="ddk_registering_irp_dispatch_routines_if"></span><span id="DDK_REGISTERING_IRP_DISPATCH_ROUTINES_IF"></span>


*DriverObject*パラメーター、フィルター ドライバーの[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチンは、フィルター ドライバーへのポインターを提供[**ドライバーオブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_driver_object)します。 I/O 要求パケット (IRP) ディスパッチ ルーチンを登録するにこれらのルーチンのエントリ ポイントを格納する必要があります、 **MajorFunction**ドライバー オブジェクトのメンバー。 たとえば、仮定"MyLegacyFilter"ドライバーは次のように、ディスパッチ ルーチンのエントリ ポイントを設定できます。

```cpp
for (i = 0; i <= IRP_MJ_MAXIMUM_FUNCTION; i++) {
    DriverObject->MajorFunction[i] = MyLegacyFilterDispatch;
}
DriverObject->MajorFunction[IRP_MJ_CREATE] = MyLegacyFilterCreate;
DriverObject->MajorFunction[IRP_MJ_CLOSE] = MyLegacyFilterClose;
DriverObject->MajorFunction[IRP_MJ_FILE_SYSTEM_CONTROL] = MyLegacyFilterFsControl;
```

なお、上記**の**ループが IRP 主な機能のすべてのコードの既定のディスパッチ ルーチンを割り当てます。 それ以外の場合 I/O マネージャーがステータスで、認識されない IRP が完了するため、この割り当ては、ことをお勧め\_無効な\_デバイス\_既定で要求します。 ファイル システム フィルター ドライバーがする必要がありますので、このような要求はドライバー スタックの下位にある別のドライバーのためのものは、通常この方法で未知の Irp 拒否されません。 このため、既定のディスパッチ ルーチンは通常、下位レベルの次のドライバーに IRP を渡します。

 

 




