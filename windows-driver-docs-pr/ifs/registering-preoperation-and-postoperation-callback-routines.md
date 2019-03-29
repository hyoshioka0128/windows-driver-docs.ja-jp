---
title: 操作前と操作後のコールバック ルーチンの登録
description: 操作前と操作後のコールバック ルーチンの登録
ms.assetid: 9f89ca46-8a8f-422f-9dbe-2620b944a3ae
keywords:
- preoperation コールバック ルーチン WDK ファイル システム ミニフィルターを登録します。
- postoperation コールバック ルーチン WDK ファイル システム ミニフィルターを登録します。
- コールバック ルーチンを登録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e26784ccc76f44d5af7e001502467719aa759d71
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581985"
---
# <a name="registering-preoperation-and-postoperation-callback-routines"></a>操作前と操作後のコールバック ルーチンの登録


## <span id="ddk_registering_preoperation_and_postoperation_callback_routines_if"></span><span id="DDK_REGISTERING_PREOPERATION_AND_POSTOPERATION_CALLBACK_ROUTINES_IF"></span>


登録する[ **preoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551109)と[ **postoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551107)、ミニフィルター ドライバーは、1 回の呼び出し[ **FltRegisterFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544305)でその**DriverEntry**ルーチン。 *登録*パラメーター **FltRegisterFilter**、ミニフィルター ドライバーへのポインターを渡す、 [ **FLT\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff544811)構造体。 **OperationRegistration**この構造体のメンバーの配列へのポインターを格納する[ **FLT\_操作\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff544668)ミニフィルター ドライバーをフィルター処理する必要がある I/O 操作の種類ごとに 1 つずつ構造。

各 FLT\_操作\_の最後のものを除く、配列内の登録の構造体には、次の情報が含まれています。

-   操作の主な機能のコード。 参照してください[FLT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters) I/O 操作、およびその要求の種類に固有のパラメーターについてです。

-   読み取りおよび書き込み操作 (IRP\_MJ\_読み取りおよび IRP\_MJ\_書き込み)、無視するかどうかを指定するフラグのセットには、I/O、ページング I/O、またはその両方の IRP ベースの I/O 操作がキャッシュされています。

-   最大で 1 つの preoperation コールバック ルーチンと 1 つの postoperation コールバック ルーチンのエントリ ポイント

配列内の最後の要素である必要があります {0} IRP\_MJ\_操作\_終了しました。

ミニフィルター ドライバーには、スキャナーのサンプルから取得されますが、次のコード例は、FLT の配列を示しています。\_操作\_登録構造体。 スキャナー サンプル ミニフィルター ドライバーは IRP の preoperation と postoperation コールバック ルーチンに登録\_MJ\_IRP の preoperation コールバック ルーチンの作成と\_MJ\_クリーンアップと IRP\_MJ\_書き込み操作です。

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

 

 




