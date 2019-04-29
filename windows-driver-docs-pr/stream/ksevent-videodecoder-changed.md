---
title: KSEVENT\_VIDEODECODER\_CHANGED
description: KSEVENT\_VIDEODECODER\_CHANGED イベントは、新しい物理入力からコネクタをカーネル モードのビデオ キャプチャ ミニドライバー DirectShow がユーザー モードでの選択などのアクションを伝達します。
ms.assetid: cb197233-fce3-4580-95d3-94605fd1f3e4
keywords:
- KSEVENT_VIDEODECODER_CHANGED ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSEVENT_VIDEODECODER_CHANGED
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa71eb42d32a9b9470b89d5fe1b4875bd2701a0d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329734"
---
# <a name="kseventvideodecoderchanged"></a>KSEVENT\_VIDEODECODER\_CHANGED


KSEVENT\_VIDEODECODER\_CHANGED イベントは、新しい物理入力からコネクタをカーネル モードのビデオ キャプチャ ミニドライバー DirectShow がユーザー モードでの選択などのアクションを伝達します。

## <span id="ddk_ksevent_videodecoder_changed_ks"></span><span id="DDK_KSEVENT_VIDEODECODER_CHANGED_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>イベント記述子の種類</th>
<th>イベント値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561937" data-raw-source="[&lt;strong&gt;KSE_NODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561937)"><strong>KSE_NODE</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561750" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561750)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

DirectShow フィルターと KsProxy の詳細については、次を参照してください。[カーネル ストリーミング プロキシ](https://msdn.microsoft.com/library/windows/hardware/ff560877)します。

 

 





