---
title: IrqlKeWaitForMultipleObjects ルール (wdm)
description: IrqlKeWaitForMultipleObjects ルールでは、タイムアウト パラメーターに基づいて適切な IRQL で KeWaitForMultipleObjects ルーチンの呼び出し元を実行する必要がありますを指定します。
ms.assetid: FC3E3544-95FB-4283-B030-66D74D0F7848
ms.date: 05/21/2018
keywords:
- IrqlKeWaitForMultipleObjects ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlKeWaitForMultipleObjects
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0e55ed355ccb1fbd8abef65a71ad8f0ade1fe4ea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353882"
---
# <a name="irqlkewaitformultipleobjects-rule-wdm"></a>IrqlKeWaitForMultipleObjects ルール (wdm)


**IrqlKeWaitForMultipleObjects**ことを指定するルールの呼び出し元、 [ **KeWaitForMultipleObjects** ](https://msdn.microsoft.com/library/windows/hardware/ff553324) に基づいて適切なIRQLでルーチンを実行する必要があります*タイムアウト*パラメーター。

呼び出し元**IrqlKeWaitForMultipleObjects** IRQL でルーチンを実行できる&lt;= ディスパッチ\_レベル、を除き、次の状況で。

-   場合*タイムアウト* &lt; &gt; 0 の場合、呼び出し元の[ **KeWaitForMultipleObjects** ](https://msdn.microsoft.com/library/windows/hardware/ff553324) IRQL でルーチンを実行する必要があります&lt;APCを=\_レベルです。
-   場合*タイムアウト*! = NULL と\**タイムアウト*= 0 の場合、呼び出し元の[ **KeWaitForMultipleObjects** ](https://msdn.microsoft.com/library/windows/hardware/ff553324)ルーチンを実行する必要がありますIRQL = ディスパッチ\_レベル。

-   場合*タイムアウト* = **NULL**、または\**タイムアウト*! = 0 の場合、呼び出し元の[ **KeWaitForMultipleObjects**](https://msdn.microsoft.com/library/windows/hardware/ff553324)ルーチンは、IRQL で実行する必要があります&lt;APC を =\_レベル。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IrqlKeWaitForMultipleObjects</strong>ルール。</p>
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

[**KeWaitForMultipleObjects**](https://msdn.microsoft.com/library/windows/hardware/ff553324)
 

 





