---
title: I/o 操作の完了処理を実行しています
description: I/o 操作の完了処理を実行しています
ms.assetid: 7e65c21c-d38f-4804-8c07-6cd89f6a6dd6
keywords:
- postoperation コールバックルーチン WDK ファイルシステムミニフィルター、完了処理
- i/o 要求の完了 (WDK ファイルシステム)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 099f82a4082a7e92b66471704d6cefaef3edffbb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841034"
---
# <a name="performing-completion-processing-for-an-io-operation"></a>I/o 操作の完了処理を実行しています


## <span id="ddk_performing_completion_processing_for_an_io_operation_if"></span><span id="DDK_PERFORMING_COMPLETION_PROCESSING_FOR_AN_IO_OPERATION_IF"></span>


ミニフィルタードライバーの[**postoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)は、基になるファイルシステム、レガシフィルター、またはミニフィルタードライバーインスタンススタック内の高度が低い別のミニフィルタードライバーによって i/o 操作が完了したときに呼び出されます。

さらに、ミニフィルタードライバーインスタンスが破棄されている場合、フィルターマネージャーは、インスタンスが[**preoperation コール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)バックを受信し、 [**postoperation コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)を待機しているすべての i/o 操作を "ドレイン" します。 このような状況では、フィルターマネージャーは、i/o 操作が完了していない場合でもミニフィルタードライバーの postoperation コールバックルーチンを呼び出し、*フラグ*入力に\_ドレインフラグを設定して FLTFL\_POST\_操作を設定します。引き.

FLTFL\_POST\_操作\_ドレインフラグが設定されている場合、ミニフィルタードライバーは通常の完了処理を実行できません。 代わりに、必要なクリーンアップのみを実行する必要があります。たとえば、その preoperation コールバックルーチンの完了時パラメーターに対してミニフィルタードライバーによって割り当て*られた*メモリを解放し、FLT\_postop\_終了した場合は、を返し\_プロセス.

ここでは、次のトピックについて説明します。

[完了処理が安全な IRQL で実行されることの確認](ensuring-that-completion-processing-is-performed-at-safe-irql.md)

 

 




