---
title: KsTimedFilterCallbacks ルール)
description: KsTimedFilterCallbacks ルールでは、カーネル ストリーミング (KS) ミニポート ドライバーが 500 ミリ秒以内で、フィルターのコールバック関数から返すことを指定します。
ms.assetid: 5F631D49-405F-4F1A-A280-FEFB4ADA460D
ms.date: 05/21/2018
keywords:
- KsTimedFilterCallbacks ルール)
topic_type:
- apiref
api_name:
- KsTimedFilterCallbacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f9144b7a72b86fe1d3a75473ece4ef3c7f2f4994
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364692"
---
# <a name="kstimedfiltercallbacks-rule-"></a>KsTimedFilterCallbacks ルール)


KsTimedFilterCallbacks ルールでは、カーネル ストリーミング (KS) ミニポート ドライバーが 500 ミリ秒以内で、フィルターのコールバック関数から返すことを指定します。

|              |     |
|--------------|-----|
| ドライバー モデル | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00082003) |

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
<p>次に、例を示します。</p>
<p><strong>verifier /domain ks</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>詳細については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>します。</p></td>
</tr>
</tbody>
</table>

 

 

 





