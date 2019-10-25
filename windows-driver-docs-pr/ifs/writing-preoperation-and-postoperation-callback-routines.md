---
title: 操作前と操作後のコールバック ルーチンの記述
description: 操作前と操作後のコールバック ルーチンの記述
ms.assetid: ad706d01-7a14-4730-8189-c465637987dc
keywords:
- ファイルシステムミニフィルタードライバー WDK、preoperation コールバックルーチン
- ミニフィルタードライバー WDK、preoperation コールバックルーチン
- preoperation コールバックルーチン WDK ファイルシステムミニフィルター、preoperation コールバックルーチンについて
- postoperation コールバックルーチン WDK ファイルシステムミニフィルター、postoperation コールバックルーチンについて
- ファイルシステムミニフィルタードライバー WDK、postoperation コールバックルーチン
- ミニフィルタードライバー WDK、postoperation コールバックルーチン
- preoperation コールバックルーチン WDK ファイルシステムミニフィルター
- postoperation コールバックルーチン WDK ファイルシステムミニフィルター
- I/o WDK ファイルシステム
- コールバックルーチン WDK ファイルシステム
- i/o 操作のフィルター選択 WDK ファイルシステムミニフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61de2e292567ee882dd94ff962c20cd712e1b3ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840918"
---
# <a name="writing-preoperation-and-postoperation-callback-routines"></a>操作前と操作後のコールバック ルーチンの記述


## <span id="ddk_writing_preoperation_and_postoperation_callback_routines_if"></span><span id="DDK_WRITING_PREOPERATION_AND_POSTOPERATION_CALLBACK_ROUTINES_IF"></span>


**Driverentry**ルーチンでは、ミニフィルタードライバーは、フィルター処理に必要な i/o 操作の種類ごとに1つの[**preoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)と、最大で1つの[**postoperation コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)ルーチンを登録できます。

従来のファイルシステムフィルタードライバーとは異なり、ミニフィルタードライバーでは、フィルター処理する i/o 操作の種類を選択できます。 ミニフィルタードライバーは、postoperation コールバックを登録せずに、特定の種類の i/o 操作に対して preoperation コールバックルーチンを登録できます。逆の場合も同様です。 ミニフィルタードライバーは、preoperation または postoperation コールバックルーチンが登録されている i/o 操作だけを受信します。

*Preoperation コールバックルーチン*は、レガシフィルタードライバーモデルのディスパッチルーチンに似ています。 フィルターマネージャーは、i/o 操作を処理するときに、この種類の i/o 操作のために登録されているミニフィルタードライバーインスタンススタック内の、各ミニフィルタードライバーの preoperation コールバックルーチンを呼び出します。 スタック内の最上位のミニフィルタードライバー (つまり、インスタンスの上位レベルが最高の場合) は、最初に操作を受信します。 ミニフィルタードライバーは、操作の処理を終了すると、操作をフィルターマネージャーに返します。これにより、操作が次に最も大きいミニフィルタードライバーに渡されます。 ミニフィルタードライバーインスタンススタック内のすべてのミニフィルタードライバーで i/o 操作が処理された場合--フィルターマネージャーは、その操作をレガシフィルターとファイルシステムに送信します (ただし、フィルターマネージャーによって処理されます)。

*Postoperation コールバックルーチン*は、レガシフィルタードライバーモデルの完了ルーチンに似ています。 I/o 操作の完了処理は、i/o マネージャーが操作をファイルシステムに渡したときと、その操作の完了ルーチンが登録されているレガシフィルターによって開始されます。 これらの完了ルーチンが完了すると、フィルターマネージャーは操作の完了処理を実行します。 フィルターマネージャーは、この種類の i/o 操作用に登録されているミニフィルタードライバーインスタンススタックで、各ミニフィルタードライバーの postoperation コールバックルーチンを呼び出します。 スタック内の一番下のミニフィルタードライバー (つまり、インスタンスが最も低い標高を持つもの) は、最初に操作を受信します。 このミニフィルタードライバーは、操作の処理を終了すると、それをフィルターマネージャーに返します。これにより、操作が次に最も低いミニフィルタードライバーに渡されます。

このセクションの内容:

[Preoperation および Postoperation コールバックルーチンを登録しています](registering-preoperation-and-postoperation-callback-routines.md)

[ミニフィルタードライバーでの i/o 操作のフィルター処理](filtering-i-o-operations-in-a-minifilter-driver.md)

[プリ操作コールバックルーチンの書き込み](writing-preoperation-callback-routines.md)

[Postoperation コールバックルーチンを書き込んでいます](writing-postoperation-callback-routines.md)

[I/o 操作のパラメーターの変更](modifying-the-parameters-for-an-i-o-operation.md)

[I/o 操作のバッファリング方法の決定](determining-the-buffering-method-for-an-i-o-operation.md)

[I/o 操作のユーザーバッファーへのアクセス](accessing-the-user-buffers-for-an-i-o-operation.md)

 

 




