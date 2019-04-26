---
title: NDIS ドライバーの規則
description: NDIS ドライバーの規則
ms.assetid: fd31b797-1175-4f65-8fa0-a50acd01f446
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 18051a880e7f048efc37ece0e81e62f36cb50362
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340126"
---
# <a name="rules-for-ndis-drivers"></a>NDIS ドライバーの規則


ここでは、について説明します、 [Static Driver Verifier ルール](https://msdn.microsoft.com/library/windows/hardware/ff552839)NDIS ドライバー、ドライバーの検証に含めることができます。

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
<td align="left"><p><a href="default-rule-set--ndis-.md" data-raw-source="[Default rule set (NDIS)](default-rule-set--ndis-.md)">既定のルール設定 (NDIS)</a></p></td>
<td align="left"><p>既定の規則セット (Default.sdv) では、推奨される一連のドライバーを分析するときに使用する規則を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ddi-usage-rule-set--ndis-.md" data-raw-source="[DDI usage rule set (NDIS)](ddi-usage-rule-set--ndis-.md)">DDI 使用量ルール セット (NDIS)</a></p></td>
<td align="left"><p>これらの規則を使用すると、ドライバー、正しく使用する NDIS Ddi 正しくを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="irql-rule-set--ndis-.md" data-raw-source="[IRQL rule set (NDIS)](irql-rule-set--ndis-.md)">IRQL ルール セット (NDIS)</a></p></td>
<td align="left"><p>これらの規則を使用すると、ドライバーが必要な IRQL で DDI 呼び出しを行うことを確認します。</p>
<p>IRQL の規則に従っていないドライバーは、デッドロック状態またはコンピューターがクラッシュする可能性のある操作中に重大な問題を発生することができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="locking-rule-set--ndis-.md" data-raw-source="[Locking rule set (NDIS)](locking-rule-set--ndis-.md)">ロックの規則の設定 (NDIS)</a></p></td>
<td align="left"><p>ドライバーが正しく共有リソースを管理することを確認するのにには、これらの規則を使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="memory-usage-rule-set--ndis-.md" data-raw-source="[Memory usage rule set (NDIS)](memory-usage-rule-set--ndis-.md)">メモリ使用量ルール セット (NDIS)</a></p></td>
<td align="left"><p>これらの規則を使用すると、ドライバーが正しく割り当てし、メモリを解放するのに NDIS 関数を呼び出すことを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="miscellaneous-rule-set--ndis-.md" data-raw-source="[Miscellaneous rule set (NDIS)](miscellaneous-rule-set--ndis-.md)">その他のルール セット (NDIS)</a></p></td>
<td align="left"><p>これらの規則を使用すると、タイマー、一時停止操作、キー、文字列、およびバインディングの適切な処理の要件の一般的なセットが正しくに、ドライバーに従うことを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="oidprocessing-rule-set--ndis-.md" data-raw-source="[OidProcessing rule set (NDIS)](oidprocessing-rule-set--ndis-.md)">OidProcessing ルール セット (NDIS)</a></p></td>
<td align="left"><p>ドライバーが正しく OID 要求を処理することを確認するのにには、これらの規則を使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="warning-rule-set--ndis-.md" data-raw-source="[Warning rule set (NDIS)](warning-rule-set--ndis-.md)">警告ルール設定 (NDIS)</a></p></td>
<td align="left"><p>これらの規則を使用すると、さまざまなコンテキストでは、ドライバーが Irp を正しく処理を次のように Microsoft が推奨されるベスト プラクティスを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-wifi-verification-rule-set.md" data-raw-source="[NDIS/WIFI verification rule set](ndis-wifi-verification-rule-set.md)">NDIS/WIFI 検証規則セット</a></p></td>
<td align="left"><blockquote>
[!Note]<br />
Windows 8.1 以降、これらのルールでは、NDIS/WIFI ドライバーをテストできます。
</blockquote>
 </td>
</tr>
</tbody>
</table>

 

 

 





