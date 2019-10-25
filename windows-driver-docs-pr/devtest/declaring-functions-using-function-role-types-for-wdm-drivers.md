---
title: WDM ドライバーの関数役割型を使用した関数の宣言
description: WDM ドライバーの関数役割型を使用した関数の宣言
ms.assetid: 3260b53e-82be-4dbc-8ac5-d0e52de77f9d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52a42d75ee0447ce0fc250ead2afb40065feaa9e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840285"
---
# <a name="declaring-functions-using-function-role-types-for-wdm-drivers"></a>WDM ドライバーの関数役割型を使用した関数の宣言


WDM ドライバーを分析するときにドライバーのエントリポイントについて通知するには、関数ロール型宣言を使用して関数を宣言する必要があります。 関数ロールの種類は、Wdm で定義されています。 WDM ドライバーの*driverentry*ルーチンの各エントリポイントは、対応するロールの種類を指定して宣言する必要があります。 ロールの種類は、WDM ドライバーで認識されたエントリポイントに対応する、定義済みの typedef です。

たとえば、 *CsampUnload*というドライバーの[**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンの関数ロール型の宣言を作成するには、定義済みの typedef ドライバー\_アンロードロールの種類の宣言を使用します。 関数の役割の型の宣言は、関数定義の前に記述する必要があります。

```
DRIVER_UNLOAD CsampUnload;
```

*CsampUnload*関数の定義は変更されません。

```
VOID
CsampUnload(
    IN PDRIVER_OBJECT DriverObject
    )
{
    ...
}
```

SDV は、次の表に示すエントリポイントの種類を認識します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WDM 関数ロールの種類</th>
<th align="left">WDM ルーチン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DRIVER_INITIALIZE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize" data-raw-source="[&lt;em&gt;DriverEntry&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)"><em>DriverEntry</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>DRIVER_STARTIO</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio" data-raw-source="[&lt;em&gt;StartIO&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)"><em>StartIO</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>DRIVER_UNLOAD</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload" data-raw-source="[&lt;em&gt;Unload&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)"><em>取り除き</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>DRIVER_ADD_DEVICE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)"><em>AddDevice</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
<strong><em>Dispatch_type</em>(</strong> <em>type</em> <strong>)</strong> DRIVER_DISPATCH</td>
<td align="left"><p>ドライバーによって使用されるディスパッチルーチン。 「<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines" data-raw-source="[Writing Dispatch Routines](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines)">ディスパッチルーチンの記述</a>」を参照してください。 ドライバーエントリポイントを指定するには、  <strong><em>Dispatch_type</em>(</strong><em>型</em><strong>)</strong>注釈を DRIVER_DISPATCH role 型宣言と組み合わせて使用する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IO_COMPLETION_ROUTINE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;em&gt;IoCompletion&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)"><em>IoCompletion</em></a></p>
<p><em>Iosetcompletion ルーチン</em>または<em>IoSetCompletionRoutineEx</em>を呼び出して、2番目のパラメーターとして<em>iocompletion</em>ルーチンに関数ポインターを渡すことによって、 <em>iocompletion</em>ルーチンを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DRIVER_CANCEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel" data-raw-source="[&lt;em&gt;Cancel&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)"><em>キャンセル</em></a></p>
<p><strong>Cancel</strong>ルーチンは、 <strong>iosetcancelroutine</strong>を呼び出し、関数の2番目のパラメーターとして IRP のキャンセルルーチンに関数ポインターを渡すことによって設定されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IO_DPC_ROUTINE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine" data-raw-source="[&lt;em&gt;DpcForIsr&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)"><em>DpcForIsr</em></a></p>
<p>DpcForIsr ルーチンは、 <em>Io Edpcrequest</em>を呼び出し、関数ポインターを2番目のパラメーターとして<em>DpcForIsr</em>ルーチンに渡すことによって登録されます。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine" data-raw-source="[&lt;em&gt;DpcForIsr&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)"></a> DPC をキューに接続するには、同じ DPC オブジェクトを使用して、ISR ルーチンから<em>IoQueueDpc</em>を呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KDEFERRED_ROUTINE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine" data-raw-source="[&lt;em&gt;CustomDpc&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)"><em>CustomDpc</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine" data-raw-source="[&lt;em&gt;CustomDpc&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)"><em>Customdpc</em></a>ルーチンは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedpc" data-raw-source="[&lt;strong&gt;KeInitializeDpc&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedpc)"><strong>Keinitializer edpc</strong></a>を呼び出し、2番目のパラメーターとして<em>customdpc</em>に関数ポインターを渡すことによって設定されます。 ドライバーの<em>Customdpc</em>をキューに置いて、同じ DPC オブジェクトを使用して、ISR ルーチンから<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc" data-raw-source="[&lt;strong&gt;KeInsertQueueDpc&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)"><strong>KeInsertQueueDpc</strong></a>を呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSERVICE_ROUTINE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine" data-raw-source="[&lt;em&gt;InterruptService&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)"><em>InterruptService</em></a></p>
<p>InterruptService ルーチン (ISR) は、デバイスの割り込みを処理し、必要に応じて受信したデータの割り込み後の処理をスケジュールします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>REQUEST_POWER_COMPLETE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-request_power_complete" data-raw-source="[&lt;em&gt;PowerCompletion&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-request_power_complete)"><em>Powercompletion</em></a>コールバックルーチンは、電源 IRP の処理を完了します。 他のすべてのドライバーが IRP を完了した後に、ドライバーが追加のタスクを実行する必要がある場合、ドライバーは、IRP を割り当てる<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp" data-raw-source="[&lt;strong&gt;PoRequestPowerIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)"><strong>PoRequestPowerIrp</strong></a>ルーチンの呼び出し中に<em>powercompletion</em>コールバックルーチンを登録します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WORKER_THREAD_ROUTINE</p></td>
<td align="left"><p><em>ルーチン</em></p>
<p><em>ルーチン</em>は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl" data-raw-source="[&lt;strong&gt;ExInitializeWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)"><strong>exinitializeworkitem</strong></a>関数の2番目のパラメーターで指定されるコールバックルーチンです。</p>
<p><em>ルーチン</em>は、ドライバーが<strong>exqueueworkitem</strong>を呼び出して作業項目をシステムキューに追加する場合にのみ、このように宣言する必要があります。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idannotating_driver_dispatch_routinesspanspan-idannotating_driver_dispatch_routinesspandeclaring-driver-dispatch-routines"></a><span id="annotating_driver_dispatch_routines"></span><span id="ANNOTATING_DRIVER_DISPATCH_ROUTINES"></span>ドライバーディスパッチルーチンの宣言

ディスパッチルーチンの関数ロール型の宣言には、追加情報が必要です。 主要な IRP 関数コードを提供するディスパッチルーチンの宣言で、注釈 **\_ディスパッチ\_型\_(** <em>型</em> **)** を使用します。 この*型*は、主な i/o 関数コードです (たとえば、IRP\_MJ\_CREATE、IRP\_MJ\_CLOSE、IRP\_MJ\_システム\_コントロール)。

ドライバーのディスパッチルーチンを宣言する方法の例については、キャンセルサンプルドライバー (Cancel) のソースコードを参照してください。 ドライバーのヘッダーファイル (Cancel. h) には、 *CsampCleanup*の関数ロール型宣言があります。これは、IRP\_MJ\_クリーンアップ i/o 関数コードを処理するドライバーディスパッチルーチンです。 **\_ディスパッチ\_type\_ (** <em>型</em> **)** 注釈は、ドライバー\_ディスパッチロールの種類の宣言の前にあります。

*CsampCleanup*ルーチンは次のように宣言されます。

```
_Dispatch_type_(IRP_MJ_CLEANUP)
DRIVER_DISPATCH CsampCleanup;
```

Cancel サンプルドライバーには、IRP\_MJ\_CREATE と IRP\_MJ\_CLOSE i/o 関数コードの両方を処理するドライバーディスパッチルーチン*CsampCreateClose*もあります。 *CsampCreateClose*ルーチンは、Cancel. h で宣言されています。 このルーチンは2つの i/o 関数コードを処理するので、ドライバー\_ディスパッチロールの種類の宣言に加えて、2つの **\_ディスパッチ\_型\_** 注釈を必要とします。

```
_Dispatch_type_(IRP_MJ_CREATE)
_Dispatch_type_(IRP_MJ_CLOSE)
DRIVER_DISPATCH CsampCreateClose;
```

フィルタードライバーに、IRP\_MJ\_CREATE、IRP\_MJ\_CLOSE、IRP\_MJ\_CLEANUP、および IRP\_MJ\_デバイスを処理する、 *FilterDispatchIo*というドライバーディスパッチルーチンがあるとします。I/o 関数コードを制御します。

*FilterDispatchIo*ルーチンは、次のように resource.h で宣言されています。

```
_Dispatch_type_(IRP_MJ_CREATE)
_Dispatch_type_(IRP_MJ_CLOSE)
_Dispatch_type_(IRP_MJ_CLEANUP)
_Dispatch_type_(IRP_MJ_DEVICE_CONTROL)
DRIVER_DISPATCH FilterDispatchIo;
```

### <a name="span-idquick_steps__how_to_annotate_a_wdm_driverspanspan-idquick_steps__how_to_annotate_a_wdm_driverspanquick-steps-how-to-annotate-a-wdm-driver"></a><span id="quick_steps__how_to_annotate_a_wdm_driver"></span><span id="QUICK_STEPS__HOW_TO_ANNOTATE_A_WDM_DRIVER"></span>簡単な手順: WDM ドライバーに注釈を付ける方法

関数ロール型を使用して関数を宣言する手順は次のとおりです。

1.  *Driverentry*ルーチンのソースコードを見つけます。

2.  次のポインターに割り当てられているルーチンが、関数ロール型を使用して宣言されていることを確認します。

    ```
    DriverObject->DriverStartIo
    DriverObject->Unload
    DriverObject->DriverExtension->AddDevice 
    ```

    たとえば、次のコード例は、これらのポインター (*myDriverStartIO*、 *myunload*、および*myAddDevice*) に対応するルーチンの関数ロール型宣言を示しています。

    ```
    DRIVER_STARTIO myDriverStartIo;
    DRIVER_UNLOAD myUnload;
    DRIVER_ADD_DEVICE myAddDevice 
    ```

3.  次のポインターに割り当てられているルーチンが、ドライバー\_ディスパッチのロールの種類を使用して宣言されていて、 **\_ディスパッチ\_型\_** 注釈を持っていることを確認します。

    ```
    DriverObject->MajorFunction[IRP_MJ_xxx]
    ```

    次に、例を示します。

    ```
    _Dispatch_type_(IRP_MJ_CLEANUP)
    DRIVER_DISPATCH CsampCleanup;
    ```

### <a name="span-idfunction_parameters_and_function_role_typesspanspan-idfunction_parameters_and_function_role_typesspanfunction-parameters-and-function-role-types"></a><span id="function_parameters_and_function_role_types"></span><span id="FUNCTION_PARAMETERS_AND_FUNCTION_ROLE_TYPES"></span>関数のパラメーターと関数のロール型

C プログラミング言語で必要とされるように、関数定義で使用するパラメーター型は、関数プロトタイプのパラメーター型 (この場合は関数ロール型) と一致する必要があります。 SDV は分析のために関数シグネチャに依存しており、署名が一致しない関数は無視されます。

たとえば、IO\_COMPLETION\_ルーチン関数のロールの種類を使用して、 [**Iocompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを宣言する必要があります。

```
IO_COMPLETION_ROUTINE myCompletionRoutine;
```

*Mycompletion ルーチン*を実装する場合、パラメーターの型は、IO\_の完了\_ルーチン (つまり、pdevice\_オブジェクト、pirp、pdevice によって使用されるものと一致する必要があります (構文については「 [**iocompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチン」を参照してください)。

```
NTSTATUS
myCompletionRoutine(
 PDEVICE_OBJECT  DeviceObject,
 PIRP  Irp,
 PVOID  Context
 )
{
}
```

## <a name="span-idrunning_code_analysis_for_drivers_to_verify_the_function_declarationsspanspan-idrunning_code_analysis_for_drivers_to_verify_the_function_declarationsspan-running-code-analysis-for-drivers-to-verify-the-function-declarations"></a><span id="running_code_analysis_for_drivers_to_verify_the_function_declarations"></span><span id="RUNNING_CODE_ANALYSIS_FOR_DRIVERS_TO_VERIFY_THE_FUNCTION_DECLARATIONS"></span>ドライバーのコード分析を実行して関数の宣言を検証する


ソースコードが準備されているかどうかを判断するために、[ドライバーのコード分析](code-analysis-for-drivers.md)を実行します。 ドライバーのコード分析では、関数ロールの種類の宣言をチェックします。また、関数定義のパラメーターが関数ロール型のパラメーターと一致しない場合に、失敗した可能性がある関数宣言を識別したり、警告を表示したりすることができます。

 

 





