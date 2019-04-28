---
title: C28139
description: 警告 C28139 引数型と一致する必要があります。
ms.assetid: c20b39c2-eee7-4265-ac2f-39023da16549
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28139
ms.openlocfilehash: d5173df1bf4b9c5e2b62b0d976a67582f48b2270
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361388"
---
# <a name="c28139"></a>C28139


C28139 を警告します。引数の種類と一致する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>一部の関数引数の型に制限付きの算術演算子を許可する、そうでないです。 これは通常、正式な列挙型は、列挙型のメンバーが渡されませんでしたが、他の種類もためを示します。</p></td>
</tr>
</tbody>
</table>

 

関数呼び出しで列挙値は、関数宣言のパラメーターに指定した型と一致しません。 このエラーは、パラメーターが正しくコード化された、不足している、または誤順序の場合に発生することができます。 C 整数定数を使用して同じ意味で使用して、交換して使用する列挙値を許可するためには、エラーを認識せず、関数を正しくない列挙値を渡す珍しくありません。

コード分析ツールでは、このエラーを報告する場合は、WDK の関数のドキュメントを参照してください。 一部の関数に列挙値のみを許可するようにコーディングされています。 他のユーザーを許可、**ですか?:** 演算子をその型の値の間で選択するかなどとして列挙値のビット フラグをエンコードする場合に、列挙型のメンバーの算術演算子を許可します。 いくつかの場合、列挙値と定数を組み合わせることがあります。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次のコード例では、この警告を引き起こします。

```
....KeWaitForSingleObject(&MyMutex, UserRequest, UserRequest, false, NULL);
```

次のコード例は、この警告を回避できます。

```
....KeWaitForSingleObject(&MyMutex, UserRequest, UserMode, false, NULL);
```

 

 





