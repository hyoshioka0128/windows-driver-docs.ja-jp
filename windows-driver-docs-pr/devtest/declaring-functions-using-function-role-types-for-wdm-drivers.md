---
title: WDM ドライバーの関数役割型を使用した関数の宣言
description: WDM ドライバーの関数役割型を使用した関数の宣言
ms.assetid: 3260b53e-82be-4dbc-8ac5-d0e52de77f9d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 323741b3abc1f1a8653181cc554b51731f4d82ce
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394097"
---
# <a name="declaring-functions-using-function-role-types-for-wdm-drivers"></a>WDM ドライバーの関数役割型を使用した関数の宣言


SDV は、WDM ドライバーを分析するときに、通知には、ドライバーのエントリ ポイント、するには、関数の役割の種類の宣言を使用して関数を宣言する必要があります。 関数のロールの種類は、Wdm.h で定義されます。 内の各エントリ ポイント、 *DriverEntry* WDM ドライバー ルーチンは、対応するロールの種類を指定することで宣言する必要があります。 ロールの種類は、WDM ドライバーで認識されているエントリ ポイントに対応する定義済みの typedef です。

たとえば、ドライバーの関数の役割の型宣言を作成する[**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)というルーチン*CsampUnload*、定義済み typedef ドライバーを使用して、\_ロールの種類の宣言をアンロードします。 関数のロールの種類の宣言は、関数定義の前に表示する必要があります。

```
DRIVER_UNLOAD CsampUnload;
```

定義、 *CsampUnload*関数は変更されません。

```
VOID
CsampUnload(
    IN PDRIVER_OBJECT DriverObject
    )
{
    ...
}
```

SDV は、次の表に示すようにエントリ ポイントの種類を認識します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize" data-raw-source="[&lt;em&gt;DriverEntry&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)"><em>DriverEntry</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>DRIVER_STARTIO</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio" data-raw-source="[&lt;em&gt;StartIO&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)"><em>StartIO</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>DRIVER_UNLOAD</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload" data-raw-source="[&lt;em&gt;Unload&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)"><em>アンロード</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>DRIVER_ADD_DEVICE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)"><em>AddDevice</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
<strong><em>Dispatch_type</em>(</strong> <em>型</em> <strong>)</strong> DRIVER_DISPATCH</td>
<td align="left"><p>ドライバーで使用されるディスパッチ routine(s) します。 参照してください<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines" data-raw-source="[Writing Dispatch Routines](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines)">ディスパッチ ルーチンを記述</a>します。 <strong><em>Dispatch_type</em>(</strong><em>型</em><strong>)</strong> DRIVER_DISPATCH ロールの種類の宣言を指定すると、注釈を組み合わせることは、ドライバーのエントリ ポイント。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IO_COMPLETION_ROUTINE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;em&gt;IoCompletion&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)"><em>IoCompletion</em></a></p>
<p><em>IoCompletion</em>ルーチンを呼び出すことによって設定<em>IoSetCompletionRoutine</em>または<em>IoSetCompletionRoutineEx</em>への関数ポインターを渡すと、 <em>IoCompletion</em> 2 番目のパラメーターとしてルーチン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DRIVER_CANCEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel" data-raw-source="[&lt;em&gt;Cancel&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)"><em>キャンセル</em></a></p>
<p><strong>キャンセル</strong>ルーチンを呼び出すことによって設定<strong>IoSetCancelRoutine</strong>関数の 2 番目のパラメーターとして IRP の関数ポインターをキャンセル ルーチンに渡すとします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IO_DPC_ROUTINE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine" data-raw-source="[&lt;em&gt;DpcForIsr&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)"><em>DpcForIsr</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine" data-raw-source="[&lt;em&gt;DpcForIsr&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)"> <em>DpcForIsr</em> </a>ルーチンが呼び出すことによって登録されている<em>IoInitializeDpcRequest</em>への関数ポインターを渡すと、 <em>DpcForIsr</em>2 番目のパラメーターとしてルーチンです。 キューに入れる、DPC、呼び出す<em>IoQueueDpc</em>同じ DPC オブジェクトを使用して ISR ルーチンから。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KDEFERRED_ROUTINE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine" data-raw-source="[&lt;em&gt;CustomDpc&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)"><em>CustomDpc</em></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine" data-raw-source="[&lt;em&gt;CustomDpc&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)"> <em>CustomDpc</em> </a>ルーチンを呼び出すことによって設定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializedpc" data-raw-source="[&lt;strong&gt;KeInitializeDpc&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializedpc)"> <strong>KeInitializeDpc</strong> </a>への関数ポインターを渡すと、 <em>CustomDpc</em> 2 番目のパラメーター。 キューに、 <em>CustomDpc</em> 、ドライバーでは、呼び出す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertqueuedpc" data-raw-source="[&lt;strong&gt;KeInsertQueueDpc&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertqueuedpc)"> <strong>KeInsertQueueDpc</strong> </a>同じ DPC オブジェクトを使用して ISR ルーチンから。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSERVICE_ROUTINE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kservice_routine" data-raw-source="[&lt;em&gt;InterruptService&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kservice_routine)"><em>InterruptService</em></a></p>
<p>必要に応じてデバイス割り込みとスケジュール後の割り込み処理、受信したデータのサービス InterruptService ルーチン (ISR)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>REQUEST_POWER_COMPLETE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-request_power_complete" data-raw-source="[&lt;em&gt;PowerCompletion&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-request_power_complete)"> <em>PowerCompletion</em> </a>コールバック ルーチン power IRP の処理が完了するとします。 ドライバーは、その他のすべてのドライバーは IRP がドライバーの登録を完了した後、その他のタスクを実行する必要がある場合、 <em>PowerCompletion</em>コールバック ルーチンの呼び出し中に、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp" data-raw-source="[&lt;strong&gt;PoRequestPowerIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp)"> <strong>PoRequestPowerIrp</strong></a> IRP を割り当てルーチン。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WORKER_THREAD_ROUTINE</p></td>
<td align="left"><p><em>ルーチン</em></p>
<p><em>ルーチン</em>が 2 番目のパラメーターで指定されているコールバック ルーチン、 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl" data-raw-source="[&lt;strong&gt;ExInitializeWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)"> <strong>ExInitializeWorkItem</strong> </a>関数。</p>
<p><em>ルーチン</em>しか宣言できないこうすると、ドライバーを呼び出す場合<strong>ExQueueWorkItem</strong>システム キューに作業項目を追加します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idannotatingdriverdispatchroutinesspanspan-idannotatingdriverdispatchroutinesspandeclaring-driver-dispatch-routines"></a><span id="annotating_driver_dispatch_routines"></span><span id="ANNOTATING_DRIVER_DISPATCH_ROUTINES"></span>ドライバーのディスパッチ ルーチンを宣言します。

