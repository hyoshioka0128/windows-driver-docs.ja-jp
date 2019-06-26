---
title: I/O 操作の完了処理を実行する
description: I/O 操作の完了処理を実行する
ms.assetid: 7e65c21c-d38f-4804-8c07-6cd89f6a6dd6
keywords:
- postoperation コールバック ルーチン WDK ファイル システム ミニフィルター、処理の完了
- WDK のファイル システムを要求する I/O の完了
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b824e1a614491a6a314b59271581ca33cb84519
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360320"
---
# <a name="performing-completion-processing-for-an-io-operation"></a>I/O 操作の完了処理を実行する


## <span id="ddk_performing_completion_processing_for_an_io_operation_if"></span><span id="DDK_PERFORMING_COMPLETION_PROCESSING_FOR_AN_IO_OPERATION_IF"></span>


ミニフィルター ドライバーの[ **postoperation コールバック ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback)基になるファイル システム、レガシ フィルター、または他のミニフィルター ドライバーにある I/O 操作が完了したときに呼び出されますが、ミニフィルター ドライバーのインスタンスのスタックでの高度の低い。

さらに、ミニフィルター ドライバーのインスタンスが破棄されるときに、フィルター マネージャー「ドレイン」、インスタンスが受信するすべての I/O 操作を[ **preoperation コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback) を待機していますが、[**postoperation コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback)します。 フィルター マネージャーが I/O 操作が完了していないと、FLTFL を設定する場合でも、ミニフィルター ドライバーの postoperation コールバック ルーチンを呼び出すこのような状況で\_POST\_操作\_ドレイン中、フラグ*フラグ*入力パラメーター。

ときに、FLTFL\_POST\_操作\_ドレイン中のフラグが設定されて、ミニフィルター ドライバーでは、正常に終了処理は実行する必要があります。 代わりに、ミニフィルター ドライバーに割り当てられたメモリの解放など、必要なだけのクリーンアップを使用する場合を実行する必要がありますが、 *CompletionContext*パラメーターでは、preoperation コールバック ルーチンと戻り値の FLT\_POSTOP\_完了\_処理します。

このセクションには、次のトピックが含まれます。

[安全な IRQL で完了処理が実行されることを確認](ensuring-that-completion-processing-is-performed-at-safe-irql.md)

 

 




