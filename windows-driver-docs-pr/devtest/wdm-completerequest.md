---
title: CompleteRequest ルール (wdm)
description: CompleteRequest ルールは、完了ルーチンの実行後に、IoCompleteRequest ルーチンが呼び出されないことと、状態が返されないことを確認します。\_詳細\_処理\_必要な作業です。
ms.assetid: 2F6BA5D9-EC31-4C5D-8C98-EE33CE487498
ms.date: 05/21/2018
keywords:
- CompleteRequest ルール (wdm)
topic_type:
- apiref
api_name:
- CompleteRequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dd8298e3b493d7cca34dfb551edd56ba0b7293c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581310"
---
# <a name="completerequest-rule-wdm"></a>CompleteRequest ルール (wdm)


**CompleteRequest**ルールを確認、 [ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)完了ルーチンの実行し、状態を返さないルーチンが呼び出されない\_詳細\_処理\_必要な作業です。

このルールは、場合の欠陥を報告します。

-   ドライバー呼び出し[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)ときに、ドライバーには、要求が所有していません。

-   ドライバーは、呼び出しが失敗した[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)完了が必要な場合。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>CompleteRequest</strong>ルール。</p>
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

[**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)
[**IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)
[**IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686) 
 [ **RemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff561032)
 

 





