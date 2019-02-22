---
title: IrqlKeWaitForMutexObject ルール (wdm)
ms.assetid: f2e7b733-1746-4db5-b4a9-becd211e40cf
ms.date: 05/21/2018
description: ''
keywords:
- IrqlKeWaitForMutexObject ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlKeWaitForMutexObject
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1e56dbb72a4e6380fae617855c7eed206f570df7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536233"
---
# <a name="irqlkewaitformutexobject-rule-wdm"></a>IrqlKeWaitForMutexObject ルール (wdm)


**IrqlKeWaitForMutexObject**ルールを呼び出すドライバーを指定します、 [ **KeWaitForMutexObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553344) IRQL の値に基づくを適切に日常的な*タイムアウト*パラメーター。

-   場合*タイムアウト*ポイント値がゼロに、ドライバーは IRQL で実行するディスパッチ =\_レベル。

-   場合*タイムアウト*は**NULL**、または 0 以外の値へのポインター、ドライバーは IRQL で実行されて&lt;APC を =\_レベル。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IrqlKeWaitForMutexObject</strong>ルール。</p>
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

[**Kewaitforsingleobject の 1**](https://msdn.microsoft.com/library/windows/hardware/ff553350)
 

 





