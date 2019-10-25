---
title: 関数ロールの種類のエントリポイントが重複しています
description: 関数ロールの種類のエントリポイントが重複しています
ms.assetid: cf6604da-bd79-4adf-a08f-9b903aa91133
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 392d542012d83396223c12909089f4d510298577
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839561"
---
# <a name="duplicate-entry-points-for-a-function-role-type"></a>関数ロールの種類のエントリポイントが重複しています


ほとんどの関数ロールの種類では、SDV は、ドライバーがエントリポイントごとに1つのコールバック関数を持つことを前提としています。 ただし、複数のイベントコールバック関数を関連付けることができる関数ロール型がいくつかあります。 たとえば、KMDF ドライバーには、複数の[*Evttimerfunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer)または[*EvtDpcFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc) callback 関数 (.EVT\_WDF\_TIMER および .EVT\_WDF\_DPC ロールの種類の注釈を使用する) が含まれている場合があります。 この場合、SDV は、Sdv-map. h の関数型に整数を追加します。 たとえば、ドライバーに DPC コールバック関数が2つある場合、SDV はそれらを**WDF\_dpc\_1**にマップし、 **WDF\_dpc\_2\_を楽しく\_** します。

ドライバーがロールの種類のコールバック関数の最大数を超えると、SDV によって次のメッセージが表示されます。

```
Static Driver Verifier found more than one entry point for '[role type]'
```

機能ロールの種類に SDV がサポートしているエントリポイントが多い場合、ドライバーに問題があるとは限りません。 ただし、正確な検証結果を取得するには、Sdv.-map .h ファイルを編集して、重複するエントリを削除する必要があります。

たとえば、次の Sdv マップ .h ファイルは、.EVT\_WDF\_REQUEST\_COMPLETION\_ルーチンロールの種類を使用して注釈が付けられ[*た2つ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)の入力候補関数があることを示しています。 Sdv-map .h ファイルで、SDV は**Evtrequestreadcompletion ルーチン**と**EvtRequestWriteCompletionRoutine**を定義し、WDF\_REQUEST\_完了\_ルーチンを\_します。

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

重複を削除するには、2番目の完了ルーチンをコメントアウトします (\#定義の **\#d**を2つのコメント区切り記号 ( **//** ) で置き換えます。 次に、[**承認済み] = true**に設定し、検証を実行します。

```
#define fun_WDF_REQUEST_COMPLETION_ROUTINE EvtRequestReadCompletionRoutine
//efine fun_WDF_REQUEST_COMPLETION_ROUTINE EvtRequestWriteCompletionRoutine
```

検証の結果を1つの完了ルーチンで確認した後、Sdv .h ファイルをもう一度編集しますが、今回は検証した直後の完了ルーチンをコメントアウトし、コメントを削除します ( **//** を\#d に置き換えます。) を入力します。 次に、SDV をもう一度実行します。

### <a name="span-idfunction_role_types_that_support_multiple_entry_pointsspanspan-idfunction_role_types_that_support_multiple_entry_pointsspanfunction-role-types-that-support-multiple-entry-points"></a><span id="function_role_types_that_support_multiple_entry_points"></span><span id="FUNCTION_ROLE_TYPES_THAT_SUPPORT_MULTIPLE_ENTRY_POINTS"></span>複数のエントリポイントをサポートする関数ロールの種類

一部の関数ロールの種類では、複数のエントリがサポートしています。 サポートされる最大数を超えると、SDV はこれらのエントリを重複エントリとして報告します。 これらの追加エントリは、重複するエントリを処理するのと同じ方法で扱うことができます。そのためには、Sdv .h ファイルのコールバックルーチンの **\#define**ステートメントを選択的にコメントアウトし、個別の検証を行います。 たとえば、ドライバーに8つの DPC コールバック関数 (.EVT\_WDF\_DPC ロールの種類が使用されている) がある場合は、次の操作を行うことができます。

-   Sdv-map .h を編集し、楽しい\_WDF\_DPC\_5 から楽しい\_WDF\_DPC\_8 までの define ステートメントをコメントアウトします。

-   ドライバーで SDV を実行します。

-   次に、Sdv-map .h をもう一度編集して、WDF\_DPC\_5 から楽しい\_WDF\_DPC\_8 を\_定義し、WDF\_DPC\_1 ~ 楽しい\_の define ステートメントをコメントアウトします。\_WDF\_DPC\_4。

-   ドライバーで SDV を実行します。

複数のコールバック関数を持つことができる関数ロール型の一覧については、「 [Static Driver Verifier KMDF 注釈](static-driver-verifier-kmdf-function-declarations.md)」を参照してください。 リストには、これらのロールの種類で SDV がサポートするコールバック関数の最大数が表示されます。

 

 





