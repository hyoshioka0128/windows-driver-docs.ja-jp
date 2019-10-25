---
title: I/o 操作のユーザーバッファーへのアクセス
description: I/o 操作のユーザーバッファーへのアクセス
ms.assetid: 0f4334bf-eec9-4667-af02-537e3357d872
keywords:
- WDK ファイルシステムミニフィルターのバッファー
- FLT_PARAMETERS
- メモリ記述子に WDK ファイルシステムミニフィルターが一覧表示されます。
- MDLs WDK ファイルシステム
- I/o WDK ファイルシステム
- IRP ベース i/o 操作 (WDK ファイルシステムミニフィルター)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1062a9341388588e7163b5aa30365d9f65c54750
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841506"
---
# <a name="accessing-the-user-buffers-for-an-io-operation"></a>I/o 操作のユーザーバッファーへのアクセス


## <span id="ddk_accessing_the_user_buffers_for_an_io_operation_if"></span><span id="DDK_ACCESSING_THE_USER_BUFFERS_FOR_AN_IO_OPERATION_IF"></span>


I/o 操作の[**FLT\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、操作に固有の操作固有のパラメーターが含まれています。これには、操作で使用されるバッファーのバッファーアドレスとメモリ記述子リスト (MDL) が含まれます。

IRP ベースの i/o 操作の場合、操作のバッファーは次を使用して指定できます。

-   MDL のみ (通常はページング i/o 用)

-   バッファーアドレスのみ

-   バッファーアドレスと MDL

高速な i/o 操作の場合は、ユーザー領域のバッファーアドレスだけが指定されます。 バッファーを持つ高速 i/o 操作では、バッファーも直接 i/o も使用されないため、MDL パラメーターを持つことはできません。

次のトピックでは、ミニフィルタードライバー [**preoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)と[**postoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)での IRP ベースおよび高速 i/o 操作に対するバッファーアドレスと mdls の処理に関するガイドラインを提供します。

[Preoperation コールバックルーチンでのユーザーバッファーへのアクセス](accessing-user-buffers-in-a-preoperation-callback-routine.md)

[Postoperation コールバックルーチンでのユーザーバッファーへのアクセス](accessing-user-buffers-in-a-postoperation-callback-routine.md)

 

 




