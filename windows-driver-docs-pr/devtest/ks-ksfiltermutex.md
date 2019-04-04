---
title: KsFilterMutex ルール)
description: KsFilterMutex ルールでは、KS ミニポート ドライバーが取得し、正しい順序でフィルター ミュー テックスを解放を指定します。
ms.assetid: 09927C42-2F05-49F6-AFE1-E45049ED2805
ms.date: 05/21/2018
keywords:
- KsFilterMutex ルール)
topic_type:
- apiref
api_name:
- KsFilterMutex
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6bd5dadbff6d84016b218665f33b255faa715162
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573895"
---
# <a name="ksfiltermutex-rule-"></a>KsFilterMutex ルール)


KsFilterMutex ルールでは、KS ミニポート ドライバーが取得し、正しい順序でフィルター ミュー テックスを解放を指定します。

-   KS ミニポート ドライバーでは、ミュー テックスをフィルターする再帰的を取得できません。
-   スレッドは、まずそれを取得しなくても、フィルター、ミュー テックスを解放する必要がありますされません。

|              |     |
|--------------|-----|
| ドライバー モデル | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x0008100A) |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>このルールを確認するには、コマンド プロンプト ウィンドウを開きます。 Driver Verifier のコマンドを入力し、指定<strong>/domain ks</strong>します。</p>
<p>以下に例を示します。</p>
<p></p>
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

 

**verifier/domain ks** \[*オプション*\] **/driver** *&lt;yourdriver&gt;* も参照してください
--------

[AVStream でコントロールのミュー テックスをフィルター処理します。](https://msdn.microsoft.com/library/windows/hardware/ff559603)
 

 





