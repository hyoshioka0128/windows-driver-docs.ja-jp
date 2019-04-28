---
title: ミニフィルター ドライバーの登録
description: ミニフィルター ドライバーの登録
ms.assetid: 943082c9-dcff-478f-80ba-2a2e72f6ead2
keywords:
- ミニフィルター ドライバーの登録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7479cb6139d593b764aa1c69b2156944649b56cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370100"
---
# <a name="registering-the-minifilter-driver"></a>ミニフィルター ドライバーの登録


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


ミニフィルター ドライバーを呼び出す必要があります[ **FltRegisterFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544305)からその**DriverEntry**ルーチン自体を登録済みミニフィルター ドライバーのグローバル リストに追加して、提供するにはコールバック ルーチンとその他の情報、ドライバーの一覧をフィルター マネージャー。

MiniSpy サンプルでは、ミニフィルター ドライバーは、次のコード例に示すように登録されます。

```cpp
NTSTATUS status;
status = FltRegisterFilter(
           DriverObject,                  //Driver
           &FilterRegistration,           //Registration
           &MiniSpyData.FilterHandle);    //RetFilter
```

**FltRegisterFilter**が 2 つの入力パラメーター。 最初、*ドライバー*、として受信したミニフィルター ドライバーをドライバー オブジェクト ポインターは、 *DriverObject*への入力パラメーター、 **DriverEntry**ルーチン。 次に、*登録*へのポインター、 [ **FLT\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff544811)ミニフィルター ドライバーのコールバックを指すエントリを含む構造体ルーチン。

さらに、 **FltRegisterFilter**出力パラメーター、 *RetFilter*、ミニフィルター ドライバーのフィルターを不透明なポインターを受け取る。 このフィルターのポインターは、多くの場合は、必要な入力パラメーター **Flt * * * Xxx*などのルーチンをサポートして[ **FltStartFiltering** ](https://msdn.microsoft.com/library/windows/hardware/ff544569)と[ **FltUnregisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544606)します。

 

 




