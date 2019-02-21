---
title: 関数のロールの種類のエントリ ポイントを重複しています
description: 関数のロールの種類のエントリ ポイントを重複しています
ms.assetid: cf6604da-bd79-4adf-a08f-9b903aa91133
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d0c356561c2bae6c8dc73f097eac12b04e5f2f3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531514"
---
# <a name="duplicate-entry-points-for-a-function-role-type"></a>関数のロールの種類のエントリ ポイントを重複しています


ほとんどの関数の役割の種類は、SDV は、ドライバーが、最大でエントリ ポイントごとに 1 つのコールバック関数と仮定します。 ただしは、複数のイベント コールバック関数が関連付けられていることのあるいくつかの関数ロールの種類があります。 たとえば、KMDF ドライバーが複数をある[ *EvtTimerFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541823)または[ *EvtDpcFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541683) (EVTを使用するコールバック関数\_WDF\_タイマーと EVT\_WDF\_DPC ロール型の注釈)。 この場合は、SDV は、Sdv map.h 関数の型に整数を追加します。 たとえばには、ドライバーに 2 つの DPC コールバック関数がある場合は、SDV にマップする**楽しい\_WDF\_DPC\_1**と**楽しい\_WDF\_DPC\_2**.

ドライバーは、ロールの種類のコールバック関数の最大数を超えている場合、SDV には、次のメッセージが表示されます。

```
Static Driver Verifier found more than one entry point for '[role type]'
```

関数のロールの種類に SDV をサポートしているエントリ ポイントがある場合は、必要はありません、ドライバーに何らかの問題です。 ただし、正確な検証結果を取得する必要がありますを編集する Sdv。-map.h ファイルに重複するエントリを削除します。

次の Sdv map.h ファイルが 2 を示しています、 [ *CompletionRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff540745) 、EVT を使用して注釈が関数\_WDF\_要求\_完了\_ルーチン ロールの種類。 SDV では、Sdv map.h ファイルで定義両方**EvtRequestReadCompletionRoutine**と**EvtRequestWriteCompletionRoutine**楽しんで\_WDF\_要求\_完了\_ルーチン。

```
//Approved=false
#define fun_WDF_DRIVER_DEVICE_ADD OsrFxEvtDeviceAdd
#define fun_WDF_IO_QUEUE_IO_READ OsrFxEvtIoRead
#define fun_WDF_IO_QUEUE_IO_STOP OsrFxEvtIoStop
#define fun_WDF_DEVICE_D0_EXIT OsrFxEvtDeviceD0Exit
#define fun_WDF_REQUEST_COMPLETION_ROUTINE EvtRequestReadCompletionRoutine
#define fun_WDF_REQUEST_COMPLETION_ROUTINE EvtRequestWriteCompletionRoutine
#define fun_WDF_OBJECT_CONTEXT_CLEANUP OsrFxEvtDriverContextCleanup
#define fun_WDF_DEVICE_D0_ENTRY OsrFxEvtDeviceD0Entry
#define fun_WDF_DEVICE_PREPARE_HARDWARE OsrFxEvtDevicePrepareHardware
#define fun_WDF_IO_QUEUE_IO_WRITE OsrFxEvtIoWrite
#define fun_WDF_IO_QUEUE_IO_DEVICE_CONTROL OsrFxEvtIoDeviceControl
```

重複を削除するには、2 つ目の完了ルーチンをコメント (置換、  **\#d**で\#コメントの区切り記号を 2 つの定義 (**//**)。 **承認済み = true**検証を実行します。

```
#define fun_WDF_REQUEST_COMPLETION_ROUTINE EvtRequestReadCompletionRoutine
//efine fun_WDF_REQUEST_COMPLETION_ROUTINE EvtRequestWriteCompletionRoutine
```

Sdv map.h ファイルを編集して、もう一度の 1 つ完了ルーチンの検証の結果を表示した後、この時間コメントだけ確認されて完了ルーチンをチェック アウトしコメントを削除 (置換、 **//** で **\#d**) 確認されていない完了ルーチンから。 再度 SDV を実行します。

### <a name="span-idfunctionroletypesthatsupportmultipleentrypointsspanspan-idfunctionroletypesthatsupportmultipleentrypointsspanfunction-role-types-that-support-multiple-entry-points"></a><span id="function_role_types_that_support_multiple_entry_points"></span><span id="FUNCTION_ROLE_TYPES_THAT_SUPPORT_MULTIPLE_ENTRY_POINTS"></span>複数のエントリ ポイントをサポートする関数のロールの種類

関数の役割の種類によってでは、複数のエントリをサポートします。 エントリの数がサポートされている最大を超える SDV も重複するエントリとしてこれらを報告します。 これらの追加エントリは選択的にコメント アウトして重複するエントリを処理する同じ方法で扱うことができます、 **\#定義**コールバック ルーチン Sdv map.h ファイルと個別のステートメント検証します。 例では、ドライバーには、8 つの DPC コールバック関数が含まれている場合、(、EVT を使用する\_WDF\_DPC ロールの種類)、次を実行します。

-   Sdv map.h と遊びを定義するステートメントをコメント編集\_WDF\_DPC\_5 ~ 楽しい\_WDF\_DPC\_8。

-   ドライバーでは、SDV を実行します。

-   Sdv の map.h 楽しいを定義するには、もう一度編集\_WDF\_DPC\_5 ~ 楽しい\_WDF\_DPC\_8 と遊びを定義するステートメントをコメント\_WDF\_DPC\_1 fun ~\_WDF\_DPC\_4。

-   ドライバーでは、SDV を実行します。

参照してください[静的ドライバー検証ツール KMDF 注釈](static-driver-verifier-kmdf-function-declarations.md)に対して一連の機能ロールの種類を 1 つ以上のコールバック関数を持つことができます。 SDV は、これらのロールの種類でサポートされるコールバック関数の最大数を示します。

 

 





