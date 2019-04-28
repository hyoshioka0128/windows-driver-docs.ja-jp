---
title: 操作後コールバック ルーチンの記述
description: 操作後コールバック ルーチンの記述
ms.assetid: 4940e38d-107b-45c4-aa71-6e8543330f39
keywords:
- postoperation コールバック ルーチン WDK ファイル システム ミニフィルター、書き込み
- コールバック ルーチンを記述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fb1e5ca4d47cd98c0f40d13098cdd19b37bee55
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367113"
---
# <a name="writing-postoperation-callback-routines"></a>操作後コールバック ルーチンの記述


## <span id="ddk_writing_postoperation_callback_routines_if"></span><span id="DDK_WRITING_POSTOPERATION_CALLBACK_ROUTINES_IF"></span>


1 つまたは複数を使用して、ファイル システム ミニフィルター ドライバー *postoperation コールバック ルーチン*フィルター I/O 操作をします。

Postoperation コールバック ルーチンは、次の操作のいずれかを実行できます。

-   Postoperation ルーチン内で直接作業を完了を実現します。 IRQL で達成可能なすべての完了作業&lt;= ディスパッチ\_レベル。
-   安全な IRQL で作業を完了を実現します。 返す FLT\_状態\_詳細\_処理\_安全な IRQL で処理を許可するには、必要な作業とキュー ワーカー スレッド。 ワーカー スレッドを呼び出す処理が完了したら、 [ **FltCompletePendedPostOperation** ](https://msdn.microsoft.com/library/windows/hardware/ff541897) postoperation 処理を続行します。
-   正常に作成操作をキャンセルします。

[**Postoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551107)に似ていますが、*完了ルーチン*従来のファイル システム フィルター ドライバーで使用されています。

ミニフィルター ドライバーは、登録と同じ方法で特定の種類の I/O 操作の postoperation コールバック ルーチンを登録、 [ **preoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551109)-つまり、コールバックをで格納します。ルーチンのエントリ ポイントで、 **OperationRegistration**のメンバー、 [ **FLT\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff544811)ミニフィルター ドライバーに渡される構造体パラメーターとして[ **FltRegisterFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544305)でその**DriverEntry**ルーチン。

ミニフィルター ドライバーには、preoperation または postoperation コールバック ルーチンを登録する I/O 操作の種類のみが表示されます。 ミニフィルター ドライバーは、postoperation コールバックの登録を行わずに特定の種類の I/O 操作の preoperation コールバック ルーチンを登録でき、その逆です。

各 postoperation コールバック ルーチンの定義は次のとおりです。

```cpp
typedef FLT_POSTOP_CALLBACK_STATUS 
(*PFLT_POST_OPERATION_CALLBACK) ( 
    IN OUT PFLT_CALLBACK_DATA Data, 
    IN PCFLT_RELATED_OBJECTS FltObjects, 
    IN PVOID CompletionContext, 
    IN FLT_POST_OPERATION_FLAGS Flags 
    ); 
```

IRQL で postoperation コールバック ルーチンを呼び出す、完了ルーチンのような&lt;= ディスパッチ\_レベルを任意のスレッド コンテキスト。

IRQL で呼び出される、ために = ディスパッチ\_レベル、postoperation コールバック ルーチンは、下の IRQL でなど、呼び出す必要があるカーネル モードのルーチンを呼び出すことはできません[ **FltLockUserBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff543371)または[ **RtlCompareUnicodeString**](https://msdn.microsoft.com/library/windows/hardware/ff561782)します。 同じ理由から、postoperation コールバック ルーチンで使用されている任意のデータ構造は、非ページ プールから割り当てる必要があります。

次の状況とは、前のルールをいくつかの例外です。

-   ミニフィルター ドライバーの preoperation 場合、コールバック ルーチンは FLT を返します\_PREOP\_IRP ベースの I/O 操作の場合、対応する postoperation コールバック ルーチンの同期が IRQL でと呼ばれる&lt;APC を =\_レベル、preoperation コールバック ルーチンと同じスレッド コンテキスト。

-   高速な I/O 操作の postoperation コールバック ルーチンは IRQL で呼び出されます。 パッシブ =\_preoperation コールバック ルーチンと同じスレッド コンテキストでのレベル。

-   作成後のコールバック ルーチンは IRQL で呼び出される = パッシブ\_IRP を開始したスレッドのコンテキストでは、レベル\_MJ\_作成操作です。

フィルター マネージャーは、指定した I/O 操作でミニフィルター ドライバーの postoperation コールバック ルーチンを呼び出す、ミニフィルター ドライバーは一時的に、I/O 操作を制御します。 ミニフィルター ドライバーでは、これは、次のいずれかになるまで、このコントロールが保持されます。

-   返します FLT\_POSTOP\_FINISHED\_postoperation コールバック ルーチンから処理します。

-   呼び出し[ **FltCompletePendedPostOperation** ](https://msdn.microsoft.com/library/windows/hardware/ff541897) postoperation コールバック ルーチンを保留した IRP ベースの I/O 操作が処理する作業ルーチンから。

このセクションの内容:

[完了、I/O 操作の処理を実行します。](performing-completion-processing-for-an-i-o-operation.md)

[保留中の Postoperation コールバック ルーチン内の I/O 操作](pending-an-i-o-operation-in-a-postoperation-callback-routine.md)

[Postoperation コールバック ルーチン内の I/O 操作の失敗](failing-an-i-o-operation-in-a-postoperation-callback-routine.md)

 

 




