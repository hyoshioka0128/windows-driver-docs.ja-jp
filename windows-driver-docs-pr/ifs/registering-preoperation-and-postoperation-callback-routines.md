---
title: 操作前と操作後のコールバック ルーチンの登録
description: 操作前と操作後のコールバック ルーチンの登録
ms.assetid: 9f89ca46-8a8f-422f-9dbe-2620b944a3ae
keywords:
- preoperation コールバックルーチン WDK ファイルシステムミニフィルター、登録
- postoperation コールバックルーチン WDK ファイルシステムミニフィルター、登録
- 登録 (コールバックルーチンを)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0500bc598ecc9bdc954dd92bd3e4268d787673fe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841002"
---
# <a name="registering-preoperation-and-postoperation-callback-routines"></a>操作前と操作後のコールバック ルーチンの登録


## <span id="ddk_registering_preoperation_and_postoperation_callback_routines_if"></span><span id="DDK_REGISTERING_PREOPERATION_AND_POSTOPERATION_CALLBACK_ROUTINES_IF"></span>


[**Preoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)と[**postoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)を登録するために、ミニフィルタードライバーは、 **Driverentry**ルーチンで[**fltregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)を1回呼び出します。 **Fltregisterfilter**での*登録*パラメーターの場合、ミニパスドライバーは、 [**FLT\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)構造体へのポインターを渡します。 この構造体の**Operationregistration**メンバーには、 [**FLT\_\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_operation_registration)の配列へのポインターが含まれています。これは、ミニフィルタードライバーがフィルター処理する必要がある i/o 操作の種類ごとに1つです。

配列の各 FLT\_操作\_登録構造には、最後の構造体を除き、次の情報が含まれています。

-   操作の主要な関数コード。 I/o 操作の詳細については、「 [FLT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters) 」を、要求の種類に固有のパラメーターを参照してください。

-   読み取りと書き込みの操作 (IRP\_MJ\_READ および IRP\_MJ\_WRITE) の場合、キャッシュされた i/o またはページング i/o を無視するか、両方とも IRP ベースの i/o 操作を行うかを指定するフラグのセット

-   最大1つの preoperation コールバックルーチンと1つの postoperation コールバックルーチンのエントリポイント

配列の最後の要素は、{IRP\_MJ\_OPERATION\_END} である必要があります。

スキャナーのサンプルミニフィルタードライバーから取得した次のコード例では、登録構造\_FLT\_操作の配列が示されています。 スキャナーのサンプルミニフィルタードライバーは、irp\_MJ の preoperation および postoperation コールバックルーチンを登録し、IRP\_MJ\_CLEANUP および IRP\_MJ\_書き込み操作のための\_作成および事前操作コールバックルーチンを登録します。

```cpp
const FLT_OPERATION_REGISTRATION Callbacks[] = {
    {IRP_MJ_CREATE,
     0,
     ScannerPreCreate,
     ScannerPostCreate},
    {IRP_MJ_CLEANUP,
     0, 
     ScannerPreCleanup,
     NULL},
    {IRP_MJ_WRITE,
     0, 
     ScannerPreWrite,
     NULL},
    {IRP_MJ_OPERATION_END}
};
```

 

 




