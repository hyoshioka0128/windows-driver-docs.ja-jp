---
title: MarkIrpPending2 ルール (wdm)
description: MarkIrpPending2 ルールを指定するディスパッチ ルーチンは、状態を返す場合\_保留中、IoMarkIrpPending を呼び出すまたは IRP を下位のドライバーに渡されることができます。 無料の仕様の MarkIrpPending を参照してください。
ms.assetid: 91e22348-f5f3-4ba0-b8dd-ec0aa4b1df5e
ms.date: 05/21/2018
keywords:
- MarkIrpPending2 ルール (wdm)
topic_type:
- apiref
api_name:
- MarkIrpPending2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e47ff85ce9d51b2735401561f96848dd0862b18f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331340"
---
# <a name="markirppending2-rule-wdm"></a>MarkIrpPending2 ルール (wdm)


**MarkIrpPending2**ルールを指定するディスパッチ ルーチンは、状態を返す場合\_が呼び出されて、保留中[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422) IRP を渡されたまたは、下位のドライバーです。 参照してください[ **MarkIrpPending** ](wdm-markirppending.md)の無償の仕様。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>MarkIrpPending2</strong>ルール。</p>
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
[**IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)
[**kewaitforsingleobject の 1**](https://msdn.microsoft.com/library/windows/hardware/ff553350) 
 [ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
[**RemoveHeadList** ](https://msdn.microsoft.com/library/windows/hardware/ff561032)も参照してください
--------

[**MarkIrpPending**](wdm-markirppending.md)
[**IRP のキャンセルを同期します。**](https://msdn.microsoft.com/library/windows/hardware/ff564531)
 

 





