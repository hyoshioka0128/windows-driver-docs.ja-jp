---
title: IrqlExAllocatePool ルール (wdm)
description: IrqlExAllocatePool ルールでは、IRQL のディスパッチで実行されている場合にのみに、ドライバーで exallocatepoolwithtag と ExAllocatePoolWithTagPriority を呼び出すことを指定します\_レベル。
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
ms.openlocfilehash: 2a611bacfb4707c0422febdf401f277640ed5d99
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582362"
---
# <a name="irqlexallocatepool-rule-wdm"></a>IrqlExAllocatePool ルール (wdm)


**IrqlExAllocatePool**ルールでは、ドライバーを呼び出すことを指定します[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)と[ **ExAllocatePoolWithTagPriority** ](https://msdn.microsoft.com/library/windows/hardware/ff544523) IRQL でその実行はときにのみ&lt;= ディスパッチ\_レベル。

ディスパッチを実行して呼び出し元\_レベルは、非ページを指定する必要があります*Xxx*値*PoolType*します。 IRQL でを実行する呼び出し元&lt;APC を =\_レベルは、いずれかを指定できます[**プール\_型**](https://msdn.microsoft.com/library/windows/hardware/ff559707)値。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00020004) [**チェック 0 xa のバグします。IRQL\_いない\_少ない\_または\_と等しい**](https://msdn.microsoft.com/library/windows/hardware/ff560129) |

<a name="example"></a>例
-------

次の例では、 [ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)ルーチンが呼び出された後、 [ **KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)ルーチンで、設定ディスパッチする IRQL\_レベル。 **Exallocatepoolwithtag に**ルーチンを呼び出すと**プール**ルールに違反しています。

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

    KeInitializeSpinLock(&amp;SpinLock);

    //
    // KeAcquireSpinLock sets IRQL to DISPATCH_LEVEL and the previous IRQL is 
    // written to OldIrql after the lock is acquired.
    //

    KeAcquireSpinLock(&amp;SpinLock, &amp;OldIrql);
    ...

    Status = ProcessRequest(DeviceRequest);

    //
    // KeReleaseSpinLock sets IRQL to the OldIrql returned by KeAcquireSpinLock.
    //

    KeReleaseSpinLock(&amp;SpinLock, &amp;OldIrql);
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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IrqlExAllocatePool</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を選択し、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh454208" data-raw-source="[DDI compliance checking](https://msdn.microsoft.com/library/windows/hardware/hh454208)">DDI 準拠の検査</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>対象
----------

[**Exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)
[**ExAllocatePoolWithTagPriority** ](https://msdn.microsoft.com/library/windows/hardware/ff544523)も参照してください
--------

[**ハードウェアの優先度を管理する**](https://msdn.microsoft.com/library/windows/hardware/ff554368)
[**スピン ロックの使用中にエラーおよびデッドロックの防止**](https://msdn.microsoft.com/library/windows/hardware/ff559854)
 

 





