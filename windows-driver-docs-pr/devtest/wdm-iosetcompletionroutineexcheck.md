---
title: IoSetCompletionRoutineExCheck ルール (wdm)
description: IoSetCompletionRoutineExCheck ルールでは、IoSetCompletionRoutineEx ルーチンが、NTSTATUS 値を返すことを指定します。
ms.assetid: 047298DB-851A-4406-AD6D-5A276960ABE4
ms.date: 05/21/2018
keywords:
- IoSetCompletionRoutineExCheck ルール (wdm)
topic_type:
- apiref
api_name:
- IoSetCompletionRoutineExCheck
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f716ff2a6804a1a7f62bb531c18106d4ad0b2368
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558319"
---
# <a name="iosetcompletionroutineexcheck-rule-wdm"></a>IoSetCompletionRoutineExCheck ルール (wdm)


**IoSetCompletionRoutineExCheck**ルールでは、ことを指定します、 [ **IoSetCompletionRoutineEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549686)ルーチンが NTSTATUS 値を返します。 ドライバーを確認するには、この値を確認する必要があります、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチンは、呼び出す前に正常に登録されました[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)または[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)します。

場合、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチンが正常に登録されている[ **IoSetCompletionRoutineEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549686)に残っているメモリを割り当てますまで割り当てられている、 *IoCompletion*ルーチンを実行します。 ドライバーを確認する必要がありますが、 *IoCompletion*ルーチンを呼び出すことによって実行[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)または[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)それ以外の場合、カーネルのメモリがリークします。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IoSetCompletionRoutineExCheck</strong>ルール。</p>
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
[**IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)
[**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 





