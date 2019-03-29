---
title: KSPROPERTY\_RTAUDIO\_登録\_通知\_イベント
description: KSPROPERTY\_RTAUDIO\_登録\_通知\_イベント プロパティは、DMA 駆動のイベント通知のためのユーザー モード イベントを登録します。
ms.assetid: 8fd5883a-ff86-4d27-af44-a82511c9e8eb
keywords:
- KSPROPERTY_RTAUDIO_REGISTER_NOTIFICATION_EVENT オーディオ デバイス
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
ms.openlocfilehash: 47077b91cedff0931331e4430a147afad400e26d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574867"
---
# <a name="kspropertyrtaudioregisternotificationevent"></a>KSPROPERTY\_RTAUDIO\_登録\_通知\_イベント


KSPROPERTY\_RTAUDIO\_登録\_通知\_イベント プロパティは、DMA 駆動のイベント通知のためのユーザー モード イベントを登録します。 正常に呼び出した後のイベントを登録する必要があります[ **KSPROPERTY\_RTAUDIO\_バッファー\_WITH\_通知**](ksproperty-rtaudio-buffer-with-notification.md)します。

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
<th align="left">Set</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>はい</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537499" data-raw-source="[&lt;strong&gt;KSRTAUDIO_NOTIFICATION_EVENT_PROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537499)"><strong>KSRTAUDIO_NOTIFICATION_EVENT_PROPERTY</strong></a></p></td>
<td align="left"><p><strong>NULL</strong></p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンス データ) から成る、KSRTAUDIO\_通知\_イベント\_プロパティ構造を含む、 [ **KSPROPERTY** ](https://msdn.microsoft.com/library/windows/hardware/ff564262)構造体と共にユーザー モード イベントのハンドル。

このプロパティのプロパティの値 (データの操作) が**NULL**操作データが返されないためです。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_ RTAUDIO\_登録\_通知\_イベント プロパティの要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。 次の表では、可能性のあるエラー状態コードの一部を示します。

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

 

<a name="remarks"></a>コメント
-------

このプロパティは、DMA 駆動のイベント通知のユーザー モード イベントの登録に使用されます。

暗証番号 (pin) を配置すると、*実行*状態 (KSSTATE\_実行) 循環バッファーのサイクルごとに 1 ~ 2 回登録されているイベントがシグナル状態に、通知によってカウント時に要求された KSPROPERTY\_RTAUDIO\_バッファー\_WITH\_通知が呼び出されました。 KSSTATERUN の詳細については、次を参照してください。、[状態遷移](https://msdn.microsoft.com/library/windows/hardware/ff568227)トピック。

Pin を停止して、時間が閉じるときに、以前登録された各イベントの呼び出しに登録が解除後[ **KSPROPERTY\_RTAUDIO\_登録解除\_通知\_イベント**](ksproperty-rtaudio-unregister-notification-event.md).

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

[**KSPROPERTY\_RTAUDIO\_BUFFER\_WITH\_NOTIFICATION**](ksproperty-rtaudio-buffer-with-notification.md)

[**KSPROPERTY\_RTAUDIO\_登録解除\_通知\_イベント**](ksproperty-rtaudio-unregister-notification-event.md)

[状態遷移](https://msdn.microsoft.com/library/windows/hardware/ff568227)

 

 






