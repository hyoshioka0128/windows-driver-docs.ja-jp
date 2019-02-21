---
title: MarkingQueuedIrps ルール (wdm)
description: MarkingQueuedIrps ルールでは、ドライバーがさらに、スピン ロックを保持している場合にのみ処理が必要な IRP の IoMarkIrpPending を呼び出すことを指定します。 このルールは、ドライバーがドライバー管理キューに IRP を追加するときにのみ適用されます。
ms.assetid: 3a70ba52-c62f-4574-9a2e-4ba7aed82529
ms.date: 05/21/2018
keywords:
- MarkingQueuedIrps ルール (wdm)
topic_type:
- apiref
api_name:
- MarkingQueuedIrps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c74206bc8c42f60f0e8b6f24dd2f1db426f29d4f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531551"
---
# <a name="markingqueuedirps-rule-wdm"></a>MarkingQueuedIrps ルール (wdm)


**MarkingQueuedIrps**ルールでは、ドライバーを呼び出すことを指定します[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)の IRP をさらに、スピン ロックを保持している場合にのみ処理を必要とします。 このルールは、ドライバーがドライバー管理キューに IRP を追加するときにのみ適用されます。

具体的には、この規則に違反ドライバー場合にのみ*すべて*次のイベントが発生します。

-   ドライバー呼び出し[ **KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)または[ **KeAcquireInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551899)スピン ロックを取得します。

-   ドライバーは IRP をドライバー管理キューに追加する、次のルーチンのいずれかを呼び出します。
    -   [**InsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff547820)
    -   [**InsertTailList**](https://msdn.microsoft.com/library/windows/hardware/ff547823)
    -   [**KeInsertDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff552180)
    -   [**KeInsertQueueDpc**](https://msdn.microsoft.com/library/windows/hardware/ff552185)
    -   [**KeInsertByKeyDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff552178)
-   ドライバー呼び出し[ **KeReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553145)または[ **KeReleaseInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553130) を呼び出す前に、スピンロックを解除するには**IoMarkIrpPending**します。

-   ドライバーのステータスを返します\_IRP を保留します。

ドライバーを呼び出す必要があります**IoMarkIrpPending**スピン ロックを保持している場合にのみキューに置かれた IRP の。 それ以外の場合、IRP でしたデキューされた別のドライバーのルーチンで完了し、呼び出しの前に、システムによって解放**IoMarkIrpPending**原因となり、クラッシュが発生します。

詳細については、次を参照してください。 [**同期 IRP キャンセル**](https://msdn.microsoft.com/library/windows/hardware/ff564531)します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>MarkingQueuedIrps</strong>ルール。</p>
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

[**InsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff547820)
[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422) 
 [ **KeAcquireInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551899)
[**KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)
 [ **KeInsertByKeyDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff552178)
[**KeInsertDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff552180) 
 [ **KeInsertQueueDpc**](https://msdn.microsoft.com/library/windows/hardware/ff552185)
[**KeReleaseInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553130) 
[ **KeReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553145)
[**PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654) 
 [ **RemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff561032)
 

 





