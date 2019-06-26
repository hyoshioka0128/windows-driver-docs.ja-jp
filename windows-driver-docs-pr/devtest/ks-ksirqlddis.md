---
title: KsIrqlDDIs rule ()
description: KsIrqlDDIs ルールは、カーネル ストリーミング (KS) ミニポート ドライバーを呼び出す KS Ddi 適切な IRQL でレベルを指定します。
ms.assetid: 060CAFBC-3BA6-40C7-91A1-8AFCB082A683
ms.date: 05/21/2018
keywords:
- KsIrqlDDIs rule ()
topic_type:
- apiref
api_name:
- KsIrqlDDIs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 08aeb628750cb8abe9389284473613019c7c4a5e
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392772"
---
# <a name="ksirqlddis-rule-"></a>KsIrqlDDIs rule ()


KsIrqlDDIs ルールは、カーネル ストリーミング (KS) ミニポート ドライバーを呼び出す KS Ddi 適切な IRQL でレベルを指定します。

|              |     |
|--------------|-----|
| ドライバー モデル | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00081009) |

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
<p>詳細については、次を参照してください。 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>します。</p></td>
</tr>
</tbody>
</table>

 

 

 





