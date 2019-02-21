---
title: IoSetCompletionRoutineExCheckDeviceObject ルール (wdm)
description: IoSetCompletionRoutineExCheckDeviceObject ルールでは、IoSetCompletionRoutineEx には、現在のデバイス オブジェクトが渡されないと、下のデバイス オブジェクトが場合、可能性があること、競合状態を現在のデバイス オブジェクトでしたアンロードされますでもを指定しますただし、完了ルーチンが実行されていません。
ms.assetid: 037E4CED-FBC7-480F-B81F-561396A217C6
ms.date: 05/21/2018
keywords:
- IoSetCompletionRoutineExCheckDeviceObject ルール (wdm)
topic_type:
- apiref
api_name:
- IoSetCompletionRoutineExCheckDeviceObject
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8b33278fc51888bbe50e190f5557bde5ac8a8843
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527725"
---
# <a name="iosetcompletionroutineexcheckdeviceobject-rule-wdm"></a>IoSetCompletionRoutineExCheckDeviceObject ルール (wdm)


**IoSetCompletionRoutineExCheckDeviceObject**ルールを指定するには、現在のデバイス オブジェクトが渡されない場合[ **IoSetCompletionRoutineEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549686)され、下これにより、競合状態、現在のデバイス オブジェクトできません読み込まれた完了ルーチンが実行されていない場合でも、デバイス オブジェクトはします。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IoSetCompletionRoutineExCheckDeviceObject</strong>ルール。</p>
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

[**IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)
 

 