ディスパッチ ルーチンの関数の役割の型宣言では、追加情報が必要です。 注釈を使用して、 **\_ディスパッチ\_型\_(** <em>型</em> **)** IRP の主要なサービスを提供するディスパッチ ルーチンの宣言関数のコードです。 *型*主要な I/O 関数のコードは、(IRP など\_MJ\_作成、IRP\_MJ\_閉じる、IRP\_MJ\_システム\_コントロール)。

ドライバーのディスパッチ ルーチンを宣言する方法の例は、キャンセルのサンプル ドライバー (Cancel.sys) のソース コードを参照してください。 関数の役割の型宣言があるドライバー (Cancel.h) 用のヘッダー ファイルで*CsampCleanup*、IRP を処理するドライバー ディスパッチ ルーチン\_MJ\_クリーンアップ I/O 関数のコード。 **\_ディスパッチ\_型\_(** <em>型</em> **)** 注釈の前に、ドライバー\_ディスパッチ ロールの種類宣言。

*CsampCleanup*ルーチンは次のように宣言されます。

```
_Dispatch_type_(IRP_MJ_CLEANUP)
DRIVER_DISPATCH CsampCleanup;
```

キャンセルのサンプル ドライバーにもドライバーのディスパッチ ルーチンでは、 *CsampCreateClose*、両方の IRP を処理する\_MJ\_IRP の作成と\_MJ\_閉じる I/O 関数のコード。 *CsampCreateClose*ルーチンが Cancel.h で宣言されています。 このルーチンは、2 つの I/O 関数のコードを処理するため、2 つが必要 **\_ディスパッチ\_型\_** ドライバーだけでなく注釈\_ロールの種類の宣言をディスパッチします。

```
_Dispatch_type_(IRP_MJ_CREATE)
_Dispatch_type_(IRP_MJ_CLOSE)
DRIVER_DISPATCH CsampCreateClose;
```

