---
title: SafeStrings ルール (wdm)
description: SafeStrings ルールでは、ドライバーがシステムを誤ってまたは悪意のある侵入から保護する文字列操作関数のみを呼び出すことを指定します。 これらのドライバーの安全な文字列関数は、Ntstrsafe.h で定義されます。
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
ms.openlocfilehash: 64fafd6c0365963d9b62f1e9a714f0593c400332
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394082"
---
# <a name="safestrings-rule-wdm"></a>SafeStrings ルール (wdm)


**SafeStrings**ルールでは、ドライバーがシステムを誤ってまたは悪意のある侵入から保護する文字列操作関数のみを呼び出すことを指定します。 これらのドライバーの安全な文字列関数は、Ntstrsafe.h で定義されます。

このルールに準拠するには、カーネル モード ドライバー用に安全と見なされる、文字列関数を使用します。 安全な文字列関数と置き換える、安全でない関数は、「 [**安全な文字列関数を使用して**](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-safe-string-functions)します。 安全な文字列関数の 2 つのセットがあります。 安全な文字列関数の 1 つのセットでは、(、Ntstrsafe.h で定義されている場合) カーネル モード コードで使用されます。 その他の一連の安全な文字列関数は、ユーザー モード アプリケーションで使用され、Strsafe.h で定義されています。

カーネル モード ドライバーは、ユーザー モードの安全な文字列関数を使用している場合、ドライバーはこの規則に違反します。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>SafeStrings</strong>ルール。</p>
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

<a name="see-also"></a>関連項目
--------

[**安全な文字列関数を使用します。** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-safe-string-functions)
 

 





