---
title: KMDF ドライバーの規則
description: KMDF ドライバーの規則
ms.assetid: 63ac4df5-b2dc-43da-abaa-49c5de036d79
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 91900f908a3d6361c136f1b3a621753d2cee1668
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340153"
---
# <a name="rules-for-kmdf-drivers"></a>KMDF ドライバーの規則


ここでは、について説明します、 [DDI 準拠規則](static-driver-verifier-rules.md)カーネル モード ドライバー フレームワーク (KMDF) ドライバーの検証に含めることができます。

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
<td align="left"><p><a href="default-rule-set--kmdf-.md" data-raw-source="[Default rule set (KMDF)](default-rule-set--kmdf-.md)">既定のルール設定 (KMDF)</a></p></td>
<td align="left"><p>既定の規則セット (Default.sdv) では、推奨される一連のドライバーを分析するときに使用する規則を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ddi-usage-rule-set--kmdf-.md" data-raw-source="[DDI usage rule set (KMDF)](ddi-usage-rule-set--kmdf-.md)">DDI 使用量ルール セット (KMDF)</a></p></td>
<td align="left"><p>これらの規則を使用すると、ドライバー、正しく使用する KMDF Ddi 正しくを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="irpprocessing-rule-set--kmdf-.md" data-raw-source="[IrpProcessing rule set (KMDF)](irpprocessing-rule-set--kmdf-.md)">IrpProcessing ルール セット (KMDF)</a></p></td>
<td align="left"><p>これらの規則を使用すると、ドライバーが I/O 要求パケット (IRP) を正しく処理することを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="irql-rule-set--kmdf-.md" data-raw-source="[Irql rule set (KMDF)](irql-rule-set--kmdf-.md)">Irql ルール セット (KMDF)</a></p></td>
<td align="left"><p>これらの規則を使用すると、ドライバーが必要な IRQL で DDI 呼び出しを行うことを確認します。</p>
<p>IRQL の規則に従っていないドライバーは、デッドロック状態またはコンピューターがクラッシュする可能性のある操作中に重大な問題を発生することができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="locking-rule-set--kmdf-.md" data-raw-source="[Locking rule set (KMDF)](locking-rule-set--kmdf-.md)">ロックの規則 (KMDF) の設定</a></p></td>
<td align="left"><p>ドライバーが正しく共有リソースを管理することを確認するのにには、これらの規則を使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="miscellaneous-rule-set--kmdf-.md" data-raw-source="[Miscellaneous rule set (KMDF)](miscellaneous-rule-set--kmdf-.md)">その他のルール セット (KMDF)</a></p></td>
<td align="left"><p>これらの規則には、ドライバー正しく一般的な一連のデバイスの適切な処理の要件に従うことを確認するオブジェクトの場合、キー、および、ドライバーは Ddi いないは呼び出しが非 PnP ドライバーまたは po ではない非 FDO ドライバーは適切でない使用wer ポリシーの所有者です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="requestprocessing-rule-set--kmdf-.md" data-raw-source="[RequestProcessing rule set (KMDF)](requestprocessing-rule-set--kmdf-.md)">RequestProcessing ルール セット (KMDF)</a></p></td>
<td align="left"><p>これらの規則を使用すると、ドライバーが正しく完了するか、I/O 要求パケット (IRP) をキャンセルすることを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="usb-rule-set--kmdf-.md" data-raw-source="[Usb rule set (KMDF)](usb-rule-set--kmdf-.md)">Usb ルール セット (KMDF)</a></p></td>
<td align="left"><p>これらの規則を使用するには、ドライバーが USB デバイスの一部の特殊な KMDF メソッドを正しく処理することを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="warning-rule-set--kmdf-.md" data-raw-source="[Warning rule set (KMDF)](warning-rule-set--kmdf-.md)">警告ルール設定 (KMDF)</a></p></td>
<td align="left"><p>これらの規則を使用すると、さまざまなコンテキストでは、ドライバーが Irp を正しく処理を次のように Microsoft が推奨されるベスト プラクティスを確認します。</p></td>
</tr>
</tbody>
</table>

 

 

 





