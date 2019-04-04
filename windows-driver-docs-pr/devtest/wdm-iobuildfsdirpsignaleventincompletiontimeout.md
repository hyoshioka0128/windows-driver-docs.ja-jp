---
title: IoBuildFsdIrpSignalEventInCompletionTimeout ルール (wdm)
description: IoBuildFsdIrpSignalEventInCompletionTimeout 規則は、ドライバーが下まで無期限に待機する場合に、欠陥をレポート IRP のイベントがシグナル状態になる完了ルーチンで必要なドライバーが返されます。
ms.assetid: EE191EDB-62BE-46F3-92B2-CE9090AD02E2
ms.date: 05/21/2018
keywords:
- IoBuildFsdIrpSignalEventInCompletionTimeout ルール (wdm)
topic_type:
- apiref
api_name:
- IoBuildFsdIrpSignalEventInCompletionTimeout
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ab3a61b58f0a4de17ef3d3e53f1556a8d28e018e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578267"
---
# <a name="iobuildfsdirpsignaleventincompletiontimeout-rule-wdm"></a>IoBuildFsdIrpSignalEventInCompletionTimeout ルール (wdm)


**IoBuildFsdIrpSignalEventInCompletionTimeout**ルールは、ドライバーが下まで無期限に待機する場合に、欠陥を報告 IRP のイベントがシグナル状態になる完了ルーチンで必要なドライバーが返されます。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IoBuildFsdIrpSignalEventInCompletionTimeout</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>対象
----------

[**IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)
[**IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)
[**KeInitializeEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552137) 
 [ **Kewaitforsingleobject の 1**](https://msdn.microsoft.com/library/windows/hardware/ff553350)
 

 





