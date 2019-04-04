---
title: SpReturnValue ルール (storport)
description: このルールは、HwStorFindAdapter および VirtualHwStorFindAdapter のドライバーの実装が有効な状態を返すことを確認します。 有効な状態は、次の SP のいずれかの\_を返す\_FOUND、SP\_を返す\_エラー、SP\_返す\_不適切な\_構成では、または SP\_返す\_いない\_が見つかりました。
ms.assetid: 4F9E0FE3-4B1B-4C06-9DA0-8307C43E0DBA
ms.date: 05/21/2018
keywords:
- SpReturnValue ルール (storport)
topic_type:
- apiref
api_name:
- SpReturnValue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2b932c1030ad29a58f0ae55bd32a2dfd84305302
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579881"
---
# <a name="spreturnvalue-rule-storport"></a>SpReturnValue ルール (storport)


このルールを検証するドライバーの実装の[ **HwStorFindAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff557390)と[ **VirtualHwStorFindAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff568008)返す有効な状態です。 有効な状態は、次のいずれか。**SP\_返す\_が見つかりました**、 **SP\_返す\_エラー**、 **SP\_返す\_不良\_CONFIG**、または**SP\_返す\_いない\_FOUND**します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>SpReturnValue</strong>ルール。</p>
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

 

 





