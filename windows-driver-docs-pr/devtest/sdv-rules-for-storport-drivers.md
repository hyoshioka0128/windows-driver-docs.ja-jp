---
title: Storport ドライバーの規則
description: Storport ドライバーの規則
ms.assetid: C880A30B-8629-4648-B2E3-7AC8F1A9059D
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 557a9bbe0ad4411ea7ed8caec7065fb04f6e3c63
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340124"
---
# <a name="rules-for-storport-drivers"></a>Storport ドライバーの規則


ここでは、説明、 [DDI 準拠の規則](https://msdn.microsoft.com/library/windows/hardware/ff552839)Storport ドライバー、ドライバーの検証に含めることができます。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="default-rule-set--storport-.md" data-raw-source="[Default rule set (Storport)](default-rule-set--storport-.md)">既定のルール (Storport) を設定します。</a></p></td>
<td align="left"><p>既定の規則セット (Default.sdv) では、推奨される一連のドライバーを分析するときに使用する規則を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ddi-usage-rule-set--storport-.md" data-raw-source="[DDI usage rule set (Storport)](ddi-usage-rule-set--storport-.md)">DDI 使用量ルール セット (Storport)</a></p></td>
<td align="left"><p>これらの規則を使用すると、ドライバー、正しく使用する Storport Ddi 正しくを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="irql-rule-set--storport-.md" data-raw-source="[Irql rule set (Storport)](irql-rule-set--storport-.md)">Irql ルール セット (Storport)</a></p></td>
<td align="left"><p>これらの規則を使用すると、ドライバーが必要な IRQL で DDI 呼び出しを行うことを確認します。</p>
<p>IRQL の規則に従っていないドライバーは、デッドロック状態またはコンピューターがクラッシュする可能性のある操作中に重大な問題を発生することができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="locking-rule-set--storport-.md" data-raw-source="[Locking rule set (Storport)](locking-rule-set--storport-.md)">ロックの規則 (Storport) を設定します。</a></p></td>
<td align="left"><p>ドライバーが正しく共有リソースを管理することを確認するのにには、これらの規則を使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="srbprocessing-rule-set--storport-.md" data-raw-source="[SrbProcessing rule set (Storport)](srbprocessing-rule-set--storport-.md)">SrbProcessing ルール セット (Storport)</a></p></td>
<td align="left"><p>ドライバーが正しく SRB の要求を処理することを確認するのにには、これらの規則を使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="virtualstorport-rule-set--storport-.md" data-raw-source="[VirtualStorport rule set (Storport)](virtualstorport-rule-set--storport-.md)">VirtualStorport ルール セット (Storport)</a></p></td>
<td align="left"><p>これらの規則を使用するには、ドライバーが Storport ミニポート (VMiniport) を仮想ドライバーへの特定の関心のある Ddi を正しく呼び出すことを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="warning-rule-set--storport-.md" data-raw-source="[Warning rule set (Storport)](warning-rule-set--storport-.md)">警告ルール (Storport) を設定します。</a></p></td>
<td align="left"><p>これらの規則を使用すると、さまざまなコンテキストでは、ドライバーが Irp を正しく処理を次のように Microsoft が推奨されるベスト プラクティスを確認します。</p></td>
</tr>
</tbody>
</table>

 

 

 





