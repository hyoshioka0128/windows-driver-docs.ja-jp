---
title: Irql\_IrqlSetting\_関数ルール (ndis)
description: Irql\_IrqlSetting\_関数の規則は、適切な IRQL レベルで NDIS 割り込みマクロを呼び出す必要があることを指定します。
ms.assetid: 47e62c7c-bd43-4b4a-b7d6-3f64a4b8a6c8
ms.date: 05/21/2018
keywords:
- Irql_IrqlSetting_Function ルール (ndis)
topic_type:
- apiref
api_name:
- Irql_IrqlSetting_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 35bc1330fdafa1ee9d089b19157d45a2fdf18043
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370884"
---
# <a name="irqlirqlsettingfunction-rule-ndis"></a>Irql\_IrqlSetting\_関数ルール (ndis)


Irql\_IrqlSetting\_関数の規則は、適切な IRQL レベルで NDIS 割り込みマクロを呼び出す必要があることを指定します。

このルールは、次の NDIS マクロを確認します。

**NDIS\_低い\_IRQL**
**NDIS\_を発生させる\_IRQL\_TO\_ディスパッチ**

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>Irql_IrqlSetting_Function</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**NDIS\_低い\_IRQL**](https://msdn.microsoft.com/library/windows/hardware/ff565882)
[**NDIS\_を発生させる\_IRQL\_TO\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff566854)








