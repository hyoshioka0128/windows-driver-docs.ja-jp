---
title: ミニフィルター ドライバーの登録
description: ミニフィルター ドライバーの登録
ms.assetid: 943082c9-dcff-478f-80ba-2a2e72f6ead2
keywords:
- ミニフィルタードライバーを登録しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4573b29e301016f317e5fdaa7034ab562424d3db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840997"
---
# <a name="registering-the-minifilter-driver"></a>ミニフィルター ドライバーの登録


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


すべてのミニフィルタードライバーは、その**Driverentry**ルーチンから[**Fltregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)を呼び出して、登録されているミニフィルタードライバーのグローバルリストに追加し、フィルターマネージャーに、コールバックルーチンの一覧とその他の情報を提供する必要があります。ドライバー。

MiniSpy サンプルでは、次のコード例に示すようにミニフィルタードライバーが登録されています。

```cpp
NTSTATUS status;
status = FltRegisterFilter(
           DriverObject,                  //Driver
           &FilterRegistration,           //Registration
           &MiniSpyData.FilterHandle);    //RetFilter
```

**Fltregisterfilter**には2つの入力パラメーターがあります。 1つ目の*ドライバー*は、ミニフィルタードライバーが**driverobject**ルーチンに*driverobject*入力パラメーターとして受け取ったドライバーオブジェクトポインターです。 2番目の*登録*は、ミニフィルタードライバーのコールバックルーチンへのエントリポイントを含む[**FLT\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)構造体へのポインターです。

さらに、 **Fltregisterfilter**には、ミニフィルタードライバーの非透過的フィルターポインターを受け取る出力パラメーター *retfilter*があります。 このフィルターポインターは、 [**Fltstartfiltering**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering)や[**Fltstartfiltering**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunregisterfilter)など、多くの**Flt**_Xxx_サポートルーチンに必要な入力パラメーターです。

 

 




