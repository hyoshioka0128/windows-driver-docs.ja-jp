---
title: WDM ドライバーの規則
description: WDM ドライバーの規則
ms.assetid: 4e8bc895-4f36-450c-8017-996df482b90d
ms.date: 05/21/2018
keywords:
- 静的ドライバー検証ツールの WDK、規則
- StaticDV WDK、規則
- SDV の WDK、規則
- WDK Static Driver Verifier の規則
ms.localizationpriority: medium
ms.openlocfilehash: 83531f9843ad1cafb3dc6d0466b71962e0c893d8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340134"
---
# <a name="rules-for-wdm-drivers"></a>WDM ドライバーの規則


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
<td align="left"><p><a href="default-rule-set--wdm-.md" data-raw-source="[Default rule set (WDM)](default-rule-set--wdm-.md)">既定のルール設定 (WDM)</a></p></td>
<td align="left"><p>既定の規則セット (Default.sdv) では、推奨される一連のドライバーを分析するときに使用する規則を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ddi-usage-rule-set--wdm-.md" data-raw-source="[DDI usage rule set (WDM)](ddi-usage-rule-set--wdm-.md)">DDI 使用量ルール セット (WDM)</a></p></td>
<td align="left"><p>これらの規則を使用すると、ドライバー、正しく使用する WDM Ddi 正しくを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="irppending-rule-set--wdm-.md" data-raw-source="[IrpPending rule set (WDM)](irppending-rule-set--wdm-.md)">IrpPending ルール セット (WDM)</a></p></td>
<td align="left"><p>ドライバーをことを確認するこれらの規則を使用して正しく、アプリケーション I/O 要求パケット (IRP)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="irpprocessing-rule-set--wdm-.md" data-raw-source="[IrpProcessing rule set (WDM)](irpprocessing-rule-set--wdm-.md)">IrpProcessing ルール セット (WDM)</a></p></td>
<td align="left"><p>これらの規則を使用すると、ドライバーが I/O 要求パケット (IRP) を正しく処理することを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="irptracking-rule-set--wdm-.md" data-raw-source="[IrpTracking rule set (WDM)](irptracking-rule-set--wdm-.md)">IrpTracking ルール セット (WDM)</a></p></td>
<td align="left"><p>Irp が保留状態中にデバイスを削除しないようにには、ドライバーがその I/O 要求パケット (IRP) を正しく追跡することを確認するのにには、これらの規則を使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="irql-rule-set--wdm-.md" data-raw-source="[Irql rule set (WDM)](irql-rule-set--wdm-.md)">Irql ルール セット (WDM)</a></p></td>
<td align="left"><p>これらの規則を使用すると、ドライバーが必要な IRQL で DDI 呼び出しを行うことを確認します。</p>
<p>IRQL の規則に従っていないドライバーは、デッドロック状態またはコンピューターがクラッシュする可能性のある操作中に重大な問題を発生することができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="localirpprocessing-rule-set--wdm-.md" data-raw-source="[LocalIrpProcessing rule set (WDM)](localirpprocessing-rule-set--wdm-.md)">LocalIrpProcessing ルール セット (WDM)</a></p></td>
<td align="left"><p>これらの規則を使用すると、ドライバーがドライバーによって作成される I/O 要求パケット (IRP) を正しく処理することを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="locking-rule-set--wdm-.md" data-raw-source="[Locking rule set (WDM)](locking-rule-set--wdm-.md)">ロックの規則の設定 (WDM)</a></p></td>
<td align="left"><p>ドライバーが正しく共有リソースを管理することを確認するのにには、これらの規則を使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="miscellaneous-rule-set--wdm-.md" data-raw-source="[Miscellaneous rule set (WDM)](miscellaneous-rule-set--wdm-.md)">その他のルール セット (WDM)</a></p></td>
<td align="left"><p>これらの規則を使用すると、ドライバー、正しく一般的な一連のレジストリ キー、文字列とデバイス オブジェクト ポインターの適切な処理の要件に従うことを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="warning-rule-set--wdm-.md" data-raw-source="[Warning rule set (WDM)](warning-rule-set--wdm-.md)">警告ルール設定 (WDM)</a></p></td>
<td align="left"><p>これらの規則を使用すると、さまざまなコンテキストでは、ドライバーが Irp を正しく処理を次のように Microsoft が推奨されるベスト プラクティスを確認します。</p></td>
</tr>
</tbody>
</table>

 

 

 





