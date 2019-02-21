---
title: C28651
description: 警告 C28651 静的初期化子では、メンバー関数ポインターのための書き込みページ上のコピーが行われます。
ms.assetid: 2E7B61A7-FF15-46C3-87B4-36CAA2E52CAC
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28651
ms.openlocfilehash: 5b88a6b49e6bbfe43d99dd51563943688f3b92fe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559979"
---
# <a name="c28651"></a>C28651


C28651 を警告します。静的初期化子がメンバー関数ポインターのための書き込みページでコピーを原因します。

グローバルまたは静的の const 変数の静的初期化子は多くの場合、完全に評価、コンパイル時に RDATA で生成されました。 ただし場合は、初期化子は、ポインターのメンバー関数であり、非静的関数が、全体の初期化子は配置できますコピー オン ライト ページで、パフォーマンスへの影響のあります。

高速な読み込みと書き込みのページ上のコピーを最小限に抑えることが必要なバイナリの場合は、静的初期化子のすべての関数ポインターがメンバーへのポインターの関数ではないことを検討してください。 ポインターのメンバー関数が必要な場合は、実際のメンバー関数の呼び出しをラップする単純な静的メンバー関数を作成します。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例


次のコード例では、このエラーを生成します。

```
void Func()
{
    WCHAR*pszBuf=newWCHAR[MAX_PATH];
    DPA_InsertPtr(_hdpa, DA_LAST, pszBuf);
}

void CleanupDPA()
{
    int count = DPA_GetCount(_hdpa);
    for (int i = 0; i < count; i++)
{
    delete [] (LPWSTR)DPA_GetPtr(_hdpa, i);
}
}  
```

次のコード例は、このエラーを回避できます。

```
class MyClass
{
    ...
    bool memberFunc();
    static bool memberFuncWrap(MyClass *thisPtr)
        { return thisPtr->memberFunc(); }
    ...
};
const StructType MyStruct[] = {
    ...
    &MyClass::memberFuncWrap,
    ...
};  
```









