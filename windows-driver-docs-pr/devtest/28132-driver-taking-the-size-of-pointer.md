---
title: C28132
description: 警告 C28132、ポインターのサイズを取得しています。
ms.assetid: 9047cfb5-220f-42ad-ba1d-3c1bd43a3423
keywords:
- ドライバーの WDK PREfast の一覧に警告が表示される
- ドライバーの WDK PREfast の一覧にエラーが表示される
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28132
ms.openlocfilehash: 19d604687fe6cced382f764d3da73827dc6c6b5e
ms.sourcegitcommit: 9dbb1ef59c3e797bfc3cc418dd2b9bdc44940d14
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284982"
---
# <a name="c28132"></a>C28132


警告 C28132:ポインターのサイズを取得する

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>これにより、ポインターのサイズ (4 または 8) が返されます。これは、ポインターが指すオブジェクトのサイズではありません。 ポインターを逆参照するか、ポインターのサイズが意図されている場合は、代わりにポインター型または (void *) を使用します。</p></td>
</tr>
</tbody>
</table>

 

ドライバーが指す値のサイズではなく、ポインター変数のサイズを取得しています。 ドライバーがポイント先の値のサイズを必要とする場合は、値を参照するようにコードを変更します。 ドライバーが実際にポインターのサイズを必要とする場合は、ポインター型 (LPSTR、 **char\***  、または**void\*** など) のサイズを取得して、これが意図されていることを明確にします。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>よう

この警告を elicits するコード例を次に示します。

```
memset(b, 0, sizeof(b));
```

次のコード例では、この警告を回避します。

```
memset(b, 0, sizeof(*b));
```

 

 





