---
title: C28717
description: C28717 無効な VARIANT 型を警告します。
ms.assetid: e1373005-a1ff-4722-98f9-00c7e4f89370
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28717
ms.openlocfilehash: 7b8607446b9165fab9fbfc0ac6f2ad530b88c4cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371588"
---
# <a name="c28717"></a>C28717


C28717 を警告します。無効な VARIANT 型

**Vt**のフィールドを**VARIANT 構造体**特定の値のみを実行することができます。 エラーは、他の値を代入します。

**Vt**のフィールドを**バリアント**または**VARIANTARG**構造体では、次の値を受け取ることができる (論理和場合によって、 **VT\_BYREF**。や**VT\_配列**)。**VT\_空**、 **VT\_NULL**、 **VT\_I2**、 **VT\_I4**、 **VT\_R4**、 **VT\_R8**、 **VT\_CY**、 **VT\_日付**、 **VT\_BSTR**、 **VT\_ディスパッチ**、 **VT\_エラー**、 **VT\_BOOL**、 **VT\_バリアント**、 **VT\_DECIMAL**、 **VT\_レコード、VT\_不明な**、 **VT\_I1**、 **VT\_UI1**、 **VT\_UI2**、 **VT\_UI4**、 **VT\_INT**、 **VT\_UINT** (**VT\_空**と**VT\_NULL**と組み合わせて使用できない**VT\_配列**)。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

PREfast では、次の例では、警告を報告します。

```
VARIANT var;
var.vt = VT_SAFEARRAY | VT_INT;
```

次の例では、このエラーを回避します。

```
VARIANT var;
var.vt = VT_ARRAY | VT_INT;
```

 

 





