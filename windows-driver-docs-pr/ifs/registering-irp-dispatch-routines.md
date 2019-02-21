---
title: IRP ディスパッチ ルーチンを登録します。
description: IRP ディスパッチ ルーチンを登録します。
ms.assetid: 096f4bb7-2326-4e6c-b3db-a2d95ca4982b
keywords:
- IRP ディスパッチ ルーチンを登録します。
- ディスパッチ ルーチン WDK ファイル システム
- IRP ディスパッチ ルーチン WDK ファイル システムを登録します。
- Irp WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3b658a41298600c8216500b8a8c8eeeb6b8e262
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551352"
---
# <a name="registering-irp-dispatch-routines"></a>IRP ディスパッチ ルーチンを登録します。


## <span id="ddk_registering_irp_dispatch_routines_if"></span><span id="DDK_REGISTERING_IRP_DISPATCH_ROUTINES_IF"></span>


*DriverObject*パラメーター、フィルター ドライバーの[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンは、フィルター ドライバーへのポインターを提供[**ドライバーオブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff544174)します。 I/O 要求パケット (IRP) ディスパッチ ルーチンを登録するにこれらのルーチンのエントリ ポイントを格納する必要があります、 **MajorFunction**ドライバー オブジェクトのメンバー。 たとえば、仮定"MyLegacyFilter"ドライバーは次のように、ディスパッチ ルーチンのエントリ ポイントを設定できます。

```cpp
for (i = 0; i <= IRP_MJ_MAXIMUM_FUNCTION; i++) {
    DriverObject->MajorFunction[i] = MyLegacyFilterDispatch;
}
DriverObject->MajorFunction[IRP_MJ_CREATE] = MyLegacyFilterCreate;
DriverObject->MajorFunction[IRP_MJ_CLOSE] = MyLegacyFilterClose;
DriverObject->MajorFunction[IRP_MJ_FILE_SYSTEM_CONTROL] = MyLegacyFilterFsControl;
```

なお、上記**の**ループが IRP 主な機能のすべてのコードの既定のディスパッチ ルーチンを割り当てます。 それ以外の場合 I/O マネージャーがステータスで、認識されない IRP が完了するため、この割り当ては、ことをお勧め\_無効な\_デバイス\_既定で要求します。 ファイル システム フィルター ドライバーがする必要がありますので、このような要求はドライバー スタックの下位にある別のドライバーのためのものは、通常この方法で未知の Irp 拒否されません。 このため、既定のディスパッチ ルーチンは通常、下位レベルの次のドライバーに IRP を渡します。

 

 




