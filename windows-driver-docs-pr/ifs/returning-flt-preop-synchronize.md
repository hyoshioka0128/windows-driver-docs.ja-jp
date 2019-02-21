---
title: FLT_PREOP_SYNCHRONIZE を返す
description: FLT_PREOP_SYNCHRONIZE を返す
ms.assetid: b1331f8d-e230-45b2-be1b-f85d85557350
keywords:
- FLT_PREOP_SYNCHRONIZE
- 同期 WDK ファイル システム ミニフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63458ce3d59588f9702dd10684b1427365edb007
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551845"
---
# <a name="returning-fltpreopsynchronize"></a>返す FLT\_PREOP\_同期


## <span id="ddk_returning_flt_preop_synchronize_if"></span><span id="DDK_RETURNING_FLT_PREOP_SYNCHRONIZE_IF"></span>


ミニフィルター ドライバーの場合[ **preoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551109) FLT を返すことによって、I/O 操作を同期\_PREOP\_同期フィルター マネージャーの呼び出し、ミニフィルター ドライバーの[ **postoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551107) I/O の完了時にします。

フィルター マネージャーは、IRQL で preoperation コールバックと同じスレッド コンテキストにミニフィルター ドライバーの postoperation コールバック ルーチンを呼び出す&lt;APC を =\_レベル。 (このスレッド コンテキストがないこと必ずしも元のスレッドのコンテキストに注意してください)。

**注**  コールバック ルーチンが FLT を返す場合ミニフィルター ドライバーの preoperation\_PREOP\_同期がミニフィルター ドライバーが postoperation コールバック ルーチンの操作で、登録されていない、システムは、チェックのビルドをアサートします。

 

ミニフィルター ドライバーの preoperation 場合、コールバック ルーチンは FLT を返します\_PREOP\_同期の非 NULL 値を返すことの*CompletionContext*出力パラメーター。 このパラメーターは、対応する postoperation コールバック ルーチンに渡される省略可能なコンテキスト ポインターです。 Postoperation コールバック ルーチンでは、このポインターを受け取るその*CompletionContext*入力パラメーター。

ミニフィルター ドライバーの preoperation コールバック ルーチンが FLT を返す必要があります\_PREOP\_IRP ベースの I/O 操作にのみ同期します。 ただし、この状態値は、他の操作の種類の返されることができます。 フィルター マネージャーでは、FLT の場合と同様に、この戻り値が扱われます、IRP ベースの I/O 操作ではありませんが、I/O 操作の返された場合に\_PREOP\_成功\_WITH\_コールバック。 操作が IRP ベースの I/O 操作であるかどうかを確認するのには、使用、 [ **FLT\_IS\_IRP\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544654)マクロ。

ミニフィルター ドライバー FLT を返さないでください\_PREOP\_フィルター マネージャーによって、これらの操作が既に同期されているための同期は、操作を作成します。 ミニフィルター ドライバーが IRP の preoperation と postoperation コールバック ルーチンを登録済みの場合\_MJ\_、作成操作、作成後のコールバック ルーチンは IRQL で呼び出されます = パッシブ\_レベルと同じスレッド コンテキストで、コールバック ルーチンを事前に作成します。

ミニフィルター ドライバーが FLT を返す必要がありますしない\_PREOP\_非同期の読み取りまたは書き込み操作を同期します。 これにより深刻なミニフィルター ドライバーとシステムのパフォーマンスが低下するできも原因デッドロックなど、変更されたページ ライター スレッドがブロックされている場合は、します。 FLT を返す前に\_PREOP\_同期読み取りまたは書き込み操作では、操作を呼び出すことによって同期ミニフィルター ドライバーが確認する必要があります IRP ベース[ **FltIsOperationSynchronous**](https://msdn.microsoft.com/library/windows/hardware/ff543351).

次の種類の I/O 操作を同期することはできません。

-   Oplock ファイル システム コントロール (FSCTL) 操作 (**MajorFunction** IRP が\_MJ\_ファイル\_システム\_制御。**FsControlCode**は[ **FSCTL\_要求\_フィルター\_OPLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff545518)、 [ **FSCTL\_要求\_バッチ\_OPLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff545510)、 [ **FSCTL\_要求\_OPLOCK\_レベル\_1**](https://msdn.microsoft.com/library/windows/hardware/ff545538)、または[ **FSCTL\_要求\_OPLOCK\_レベル\_2**](https://msdn.microsoft.com/library/windows/hardware/ff545546))。

-   ディレクトリの変更操作の通知 (**MajorFunction** IRP が\_MJ\_ディレクトリ\_制御。**MinorFunction** IRP が\_MN\_通知\_変更\_ディレクトリ)。

-   バイト範囲ロックの要求 (**MajorFunction** IRP が\_MJ\_ロック\_制御。**MinorFunction** IRP が\_MN\_ロックします)。

FLT\_PREOP\_同期は、これらの操作に対して返されることはできません。

 

 




