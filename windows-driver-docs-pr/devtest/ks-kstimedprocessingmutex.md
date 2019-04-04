---
title: KsTimedProcessingMutex ルール)
description: KsTimedProcessingMutex ルールでは、KS ミニポート ドライバーでは、100 を超えるミリ秒間処理ミュー テックスは保持しないようにすることを指定します。
ms.assetid: 18246AAE-6328-4171-973E-4C762CF719AE
ms.date: 05/21/2018
keywords:
- KsTimedProcessingMutex ルール)
topic_type:
- apiref
api_name:
- KsTimedProcessingMutex
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b7208a4005ef1f04865724d6da5d0a992e3b1c40
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574682"
---
# <a name="kstimedprocessingmutex-rule-"></a>KsTimedProcessingMutex ルール)


KsTimedProcessingMutex ルールでは、KS ミニポート ドライバーでは、100 を超えるミリ秒間処理ミュー テックスは保持しないようにすることを指定します。

|              |     |
|--------------|-----|
| ドライバー モデル | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00082005) |

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
<p><strong>verifier /domain ks</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

 

<a name="see-also"></a>関連項目
--------

[AVStream でミュー テックスの処理](https://msdn.microsoft.com/library/windows/hardware/ff567790)
 

 





