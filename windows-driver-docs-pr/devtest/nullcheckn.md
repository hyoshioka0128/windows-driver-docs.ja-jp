---
title: NullCheck 規則 (ndis)
description: NullCheck 規則は、ドライバーコード内の NULL 値がドライバーの後で逆参照されないことを検証します。
ms.assetid: E892C9C3-854B-49EF-B69E-E2ED6438128F
ms.date: 05/21/2018
keywords:
- NullCheck 規則 (ndis)
topic_type:
- apiref
api_name:
- NullCheck
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4ddb9ec41e18cba931c6549c65b32bd0e287ecf5
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916284"
---
# <a name="nullcheck-rule-ndis"></a>NullCheck 規則 (ndis)


NullCheck 規則は、ドライバーコード内の NULL 値がドライバーの後で逆参照されないことを検証します。 このルールは、次のいずれかの条件が満たされた場合に、欠陥を報告します。

-   後で逆参照される NULL の割り当てがあります。
-   ドライバー内のプロシージャには、後で逆参照される可能性のあるグローバル/パラメーターがあります。また、ドライバーに明示的なチェックがあり、ポインターの初期値が NULL である可能性があることが示されています。

NullCheck 規則違反では、最も関連性の高いコードステートメントが [トレースツリー] ウィンドウで強調表示されます。 レポート出力の操作の詳細については、「[静的ドライバーの検証ツールレポート](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier-report)」と「[トレースビューアーに](https://docs.microsoft.com/windows-hardware/drivers/devtest/understanding-the-defect-viewer)ついて」を参照してください。

**Struct の例**

このコードスニペットは、構造体の適切な使用方法を示しています。

```
//Rule does not fail
typedef struct _B { 
    int *f; 
} B;
void GoodStruc(B *x) {
    B *y = x;
    y->f = NULL; //assign NULL
    if (x->f) {
        *(x->f) = 1;
    } //OK
    
}
```

このコードスニペットは、構造体の不適切な使用方法を示しています。 コードはコンパイルされますが、ランタイムエラーが生成されます。

```
//Rule fails
typedef struct _A {
    int *f; 
} A;

void BadStruc(A *x) {
    A *y = x;
    y->f = NULL; //assign NULL
    *(x->f) = 1; //dereferencing NULL
}
```

**関数の例**

この例では、NULL になる可能性がある関数のパラメーターがあり、後で逆参照されます。 また、ポインターの初期値が NULL であることを示す明示的なチェックがあります。

```
//Rule fails
void Bad(int *x)
{
    *x = 2; //Possibly dereferencing NULL
    if (x != NULL) //checks for null on a parameter
        *x = *x + 1;
}
```

この例では、パラメーターが NULL であると想定されていないという暗黙の事前条件があるため、規則違反はありません。

```
//Rule does not fail
void Good1(int *x)
{
     *x = 2;
     *x = *x + 1;
}
```

この2番目の例では、パラメーターが使用されるたびに、NULL に対する明示的なチェックがあります。

```
//Rule does not fail
void Good2(int *x)
{
    if (x != NULL)
        *x = 2; // ok
    if (x != NULL) //checks for null on a parameter
        *x = *x + 1;
}
```

**ドライバーモデル: NDIS**

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンパイル時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>nullcheck</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (役割の種類の宣言を使います)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

 





