---
title: 操作前コールバック ルーチン内で I/O 操作を完了する
description: 操作前コールバック ルーチン内で I/O 操作を完了する
ms.assetid: 1f339779-dc88-4673-87d5-36cee0b27fc2
keywords:
- preoperation コールバックルーチン WDK ファイルシステムミニフィルター、i/o 操作の完了
- i/o 要求の完了 (WDK ファイルシステム)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d44ceabbf4b49508ec3f01346bc42a577f53100
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841468"
---
# <a name="completing-an-io-operation-in-a-preoperation-callback-routine"></a>操作前コールバック ルーチン内で I/O 操作を完了する


## <span id="ddk_completing_an_io_operation_in_a_preoperation_callback_routine_if"></span><span id="DDK_COMPLETING_AN_IO_OPERATION_IN_A_PREOPERATION_CALLBACK_ROUTINE_IF"></span>


I/o 操作を*完了*するには、操作の処理を停止し、最後の NTSTATUS 値を割り当てて、フィルターマネージャーに返します。

ミニフィルタードライバーで i/o 操作が完了すると、フィルターマネージャーは次の処理を実行します。

-   は、現在のミニフィルタードライバー、レガシフィルター、またはファイルシステムの下にあるミニフィルタードライバーに操作を送信しません。

-   ミニフィルタードライバーインスタンススタック内の現在のミニフィルタードライバーの前にあるミニ[**操作コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)を呼び出します。

-   は、現在のミニフィルタードライバーの postoperation コールバックルーチンが存在する場合、その操作を呼び出しません。

ミニフィルタードライバーの[**preoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)は、次の手順を実行して i/o 操作を完了します。

1.  コールバックデータ構造の**Iostatus. status**フィールドを、操作の最後の NTSTATUS 値に設定します。

2.  FLT\_PREOP\_を返します。

I/o 操作を完了する preoperation コールバックルーチンで、NULL 以外の完了コンテキストを設定することはできません *([完了] 出力パラメーター* )。

ミニフィルタードライバーは、次の手順を実行して、以前に保留された i/o 操作の作業ルーチンで操作を完了することもできます。

1.  コールバックデータ構造の**Iostatus. status**フィールドを、操作の最後の NTSTATUS 値に設定します。

2.  作業ルーチンが[**FltcompleteFLT Dedpreoperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation)を呼び出すときに、コールアウト*ステータス*パラメーターで\_preop\_COMPLETE を渡しました。

I/o 操作の完了時に、ミニフィルタードライバーは、コールバックデータ構造の**iostatus. status**フィールドを操作の最終 NTSTATUS 値に設定する必要がありますが、この ntstatus 値は状態\_PENDING または STATUS\_FLT にはできません\_\_高速\_IO を許可しません。 クリーンアップまたは閉じる操作の場合、フィールドは [SUCCESS]\_[SUCCESS] になっている必要があります。 これらの操作は、他の NTSTATUS 値では完了できません。

I/o 操作の完了は、次のように、NTSTATUS 値に応じて、"成功" または "操作の失敗" と呼ばれることがよくあります。

-   I/o 操作を*成功*させるには、正常に完了したか、ステータス\_success などの情報の NTSTATUS 値を使用して、i/o 操作を完了します。

-   I/o 操作が*失敗*するようにするには、エラーまたは警告の NTSTATUS 値を使用して完了する必要があります。たとえば、状態\_無効\_デバイス\_の要求または状態\_バッファー\_オーバーフローします。

NTSTATUS 値は、ntstatus に定義されています。 これらの値は、成功、情報、警告、エラーの4つのカテゴリに分類されます。 これらの値の詳細については、「 [NTSTATUS 値の使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-ntstatus-values)」を参照してください。

 

 




