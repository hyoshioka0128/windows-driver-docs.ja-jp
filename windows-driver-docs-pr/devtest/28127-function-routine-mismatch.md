---
title: C28127
description: 警告 C28127 ルーチンとして使用されている関数が想定される型と一致も一致しません。
ms.assetid: ae8f554b-c1e1-42a7-b1ad-c5554af25953
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28127
ms.openlocfilehash: 2018d426dbcc0a1dfcca37e62d9e1fa943b4f9b9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361405"
---
# <a name="c28127"></a>C28127


C28127 を警告します。ルーチンとして使用されている関数は、想定される型と一致しないと一致します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>差が、実際の関数は、値を返し、予想される関数の型が void である可能性があります。</p></td>
</tr>
</tbody>
</table>

 

ドライバーが渡すか、予期しない型 (つまり、関数シグネチャ) の関数 (ポインター) を割り当てます。 これは、場合によく発生 C で、有効な戻り値が関数の型は VOID にする (暗黙) を持つ関数**int**値が実際に指定されたを返します。 パラメーターは、互換性のあるが同一ではない場合にも発生します。 一般に、コールバック関数する必要があります、予期された型正確に一致、関数の typedef を使用してこれが最も簡単に実行します。

この型が一致しないメッセージは、コード分析ツールがコールバックを認識できることを確認するには、主に設計されています。

 

 





