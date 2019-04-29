---
title: KSPROPERTY\_RTAUDIO\_登録解除\_通知\_イベント
description: KSPROPERTY\_RTAUDIO\_登録解除\_通知\_イベント プロパティには、DMA 駆動のイベント通知からのユーザー モード イベントが登録解除します。次の表では、このプロパティの機能をまとめたものです。
ms.assetid: 76ed7dfe-465a-4fdf-97e6-7a65b8971aee
keywords:
- KSPROPERTY_RTAUDIO_UNREGISTER_NOTIFICATION_EVENT オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_UNREGISTER_NOTIFICATION_EVENT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: db873ce4b65d2b72d3fca6c4a0ef6444360c37d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332648"
---
# <a name="kspropertyrtaudiounregisternotificationevent"></a>KSPROPERTY\_RTAUDIO\_登録解除\_通知\_イベント


KSPROPERTY\_RTAUDIO\_登録解除\_通知\_イベント プロパティには、DMA 駆動のイベント通知からのユーザー モード イベントが登録解除します。

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
<td align="left"><p>〇</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537499" data-raw-source="[&lt;strong&gt;KSRTAUDIO_NOTIFICATION_EVENT_PROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537499)"><strong>KSRTAUDIO_NOTIFICATION_EVENT_PROPERTY</strong></a></p></td>
<td align="left"><p><strong>NULL</strong></p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンス データ) から成る、KSRTAUDIO\_通知\_イベント\_プロパティ構造を含む、 [ **KSPROPERTY** ](https://msdn.microsoft.com/library/windows/hardware/ff564262)構造体と共にユーザー モード イベントのハンドル。

このプロパティのプロパティの値 (データの操作) が**NULL**操作データが返されないためです。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_ RTAUDIO\_登録解除\_通知\_イベント プロパティの要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。 次の表では、可能性のあるエラー状態コードの一部を示します。

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
<td align="left"><p>STATUS_NOT_SUPPORTED</p></td>
<td align="left"><p>イベント通知はサポートされていません。</p></td>
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

このプロパティは、DMA 駆動のイベント通知からのユーザー モード イベントの登録を解除するに使用されます。

実行の状態に、暗証番号 (pin) を配置すると (KSSTATE\_実行) 循環バッファーのサイクルごとに 1 ~ 2 回登録されているイベントがシグナル状態に、通知によってカウント時に要求された[ **KSPROPERTY\_RTAUDIO\_バッファー\_WITH\_通知**](ksproperty-rtaudio-buffer-with-notification.md)が呼び出されました。 KSSTATE の詳細については\_を実行しを参照してください、[状態遷移](https://msdn.microsoft.com/library/windows/hardware/ff568227)トピック。

暗証番号 (pin) を停止すると、前の手順では、それを閉じるに登録されている各イベントする必要があります登録を解除する KSPROPERTY への呼び出しを使用して\_RTAUDIO\_登録解除\_通知\_イベント。

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


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

[**KSRTAUDIO\_通知\_イベント\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/ff537499)

[**KSPROPERTY\_RTAUDIO\_BUFFER\_WITH\_NOTIFICATION**](ksproperty-rtaudio-buffer-with-notification.md)

[**KSPROPERTY\_RTAUDIO\_登録\_通知\_イベント**](ksproperty-rtaudio-register-notification-event.md)

 

 






