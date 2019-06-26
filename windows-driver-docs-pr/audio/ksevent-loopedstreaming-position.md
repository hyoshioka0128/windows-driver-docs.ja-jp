---
title: KSEVENT\_LOOPEDSTREAMING\_位置
description: KSEVENT\_LOOPEDSTREAMING\_位置イベントは、オーディオのストリーム バッファーをループ内の指定位置に達したことを示します。使用状況概要 TableTargetEvent 記述子 TypeEvent 値 TypePinKSEVENTLOOPEDSTREAMING\_位置\_イベント\_データ イベント値の型 (データの操作) は、LOOPEDSTREAMING\_の位置\_イベント\_位置イベントが発生したときに、システムがクライアントに送信する通知の種類を次の情報を含むデータ構造です。イベントをトリガーするバッファーの位置。
ms.assetid: 6609ddac-e506-4fab-b580-0def30be2e9c
keywords:
- KSEVENT_LOOPEDSTREAMING_POSITION オーディオ デバイス
topic_type:
- apiref
api_name:
- KSEVENT_LOOPEDSTREAMING_POSITION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b99906618a060df0626c319e91652b672c1fadcc
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391536"
---
# <a name="kseventloopedstreamingposition"></a>KSEVENT\_LOOPEDSTREAMING\_位置


KSEVENT\_LOOPEDSTREAMING\_位置イベントは、オーディオのストリーム バッファーをループ内の指定位置に達したことを示します。

**使用状況の概要テーブル**

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">対象</th>
<th align="left">イベント記述子の種類</th>
<th align="left">イベント値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-loopedstreaming_position_event_data" data-raw-source="[&lt;strong&gt;LOOPEDSTREAMING_POSITION_EVENT_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-loopedstreaming_position_event_data)"><strong>LOOPEDSTREAMING_POSITION_EVENT_DATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

イベント値の型 (データの操作) は、LOOPEDSTREAMING\_位置\_イベント\_次の情報を含むデータ構造です。

-   位置のイベントが発生したときに、システムがクライアントに送信する通知の種類。

-   イベントをトリガーするバッファーの位置。

このイベントは、システム内部使用のみのものです。

<a name="remarks"></a>注釈
-------

WavePci と WaveCyclic ポート ドライバーには、Windows Server 2003、Windows XP、Windows 2000、Windows Me、および Windows 98、KSEVENT の独自の組み込みハンドラーが含まれて\_LOOPEDSTREAMING\_イベントの位置。 WavePci と WaveCyclic ミニポート ドライバーは、これらのイベント ハンドラーを実装しないでください。

波のいずれも Windows Vista で*Xxx*ポート ドライバーは、イベント ハンドラーまたは KSEVENT の他のサポートを実装\_LOOPEDSTREAMING\_イベントの位置。

ループのバッファーが型のオーディオ ストリームのデータ バッファー [ **KSINTERFACE\_標準\_るーぷさいせいぼたん\_ストリーミング**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksinterface-standard-looped-streaming)します。 Play またはカーソルの記録がループのバッファーの末尾に達すると、カーソルは、バッファーの先頭にラップします。

ループのバッファー、バッファーの位置と再生およびレコードのカーソルに関する詳細については、次を参照してください。[オーディオ位置プロパティ](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-position-property)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))

[**KSINTERFACE\_標準\_るーぷさいせいぼたん\_ストリーミング**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksinterface-standard-looped-streaming)

[**LOOPEDSTREAMING\_位置\_イベント\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-loopedstreaming_position_event_data)

 

 






