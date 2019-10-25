---
title: KSEVENT\_LOOPEDSTREAMING\_POSITION
description: KSEVENT\_LOOPEDSTREAMING\_POSITION イベントは、オーディオストリームがループバッファー内の指定された位置に達したことを示します。使用状況の概要 TableTargetEvent Descriptor TypeEvent Value TypePinKSEVENTLOOPEDSTREAMING\_POSITION\_イベント\_データイベントの値の種類 (操作データ) は、イベント\_データ\_イベントの\_位置にあります次の情報を含む構造体は、位置イベントが発生したときにシステムがクライアントに送信する通知の種類を示します。イベントをトリガーするバッファー位置。
ms.assetid: 6609ddac-e506-4fab-b580-0def30be2e9c
keywords:
- KSEVENT_LOOPEDSTREAMING_POSITION オーディオデバイス
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
ms.openlocfilehash: 941c651f54369090bf05892cda10465056f51fe7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833139"
---
# <a name="ksevent_loopedstreaming_position"></a>KSEVENT\_LOOPEDSTREAMING\_POSITION


KSEVENT\_LOOPEDSTREAMING\_POSITION イベントは、オーディオストリームがループバッファー内の指定された位置に達したことを示します。

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
<th align="left">イベント値の種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-loopedstreaming_position_event_data" data-raw-source="[&lt;strong&gt;LOOPEDSTREAMING_POSITION_EVENT_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-loopedstreaming_position_event_data)"><strong>LOOPEDSTREAMING_POSITION_EVENT_DATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

イベント値の種類 (操作データ) は、次の情報を含むイベント\_データ構造\_LOOPEDSTREAMING\_位置です。

-   位置イベントが発生したときにシステムがクライアントに送信する通知の種類。

-   イベントをトリガーするバッファー位置。

このイベントは、システムによる内部使用のみを目的としています。

<a name="remarks"></a>注釈
-------

Windows Server 2003、Windows XP、Windows 2000、Windows Me、および Windows 98 では、WavePci および WaveCyclic port ドライバーに KSEVENT\_LOOPEDSTREAMING\_POSITION イベント用の独自の組み込みハンドラーが含まれています。 WavePci および WaveCyclic ミニポートドライバーは、これらのイベントのハンドラーを実装することはできません。

Windows Vista では、Wave*Xxx*ポートドライバーでは、イベントハンドラーや、KSEVENT\_LOOPEDSTREAMING\_POSITION イベントに対するその他のサポートは実装されていません。

ループバッファーは、型[**Ksinterface\_標準\_ループ\_ストリーミング**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksinterface-standard-looped-streaming)のオーディオストリームのデータバッファーです。 再生カーソルまたはレコードカーソルがループバッファーの最後に達すると、カーソルがバッファーの先頭に折り返されます。

ループバッファー、バッファー位置、および再生およびレコードのカーソルの詳細については、「 [Audio Position プロパティ](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-position-property)」を参照してください。

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
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))

[**KSK インターフェイス\_STANDARD\_ループ\_ストリーミング**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksinterface-standard-looped-streaming)

[**LOOPEDSTREAMING\_POSITION\_イベント\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-loopedstreaming_position_event_data)

 

 






