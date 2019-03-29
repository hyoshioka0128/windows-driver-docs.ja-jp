---
title: C30034
description: C30034 する可能性が割り当てられている実行可能なメモリ割り当て関数をフラグ値を渡すことを警告します。
ms.assetid: 11B06B23-17B4-4B97-A1EE-3351B72B7B1D
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C30034
ms.openlocfilehash: dded5285c83771be4df8fc3b2402aa4d50a570ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581117"
---
# <a name="c30034"></a>C30034


C30034 を警告します。フラグの値を割り当てられている実行可能なメモリの原因となる割り当て関数に渡します。 割り当て関数が実行可能ファイルの非ページ プールのフォームを要求していないことを確認してください。

禁止\_MEM\_割り当て\_かもしれません\_UNSAFE

実行可能ファイルの非ページ プールの割り当てが可能になる関数の呼び出しが検出されました。 パラメーターが使用されることを示す結果の割り当てがあります非実行可能、実際がない可能性が高いと判断され、実行可能ファイルのメモリが割り当てられています。 これは、省略可能な割り当て関数をパラメーターとして受け取る関数で最も一般的です。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例


次のコード生成の場合は、不明なので、この警告*pAllocate*この - 指定した型の 4 番目のパラメーター (0 で、実行可能ファイル) を割り当てます内から割り当ての種類が設定されている場合、または*pAllocate します。*

```
ExInitializeNPagedLookasideList(   pLookaside,
                pAllocate,
                pFree,
                0,
                size,
                tag,
                depth);
```

次のコードは、この警告を回避できます。

```
ExInitializeNPagedLookasideList(   pLookaside,
                pAllocate,
                pFree,
                POOL_NX_ALLOCATION,
                size,
                tag,
                depth);
```

 

 





