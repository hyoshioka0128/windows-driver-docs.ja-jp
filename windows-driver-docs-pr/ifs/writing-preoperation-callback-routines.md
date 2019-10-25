---
title: 操作前コールバック ルーチンの記述
description: 操作前コールバック ルーチンの記述
ms.assetid: 3f863c44-152e-43c9-8ef5-ec426986a3fe
keywords:
- preoperation コールバックルーチン WDK ファイルシステムミニフィルター、書き込み
- コールバックルーチンの記述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16ed8db6369565dd0695d6c9a5dec54daaf5f47b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840915"
---
# <a name="writing-preoperation-callback-routines"></a>操作前コールバック ルーチンの記述


## <span id="ddk_writing_preoperation_callback_routines_if"></span><span id="DDK_WRITING_PREOPERATION_CALLBACK_ROUTINES_IF"></span>


ファイルシステムミニフィルタードライバーは、1つまたは複数の*preoperation コールバックルーチン*を使用して、i/o 操作をフィルター処理します。 [**Preoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)は、従来のファイルシステムフィルタードライバーで使用されるディスパッチルーチンに似ています。

ミニフィルタードライバーは、 [**FLT\_REGISTRATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)構造体の**operationregistration**メンバーにコールバックルーチンのエントリポイントを格納することによって、特定の種類の i/o 操作に対して preoperation コールバックルーチンを登録します。 ミニパスドライバーは、このメンバーを**Driverentry**ルーチンの[**Fltregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)にパラメーターとして渡します。

ミニフィルタードライバーは、preoperation または postoperation コールバックルーチンが登録されている種類の i/o 操作だけを受け取ります。 ミニフィルタードライバーは、 [**postoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)を登録せずに、特定の種類の i/o 操作に対して preoperation コールバックルーチンを登録できます。また、その逆も可能です。

次の表は、特定の使用シナリオとその戻り値に対する preoperation コールバックルーチンの実装を示しています。

| 使用シナリオ                                                                                                                                                                        | 実装                                                                                                                                       | 返される値                      |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------|
| このルーチンは操作に関連しないため、操作の最終ステータスを必要としないか、postoperation コールバックがありません。                                             | 完了時にミニフィルターの postoperation コールバックを呼び出さずに、i/o 操作をパススルーします。                                                | FLT\_PREOP\_SUCCESS\_\_コールバックなし   |
| ルーチンには、操作の最終状態が必要です。                                                                                                                               | 操作を通過し、ミニパスコールバックルーチンを呼び出す必要があります。                                                     | \_コールバックを使用した FLT\_PREOP\_成功\_ |
| ミニフィルターを完了するか、今後この操作の処理を続行する必要があります。                                                                                                     | 操作を保留中の状態にします。 後で操作を完了するには、 [**Fltcompletependedpreoperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation)を使用します。 **FLT_PREOP_PENDING**を返す事前操作ルーチンと**Fltcompletependingoperation**が呼び出される間に、許容される競合が発生する可能性があることに注意してください。 フィルターマネージャーは、ドライバーからの入力なしにこのシナリオを処理します。 | FLT\_PREOP\_保留中                 |
| Postoperation の処理は、ディスパッチルーチンが呼び出されたのと同じスレッドのコンテキストで行われる必要があります。 これにより、一貫性のある IRQL が確保され、ローカル変数の状態が維持されます。 | 操作を postoperation と同期します。                                                                                                    | FLT\_PREOP\_SYNCHRONIZE             |
| Preoperation コールバックルーチンは、操作を完了する必要があります。                                                                                                                    | 操作の処理を停止し、最後の NTSTATUS 値を割り当てます。                                                                                   | FLT\_PREOP\_完了                |


すべての preoperation コールバックルーチンは、次のように定義されます。

```cpp
typedef FLT_PREOP_CALLBACK_STATUS 
(*PFLT_PRE_OPERATION_CALLBACK) ( 
    IN OUT PFLT_CALLBACK_DATA Data, 
    IN PCFLT_RELATED_OBJECTS FltObjects, 
    OUT PVOID *CompletionContext 
    ); 
```

ディスパッチルーチンと同様に、preoperation コールバックルーチンは、IRQL = パッシブ\_レベル、または IRQL = APC\_レベルで呼び出すことができます。 通常、これは、i/o 要求を発信したスレッドのコンテキストで、IRQL = パッシブ\_レベルで呼び出されます。 高速 i/o およびファイルシステムフィルター (FsFilter) 操作の場合、preoperation コールバックルーチンは常に IRQL = パッシブ\_レベルで呼び出されます。 ただし、IRP ベースの操作では、より高いフィルターまたはミニフィルタードライバーによってワーカースレッドによる処理が pends された場合、システムワーカースレッドのコンテキストでミニフィルタードライバーの preoperation コールバックルーチンを呼び出すことができます。

IRQL &gt; APC\_レベルで、postoperation ルーチンでコンテキストオブジェクトを取得することはできません。 代わりに、preoperation ルーチンでコンテキストオブジェクトを取得し、それを postoperation ルーチンに渡すか、または IRQL &lt;= APC\_LEVEL で postoperation 処理を実行します。 コンテキストの詳細については、「[コンテキストの管理](managing-contexts.md)」を参照してください。

フィルターマネージャーが、特定の i/o 操作に対してミニフィルタードライバーの preoperation コールバックルーチンを呼び出すと、ミニフィルタードライバーによって i/o 操作が一時的に制御されます。 ミニフィルタードライバーは、次のいずれかの操作を実行するまで、このコントロールを保持します。

-   Preop コールバックルーチンから PENDING\_PREOP\_PENDING 以外の状態値を返します。

-   Preoperation コールバックルーチンで保留されていた操作を処理した作業ルーチンから[**Fltcompletependedpreoperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation)を呼び出します。

このセクションの内容:

[I/o 操作をミニフィルターインスタンススタックに渡す](passing-an-i-o-operation-down-the-minifilter-driver-instance-stack.md)

[Preoperation コールバックルーチンでの i/o 操作の完了](completing-an-i-o-operation-in-a-preoperation-callback-routine.md)

[Preoperation コールバックルーチンで高速 i/o 操作を禁止する](disallowing-a-fast-i-o-operation-in-a-preoperation-callback-routine.md)

[プリ操作コールバックルーチンで i/o 操作を保留しています](pending-an-i-o-operation-in-a-preoperation-callback-routine.md)

 

 




