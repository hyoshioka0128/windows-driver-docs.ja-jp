---
title: PcUnmapAllocatedPages ルール (オーディオ)
description: PcUnmapAllocatedPages ルールでは、A PortCls ミニポート ドライバーが、最初のマッピング解除せずに現在割り当てられて、MDL にマップされないことを指定します。PortCls ミニポート ドライバー IMiniportWaveRTStream インターフェイスを使用して解放する前にメモリの割り当てを解除します。
ms.assetid: 0ADF523C-9480-4AD2-8B98-23C95571CB0B
ms.date: 05/21/2018
keywords:
- PcUnmapAllocatedPages ルール (オーディオ)
topic_type:
- apiref
api_name:
- PcUnmapAllocatedPages
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c246b6dd5dade792113289a5840e30cc9604a540
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581112"
---
# <a name="pcunmapallocatedpages-rule-audio"></a>PcUnmapAllocatedPages ルール (オーディオ)


PcUnmapAllocatedPages ルールを使用することを指定します。

-   PortCls ミニポート ドライバーは、最初解除せずに現在割り当てられて、MDL にマップされません。
-   PortCls ミニポート ドライバーを使用して解放する前にメモリの割り当てを解除、 [IMiniportWaveRTStream](https://msdn.microsoft.com/library/windows/hardware/ff536738)インターフェイス。

|              |       |
|--------------|-------|
| ドライバー モデル | オーディオ |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00071004) |

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

 

 

 





