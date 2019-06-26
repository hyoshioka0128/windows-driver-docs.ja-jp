---
title: PcIrqlIport ルール (オーディオ)
description: PcIrqlIport ルールでは、こと PortCls ミニポート ドライバー呼び出す必要があります PortCls IPort インターフェイスで適切な IRQL レベルを指定します。
ms.assetid: 59E22F37-3377-4B98-8613-EF5ED0CB63D9
ms.date: 05/21/2018
keywords:
- PcIrqlIport ルール (オーディオ)
topic_type:
- apiref
api_name:
- PcIrqlIport
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 29ccf444cd7bcc80763579d7dc0f423d85e5aa8f
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394030"
---
# <a name="pcirqliport-rule-audio"></a>PcIrqlIport ルール (オーディオ)


PcIrqlIport ルールでは、こと PortCls ミニポート ドライバー呼び出す必要があります PortCls IPort インターフェイスで適切な IRQL レベルを指定します。

|              |       |
|--------------|-------|
| ドライバー モデル | オーディオ |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00071003) |

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
<td align="left"><p>このルールを確認するには、コマンド プロンプト ウィンドウを開きます。 Driver Verifier のコマンドを入力し、指定<strong>/domain オーディオ</strong>します。</p>
<p>以下に例を示します。</p>
<p><strong>verifier /domain audio</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>詳細については、次を参照してください。 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>します。</p></td>
</tr>
</tbody>
</table>

 

 

 





