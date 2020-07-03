---
title: PcTimedWaveRtStreamSetState ルール (オーディオ)
description: PcTimedWaveRtStreamSetState ルールは、ProtCls ミニポートドライバーが、必要な時間内に IMiniportWaveRTStream SetState を介して状態遷移を行うことを指定します。
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
ms.openlocfilehash: 070e95abca5263b3a32e618e69cdad3fdda98472
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917704"
---
# <a name="pctimedwavertstreamsetstate-rule-audio"></a>PcTimedWaveRtStreamSetState ルール (オーディオ)


PcTimedWaveRtStreamSetState 規則は、ProtCls ミニポートドライバーが、必要な時間内に[**IMiniportWaveRTStream:: SetState**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536756(v=vs.85))を介して状態遷移を行うことを指定します。

**ドライバーモデル: オーディオ**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証ツール \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00072001) |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>この規則を確認するには、コマンドプロンプトウィンドウを開きます。 Driver Verifier コマンドを入力し、 <strong>/domain audio</strong>を指定します。</p>
<p>たとえば、次のように入力します。</p>
<p><strong>verifier/domain audio</strong> [<em>オプション</em>] <strong>/driver</strong> <em> &lt; ドライバー &gt; </em>の設定</p>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

 

 





