---
title: 操作後コールバック ルーチン内で I/O 操作を失敗とする
description: 操作後コールバック ルーチン内で I/O 操作を失敗とする
ms.assetid: 45897bca-1573-42c5-ad00-3198b7362d9e
keywords:
- postoperation コールバックルーチン WDK ファイルシステムミニフィルター、失敗した操作
- 失敗した i/o 操作 WDK ファイルシステムミニフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e6c04094ddb327357b77d8dd5918e17afa621d8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841418"
---
# <a name="failing-an-io-operation-in-a-postoperation-callback-routine"></a>操作後コールバック ルーチン内で I/O 操作を失敗とする


## <span id="ddk_failing_an_io_operation_in_a_postoperation_callback_routine_if"></span><span id="DDK_FAILING_AN_IO_OPERATION_IN_A_POSTOPERATION_CALLBACK_ROUTINE_IF"></span>


ミニフィルタードライバーの[**postoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)は、成功した i/o 操作を失敗させる可能性がありますが、i/o 操作の失敗によって操作の効果を元に戻すことはできません。 ミニフィルタードライバーは、操作を元に戻すために必要な処理を実行します。

たとえば、ミニフィルタードライバーの作成後のコールバックルーチンは、次の手順を実行して、正常な IRP\_MJ\_作成操作に失敗する可能性があります。

1.  作成操作で作成または開かれたファイルを閉じるには、 [**Fltcancelfileopen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen)を呼び出します。 **Fltcancelfileopen**では、ファイルに対する変更は元に戻されないことに注意してください。 たとえば、 **Fltcancelfileopen**は、新しく作成されたファイルを削除したり、切り捨てられたファイルを以前のサイズに復元したりすることはありません。

2.  コールバックデータ構造の**Iostatus. status**フィールドを、操作の最後の NTSTATUS 値に設定します。 この値は、状態\_アクセス\_拒否されたなどの有効なエラーの値である必要があります。

3.  コールバックデータ構造の**Iostatus. 情報**フィールドをゼロに設定します。

4.  FLT\_POSTOP\_返され\_処理が終了しました。

コールバックデータ構造の**iostatus. status**フィールドを、操作の最終 NTSTATUS 値に設定するときは、ミニフィルタードライバーで有効なエラー ntstatus 値を指定する必要があります。 ミニフィルタードライバーでは、\_高速\_IO を許可\_\_FLT を指定できないことに注意してください。フィルターマネージャーのみがこの NTSTATUS 値を使用できます。

[**Fltcancelfileopen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen)の呼び出し元は、IRQL &lt;= APC\_レベルで実行されている必要があります。 ただし、ミニフィルタードライバーは、作成後のコールバックルーチンから安全にこのルーチンを呼び出すことができます。これは、IRP\_MJ\_CREATE 操作の場合、postoperation コールバックルーチンが、スレッドのコンテキストで IRQL = パッシブ\_レベルで呼び出されるためです。これで作成操作が開始されました。

 

 




