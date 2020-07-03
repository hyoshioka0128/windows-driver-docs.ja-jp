---
title: SafeStrings ルール (wdm)
description: SafeStrings 規則は、意図しない、または悪意のある侵入からシステムを保護する文字列操作関数だけがドライバーによって呼び出されるように指定します。 これらのドライバーの安全な文字列関数は、、Ntstrsafe.h で定義されています。
ms.assetid: 77e949cf-b184-4235-80c4-4718d4808d11
ms.date: 05/21/2018
keywords:
- SafeStrings ルール (wdm)
topic_type:
- apiref
api_name:
- SafeStrings
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0613e89440b7a10782e6d8908341bcb2765b5c33
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917201"
---
# <a name="safestrings-rule-wdm"></a>SafeStrings ルール (wdm)


**Safestrings**規則は、意図しない、または悪意のある侵入からシステムを保護する文字列操作関数だけがドライバーによって呼び出されるように指定します。 これらのドライバーの安全な文字列関数は、、Ntstrsafe.h で定義されています。

この規則に準拠するには、カーネルモードドライバーで安全と見なされる文字列関数を使用します。 安全な文字列関数と置換される unsafe 関数は、 [**「Safe 文字列関数の使用**](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-safe-string-functions)」に記載されています。 安全な文字列関数には、2つのセットがあります。 安全な文字列関数の1つのセットは、(、Ntstrsafe.h で定義されている) カーネルモードコードで使用します。 セーフ文字列関数のもう1つのセットは、ユーザーモードアプリケーションで使用するためのもので、Strsafe で定義されています。

カーネルモードドライバーでユーザーモードのセーフ文字列関数が使用されている場合、ドライバーはこの規則に違反します。

**ドライバーモデル: WDM**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>safestrings</strong>ルールを指定します。</p>
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

<a name="see-also"></a>こちらもご覧ください
--------

[**セーフ文字列関数の使用**](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-safe-string-functions)
 

 





