---
title: KSK プロパティ\_RTAUDIO\_登録\_通知\_イベント
description: KSK プロパティ\_RTAUDIO\_REGISTER\_NOTIFICATION\_イベントプロパティによって、DMA ドリブンイベント通知のユーザーモードイベントが登録されます。
ms.assetid: 8fd5883a-ff86-4d27-af44-a82511c9e8eb
keywords:
- KSPROPERTY_RTAUDIO_REGISTER_NOTIFICATION_EVENT オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_REGISTER_NOTIFICATION_EVENT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4368b035acb6fa01c5d63dda2a404e91574cbd5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830595"
---
# <a name="ksproperty_rtaudio_register_notification_event"></a>KSK プロパティ\_RTAUDIO\_登録\_通知\_イベント


KSK プロパティ\_RTAUDIO\_REGISTER\_NOTIFICATION\_イベントプロパティによって、DMA ドリブンイベント通知のユーザーモードイベントが登録されます。 [ **\_通知を使用して Ksk プロパティ\_RTAUDIO\_BUFFER\_を**](ksproperty-rtaudio-buffer-with-notification.md)正常に呼び出した後、イベントを登録する必要があります。

次の表は、このプロパティの機能をまとめたものです。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">[購入]</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[はい]</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_notification_event_property" data-raw-source="[&lt;strong&gt;KSRTAUDIO_NOTIFICATION_EVENT_PROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_notification_event_property)"><strong>KSRTAUDIO_NOTIFICATION_EVENT_PROPERTY</strong></a></p></td>
<td align="left"><p><strong>空白</strong></p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンスデータ) は、ユーザーモードのイベントハンドルと共に[**Ksk プロパティ**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))構造体を含む KSRTAUDIO\_NOTIFICATION\_イベント\_プロパティ構造で構成されます。

操作データが返されないため、このプロパティのプロパティ値 (操作データ) は**NULL**になります。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

RTAUDIO\_REGISTER\_NOTIFICATION\_イベントプロパティ要求\_ KSK プロパティは、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。 次の表に、発生する可能性のあるエラー状態コードを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態コード</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_NOT_SUPPORTED</p></td>
<td align="left"><p>イベント通知はサポートされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td align="left"><p>バッファーのメモリを割り当てることができません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_DEVICE_NOT_READY</p></td>
<td align="left"><p>デバイスの準備ができていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、DMA ドリブンイベント通知のユーザーモードイベントを登録するために使用されます。

Pin が*実行*状態になったとき (ksk 状態\_実行)、ksk プロパティ\_rtaudio\_buffer に要求された通知の数に応じて、循環オーディオバッファーのサイクルごとに1回または2回、登録されたイベントが通知され @no__\_通知と共に t_4_ が呼び出されました。 KSK の詳細については、「[状態遷移](https://docs.microsoft.com/windows-hardware/drivers/stream/state-transitions)」トピックを参照してください。

Pin の停止後、閉じた時刻より前に、登録されている各イベントは、Ksk プロパティ\_RTAUDIO の呼び出しによって登録解除され、 [ **\_NOTIFICATION\_イベントの登録を解除\_** ](ksproperty-rtaudio-unregister-notification-event.md)ます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista 以降の Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[ **\_通知での RTAUDIO\_バッファー\_\_KSK プロパティ**](ksproperty-rtaudio-buffer-with-notification.md)

[**KSK プロパティ\_RTAUDIO\_\_通知\_イベントの登録を解除します**](ksproperty-rtaudio-unregister-notification-event.md)

[状態遷移](https://docs.microsoft.com/windows-hardware/drivers/stream/state-transitions)

 

 






