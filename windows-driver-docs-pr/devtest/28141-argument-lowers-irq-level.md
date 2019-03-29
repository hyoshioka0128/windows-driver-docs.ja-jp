---
title: C28141
description: 警告 C28141 引数によって IRQ レベルは、現在の IRQL 未満に設定して、その目的には、この関数を使用することはできません。
ms.assetid: 5cf30e4b-beef-42e0-9d1c-85418b601acb
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28141
ms.openlocfilehash: b66bc9b71a740a3bf096790db9c6ebf35a44e988
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464306"
---
# <a name="c28141"></a>C28141


C28141 を警告します。引数によって IRQ レベルを現在の IRQL では、以下に設定して、この関数は、目的のために使用できません。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>IRQL が最後に設定&lt; <em>IRQL</em> &gt;行&lt;<em>行番号</em>&gt;"</p></td>
</tr>
</tbody>
</table>

 

呼び出し元が実行して IRQL を関数呼び出しを不適切に使用されています。 通常、関数呼び出しは、一般的なルーチンの一部として、IRQL を削減または呼び出し元の IRQL を発生させるためのものでは。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次のコード例では、この警告を引き起こします。

```
KeRaiseIrql(DISPATCH_LEVEL, &OldIrql);
KeRaiseIrql(PASSIVE_LEVEL, &OldIrql);
```

次のコード例は、この警告を回避できます。

```
KeRaiseIrql(DISPATCH_LEVEL, &OldIrql);
KeLowerIrql(OldIrql);
```

 

 





