---
title: C28123
description: 警告 C28123、関数は、高い IRQ レベルで呼び出されるは許可されていません。 先行する関数の呼び出しは、この制約と一貫性がありません。
ms.assetid: 6b40a485-f4f7-4c68-8575-960faa8cb87b
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28123
ms.openlocfilehash: 65a46c21162db7e0fd3fc49cc800c3a17638732c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361400"
---
# <a name="c28123"></a>C28123


C28123 を警告します。関数は、高い IRQ レベルで呼び出されるは許可されません。 先行する関数の呼び出しは、この制約と一貫性がありません。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>エラーが、実際にはいくつか前を呼び出して、範囲が限定される可能性があります。</p></td>
</tr>
</tbody>
</table>

 

呼び出し元関数の大きすぎる IRQL でドライバーを実行して、関数内で前の呼び出しの最小許容 IRQL がこの呼び出しで必要な最大の IRQL より大きい。

コード分析ツールでは、この警告を報告、ときに、関数のシーケンスの WDK のマニュアルを参照し、IRQL の各関数を呼び出すことができますを確認します。

コード分析ツールでは、現在の IRQL を推測し、エラーを検出するために、IRQL の話は推定場合にのみ、この警告を報告します。 この推定に基づきますが、*関数シグネチャ*(引数と結果型) または分析されて、関数の実行パスの前の呼び出しから。

 

 





