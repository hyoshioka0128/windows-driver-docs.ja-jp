---
title: 取得と解放のセマンティクス
description: 取得と解放のセマンティクス
ms.assetid: a0852881-c33f-427a-be8a-5b9edac81f9a
keywords:
- WDK のカーネルの同期セマンティクスを取得します。
- 同期の WDK カーネル、解放のセマンティクス
- WDK のカーネルのセマンティクスを取得します。
- 解放のセマンティクス WDK カーネル
- セマンティクスの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: df00cf901bb64b0406ab6b658d08b8627b261238
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387017"
---
# <a name="acquire-and-release-semantics"></a>取得と解放のセマンティクス





操作が*取得セマンティクス*場合、他のプロセッサは、後続の操作の効果の前にその効果を常に表示されます。 操作が*解放のセマンティクス*場合は、操作自体の前にすべて上記の操作の効果を他のプロセッサが表示されます。

次のコード例を検討してください。

```cpp
 a++;
 b++;
 c++;
```

もう 1 つのプロセッサの観点から、上述の操作は、任意の順序で発生する表示できます。 たとえば、他のプロセッサが表示の増分`b`のインクリメントする前に`a`します。

などのアトミック操作を**Interlocked * Xxx*** ルーチンの実行が両方とも取得および解放のセマンティクスを既定では。 ただし、Itanium ベースのプロセッサは、取得のみがやのみ解放のセマンティクスを両方が指定されているよりも高速の操作を実行します。 そのため、システムが提供**Interlocked*Xxx*Acquire**と**Interlocked*Xxx*リリース**のいくつかのバージョン**Interlocked * Xxx*** ルーチン。

たとえば、 [ **InterlockedIncrementAcquire** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547916(v=vs.85))ルーチンは、変数をインクリメントするためのセマンティクスを取得します。 上記のコード例を次のように書き換える: 場合

```cpp
 InterlockedIncrementAcquire(&a);
 b++;
 c++;
```

他のプロセッサがの増分値を表示して常に`a`のインクリメントする前に`b`と`c`します。

同様に、 [ **InterlockedIncrementRelease** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547919(v=vs.85))ルーチンは、変数をインクリメントするためのセマンティクスをリリースします。 コード例は、次のように、もう一度:unchecked: 場合

```cpp
 a++;
 b++;
 InterlockedIncrementRelease(&c);
```

他のプロセッサがの増分値を表示して常に`a`と`b`のインクリメントする前に`c`します。

持つのみ命令を取得または解放のセマンティクスのみに、プロセッサが提供されない場合は、両方の種類のセマンティクスを提供する、対応するルーチンが使用されます。 たとえば、x86 の両方のプロセッサ**InterlockedIncrementAcquire**と**InterlockedIncrementRelease**に相当**InterlockedIncrement**します。

次の表には、取得専用であり、リリース専用のバリエーションがあるルーチンが一覧表示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>インタロックされた<em>Xxx</em>ルーチン</th>
<th>取得のセマンティクスにのみのバージョン</th>
<th>リリースのセマンティクスのみのバージョン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-interlockedincrement" data-raw-source="[&lt;strong&gt;InterlockedIncrement&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-interlockedincrement)"><strong>InterlockedIncrement</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547916(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedIncrementAcquire&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547916(v=vs.85))"><strong>InterlockedIncrementAcquire</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547919(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedIncrementRelease&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547919(v=vs.85))"><strong>InterlockedIncrementRelease</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-interlockeddecrement" data-raw-source="[&lt;strong&gt;InterlockedDecrement&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-interlockeddecrement)"><strong>InterlockedDecrement</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547875(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedDecrementAcquire&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547875(v=vs.85))"><strong>InterlockedDecrementAcquire</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547883(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedDecrementRelease&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547883(v=vs.85))"><strong>InterlockedDecrementRelease</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-interlockedcompareexchange" data-raw-source="[&lt;strong&gt;InterlockedCompareExchange&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-interlockedcompareexchange)"><strong>InterlockedCompareExchange</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547857(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedCompareExchangeAcquire&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547857(v=vs.85))"><strong>InterlockedCompareExchangeAcquire</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547867(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedCompareExchangeRelease&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547867(v=vs.85))"><strong>InterlockedCompareExchangeRelease</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




