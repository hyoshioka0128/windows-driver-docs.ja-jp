---
title: C28120
description: 警告 C28120、関数は、現在の IRQ レベルで呼び出されるは許可されていません。 現在のレベルが低すぎます。
ms.assetid: a31a7c97-e27a-4a6a-a172-41d87cab236d
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28120
ms.openlocfilehash: e92d9ed3dfdb9788ab007d7cee8f2d281cd1bcb4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361434"
---
# <a name="c28120"></a>C28120


C28120 を警告します。関数は、現在の IRQ レベルで呼び出されるは許可されません。 現在のレベルが低すぎます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>IRQL が最後に設定&lt;<em>値</em>&gt;行&lt;<em>行番号</em>&gt;します。 レベルは、関数のシグネチャから推論されましたがある可能性があります。</p></td>
</tr>
</tbody>
</table>

 

ドライバーは、IRQL 小さすぎる場合、呼び出し元関数で実行しています。

コード分析ツールでは、この警告を報告、関数の WDK のマニュアルを参照を関数を呼び出すことができますの IRQL を確認します。

コード分析ツールでは、現在の IRQL を推測し、エラーを検出するために、IRQL の話は推定場合にのみ、この警告を報告します。 この推定に基づきますが、*関数シグネチャ*(引数と結果型) または現在のパスの前の呼び出しから分析されて、関数の。

コード分析ツールは、位置、ドライバーが実行中の IRQL を特定できない場合、間違った IRQL で、関数が呼び出される場合でも、この警告は報告されます。

同様の状況については、次を参照してください。[警告 28121](28121-irq-execution-too-high.md)します。

 

 





