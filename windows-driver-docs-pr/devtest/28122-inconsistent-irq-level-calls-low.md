---
title: C28122
description: 警告 C28122、関数は、低い IRQ レベルで呼び出されるは許可されていません。 先行する関数の呼び出しは、この制約と一貫性がありません。
ms.assetid: 4bc2f85e-055c-4821-9260-a223be787daf
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28122
ms.openlocfilehash: a389313c6c9a794ba516c288dd9ceb9e077855ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361432"
---
# <a name="c28122"></a>C28122


C28122 を警告します。関数は、低い IRQ レベルで呼び出されるは許可されません。 先行する関数の呼び出しは、この制約と一貫性がありません。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>最大の有効な IRQL が最後に設定&lt; <em>IRQL</em> &gt;行&lt;<em>行番号</em>&gt;します。 エラーが、実際にはいくつか前を呼び出して、範囲が限定される可能性があります。</p></td>
</tr>
</tbody>
</table>

 

ドライバーが小さすぎる場合、呼び出し元関数 IRQL で実行して、現在の関数の前の呼び出しの最大許容 IRQL がこの呼び出しに必要な最小の IRQL を下回る。

コード分析ツールでは、この警告を報告、ときに、関数のシーケンスの WDK のマニュアルを参照し、IRQL の各関数を呼び出すことができますを確認します。

コード分析ツールでは、現在の IRQL を推測し、エラーを検出するために、IRQL の話は推定場合にのみ、この警告を報告します。 この推定に基づきますが、*関数シグネチャ*(引数と結果型) または分析されて、関数の実行パスの前の呼び出しから。

同様の状況については、次を参照してください。[警告 28123](28123-inconsistent-irq-level-calls-high.md)します。

 

 





