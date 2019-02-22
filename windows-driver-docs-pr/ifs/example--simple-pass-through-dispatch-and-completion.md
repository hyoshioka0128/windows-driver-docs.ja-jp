---
title: 例の単純なパススルー ディスパッチと完了
description: 例の単純なパススルー ディスパッチと完了
ms.assetid: dae3a450-37b1-470b-a0f3-4108075e06ac
keywords:
- IRP の完了ルーチン WDK ファイル システム、例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2deba7b3bc230bd92ee4e6ec35651063035c4d08
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561061"
---
# <a name="example-simple-pass-through-dispatch-and-completion"></a>以下に例を示します。単純なパススルー ディスパッチと完了


## <span id="ddk_example_simple_pass_through_dispatch_and_completion_if"></span><span id="DDK_EXAMPLE_SIMPLE_PASS_THROUGH_DISPATCH_AND_COMPLETION_IF"></span>


IRP の完了ルーチンを設定して、IRP を渡す、ディスパッチ ルーチンは、次の操作を行う必要があります。

-   呼び出す[ **IoCopyCurrentIrpStackLocationToNext** ](https://msdn.microsoft.com/library/windows/hardware/ff548387)パラメーターの現在のスタックの場所から下位レベルの次のドライバーのコピー。

-   呼び出す[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679) IRP の完了ルーチンを指定します。

-   呼び出す[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)を下位レベルの次のドライバーに IRP を渡します。

この手法は、次のコード例に示します。

### <a name="span-iddispatchroutinespanspan-iddispatchroutinespanspan-iddispatchroutinespandispatch-routine"></a><span id="Dispatch_Routine"></span><span id="dispatch_routine"></span><span id="DISPATCH_ROUTINE"></span>ディスパッチ ルーチン

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

この例への呼び出しで[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679) IRP の完了ルーチンを設定します。

最初の 2 つのパラメーターへの呼び出しで[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)は IRP 完了ルーチンの名前へのポインター。 3 番目のパラメーターでは、完了ルーチンに渡されるドライバー定義構造体へのポインターです。 この構造体には、完了ルーチンが IRP の完了処理を実行するときに必要のあるコンテキスト情報が含まれています。 Context 構造は、IRQL のディスパッチの完了ルーチンを呼び出すことがあるために、非ページ プールから割り当てる必要がある\_レベル。

最後の 3 つのパラメーターに渡す[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)が I/O 要求が成功すると、失敗した場合、またはが取り消されたときに、完了ルーチンを呼び出すかどうかを指定するフラグ。

### <a name="span-idcompletionroutinespanspan-idcompletionroutinespanspan-idcompletionroutinespancompletion-routine"></a><span id="Completion_Routine"></span><span id="completion_routine"></span><span id="COMPLETION_ROUTINE"></span>完了ルーチン

ディスパッチ ルーチンが完了ルーチンを設定し、呼び出した後すぐに返された場合[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336) (ように、上記のディスパッチ ルーチン)、対応する完了ルーチンを確認する必要があります、IRP の PendingReturned フラグを設定し、設定されている場合は、呼び出す**IoMarkIrpPending**します。 状態を返す必要があります\_成功すると、次の例に示すようにします。

```cpp
if (Irp->PendingReturned) {
    IoMarkIrpPending( Irp );
}
return STATUS_SUCCESS;
```

### <a name="span-idadvantagesofthisapproachspanspan-idadvantagesofthisapproachspanspan-idadvantagesofthisapproachspanadvantages-of-this-approach"></a><span id="Advantages_of_This_Approach"></span><span id="advantages_of_this_approach"></span><span id="ADVANTAGES_OF_THIS_APPROACH"></span>このアプローチの利点

完了ルーチンを設定すると、下位レベルのドライバーが処理された後、プロセス、IRP をさらに、ドライバーができます。 完了ルーチンでは、要求された I/O 操作の結果に基づいて IRP の処理方法を決定できます。

### <a name="span-iddisadvantagesofthisapproachspanspan-iddisadvantagesofthisapproachspanspan-iddisadvantagesofthisapproachspandisadvantages-of-this-approach"></a><span id="Disadvantages_of_This_Approach"></span><span id="disadvantages_of_this_approach"></span><span id="DISADVANTAGES_OF_THIS_APPROACH"></span>このアプローチの欠点

IRQL で任意のスレッド コンテキストで実行されるため&lt;= ディスパッチ\_レベル、完了のルーチンに対して実行できる限定的な処理だけ IRP します。

 

 




