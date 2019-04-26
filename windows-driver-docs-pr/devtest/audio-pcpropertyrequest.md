---
title: PcPropertyRequest ルール (オーディオ)
description: PcPropertyRequest ルール指定 PortCls ミニポート ドライバーは、状態の NtStatus 値を持つ PcCompletePendingPropertyRequest を呼び出さないで\_保留します。
ms.assetid: 7D06F924-512F-4D21-98CD-B9E60CC8A6AB
ms.date: 05/21/2018
keywords:
- PcPropertyRequest ルール (オーディオ)
topic_type:
- apiref
api_name:
- PcPropertyRequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c0f552ae223841a10520ce2a6bba689dd9952bb8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343144"
---
# <a name="pcpropertyrequest-rule-audio"></a>PcPropertyRequest ルール (オーディオ)


PcPropertyRequest ルールでは、PortCls ミニポート ドライバーが呼び出す必要がありますしないことを指定します、 [ **PcCompletePendingPropertyRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff537687)で、 *NtStatus* STATUS の値\_保留します。

|              |       |
|--------------|-------|
| ドライバー モデル | オーディオ |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00071008) |

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
<p>詳細については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>します。</p></td>
</tr>
</tbody>
</table>

 

 

 





