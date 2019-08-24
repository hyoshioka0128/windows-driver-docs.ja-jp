---
title: C28118
description: irq-呼び出し元を超えています
ms.assetid: ''
keywords:
- ドライバーの WDK PREfast の一覧に警告が表示される
- ドライバーの WDK PREfast の一覧にエラーが表示される
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28118
ms.openlocfilehash: 8e92343225daba43c7d38bbe29d77e56cb37f61b
ms.sourcegitcommit: 4a3e5c2c6f9d1b6ea03e81e4da641a48122b2307
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2019
ms.locfileid: "70014870"
---
# <a name="c28118"></a>C28118

要するC28118:現在の関数は、% func% (% level%) に許可されている最大値を超える IRQ レベルで実行できます。 以前の関数呼び出しまたは注釈には、その関数の使用との一貫性がありません。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>現在の関数には<em>IRQL_requires_max</em>が必要な場合があります。または、以前の呼び出しによって制限が設定されている可能性があります。</p></td>
</tr>
</tbody>
</table>

呼び出される関数は、なんらかの IRQL で呼び出されるように制限されています。  呼び出し側 (現在の) 関数は、高い IRQL で実行できるようになりました。その呼び出しを行うと、呼び出された関数がで動作できない IRQL で実行される可能性があります。

PREfast は、現在の IRQ レベルに対して何ができるかを推測しようとします。この警告は、エラーを検出するのに十分な IRQ レベルを推定した場合にのみ生成されます。  推論は、分析対象の関数のシグネチャまたは現在のパスに対する以前の呼び出しから取得される場合があります。
