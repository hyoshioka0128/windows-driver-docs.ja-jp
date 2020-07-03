---
title: TargetRelationNeedsRef ルール (wdm)
description: TargetRelationNeedsRef ルールは、TargetDeviceRelation クエリを処理するときに、ドライバーの DispatchPnP ルーチンが、子デバイスの PDO ObReferenceObjectObReferenceObjectByHandleObReferenceObjectByPointer を参照するために次の関数のいずれかを呼び出すことを指定します。
ms.assetid: a341ff7a-1b36-4dfc-9e73-8268ed5b9a78
ms.date: 05/21/2018
keywords:
- TargetRelationNeedsRef ルール (wdm)
topic_type:
- apiref
api_name:
- TargetRelationNeedsRef
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 12e7305958f542e694f525aca7726fb6a1a7384a
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917057"
---
# <a name="targetrelationneedsref-rule-wdm"></a>TargetRelationNeedsRef ルール (wdm)


**TargetRelationNeedsRef**ルールは、 *TargetDeviceRelation*クエリを処理するときに、ドライバーの[**DispatchPnP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンが、次のいずれかの関数を呼び出して子デバイスの PDO を参照することを指定します。

-   [**Obreferenceobject へ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)

-   [**ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)

-   [**ObReferenceObjectByPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer)

この規則は、 `Irp->IoStatus.Information` 新しい**NULL**以外の値を指すようにポインターを設定することによって、ドライバーが IRP を完了した場合にのみ適用されます。 ドライバーが IRP を下位のドライバーに渡すときには適用されません。

このルールでは、の有効な値として修飾されているが指定されていません `Irp->IoStatus.Information` 。 この規則は、ドライバーが値を変更し、新しい値が**NULL**でない場合にのみ適用されます。 有効な値は、要求された \_ 関係情報を含むデバイスの関係構造体へのポインターです。

このルールは、バスドライバーにのみ適用されます。

**ドライバーモデル: WDM**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>TargetRelationNeedsRef</strong>規則を指定します。</p>
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

<a name="applies-to"></a>適用対象
----------

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 
[**Obreferenceobjectbyhandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle) 
[**Obreferenceobjectbypointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer) 
[**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)関連項目
--------

[**DanglingDeviceObjectReference**](wdm-danglingdeviceobjectreference.md)
 

 





