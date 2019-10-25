---
title: インタロックされたオペランドのドライバー注釈
description: インタロックされたオペランドのドライバー注釈
ms.assetid: 33C85016-765B-42BF-9F38-BB682951B20C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5312d9f1aa7f94af3398ede639fbbbb867696abf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840277"
---
# <a name="driver-annotations-for-interlocked-operands"></a>インタロックされたオペランドのドライバー注釈


大規模な関数のファミリは、インタロックされたプロセッサ命令を使用してアクセスする必要がある変数のアドレスをパラメーターの1つとして受け取ります。 これらはキャッシュ読み取り-アトミック命令です。オペランドが正しく使用されていないと、非常に微妙なバグの結果になります。

関数パラメーターに次の注釈を使用して、それをインタロックされたオペランドとして識別します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">インタロックオペランド注釈</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="_Interlocked_operand_"></span><span id="_interlocked_operand_"></span><span id="_INTERLOCKED_OPERAND_"></span><em>Interlocked_operand</em></p></td>
<td align="left"><p>注釈付き関数のパラメーターは、いずれかのインタロックされた関数のターゲットオペランドです。 これらのオペランドには、特定の追加プロパティが必要です。</p></td>
</tr>
</tbody>
</table>



\_インタロックされた\_オペランド\_ で注釈が付けられた関数パラメーターは、プロセス間で共有される必要があります。 この注釈で使用される変数は次のようにする必要があります。

-   Volatile として宣言さ**れています。**

-   ローカル変数ではありません。 ローカル変数の使用は、通常、関数の意図が誤解されていることを示します。 ローカル変数が何らかの方法で共有されている場合でも、システムのページング要件によって、別のプロセスでの変数のアドレス指定が問題になります。

-   インタロックされた関数以外ではアクセスできません。 インタロックされた関数を明示的に使用しないと、操作は古いデータにアクセスしたり、1つのプロセッサのキャッシュでのみ発生する可能性があります。また、システムの残りの部分に到達するまでに遅延が生じる可能性があります。

システム指定の関数には、既にインタロックされたオペランドに注釈が付けられています。

次の例は、 [**InterlockedExchange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedexchange)関数の注釈を示しています。 この注釈は、ターゲットパラメーターに常に、インタロックされた操作を使用してアクセスする必要があることを指定します。

```
LONG  
InterlockedExchange (  
    _Inout_ _Interlocked_operand_ LONG volatile *Target,  
    _In_ LONG Value  
    );  
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ドライバーの SAL 2.0 注釈](sal-2-annotations-for-windows-drivers.md)










