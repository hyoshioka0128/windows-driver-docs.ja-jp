---
title: KSPROPERTY\_RTAUDIO\_バッファー\_WITH\_通知
description: KSPROPERTY\_RTAUDIO\_バッファー\_WITH\_通知プロパティは、ドライバーによって割り当てられた循環バッファーのオーディオ データを指定し、イベント通知の要件を特定します。次の表では、このプロパティの機能をまとめたものです。
ms.assetid: a66727ae-03d6-41b5-b5c9-3b04352b3b83
keywords:
- KSPROPERTY_RTAUDIO_BUFFER_WITH_NOTIFICATION オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_BUFFER_WITH_NOTIFICATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b6066efff020fb8c8d61ac298e1fbe1edcd5bb7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354393"
---
# <a name="kspropertyrtaudiobufferwithnotification"></a>KSPROPERTY\_RTAUDIO\_バッファー\_WITH\_通知


KSPROPERTY\_RTAUDIO\_バッファー\_WITH\_通知プロパティは、ドライバーによって割り当てられた循環バッファーのオーディオ データを指定し、イベント通知の要件を特定します。

次の表では、このプロパティの機能をまとめたものです。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">取得</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>〇</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_buffer_property_with_notification" data-raw-source="[&lt;strong&gt;KSRTAUDIO_BUFFER_PROPERTY_WITH_NOTIFICATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_buffer_property_with_notification)"><strong>KSRTAUDIO_BUFFER_PROPERTY_WITH_NOTIFICATION</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_buffer" data-raw-source="[&lt;strong&gt;KSRTAUDIO_BUFFER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_buffer)"><strong>KSRTAUDIO_BUFFER</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンス データ) から成る、KSRTAUDIO\_バッファー\_プロパティ\_WITH\_通知の構造体を含む、 [ **KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))の他のメンバーと構造体。 クライアントは、構造体に、要求されたバッファー サイズを書き込みます。 クライアントとしてベース アドレスを指定する必要があります**NULL**特定のベース アドレスが必要な場合を除き、します。

このプロパティは、DMA 駆動のイベント通知を使用するときに使用されます。 に基づいて、 **NotificationCount**メンバーが、登録に 1 回だけ (最後) のイベントがシグナル状態で 2 回 (中間点と終了) または循環バッファーを巡回ごと。 使用してイベントの登録[ **KSPROPERTY\_RTAUDIO\_登録\_通知\_イベント**](ksproperty-rtaudio-register-notification-event.md) KSPROPERTY の呼び出しに成功した後\_RTAUDIO\_バッファー\_WITH\_通知します。

プロパティの値 (データの操作) は、型の構造体[ **KSRTAUDIO\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_buffer)します。 ドライバーは、実際のバッファー サイズ、ベース アドレスは、割り当て済み循環バッファーのメモリ バリアのフラグと、この構造体を格納します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_RTAUDIO\_バッファー\_WITH\_通知プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。 次の表では、可能性のあるエラー状態コードの一部を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>バッファーの属性の組み合わせを指定して循環バッファーを割り当てることはできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td align="left"><p>メモリ バッファーを割り当てられません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_DEVICE_NOT_READY</p></td>
<td align="left"><p>デバイスができていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ベース アドレスは、循環バッファーの先頭にある仮想メモリ アドレスです。 クライアントは、このアドレスにバッファーに直接アクセスできます。 バッファーが仮想メモリ内で連続しています。 ドライバーは、バッファーが物理メモリ内で連続しているかどうかを決定します。

クライアントでは、ベース アドレスを設定するプロパティ記述子で**NULL**します。 ドライバーは、割り当てられたバッファーの仮想アドレスにプロパティ値のベース アドレスを設定します。

通常、オーディオ ハードウェアは、オーディオのバッファーが開始され、サンプルの境界の終了、または他の種類のハードウェアに依存する配置の制約を満たしている必要があります。 十分なメモリを使用できる場合、バッファーの実際のサイズは (増減) を最も近いサンプルまたは他のハードウェアに制約がある境界に丸められたもの、要求されたサイズにします。 それ以外の場合、実際のサイズでは、要求されたサイズより小さくすることができます。

場合、KSPROPERTY\_RTAUDIO\_バッファー\_WITH\_通知プロパティ要求が成功すると、プロパティの値型 KSRTAUDIO の構造体である\_バッファーのサイズとアドレスが含まれています、ドライバーが割り当てたバッファー。

このプロパティを介して割り当てられたバッファーを解放、暗証番号 (pin) を自動的に終了します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista 以降の Windows オペレーティング システムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSRTAUDIO\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_buffer)

[**KSRTAUDIO\_バッファー\_プロパティ\_WITH\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_buffer_property_with_notification)

[**KSPROPERTY\_RTAUDIO\_登録\_通知\_イベント**](ksproperty-rtaudio-register-notification-event.md)

 

 






