---
title: フラグ\_Irql ルール (ndis)
description: フラグ\_Irql ルールでは、KeGetCurrentIrql をディスパッチ レベルのフラグ パラメーターが現在の IRQL を示すコールバック関数内で呼び出されませんする必要がありますを指定します。
ms.assetid: 19c5c497-9648-4be9-87d1-82f4fa295351
ms.date: 05/21/2018
keywords:
- Flags_Irql ルール (ndis)
topic_type:
- apiref
api_name:
- Flags_Irql
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cdec7218321d266784d63edb5b6dfcad933bb711
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323815"
---
# <a name="flagsirql-rule-ndis"></a>フラグ\_Irql ルール (ndis)


**フラグ\_Irql**ルールを指定する**KeGetCurrentIrql**ディスパッチ レベルのフラグ パラメーターが現在の IRQL を示すコールバック関数の中でないと呼ばれる必要があります。

ディスパッチのレベルのフラグの正しい使用では、IRQL を設定しようと不要なを回避できます。 このフラグを使用する方法の詳細については、次を参照してください。[ディスパッチ IRQL 追跡](https://msdn.microsoft.com/library/windows/hardware/ff546448)します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>Flags_Irql</strong>ルール。</p>
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

 

 





