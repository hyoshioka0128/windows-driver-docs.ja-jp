---
title: C28624
description: Release() LResultFromObject からカウントをインクリメントに一致する C28624 いいえ呼び出しを警告します。
ms.assetid: e769d232-ef6e-4b70-8cac-f4dd43807e1d
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28624
ms.openlocfilehash: 115bc9a5f20f0612b51d05286c67456056a9b109
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570821"
---
# <a name="c28624"></a>C28624


C28624 を警告します。LResultFromObject からカウントをインクリメントを一致するように Release() への呼び出しはありません。

**LresultFromObject**新しい IAccessible オブジェクトの参照カウントが増加します。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次のコード例では、この警告を生成します。

```
{
 IAccessible *pacc = CreateNewIAccessible();
 LRESULT lTemp = LresultFromObject(riid, NULL, pacc );
}

{
 IAccessible *pacc = NULL;
 // Get new interface (from same object)
 QueryInterface( & pacc );

 // Lresult will internally bump up the refcount
 // to hold onto the object.
 
 LRESULT lTemp = LresultFromObject( riid, NULL, pacc );
}
```

次の例では、このエラーを回避します。

```
{
 IAccessible *pacc = CreateNewIAccessible();
 // Lresult internally increases the refcount to
 // hold onto the object.
 LRESULT lTemp = LresultFromObject(riid, NULL, pacc );

 // We no longer need our pacc interface, so we release it.

 pacc->Release();
}
```

 

 





