---
title: FLT_PREOP_SYNCHRONIZE が返される場合
description: FLT_PREOP_SYNCHRONIZE が返される場合
ms.assetid: b1331f8d-e230-45b2-be1b-f85d85557350
keywords:
- FLT_PREOP_SYNCHRONIZE
- WDK ファイルシステムミニフィルターの同期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96fa564840fc874ecd3e53923ece3122c86b6a7f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840993"
---
# <a name="returning-flt_preop_synchronize"></a>FLT\_PREOP\_SYNCHRONIZE を返す


## <span id="ddk_returning_flt_preop_synchronize_if"></span><span id="DDK_RETURNING_FLT_PREOP_SYNCHRONIZE_IF"></span>


ミニフィルタードライバーの[**preoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)が、FLT\_preoperation\_SYNCHRONIZE を返すことによって i/o 操作を同期する場合、フィルターマネージャーは、i/o の完了時にミニフィルタードライバーの[**postoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)を呼び出します。

フィルターマネージャーは、呼び出し元が preoperation コールバックと同じスレッドコンテキストでミニフィルタードライバーの postoperation コールバックルーチンを呼び出します (IRQL &lt;= APC\_LEVEL)。 (このスレッドコンテキストは、必ずしも元のスレッドのコンテキストではないことに注意してください)。

ミニフィルタードライバーの preoperation コールバックルーチンから FLT\_PREOPERATION\_SYNCHRONIZE が返されても、ミニフィルタードライバーが操作の postoperation コールバックルーチンを登録していない場合は、チェックされたビルドに対してシステムが**アサート   ます**。

 

ミニフィルタードライバーの preoperation コールバックルーチンから FLT\_PREOPERATION\_SYNCHRONIZE が返された場合 *、その完了後の出力パラメーター*に NULL 以外の値を返すことができます。 このパラメーターは、対応する postoperation コールバックルーチンに渡される省略可能なコンテキストポインターです。 Postoperation コールバックルーチンは、このポインターを完了後*の入力パラメーター*に受け取ります。

ミニフィルタードライバーの preoperation コールバックルーチンは、IRP ベースの i/o 操作の場合にのみ、FLT\_PREOPERATION\_SYNCHRONIZE を返す必要があります。 ただし、この状態値は、他の種類の操作でも返すことができます。 IRP ベースの i/o 操作ではない i/o 操作に対して返された場合、フィルターマネージャーは、この戻り値を\_コールバックと共に\_PREOP\_成功\_として扱います。 操作が IRP ベースの i/o 操作であるかどうかを判断するには、 [**FLT\_is\_irp\_operation**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))マクロを使用します。

ミニフィルタードライバーは、create 操作に対して FLT\_PREOP\_SYNCHRONIZE を返さないようにする必要があります。これらの操作は既にフィルターマネージャーによって同期されているためです。 ミニフィルタードライバーで、IRP\_\_MJ の preoperation および postoperation コールバックルーチンが登録されている場合、作成後のコールバックルーチンは、作成前のコールバックルーチンと同じスレッドコンテキストで、IRQL = パッシブ\_レベルで呼び出されます。

ミニフィルタードライバーは、非同期の読み取り操作または書き込み操作のために、FLT\_PREOP\_SYNCHRONIZE を返さないようにする必要があります。 このようにすると、ミニフィルタードライバーとシステムのパフォーマンスが著しく低下し、変更されたページライタースレッドがブロックされた場合などにデッドロックが発生する可能性もあります。 IRP ベースの読み取り操作または書き込み操作に対して FLT\_PREOP\_SYNCHRONIZE を返す前に、ミニフィルタードライバーは、 [**FltIsOperationSynchronous**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltisoperationsynchronous)を呼び出して、操作が同期されていることを確認する必要があります。

次の種類の i/o 操作は同期できません。

-   Oplock ファイルシステム制御 (FSCTL) 操作 (**MajorFunction**は IRP\_MJ\_ファイル\_システム\_コントロール;**Fscontrolcode**は[**FSCTL\_request\_FILTER\_OPLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-request-filter-oplock)、 [**FSCTL\_request\_BATCH\_OPLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-request-batch-oplock)、 [**FSCTL\_request\_oplock\_level\_1**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-request-oplock-level-1)、または[**FSCTL\_request\_oplock\_level\_2**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-request-oplock-level-2)) です。

-   ディレクトリの変更操作を通知する (**MajorFunction** is IRP\_MJ\_DIRECTORY\_CONTROL;**Minorfunction**は、\_\_ディレクトリの変更を通知\_通知を\_します。)

-   バイト範囲ロック要求 (**MajorFunction**は IRP\_MJ\_LOCK\_CONTROL;**Minorfunction**は、IRP\_\_ロックされています。)

これらの操作のいずれに対しても、FLT\_PREOP\_SYNCHRONIZE を返すことはできません。

 

 




