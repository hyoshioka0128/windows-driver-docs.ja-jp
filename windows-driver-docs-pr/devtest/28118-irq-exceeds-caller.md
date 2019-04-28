---
title: C28118
description: irq を超える呼び出し
ms.assetid: ''
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28118
ms.openlocfilehash: cbd3d7b47e1ec7c78d78b8f974d55d4e47551329
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361447"
---
# <a name="c28118"></a>C28118

警告:C28118:初期化をクリアまたは更新する必要がある特定のフィールドのまま、IRP スタック エントリ全体をコピーします。

現在の関数は %func (% レベル %) に許可される最大値を超える IRQ レベルで実行を許可します。 先行する関数の呼び出しまたは注釈が、その関数の使用と一貫性がありません。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>現在の関数が必要があります<em>IRQL_requires_max</em>、か、制限がいくつか前の呼び出しで設定されている可能性があります。</p></td>
</tr>
</tbody>
</table>

呼び出される関数は、いくつかの IRQL 以下で呼び出されるに制限されます。  呼び出し元の (現在の) 関数がいくつかの上位の IRQL で実行が許可され、その呼び出しを行う可能性が、呼び出された関数では操作できません。 IRQL で実行します。

PREfast は、現在の IRQ レベルについて可能なデータを推測しようとしてくださいし、エラーを検出するために IRQ レベルに関する十分な推定が場合にのみ、この警告が生成されることに注意してください。  分析対象の関数のシグネチャまたは前の呼び出し、現在のパスに沿ったから推論があります。
