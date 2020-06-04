---
title: WDM ドライバーの関数役割型を使用した関数の宣言
description: WDM ドライバーの関数役割型を使用した関数の宣言
ms.assetid: 3260b53e-82be-4dbc-8ac5-d0e52de77f9d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8710aff79de9d8772229a6b3b38c8b2efeb07f16
ms.sourcegitcommit: a386cf5ac5a157dfe1041e7c23b6e70a33ca2704
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/03/2020
ms.locfileid: "84330062"
---
# <a name="declaring-functions-using-function-role-types-for-wdm-drivers"></a>WDM ドライバーの関数役割型を使用した関数の宣言

> [!NOTE]
> Windows 10 バージョン2004以降、[スタティックドライバー検証ツール](https://review.docs.microsoft.com/en-us/windows-hardware/drivers/devtest/static-driver-verifier)(sdv) では、WDM ドライバーのディスパッチルーチンのロールの種類を識別するための注釈が不要になりました。  このページの「*基本および高度な初期化*」セクションのガイダンスに従ってください。

WDM ドライバーを分析するときにドライバーのエントリポイントについて通知するには、関数ロール型宣言を使用して関数を宣言する必要があります。 関数ロールの種類は、Wdm で定義されています。 WDM ドライバーの*driverentry*ルーチンの各エントリポイントは、対応するロールの種類を指定して宣言する必要があります。 ロールの種類は、WDM ドライバーで認識されたエントリポイントに対応する、定義済みの typedef です。

たとえば、 *CsampUnload*というドライバーの[**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンの関数ロール型の宣言を作成するには、定義済みの typedef ドライバーのアンロードロールの種類の宣言を使用し \_ ます。 関数の役割の型の宣言は、関数定義の前に記述する必要があります。

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
<strong><em>Dispatch_type</em>(</strong> <em>型</em> <strong>)</strong> DRIVER_DISPATCH</td>
<td align="left"><p>ドライバーによって使用されるディスパッチルーチン。 「<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines" data-raw-source="[Writing Dispatch Routines](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines)">ディスパッチルーチンの記述</a>」を参照してください。</p></td>
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
<p>DpcForIsr ルーチンは、 <em>Io Edpcrequest</em>を呼び出し、関数ポインターを2番目のパラメーターとして<em>DpcForIsr</em>ルーチンに渡すことによって登録されます。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine" data-raw-source="[&lt;em&gt;DpcForIsr&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)"><em>DpcForIsr</em></a> DPC をキューに接続するには、同じ DPC オブジェクトを使用して、ISR ルーチンから<em>IoQueueDpc</em>を呼び出します。</p></td>
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
<td align="left"><p><em>ルーチンによって返される値</em></p>
<p><em>ルーチン</em>は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl" data-raw-source="[&lt;strong&gt;ExInitializeWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)"><strong>exinitializeworkitem</strong></a>関数の2番目のパラメーターで指定されるコールバックルーチンです。</p>
<p><em>ルーチン</em>は、ドライバーが<strong>exqueueworkitem</strong>を呼び出して作業項目をシステムキューに追加する場合にのみ、このように宣言する必要があります。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idannotating_driver_dispatch_routinesspanspan-idannotating_driver_dispatch_routinesspandeclaring-driver-dispatch-routines"></a><span id="annotating_driver_dispatch_routines"></span><span id="ANNOTATING_DRIVER_DISPATCH_ROUTINES"></span>ドライバーディスパッチルーチンの宣言

Windows 10 バージョン2004以降では、WDM ドライバーの Driverobject ルーチンの DriverObject->MajorFunction テーブルの初期化に基づいて、ディスパッチルーチンの関数ロール型の宣言が IRP カテゴリに自動的に調整されます。  

ドライバー Foo は、SDV に準拠するために、基本または高度な宣言のスタイルを使用して、ロールの宣言を行う必要があります。  

#### <a name="basic-and-advanced-initializations"></a>基本初期化と高度な初期化

基本スタイルは次の例のようになります (ディスパッチルーチン名 FooCreate と FooCleanup は単純な例であり、適切な名前を使用できます)。

```
DriverObject->MajorFunction[IRP_MJ_CREATE] = FooCreate; //Basic style
DriverObject->MajorFunction[IRP_MJ_CLEANUP] = FooCleanup;
```

必要なリストを短縮するために、より高度な方法を取ることができます。  複数の IRP カテゴリに対して同じディスパッチルーチンが使用されていますが、ドライバーは次のように2つの初期化をエンコードできます。

```
DriverObject->MajorFunction[IRP_MJ_CREATE] = 
DriverObject->MajorFunction[IRP_MJ_CLEANUP] = FooCreateCleanup; // Advanced style for a multi-role dispatch routine 
```

ドライバーが SDV を正常に実行できるようにするには、**ドライバーは、上に示した*基本*スタイルまたは*高度な*スタイルのいずれかを使用する必要があり**ます。  この2つの方法のいずれかが使用されていない場合、ドライバーの SDV 検証**は想定どおりに動作しません**。

### <a name="span-idfunction_parameters_and_function_role_typesspanspan-idfunction_parameters_and_function_role_typesspanfunction-parameters-and-function-role-types"></a><span id="function_parameters_and_function_role_types"></span><span id="FUNCTION_PARAMETERS_AND_FUNCTION_ROLE_TYPES"></span>関数のパラメーターと関数のロール型

C プログラミング言語で必要とされるように、関数定義で使用するパラメーター型は、関数プロトタイプのパラメーター型 (この場合は関数ロール型) と一致する必要があります。 SDV は分析のために関数シグネチャに依存しており、署名が一致しない関数は無視されます。

たとえば、IO 完了ルーチンの役割の種類を使用して、 [**Iocompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを宣言する必要があり \_ \_ ます。

```
IO_COMPLETION_ROUTINE myCompletionRoutine;
```

*Mycompletion ルーチン*を実装する場合、パラメーターの型は、IO \_ 完了ルーチン ( \_ つまり、PDEVICE オブジェクト、PIRP、および pdevice) で使用されているものと一致する必要があり \_ ます (構文については、「 [**iocompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチン」を参照してください)。

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
