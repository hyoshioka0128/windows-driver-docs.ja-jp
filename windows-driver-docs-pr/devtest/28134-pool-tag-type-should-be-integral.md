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
ms.openlocfilehash: 373e85d31a3ca2bc9d90974523d0d2d9abbb2c39
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350415"
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
<td align="left"><p>文字リテラル二重引用符で文字列ではなく単一引用符 ('gaT_') を使用して、プール タグ名があります。 逆バイト順で通常は。</p></td>
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
p = ExAllocatePoolWithTag(NonPagedPool, 30, 'gaT_');
```

 

 





