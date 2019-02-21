---
title: C28134
description: 警告 C28134 プール タグの種類 は整数、いない文字列または文字列のポインター。
ms.assetid: f61aec4c-4072-421f-aa6d-d9399d0c439c
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28134
ms.openlocfilehash: 525052c57703d81d4b13ac601165e2a4be860060
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557970"
---
# <a name="c28134"></a>C28134


C28134 を警告します。プール タグの種類が整数、いない文字列または文字列ポインターにする必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>プール タグ名は文字リテラルは単一引用符を使用する必要があります (&#39;gaT_&#39;)、二重引用符で文字列ではありません。 逆バイト順で通常は。</p></td>
</tr>
</tbody>
</table>

 

ドライバーなど、プール タグを代入する関数の呼び出しは[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)、プール タグの値を指定する単一引用符でリテラル以外の値を使用してですが。 プール タグでは、引用符で囲まれた文字列を使用しません。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次のコード例では、この警告を引き起こします。

```
p = ExAllocatePoolWithTag(NonPagedPool, 30, "_Tag");
```

次のコード例は、この警告を回避できます。

```
p = ExAllocatePoolWithTag(NonPagedPool, 30, &#39;gaT_&#39;);
```

 

 





