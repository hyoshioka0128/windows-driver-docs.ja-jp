---
title: CompletionRoutineRegistered ルール (wdm)
description: CompletionRoutineRegistered ルールでは、こと IoSetCompletionRoutineEx を使用して、IoCompletion ルーチンを登録すると、ディスパッチ ルーチンの場合、ディスパッチ ルーチン呼び出す必要がありますそれ以降保留または PoCallDriver を指定します。
ms.assetid: ee0d813c-3bcc-4688-902c-1a2d15ddfd09
ms.date: 05/21/2018
keywords:
- CompletionRoutineRegistered ルール (wdm)
topic_type:
- apiref
api_name:
- CompletionRoutineRegistered
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e980d7380cb33475be8ed9d522c5586c9d1bc421
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574170"
---
# <a name="completionroutineregistered-rule-wdm"></a>CompletionRoutineRegistered ルール (wdm)


**CompletionRoutineRegistered**規則で指定された場合、ディスパッチ ルーチンのレジスタを[ **IoCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチンを使用して[ **IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)、ディスパッチ ルーチンを呼び出す必要がありますそれ以降[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)または[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654).

**IoSetCompletionRoutineEx**ルーチンがまで割り当てられたままにするメモリを割り当て、 **IoCompletion**ルーチンを実行します。 ドライバーを確認する必要がありますが、 **IoCompletion**ルーチンを呼び出すことによって実行**保留**または**PoCallDriver**、それ以外のカーネルのメモリがリークします。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>CompletionRoutineRegistered</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)
[**IoSetCompletionRoutineEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549686) 
 [ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 