たとえば、フィルター ドライバーがドライバーと呼ばれるルーチンをディスパッチ*FilterDispatchIo* IRP を処理する\_MJ\_作成、IRP\_MJ\_閉じる、IRP\_MJ\_クリーンアップ、および IRP\_MJ\_デバイス\_コントロール I/O 関数のコード。

*FilterDispatchIo*ルーチンが Filter.h で次のように宣言されています。

```
_Dispatch_type_(IRP_MJ_CREATE)
_Dispatch_type_(IRP_MJ_CLOSE)
_Dispatch_type_(IRP_MJ_CLEANUP)
_Dispatch_type_(IRP_MJ_DEVICE_CONTROL)
DRIVER_DISPATCH FilterDispatchIo;
```

### <a name="span-idquickstepshowtoannotateawdmdriverspanspan-idquickstepshowtoannotateawdmdriverspanquick-steps-how-to-annotate-a-wdm-driver"></a><span id="quick_steps__how_to_annotate_a_wdm_driver"></span><span id="QUICK_STEPS__HOW_TO_ANNOTATE_A_WDM_DRIVER"></span>簡単な手順:WDM ドライバーの注釈を設定する方法

関数のロールの種類を使用して関数を宣言するための手順は次のとおりです。

1.  ソース コードを見つけたり、 *DriverEntry*ルーチン。

2.  ロールの種類の関数を使用して、次のポインターに割り当てられているルーチンを宣言することを確認します。

    ```
    DriverObject->DriverStartIo
    DriverObject->Unload
    DriverObject->DriverExtension->AddDevice 
    ```

    たとえば、次のコード例を示しています関数は、これらのポインターに対応するルーチンの役割の型宣言 (*myDriverStartIO*、 *myUnload*、および*myAddDevice*).

    ```
    DRIVER_STARTIO myDriverStartIo;
    DRIVER_UNLOAD myUnload;
    DRIVER_ADD_DEVICE myAddDevice 
    ```

3.  ドライバーを使用して、次のポインターに割り当てられているルーチンを宣言することを確認します。\_ディスパッチ ロールの種類あること、および、 **\_ディスパッチ\_型\_** 注釈。

    ```
    DriverObject->MajorFunction[IRP_MJ_xxx]
    ```

    例:

    ```
    _Dispatch_type_(IRP_MJ_CLEANUP)
    DRIVER_DISPATCH CsampCleanup;
    ```

### <a name="span-idfunctionparametersandfunctionroletypesspanspan-idfunctionparametersandfunctionroletypesspanfunction-parameters-and-function-role-types"></a><span id="function_parameters_and_function_role_types"></span><span id="FUNCTION_PARAMETERS_AND_FUNCTION_ROLE_TYPES"></span>関数パラメーターと関数のロールの種類

C プログラミング言語で必要に応じて関数定義で使用するパラメーターの型は、関数プロトタイプのパラメーターの型と一致する必要があります。 またはこの場合、関数のロールを入力します。 SDV は、分析関数のシグネチャに依存し、一致しないシグネチャを持つ関数を無視します。

たとえば、宣言する必要があります、 [ **IoCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) 、IO を使用してルーチン\_完了\_ルーチン関数ロールの種類。

```
IO_COMPLETION_ROUTINE myCompletionRoutine;
```

実装に*myCompletionRoutine*、IO によって使用されるパラメーターの型が一致する必要があります\_完了\_ルーチン、つまり、PDEVICE\_オブジェクト、PIRP、および PVOID (を参照してください[ **IoCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)構文の日常的な)。

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

## <a name="span-idrunningcodeanalysisfordriverstoverifythefunctiondeclarationsspanspan-idrunningcodeanalysisfordriverstoverifythefunctiondeclarationsspan-running-code-analysis-for-drivers-to-verify-the-function-declarations"></a><span id="running_code_analysis_for_drivers_to_verify_the_function_declarations"></span><span id="RUNNING_CODE_ANALYSIS_FOR_DRIVERS_TO_VERIFY_THE_FUNCTION_DECLARATIONS"></span> Code Analysis for Drivers は、関数宣言を確認するを実行しています。


ソース コードを準備するかどうかを判断するために、実行[Code Analysis for Drivers](code-analysis-for-drivers.md)します。 関数の役割の型宣言に対するドライバーのチェックのコード分析とされなかった可能性が関数宣言を特定するのに役立ちますまたは関数のロールの種類の関数定義のパラメーターが一致しない場合に警告を表示します。

 

 





