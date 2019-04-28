---
title: C28121
description: 警告 C28121、関数は、現在の IRQ レベルで呼び出されるは許可されていません。 現在のレベルが多すぎます。
ms.assetid: f0ab65ee-e160-4118-b001-7a8ba83d9671
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28121
ms.openlocfilehash: 8c7ad92e21834e7083174855d94f8308a580c44c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361448"
---
# <a name="c28121"></a>C28121


C28121 を警告します。関数は、現在の IRQ レベルで呼び出されるは許可されません。 現在のレベルが多すぎます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>IRQL が最後に設定&lt; <em>IRQL</em> &gt;行&lt;<em>行番号</em>&gt;します。レベルは、関数のシグネチャから推論されましたがある可能性があります。</p></td>
</tr>
</tbody>
</table>

 

ドライバーは、これを呼び出している関数に対して大きすぎる IRQL で実行しています。

コード分析ツールでは、この警告を報告、関数の WDK のマニュアルを参照を関数を呼び出すことができますの IRQL を確認します。

コード分析ツールでは、現在の IRQL を推測し、エラーを検出するために、IRQL の話は推定場合にのみ、この警告を報告します。 この推定に基づきますが、*関数シグネチャ*(引数と結果型) または現在のパスの前の呼び出しから分析されて、関数の。

コード分析ツールは、位置、ドライバーが実行中の IRQL を特定できない場合、間違った IRQL で、関数が呼び出される場合でも、この警告は報告されます。

 

 





