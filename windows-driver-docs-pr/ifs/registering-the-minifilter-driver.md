---
title: ミニフィルター ドライバーの登録
description: ミニフィルター ドライバーの登録
ms.assetid: 943082c9-dcff-478f-80ba-2a2e72f6ead2
keywords:
- ミニフィルター ドライバーの登録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0dcfc9e79596faee7fc47775c8d8279c8c9b05f
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716814"
---
# <a name="registering-the-minifilter-driver"></a>ミニフィルター ドライバーの登録


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


ミニフィルター ドライバーを呼び出す必要があります[ **FltRegisterFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltregisterfilter)からその**DriverEntry**ルーチン自体を登録済みミニフィルター ドライバーのグローバル リストに追加して、提供するにはコールバック ルーチンとその他の情報、ドライバーの一覧をフィルター マネージャー。

MiniSpy サンプルでは、ミニフィルター ドライバーは、次のコード例に示すように登録されます。

```cpp
NTSTATUS status;
status = FltRegisterFilter(
           DriverObject,                  //Driver
           &FilterRegistration,           //Registration
           &MiniSpyData.FilterHandle);    //RetFilter
```

**FltRegisterFilter**が 2 つの入力パラメーター。 最初、*ドライバー*、として受信したミニフィルター ドライバーをドライバー オブジェクト ポインターは、 *DriverObject*への入力パラメーター、 **DriverEntry**ルーチン。 次に、*登録*へのポインター、 [ **FLT\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_registration)ミニフィルター ドライバーのコールバックを指すエントリを含む構造体ルーチン。

さらに、 **FltRegisterFilter**出力パラメーター、 *RetFilter*、ミニフィルター ドライバーのフィルターを不透明なポインターを受け取る。 このフィルターのポインターは、多くの場合は、必要な入力パラメーター **Flt**_Xxx_などのルーチンをサポートして[ **FltStartFiltering** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltstartfiltering)と[ **FltUnregisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltunregisterfilter)します。

 

 




