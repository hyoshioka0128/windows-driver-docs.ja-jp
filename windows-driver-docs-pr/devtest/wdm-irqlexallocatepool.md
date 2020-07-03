---
title: IrqlExAllocatePool ルール (wdm)
description: IrqlExAllocatePool 規則は、IRQL ディスパッチレベルで実行されている場合にのみ、ドライバーが ExAllocatePoolWithTag と ExAllocatePoolWithTagPriority を呼び出すように指定し \_ ます。
ms.assetid: 0bb179c5-e76b-46bc-b497-8639328d2eb2
ms.date: 05/21/2018
keywords:
- IrqlExAllocatePool ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlExAllocatePool
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bb821492a7f30f32a5394d6e0fd09c25b60aac99
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916848"
---
# <a name="irqlexallocatepool-rule-wdm"></a>IrqlExAllocatePool ルール (wdm)


**IrqlExAllocatePool**規則は、IRQL = ディスパッチレベルで実行されている場合にのみ、ドライバーが[**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)と[**Exallocatepoolwithtagpriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority)を呼び出すように指定し &lt; \_ ます。

ディスパッチレベルで実行している呼び出し元は、 \_ *pooltype*に対して非ページ*Xxx*値を指定する必要があります。 IRQL = APC レベルで実行されている呼び出し元は &lt; \_ 、任意の[**プールの \_ 種類**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_pool_type)の値を指定できます。

**ドライバーモデル: WDM**

|                                   |                                                                                                                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証ツールで \_ 検出された \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0X00020004)、 [**バグチェックの 0xa: IRQL が \_ 少ない、 \_ \_ または \_ 等しい**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xa--irql-not-less-or-equal) |

<a name="example"></a>例
-------

次の例では、 [**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)ルーチンの後に、IRQL をディスパッチレベルに設定する[**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)ルーチンが呼び出され \_ ます。 **Exallocatepoolwithtag**ルーチンは、規則に違反する**PagedPool**を使用して呼び出されます。

```ManagedCPlusPlus
NTSTATUS
DispatchRequest (
    __in PDEVICE_REQUEST DeviceRequest
    )
{  
    KIRQL OldIrql;
    KSPIN_LOCK SpinLock;
    NTSTATUS Status;
    ...

    KeInitializeSpinLock(&SpinLock);

    //
    // KeAcquireSpinLock sets IRQL to DISPATCH_LEVEL and the previous IRQL is 
    // written to OldIrql after the lock is acquired.
    //

    KeAcquireSpinLock(&SpinLock, &OldIrql);
    ...

    Status = ProcessRequest(DeviceRequest);

    //
    // KeReleaseSpinLock sets IRQL to the OldIrql returned by KeAcquireSpinLock.
    //

    KeReleaseSpinLock(&SpinLock, &OldIrql);
    ...
}

NTSTATUS
ProcessRequest (
    __in PDEVICE_REQUEST DeviceRequest
    )
{
    NTSTATUS Status;
    ...

    //
    // RULE VIOLATION! - IrqlExAllocatePool executing at DISPATCH_LEVEL must specify 
    //                   a NonPagedXxx value for PoolType. 
    //

    DeviceRequest->Context = ExAllocatePool(PagedPool, sizeof(REQUEST_CONTEXT));
    if (DeviceRequest->Context == NULL) {
        Status = STATUS_INSUFFICIENT_RESOURCES;
    }
    ...

    return Status;
}
```

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンパイル時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>IrqlExAllocatePool</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (役割の種類の宣言を使います)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">ドライバーの検証ツール</a>を実行し、[ <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">DDI 準拠チェック</a>] オプションを選択します。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>適用対象
----------

[**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) 
[**Exallocatepoolwithtagpriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority)関連項目
--------

[**ハードウェアの優先順位**](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-hardware-priorities) 
 の管理[**スピンロックを使用しているときのエラーとデッドロックの防止**](https://docs.microsoft.com/windows-hardware/drivers/kernel/preventing-errors-and-deadlocks-while-using-spin-locks)
 

 





