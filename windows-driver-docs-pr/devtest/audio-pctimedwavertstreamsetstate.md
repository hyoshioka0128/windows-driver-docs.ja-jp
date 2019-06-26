---
title: PcTimedWaveRtStreamSetState ルール (オーディオ)
description: PcTimedWaveRtStreamSetState ルールでは、ProtCls ミニポート ドライバーが必要な時間内 IMiniportWaveRTStream SetState を使用して状態遷移を使用することを指定します。
ms.assetid: D49869E0-9108-460B-8FA3-4FD99C3EA81E
ms.date: 05/21/2018
keywords:
- PcTimedWaveRtStreamSetState ルール (オーディオ)
topic_type:
- apiref
api_name:
- PcTimedWaveRtStreamSetState
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3127283fcf3fb22761078204e64d83efabbba698
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394022"
---
# <a name="pctimedwavertstreamsetstate-rule-audio"></a>PcTimedWaveRtStreamSetState ルール (オーディオ)


PcTimedWaveRtStreamSetState ルールでは、ProtCls ミニポート ドライバーを使用して状態遷移は、ことを指定します[ **IMiniportWaveRTStream::SetState** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536756(v=vs.85))必要な時間内で。

|              |       |
|--------------|-------|
| ドライバー モデル | オーディオ |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00072001) |

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

 

 

 





