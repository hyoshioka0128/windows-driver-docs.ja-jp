---
title: NullCheck ルール (storport)
description: NullCheck ルールは、ドライバーの後で、ドライバーのコード内の NULL 値が逆参照しないことを確認します。
ms.assetid: 9322B5F8-6681-4000-A64C-E66D2D4A5D6D
ms.date: 05/21/2018
keywords:
- NullCheck ルール (storport)
topic_type:
- apiref
api_name:
- NullCheck
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3f36654ec36ae331cc6a0df7f77b5514ecd3dedf
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392084"
---
# <a name="nullcheck-rule-storport"></a>NullCheck ルール (storport)


NullCheck ルールは、ドライバーの後で、ドライバーのコード内の NULL 値が逆参照しないことを確認します。 このルールは、これらの条件のいずれかが true の場合、欠陥を報告します。

-   以降は逆参照が NULL の代入です。
-   ドライバーでは、後で逆参照が NULL の可能性があるプロシージャにグローバル/パラメーターがあるし、ポインターの初期値は NULL である可能性がありますの候補を示す、ドライバーでの明示的なチェックがあります。

NullCheck ルール違反では、最も関連のコード ステートメントは、トレースのツリー ペインで強調表示されます。 レポートの出力の使用方法の詳細については、次を参照してください。[静的ドライバー検証ツールのレポート](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier-report)と[トレース ビューアーを理解する](https://docs.microsoft.com/windows-hardware/drivers/devtest/understanding-the-defect-viewer)します。

**構造体の例**

このコード スニペットでは、構造体の適切な使用を示します。

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

このコード スニペットでは、構造体の不適切な使用を示します。 コードでは、コンパイルされますが、実行時エラーが生成されます。

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

この例では null の場合、逆参照する可能性のある関数のパラメーターがそれ以降です。 さらに、ポインターの初期値は NULL である可能性がありますの候補を示す、明示的なチェックがあります。

```
//Rule fails
void Bad(int *x)
{
    *x = 2; //Possibly dereferencing NULL
    if (x != NULL) //checks for null on a parameter
        *x = *x + 1;
}
```

この例ではありません規則違反、パラメーターがないための暗黙的な前提条件が NULL であると想定する可能性があるため。

```
//Rule does not fail
void Good1(int *x)
{
     *x = 2;
     *x = *x + 1;
}
```

この 2 番目の例は、明示的なチェックの null の場合にたびに、パラメーターを使用します。

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

|              |          |
|--------------|----------|
| ドライバー モデル | Storport |

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>NullCheck</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

 

 





