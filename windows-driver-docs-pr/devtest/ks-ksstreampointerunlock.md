---
title: KsStreamPointerUnlock ルール)
description: KsStreamPointerUnlock ルールでは、ドライバーが読み込まれていない (またはデバイスを停止) する前に、カーネル ストリーミング (KS) ミニポート ドライバーはすべてのストリーム ポインターをロック解除。 を指定します。
ms.assetid: 74742111-85C2-44D2-ACDB-BE1D2D468ED5
ms.date: 05/21/2018
keywords:
- KsStreamPointerUnlock ルール)
topic_type:
- apiref
api_name:
- KsStreamPointerUnlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d8e4d3bd20c0fac35f98bfefe221039a3c9210a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573813"
---
# <a name="ksstreampointerunlock-rule-"></a>KsStreamPointerUnlock ルール)


KsStreamPointerUnlock ルールでは、ドライバーが読み込まれていない (またはデバイスを停止) する前に、カーネル ストリーミング (KS) ミニポート ドライバーはすべてのストリーム ポインターをロック解除。 を指定します。

|              |     |
|--------------|-----|
| ドライバー モデル | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00081004) |

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
<p>例:</p>
<p><strong>verifier /domain ks</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>詳細については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>します。</p></td>
</tr>
</tbody>
</table>

 

 

 





