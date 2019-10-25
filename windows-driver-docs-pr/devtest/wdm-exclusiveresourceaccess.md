---
title: ExclusiveResourceAccess ルール (wdm)
description: ExclusiveResourceAccess 規則は、ドライバーが ExReleaseResourceLite または ExReleaseResourceForThreadLite を呼び出す前に ExAcquireResourceExclusiveLite を呼び出し、ドライバーが ExReleaseResourceLite またはを呼び出していることを指定することを指定します。後続の ExAcquireResourceExclusiveLite 呼び出しの前に ExReleaseResourceForThreadLite します。
ms.assetid: 3de539c0-5af2-4ced-8111-44918f4effc4
ms.date: 05/21/2018
keywords:
- ExclusiveResourceAccess ルール (wdm)
topic_type:
- apiref
api_name:
- ExclusiveResourceAccess
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 577ce3cb8fe43439e24a79689d1e642eaefee458
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839967"
---
# <a name="exclusiveresourceaccess-rule-wdm"></a>ExclusiveResourceAccess ルール (wdm)


**ExclusiveResourceAccess**規則は、ドライバーが[**ExReleaseResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)または[**ExReleaseResourceForThreadLite**](https://msdn.microsoft.com/library/windows/hardware/ff545585)を呼び出す前に[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)を呼び出し、ドライバーがを呼び**出すように指定します。ExReleaseResourceLite**または**ExReleaseResourceForThreadLite**は、それ以降の**ExAcquireResourceExclusiveLite**の呼び出しの前に発生します。

入れ子になった呼び出しは、異なるリソースを取得して解放する場合に許可されます。 同じリソースを取得または解放するための入れ子になった呼び出しは、この規則に違反します。

この規則は、ルーチンが終了したときに、ドライバーがリソースに排他的にアクセスできないことも示します。 静的ドライバー検証ツールは、 **Driverentry**、 **AddDevice**、 **StartIo**、 **startdevice**、 **DpcForIsr**、 **Cancel**、 **Dispatch**、 **removedevice**、および**Unload**ルーチンの終了を監視します。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">この規則で見つかったバグ チェック</td>
<td align="left"></td>
</tr>
</tbody>
</table>

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>ExclusiveResourceAccess</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (ロールの種類の宣言を使用します)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)
[**ExReleaseResourceForThreadLite**](https://msdn.microsoft.com/library/windows/hardware/ff545585)
[**ExReleaseResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)参照
--------

[**スピンロックを使用しているときのエラーとデッドロックの防止**](https://docs.microsoft.com/windows-hardware/drivers/kernel/preventing-errors-and-deadlocks-while-using-spin-locks)
 

 





