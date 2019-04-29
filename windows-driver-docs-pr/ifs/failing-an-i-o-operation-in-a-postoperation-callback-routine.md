---
title: 操作後コールバック ルーチン内で I/O 操作を失敗とする
description: 操作後コールバック ルーチン内で I/O 操作を失敗とする
ms.assetid: 45897bca-1573-42c5-ad00-3198b7362d9e
keywords:
- postoperation コールバック ルーチン WDK ファイル システム ミニフィルター、失敗した操作
- I/O 操作の WDK ファイル システム ミニフィルターの失敗
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f83823796137d940872f2759d5d6e40f3559eadd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383842"
---
# <a name="failing-an-io-operation-in-a-postoperation-callback-routine"></a>操作後コールバック ルーチン内で I/O 操作を失敗とする


## <span id="ddk_failing_an_io_operation_in_a_postoperation_callback_routine_if"></span><span id="DDK_FAILING_AN_IO_OPERATION_IN_A_POSTOPERATION_CALLBACK_ROUTINE_IF"></span>


ミニフィルター ドライバーの[ **postoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551107) I/O 操作の成功をフェールオーバーできますが、単に、I/O 操作が失敗しても、操作の効果は取り消されません。 ミニフィルター ドライバーは、操作を元に戻すために必要な処理を実行します。

たとえば、ミニフィルター ドライバーの作成後のコールバック ルーチンには、成功した IRP が失敗する可能性が\_MJ\_次の手順を実行することによって作成操作。

1.  呼び出す[ **FltCancelFileOpen** ](https://msdn.microsoft.com/library/windows/hardware/ff541784)を作成または作成操作によって開かれたファイルを閉じます。 なお**FltCancelFileOpen**ファイルへの変更を取り消すことはできません。 たとえば、 **FltCancelFileOpen**前のサイズに切り捨てられたファイルを復元または新しく作成されたファイルを削除しません。

2.  コールバックのデータ構造体の設定**IoStatus.Status**フィールドの操作の最終的な NTSTATUS 値にします。 この値は有効なエラー状態などの NTSTATUS 値である必要があります\_アクセス\_が拒否されました。

3.  コールバックのデータ構造体の設定**IoStatus.Information**フィールドをゼロにします。

4.  返す FLT\_POSTOP\_FINISHED\_処理します。

コールバックのデータ構造体の設定時に**IoStatus.Status**ミニフィルター ドライバー操作の最終的な NTSTATUS 値にフィールドが有効なエラー NTSTATUS 値を指定する必要があります。 ミニフィルター ドライバーが状態を指定できないことに注意してください\_FLT\_DISALLOW\_高速\_IO; のみ、フィルター マネージャーはこの NTSTATUS 値を使用します。

呼び出し元[ **FltCancelFileOpen** ](https://msdn.microsoft.com/library/windows/hardware/ff541784) IRQL で実行する必要があります&lt;APC を =\_レベル。 ただし、ミニフィルター ドライバーをこのルーチンから安全に呼び出す、ため、コールバック ルーチンを作成後 IRP の\_MJ\_作成操作、postoperation コールバック ルーチンは IRQL で呼び出されますパッシブ =\_レベルを、。作成操作を開始したスレッドのコンテキスト。

 

 




