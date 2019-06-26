---
title: インタロックされたオペランドのドライバー注釈
description: インタロックされたオペランドのドライバー注釈
ms.assetid: 33C85016-765B-42BF-9F38-BB682951B20C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41b7655e9e8a025af3468abb105ab1a978692b8d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371516"
---
# <a name="driver-annotations-for-interlocked-operands"></a>インタロックされたオペランドのドライバー注釈


大規模なファミリの関数は、パラメーターの 1 つとして、インタロックされたプロセッサ命令を使用してアクセスする必要がある変数のアドレスを受け取ります。 キャッシュ リード スルーのアトミック手順では、これらし、非常に微妙なバグが発生する場合は、オペランドが正しくに使用されていません。

インタロックされたオペランドとして識別するのにには、関数のパラメーターは、次の注釈を使用します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">インタロックされたオペランドの注釈</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="_Interlocked_operand_"></span><span id="_interlocked_operand_"></span><span id="_INTERLOCKED_OPERAND_"></span><em>Interlocked_operand</em></p></td>
<td align="left"><p>注釈付きの関数パラメーターは、インタロックされた関数の 1 つのターゲットのオペランドです。 これらのオペランドは、特定の追加プロパティを持つ必要があります。</p></td>
</tr>
</tbody>
</table>



関数のパラメーターの注釈が付けられた、 \_Interlocked\_オペランド\_プロセス間で共有する必要があります。 この注釈で使用する変数である必要があります。

-   宣言する**揮発性です。**

-   ローカル変数はできません。 ローカル変数の使用は、通常の関数の目的とした、誤解を示します。 ローカル変数は何らかの方法で共有されている場合でもシステム ページング要件アドレス指定変数ように別のプロセスで問題が発生します。

-   いない以外からはアクセス、interlocked 関数。 Interlocked 関数の明示的な使用、しなくても、操作は古いデータにアクセスする可能性があります、1 つのプロセッサのキャッシュでのみ発生する可能性があります。 またはシステムの残りの部分に遅れる可能性があります。

システム指定の関数は、既にインタロックされたオペランドの注釈が付いています。

次の例では、注釈には、 [ **InterlockedExchange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-interlockedexchange)関数。 この注釈は、ターゲット パラメーターは、インタロックされた操作を使用して常にアクセスする必要がありますを指定します。

```
LONG  
InterlockedExchange (  
    _Inout_ _Interlocked_operand_ LONG volatile *Target,  
    _In_ LONG Value  
    );  
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[SAL 2.0 注釈ドライバー](sal-2-annotations-for-windows-drivers.md)










