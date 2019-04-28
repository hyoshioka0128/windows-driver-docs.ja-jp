---
title: TargetRelationNeedsRef ルール (wdm)
description: TargetRelationNeedsRef ルールは、TargetDeviceRelation クエリを処理するときに、ドライバーの DispatchPnP ルーチンを呼び出す子デバイスの PDO を参照するには、次の関数のいずれかを指定しますObReferenceObjectObReferenceObjectByHandleObReferenceObjectByPointer します。
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
ms.openlocfilehash: d6b80797815341ae2edc9a1a78326856b2cd8fe2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380438"
---
# <a name="targetrelationneedsref-rule-wdm"></a>TargetRelationNeedsRef ルール (wdm)


**TargetRelationNeedsRef**ルール指定を処理するときに、 *TargetDeviceRelation*クエリ、ドライバーの[ **DispatchPnP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンは、子デバイスの PDO を参照するには、次の関数のいずれかを呼び出します。

-   [**ObReferenceObject**](https://msdn.microsoft.com/library/windows/hardware/ff558678)

-   [**ObReferenceObjectByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff558679)

-   [**ObReferenceObjectByPointer**](https://msdn.microsoft.com/library/windows/hardware/ff558686)

このルールは、設定に、ドライバーが IRP を完了時にのみ適用されます、 `Irp->IoStatus.Information` 、新しいへのポインター以外**NULL**値。 下位のドライバーをドライバーが IRP を通過するときは適用されません。

この規則は有効な値である条件を指定しない`Irp->IoStatus.Information`します。 この規則を適用のみ、ドライバーの値を変更して、新しい値がない**NULL**します。 有効な値は、デバイスへのポインター\_リレーションシップの要求された情報を含む関係の構造体。

このルールは、バス ドライバーのみに適用されます。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>TargetRelationNeedsRef</strong>ルール。</p>
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

<a name="applies-to"></a>適用対象
----------

[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**ObReferenceObjectByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff558679)
[**ObReferenceObjectByPointer**](https://msdn.microsoft.com/library/windows/hardware/ff558686) 
 [ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654)も参照してください
--------

[**DanglingDeviceObjectReference**](wdm-danglingdeviceobjectreference.md)
 

 





