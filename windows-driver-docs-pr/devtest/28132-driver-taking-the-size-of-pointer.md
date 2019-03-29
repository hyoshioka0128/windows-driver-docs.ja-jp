---
title: C28132
description: 警告 C28132 ポインターのサイズを取得します。
ms.assetid: 9047cfb5-220f-42ad-ba1d-3c1bd43a3423
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28132
ms.openlocfilehash: 7b7834d76fd7a46cda95041ab99cfd7e910db0ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574152"
---
# <a name="c28132"></a>C28132


C28132 を警告します。ポインターのサイズを取得します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>(4 または 8) のポインターのサイズを得られる、指し示されるオブジェクトのサイズではありません。 ポインターを逆参照またはポインターのサイズの場合は、ポインター型を使用して、または (void *) 代わりにします。</p></td>
</tr>
</tbody>
</table>

 

ドライバーには、ポイントされている値のサイズではなく、ポインター変数のサイズがかかっています。 ドライバーに示される値のサイズを必要とする場合は、値を参照するようにコードを変更します。 ドライバーが実際には、ポインターのサイズが必要な場合は、ポインター型のサイズを取得 (たとえば、LPSTR、 **char\\*** またはでも * * void\\* * *) 目的であるが明確にします。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次のコード例では、この警告を引き起こします。

```
memset(b, 0, sizeof(b));
```

次のコード例は、この警告を回避できます。

```
memset(b, 0, sizeof(*b));
```

 

 





