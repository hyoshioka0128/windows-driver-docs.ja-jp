---
title: C28134
description: 警告 C28134 プールタグの型は、文字列または文字列ポインターではなく、整数である必要があります。
ms.assetid: f61aec4c-4072-421f-aa6d-d9399d0c439c
keywords:
- ドライバーの WDK PREfast の一覧に警告が表示される
- ドライバーの WDK PREfast の一覧にエラーが表示される
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28134
ms.openlocfilehash: c266c44ad2ca609f53fe8203a454fbf9682243cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840318"
---
# <a name="c28134"></a>C28134


警告 C28134: プールタグの型は、文字列または文字列ポインターではなく、整数である必要があります

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>プールタグ名は、二重引用符で囲まれた文字列ではなく、単一引用符 (' gaT_ ') を使用する文字リテラルである必要があります。 通常は、逆バイト順になります。</p></td>
</tr>
</tbody>
</table>

 

ドライバーが、 [**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)などのプールタグを割り当てる関数を呼び出していますが、単一引用符で囲まれたリテラル以外の値を使用して、プールタグの値を指定しています。 プールタグに引用符で囲まれた文字列を使用しないでください。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>よう

この警告を elicits するコード例を次に示します。

```
p = ExAllocatePoolWithTag(NonPagedPool, 30, "_Tag");
```

次のコード例では、この警告を回避します。

```
p = ExAllocatePoolWithTag(NonPagedPool, 30, 'gaT_');
```

 

 





