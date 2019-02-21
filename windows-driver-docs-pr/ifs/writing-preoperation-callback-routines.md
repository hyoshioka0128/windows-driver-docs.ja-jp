---
title: Preoperation コールバック ルーチンを記述
description: Preoperation コールバック ルーチンを記述
ms.assetid: 3f863c44-152e-43c9-8ef5-ec426986a3fe
keywords:
- preoperation コールバック ルーチン WDK ファイル システム ミニフィルター、書き込み
- コールバック ルーチンを記述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06d29454c4f456bace594ecb11a55d83cc008731
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553517"
---
# <a name="writing-preoperation-callback-routines"></a>Preoperation コールバック ルーチンを記述


## <span id="ddk_writing_preoperation_callback_routines_if"></span><span id="DDK_WRITING_PREOPERATION_CALLBACK_ROUTINES_IF"></span>


1 つまたは複数を使用して、ファイル システム ミニフィルター ドライバー *preoperation コールバック ルーチン*フィルター I/O 操作をします。 [**Preoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551109)は従来のファイル システム フィルター ドライバーで使用されるディスパッチ ルーチンと似ています。

ミニフィルター ドライバーでは、特定の種類の I/O 操作の preoperation コールバック ルーチンを登録のコールバック ルーチンのエントリ ポイントを格納することにより、 **OperationRegistration**のメンバー、 [ **FLT\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff544811)構造体。 ミニフィルター ドライバーでは、このメンバーを渡すパラメーターとして[ **FltRegisterFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544305)でその**DriverEntry**ルーチン。

ミニフィルター ドライバーには、preoperation または postoperation コールバック ルーチンを登録する I/O 操作の種類のみが表示されます。 ミニフィルター ドライバーは登録を行わずに特定の種類の I/O 操作の preoperation コールバック ルーチンを登録することができます、 [ **postoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551107)、またはその逆です。

次の表では、特定の使用シナリオとその戻り値の preoperation コールバック ルーチンの実装を示します。

| 使用シナリオ                                                                                                                                                                        | 実装                                                                                                                                       | 返される値                      |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------|
| ルーチンは、操作に関連しないと、操作の最終的な状態が必要としないまたは postoperation コールバックを持ちません。                                             | 完了時にミニフィルターの postoperation コールバックを呼び出さずに、I/O 操作を渡します。                                                | FLT\_PREOP\_成功\_いいえ\_コールバック   |
| ルーチンは、操作の最終的な状態が必要です。                                                                                                                               | を通じて、postoperation コールバック ルーチンを呼び出すミニフィルターを必要とする操作を渡します。                                                     | FLT\_PREOP\_成功\_WITH\_コールバック |
| ミニフィルターは完了またはこの操作は、将来の処理を続行する必要があります。                                                                                                     | 保留中の状態に、操作を配置します。 使用[ **FltCompletePendedPreOperation** ](https://msdn.microsoft.com/library/windows/hardware/ff541913)後で、操作を完了します。 返す操作前のルーチンの間の許容の競合がある可能性があることに注意してください。 **FLT_PREOP_PENDING**、および**FltCompletePendingOperation**が呼び出されます。 フィルター マネージャーは、ドライバーからの入力を行わなくても、このシナリオを処理します。 | FLT\_PREOP\_PENDING                 |
| Postoperation 処理では、同じスレッドのコンテキストでディスパッチ ルーチンが呼び出されたことがあります。 これにより、一貫性のある IRQL とは、ローカル変数の状態を保持します。 | Postoperation で操作を同期します。                                                                                                    | FLT\_PREOP\_同期             |
| Preoperation コールバック ルーチンは、操作を完了する必要があります。                                                                                                                    | 操作の処理を停止し、最終的な NTSTATUS 値を割り当てます。                                                                                   | FLT\_PREOP\_完了                |


各 preoperation コールバック ルーチンの定義は次のとおりです。

```cpp
typedef FLT_PREOP_CALLBACK_STATUS 
(*PFLT_PRE_OPERATION_CALLBACK) ( 
    IN OUT PFLT_CALLBACK_DATA Data, 
    IN PCFLT_RELATED_OBJECTS FltObjects, 
    OUT PVOID *CompletionContext 
    ); 
```

ディスパッチ ルーチンのように、IRQL で preoperation コールバック ルーチンを呼び出すことができます = パッシブ\_レベル、または IRQL = APC\_レベル。 IRQL で呼び出された通常 = パッシブ\_I/O 要求を生成したスレッドのコンテキストでのレベル。 Preoperation コールバック ルーチンに常に IRQL でと呼ばれる高速な I/O とファイル システム フィルター (FsFilter) 操作では、パッシブ =\_レベル。 ただし、IRP ベースの操作では、ミニフィルター ドライバーの preoperation コールバック ルーチンを呼び出すシステム ワーカー スレッドのコンテキストで上位フィルターまたはミニフィルター ドライバー アプリケーションの場合、操作を処理するため、ワーカー スレッドが。

IRQL で postoperation ルーチン内でコンテキスト オブジェクトを取得できない&gt;APC\_レベル。 代わりに、preoperation ルーチンの中に、コンテキスト オブジェクトを取得する postoperation ルーチンに渡すか IRQL で postoperation 処理を行う&lt;APC を =\_レベル。 コンテキストの詳細については、次を参照してください。[管理コンテキスト](managing-contexts.md)します。

フィルター マネージャーは、指定した I/O 操作でミニフィルター ドライバーの preoperation コールバック ルーチンを呼び出す、ミニフィルター ドライバーは一時的に、I/O 操作を制御します。 ミニフィルター ドライバーでは、これは、次のいずれかになるまで、このコントロールが保持されます。

-   FLT 以外のステータス値を返します\_PREOP\_preoperation コールバック ルーチンから保留します。

-   呼び出し[ **FltCompletePendedPreOperation** ](https://msdn.microsoft.com/library/windows/hardware/ff541913) preoperation コールバック ルーチンを保留していた操作が処理する作業ルーチンから。

このセクションの内容:

[下位のミニフィルター インスタンス スタック、I/O 操作を渡す](passing-an-i-o-operation-down-the-minifilter-driver-instance-stack.md)

[Preoperation コールバック ルーチン内の I/O 操作の完了](completing-an-i-o-operation-in-a-preoperation-callback-routine.md)

[Preoperation コールバック ルーチンで高速な I/O 操作を禁止しています](disallowing-a-fast-i-o-operation-in-a-preoperation-callback-routine.md)

[保留中の Preoperation コールバック ルーチン内の I/O 操作](pending-an-i-o-operation-in-a-preoperation-callback-routine.md)

 

 




