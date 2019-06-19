---
title: IrqlExApcLte3 ルール (wdm)
description: IrqlExApcLte3 ルールでは、IRQL APC_LEVEL でのみ、ドライバーが、次のエグゼクティブ サポート ルーチンを呼び出すことを指定します。
ms.assetid: 80668699-dfca-4fb9-8ffe-d20be00542dc
ms.date: 05/21/2018
keywords:
- IrqlExApcLte3 ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlExApcLte3
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 83b7724619da6e0896a3592cc7b64e6d7758f8e6
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161510"
---
# <a name="irqlexapclte3-rule-wdm"></a>IrqlExApcLte3 ルール (wdm)


**IrqlExApcLte3**ルールでは、ドライバーが IRQL でのみ、次のエグゼクティブ サポート ルーチンを呼び出すことを指定します&lt;APC を =\_レベル。

-   [**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)

-   [**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)

-   [**ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)

-   [**ExAcquireSharedWaitForExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544370)

-   [**ExConvertExclusiveToSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544558)

-   [**ExDeleteResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff544578)

IRQL に関連するエラーが発生したドライバーは、重大な問題が発生して、コンピューターのクラッシュが発生する可能性があります。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                                                                                                                     |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x20007) [**チェック 0 xa のバグします。IRQL\_いない\_少ない\_または\_と等しい**](https://msdn.microsoft.com/library/windows/hardware/ff560129) |

<a name="example"></a>例
-------

次のコードには、このルールに違反しています。

```ManagedCPlusPlus
NTSTATUS
DispatchRequest (
    _In_ PDEVICE_REQUEST DeviceRequest
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
    _In_ PDEVICE_REQUEST DeviceRequest
    )
{
    ERESOURCE Resource;
    NTSTATUS Status;
    ...

    Resource = DeviceRequest->GetTableLock();

    //
    // RULE VIOLATION! - ExAcquireSharedStarveExclusive can be called only at 
    //                   IRQL <= APC_LEVEL. 
    //

    if(!ExAcquireSharedStarveExclusive(&Resource, FALSE)) {
        return STATUS_UNSUCCESSFUL;
    }

    ...

    ExReleaseResourceLite(&Resource);
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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IrqlExApcLte3</strong>ルール。</p>
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

 

<a name="applies-to"></a>適用対象
----------

[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)
[**ExAcquireResourceSharedLite** ](https://msdn.microsoft.com/library/windows/hardware/ff544363) 
 [ **ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)
[**ExAcquireSharedWaitForExclusive** ](https://msdn.microsoft.com/library/windows/hardware/ff544370) 
 [ **ExConvertExclusiveToSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544558)
[**ExDeleteResourceLite** ](https://msdn.microsoft.com/library/windows/hardware/ff544578)も参照してください
--------

[ハードウェアの優先度を管理する](https://msdn.microsoft.com/library/windows/hardware/ff554368)
[スピン ロックの使用中にエラーおよびデッドロックの防止](https://msdn.microsoft.com/library/windows/hardware/ff559854)
 

 





