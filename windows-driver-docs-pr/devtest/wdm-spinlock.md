---
title: SpinLock ルール (wdm)
description: スピンロックのルールでは、KeAcquireSpinLock を呼び出した後、ドライバーを呼び出す KeReleaseSpinLock KeAcquireSpinLock または KeAcquireSpinLockRaiseToDpc の後続の呼び出しの前に指定します。
ms.assetid: 3add467d-72b9-439f-b9a3-68f3d1e5b772
ms.date: 05/21/2018
keywords:
- SpinLock ルール (wdm)
topic_type:
- apiref
api_name:
- SpinLock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e04d5eef329968205ca9ba732cd7b1406824537d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559627"
---
# <a name="spinlock-rule-wdm"></a>SpinLock ルール (wdm)


**スピンロック**ルールを指定するには、呼び出した後[ **KeAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551917)、ドライバー呼び出し[ **KeReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553145)後続の呼び出しの前に**KeAcquireSpinLock**または[ **KeAcquireSpinLockRaiseToDpc**](https://msdn.microsoft.com/library/windows/hardware/ff551928)します。

取得、さまざまなリソースに対するロックを解除する場合、入れ子になった呼び出しが許可されます。 取得するか、同じリソースのロックを解放する入れ子になった呼び出しでは、この規則に違反します。

このルールは、ドライバーが使用されていることを指定しますも[ **KeReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553145)ディスパッチ ルーチンの前にすべてのスピン ロックを解放またはルーチンの終了をキャンセルします。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00040009) |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、<strong>スピンロック</strong>ルール。</p>
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

[**KeAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551917)
[**KeAcquireSpinLockRaiseToDpc**](https://msdn.microsoft.com/library/windows/hardware/ff551928)
[**KeReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553145) 
 [ **KeTryToAcquireSpinLockAtDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553317)
 

 





