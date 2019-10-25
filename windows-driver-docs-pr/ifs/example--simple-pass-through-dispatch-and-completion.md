---
title: 単純なパススルーディスパッチと完了の例
description: 単純なパススルーディスパッチと完了の例
ms.assetid: dae3a450-37b1-470b-a0f3-4108075e06ac
keywords:
- IRP 完了ルーチン WDK ファイルシステム、例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfcae8b6d968581e660060832441237c55be47f8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841422"
---
# <a name="example-simple-pass-through-dispatch-and-completion"></a>例: 単純なパススルーディスパッチと完了


## <span id="ddk_example_simple_pass_through_dispatch_and_completion_if"></span><span id="DDK_EXAMPLE_SIMPLE_PASS_THROUGH_DISPATCH_AND_COMPLETION_IF"></span>


IRP の完了ルーチンを設定して IRP を停止するには、ディスパッチルーチンで次の操作を行う必要があります。

-   [**Iocopycurrent entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)呼び出して、現在のスタックの場所から次の下位レベルのドライバーのパラメーターにコピーします。

-   [**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出して、IRP の完了ルーチンを指定します。

-   [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出して、次の下位レベルのドライバーに IRP を渡します。

この手法を次のコード例に示します。

### <a name="span-iddispatch_routinespanspan-iddispatch_routinespanspan-iddispatch_routinespandispatch-routine"></a><span id="Dispatch_Routine"></span><span id="dispatch_routine"></span><span id="DISPATCH_ROUTINE"></span>ディスパッチルーチン

```cpp
IoCopyCurrentIrpStackLocationToNext( Irp ); 
IoSetCompletionRoutine( Irp,                                 // Irp
                        MyLegacyFilterPassThroughCompletion, // CompletionRoutine
                        (PVOID)recordList,                   // Context
                        TRUE,                                // InvokeOnSuccess
                        TRUE,                                // InvokeOnError
                        TRUE);                               // InvokeOnCancel
return IoCallDriver ( NextLowerDriverDeviceObject, Irp ); 
```

この例では、 [**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出して、IRP の完了ルーチンを設定します。

[**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)の呼び出しの最初の2つのパラメーターは、IRP へのポインターと、完了ルーチンの名前です。 3番目のパラメーターは、完了ルーチンに渡されるドライバー定義の構造体へのポインターです。 この構造体には、IRP で完了処理を実行するときに完了ルーチンが必要とするコンテキスト情報が含まれます。 完了ルーチンは IRQL ディスパッチ\_レベルで呼び出すことができるので、非ページプールからコンテキスト構造を割り当てる必要があります。

[**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)に渡される最後の3つのパラメーターは、i/o 要求が成功したとき、失敗したとき、または取り消されたときに、完了ルーチンを呼び出すかどうかを指定するフラグです。

### <a name="span-idcompletion_routinespanspan-idcompletion_routinespanspan-idcompletion_routinespancompletion-routine"></a><span id="Completion_Routine"></span><span id="completion_routine"></span><span id="COMPLETION_ROUTINE"></span>完了ルーチン

ディスパッチルーチンが完了ルーチンを設定し、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出した後 (上記のディスパッチルーチンに示されているように) すぐに戻る場合は、対応する完了ルーチンが IRP の pendingreturned フラグをチェックし、設定されている場合は、を呼び出し**ます。IoMarkIrpPending**。 その後、次の例に示すように、STATUS\_SUCCESS が返されます。

```cpp
if (Irp->PendingReturned) {
    IoMarkIrpPending( Irp );
}
return STATUS_SUCCESS;
```

### <a name="span-idadvantages_of_this_approachspanspan-idadvantages_of_this_approachspanspan-idadvantages_of_this_approachspanadvantages-of-this-approach"></a><span id="Advantages_of_This_Approach"></span><span id="advantages_of_this_approach"></span><span id="ADVANTAGES_OF_THIS_APPROACH"></span>このアプローチの利点

完了ルーチンを設定すると、ドライバーは、下位レベルのドライバーによって処理された後に、IRP をさらに処理することができます。 完了ルーチンは、要求された i/o 操作の結果に基づいて、IRP を処理する方法を決定できます。

### <a name="span-iddisadvantages_of_this_approachspanspan-iddisadvantages_of_this_approachspanspan-iddisadvantages_of_this_approachspandisadvantages-of-this-approach"></a><span id="Disadvantages_of_This_Approach"></span><span id="disadvantages_of_this_approach"></span><span id="DISADVANTAGES_OF_THIS_APPROACH"></span>このアプローチの欠点

IRQL &lt;= ディスパッチ\_レベルでは任意のスレッドコンテキストで実行されるため、完了ルーチンは、IRP に対して制限付きの処理のみを実行できます。

 

 




