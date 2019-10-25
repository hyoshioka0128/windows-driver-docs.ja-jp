---
title: 取得と解放のセマンティクス
description: 取得と解放のセマンティクス
ms.assetid: a0852881-c33f-427a-be8a-5b9edac81f9a
keywords:
- 同期 WDK カーネル、取得セマンティクス
- 同期 WDK カーネル、リリースセマンティクス
- 取得セマンティクス WDK カーネル
- リリースセマンティクス WDK カーネル
- セマンティクス WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaccf7b1968ea5bd4f639b8117c26f61bbf739e0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837285"
---
# <a name="acquire-and-release-semantics"></a>取得と解放のセマンティクス





他のプロセッサが、それ以降の操作の影響を受ける前に常にその効果を確認する場合、操作は*取得セマンティクス*を持ちます。 操作自体の影響が発生する前に、他のプロセッサが上記の操作の効果をすべて確認する場合は、操作に*解放のセマンティクス*があります。

次のコード例について考えてみます。

```cpp
 a++;
 b++;
 c++;
```

別のプロセッサの観点から、上記の操作は任意の順序で発生するように見えます。 たとえば、他のプロセッサでは、`a`のインクリメントの前に `b` のインクリメントが表示される場合があります。

インタロックされた *** Xxx*** ルーチンによって実行されるようなアトミック操作には、既定で取得と解放の両方のセマンティクスがあります。 ただし、Itanium ベースのプロセッサは、両方を持っている場合よりも、解放のセマンティクスだけを取得または解放する操作を実行します。 そのため、インタロックされた *** Xxx*** ルーチンの一部については、**インタロック*Xxx*の取得**と**インタロック*xxx*のリリース**バージョンがシステムによって提供されます。

たとえば、 [**InterlockedIncrementAcquire**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547916(v=vs.85))ルーチンは取得セマンティクスを使用して変数をインクリメントします。 前のコード例を書き直しする場合は、次のようにします。

```cpp
 InterlockedIncrementAcquire(&a);
 b++;
 c++;
```

その他のプロセッサでは、`b` と `c`が増加する前に、`a` のインクリメントが常に表示されます。

同様に、 [**InterlockedIncrementRelease**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547919(v=vs.85))ルーチンは、リリースセマンティクスを使用して変数をインクリメントします。 コード例を再度書き直しする場合は、次のようにします。

```cpp
 a++;
 b++;
 InterlockedIncrementRelease(&c);
```

その他のプロセッサでは、`c`のインクリメントの前に `a` と `b` の増分が常に表示されます。

プロセッサが、単に取得または解放のセマンティクスのみを持つ命令を提供しない場合、システムは、両方の種類のセマンティクスを提供する対応するルーチンを使用します。 たとえば、x86 プロセッサでは、 **InterlockedIncrementAcquire**と**InterlockedIncrementRelease**の両方が**InterlockedIncrement**に相当します。

次の表は、取得専用とリリース専用の両方のバリアントを含むルーチンを示しています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>インタロック<em>Xxx</em>ルーチン</th>
<th>取得-セマンティクスのみのバージョン</th>
<th>リリース-セマンティックのみのバージョン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedincrement" data-raw-source="[&lt;strong&gt;InterlockedIncrement&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedincrement)"><strong>InterlockedIncrement</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547916(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedIncrementAcquire&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547916(v=vs.85))"><strong>InterlockedIncrementAcquire</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547919(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedIncrementRelease&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547919(v=vs.85))"><strong>InterlockedIncrementRelease</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockeddecrement" data-raw-source="[&lt;strong&gt;InterlockedDecrement&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockeddecrement)"><strong>InterlockedDecrement</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547875(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedDecrementAcquire&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547875(v=vs.85))"><strong>InterlockedDecrementAcquire</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547883(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedDecrementRelease&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547883(v=vs.85))"><strong>InterlockedDecrementRelease</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedcompareexchange" data-raw-source="[&lt;strong&gt;InterlockedCompareExchange&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedcompareexchange)"><strong>InterlockedCompareExchange</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547857(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedCompareExchangeAcquire&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547857(v=vs.85))"><strong>InterlockedCompareExchangeAcquire</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547867(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedCompareExchangeRelease&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547867(v=vs.85))"><strong>InterlockedCompareExchangeRelease</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




