---
title: StorPortFindAdapter ルール (storport)
description: HwStorFindAdapter ルーチンは、ポート、MaximumTransferLength と NumberOfPhysicalBreaks フィールドを設定する必要があります\_構成\_情報構造体。
ms.assetid: 8BE79E99-078E-4CCE-A6C1-0DEB1F1252DA
ms.date: 05/21/2018
keywords:
- StorPortFindAdapter ルール (storport)
topic_type:
- apiref
api_name:
- StorPortFindAdapter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1053f535c4246e6afd29732ef2f52f6b160a04e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574259"
---
# <a name="storportfindadapter-rule-storport"></a>StorPortFindAdapter ルール (storport)


[ **HwStorFindAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff557390)ルーチンを設定する必要があります、 **MaximumTransferLength**と**NumberOfPhysicalBreaks** 内のフィールド**ポート\_構成\_情報**構造体。 これら両方のフィールドの値は、既定では、 **SP\_初期化されていない\_値**します。 これらのフィールドのいずれかに設定されたままの場合**SP\_初期化されていない\_値**から終了時に**FindAdapter**ドライバーが、規則に失敗します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>StorPortFindAdapter</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

 

 





