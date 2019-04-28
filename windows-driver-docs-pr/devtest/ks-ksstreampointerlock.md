---
title: KsStreamPointerLock ルール)
description: KsStreamPointerLock ルールでは、カーネル ストリーミング (KS) ミニポート ドライバーが、正しい順序で KsStreamPointerLock と KsStreamPointerUnlock 関数を使用することを指定します。
ms.assetid: 365C8656-57F1-4774-9859-B67D64403BB3
ms.date: 05/21/2018
keywords:
- KsStreamPointerLock ルール)
topic_type:
- apiref
api_name:
- KsStreamPointerLock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 334f719996bbf8c553b2378befbddf16a09b1e60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364703"
---
# <a name="ksstreampointerlock-rule-"></a>KsStreamPointerLock ルール)


KsStreamPointerLock ルールでは、カーネル ストリーミング (KS) ミニポート ドライバーが使用するように指定、 [ **KsStreamPointerLock** ](https://msdn.microsoft.com/library/windows/hardware/ff567134)と[ **KsStreamPointerUnlock**](https://msdn.microsoft.com/library/windows/hardware/ff567137)正しいシーケンスで機能します。

ミニポート ドライバーが既にロックされているストリーム ポインターをロックしようとしています。 いない、または既にロックされていないストリーム ポインターのロックを解除しようとしています。 必要があります。

|              |     |
|--------------|-----|
| ドライバー モデル | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00081003) |

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

 

 

 





