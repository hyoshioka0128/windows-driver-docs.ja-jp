---
title: 操作後コールバック ルーチンの記述
description: 操作後コールバック ルーチンの記述
ms.assetid: 4940e38d-107b-45c4-aa71-6e8543330f39
keywords:
- postoperation コールバックルーチン WDK ファイルシステムミニフィルター、書き込み
- コールバックルーチンの記述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22a41557c7994e7cf5ac38da43fb858c7c7a08f1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840920"
---
# <a name="writing-postoperation-callback-routines"></a>操作後コールバック ルーチンの記述


## <span id="ddk_writing_postoperation_callback_routines_if"></span><span id="DDK_WRITING_POSTOPERATION_CALLBACK_ROUTINES_IF"></span>


ファイルシステムミニフィルタードライバーは、1つまたは複数の*postoperation コールバックルーチン*を使用して、i/o 操作をフィルター処理します。

Postoperation コールバックルーチンは、次のいずれかのアクションを実行できます。

-   Postoperation ルーチンで、完了作業を直接実行します。 すべての完了作業は、IRQL &lt;= ディスパッチ\_レベルで実現できます。
-   安全な IRQL で完了作業を実行します。 \_\_状態を返します。\_処理\_必要であり、ワーカースレッドをキューに置いて、安全な IRQL での処理を許可します。 処理が完了すると、ワーカースレッドは[**Fltcompletependedpostoperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpostoperation)を呼び出して postoperation 処理を続行します。
-   正常な作成操作をキャンセルします。

[**Postoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)は、従来のファイルシステムフィルタードライバーで使用される*完了ルーチン*に似ています。

ミニフィルタードライバーは、特定の種類の i/o 操作に対して postoperation コールバックルーチンを登録します。これは、 [**preoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)を登録するのと同じ方法で、つまり、コールバックルーチンのエントリポイントを operationregistration に格納します。 [**FLT\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)構造のメンバーで、ミニフィルタードライバーは、その**Driverentry**ルーチンの[**fltregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)にパラメーターとして渡します。

ミニフィルタードライバーは、preoperation または postoperation コールバックルーチンが登録されている種類の i/o 操作だけを受け取ります。 ミニフィルタードライバーは、postoperation コールバックを登録せずに、特定の種類の i/o 操作に対して preoperation コールバックルーチンを登録できます。逆の場合も同様です。

すべての postoperation コールバックルーチンは、次のように定義されます。

```cpp
typedef FLT_POSTOP_CALLBACK_STATUS 
(*PFLT_POST_OPERATION_CALLBACK) ( 
    IN OUT PFLT_CALLBACK_DATA Data, 
    IN PCFLT_RELATED_OBJECTS FltObjects, 
    IN PVOID CompletionContext, 
    IN FLT_POST_OPERATION_FLAGS Flags 
    ); 
```

完了ルーチンと同様に、postoperation コールバックルーチンは、任意のスレッドコンテキストで、IRQL &lt;= ディスパッチ\_レベルで呼び出されます。

IRQL = ディスパッチ\_レベルで呼び出すことができるため、postoperation コールバックルーチンは、 [**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)や[**RtlCompareUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcompareunicodestring)などの低い irql で呼び出す必要があるカーネルモードルーチンを呼び出すことはできません。 同じ理由から、postoperation コールバックルーチンで使用されるデータ構造は、非ページプールから割り当てられる必要があります。

次のような状況では、上記の規則に対していくつかの例外があります。

-   ミニフィルタードライバーの preoperation コールバックルーチンが、IRP ベースの i/o 操作に対して FLT\_PREOPERATION\_SYNCHRONIZE を返した場合、対応する postoperation コールバックルーチンは、同じスレッド内の IRQL &lt;= APC\_レベルで呼び出されます。preoperation コールバックルーチンとしてのコンテキスト。

-   高速 i/o 操作の postoperation コールバックルーチンは、preoperation コールバックルーチンと同じスレッドコンテキストで、IRQL = パッシブ\_レベルで呼び出されます。

-   作成後のコールバックルーチンは、IRP\_MJ\_CREATE 操作を開始したスレッドのコンテキストで、IRQL = パッシブ\_レベルで呼び出されます。

フィルターマネージャーが、特定の i/o 操作に対してミニフィルタードライバーの postoperation コールバックルーチンを呼び出すと、ミニフィルタードライバーによって i/o 操作が一時的に制御されます。 ミニフィルタードライバーは、次のいずれかの操作を実行するまで、このコントロールを保持します。

-   Postoperation コールバックルーチンからの処理\_完了した FLT\_POSTOP\_を返します。

-   Postoperation コールバックルーチンで保留されていた IRP ベース i/o 操作を処理した作業ルーチンから[**Fltcompletependedpostoperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpostoperation)を呼び出します。

このセクションの内容:

[I/o 操作の完了処理を実行しています](performing-completion-processing-for-an-i-o-operation.md)

[Postoperation コールバックルーチンで i/o 操作を保留しています](pending-an-i-o-operation-in-a-postoperation-callback-routine.md)

[Postoperation コールバックルーチンでの i/o 操作の失敗](failing-an-i-o-operation-in-a-postoperation-callback-routine.md)

 

 




