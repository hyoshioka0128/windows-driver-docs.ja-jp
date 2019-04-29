---
title: KSPROPERTY\_RTAUDIO\_GETREADPACKET
description: KSPROPERTY\_RTAUDIO\_GETREADPACKET がキャプチャされたオーディオ パケットに関する情報を返します。
ms.assetid: BA52CDCE-0178-4C90-A82C-15800DD3709E
keywords:
- KSPROPERTY_RTAUDIO_GETREADPACKET オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_GETREADPACKET
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 12/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0894f0b083b69895457cdf4ee36b384c8d880202
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332677"
---
# <a name="kspropertyrtaudiogetreadpacket"></a>KSPROPERTY\_RTAUDIO\_GETREADPACKET


KSPROPERTY\_RTAUDIO\_GETREADPACKET がキャプチャされたオーディオ パケットに関する情報を返します。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

 
|取得|設定|対象|プロパティ記述子の型|プロパティ値の型|
|--- |--- |--- |--- |--- |
|〇|いいえ|Pin|[KSPROPERTY](https://msdn.microsoft.com/library/windows/hardware/ff564262)|[KSRTAUDIO_GETREADPACKET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_getreadpacket_info)|


プロパティ記述子 (インスタンス データ) が、 [ **KSPROPERTY** ](https://msdn.microsoft.com/library/windows/hardware/ff564262)構造体。 要求を送信する前に、クライアントは、パケットの数、パケットの長さ、およびその他の情報を示す値を含む構造体を読み込みます。

プロパティの値は型の変数[ **KSRTAUDIO\_GETREADPACKET\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_getreadpacket_info)します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_RTAUDIO\_GETREADPACKET プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

ステータス\_デバイス\_いない\_準備 - ドライバーは、新しいデータが使用できない場合にこのエラーを返します。

<a name="remarks"></a>注釈
-------

読み取りが WaveRT バッファーからのオーディオ データをキャプチャする前に、OS は、使用できるデータに関する情報を取得するには、このルーチンを呼び出します。

パケット番号は、ストリーム内のパケットを識別します。 ストリームが KSSTATE の場合 0 にリセットされます\_を停止します。 数は、キャプチャされた各バッファーで進めます。 パケット番号からは、OS は WaveRT バッファー内のパケットの場所を派生させることができ、ストリームの先頭にパケット相対のストリームの位置を派生させることもできます。

パケット サイズは、WaveRT バッファー サイズで割った値に渡される NotificationCount [ **KSPROPERTY\_RTAUDIO\_バッファー\_WITH\_通知**](ksproperty-rtaudio-buffer-with-notification.md). OS は、いつでもこのルーチンを呼び出すことができます。 通常の運用では、OS は、ドライバーは、バッファーの通知イベントを設定後、または前回の呼び出しが MoreData に対して true を返しますにこのルーチンを呼び出します。 オペレーティング システムがこのルーチンを呼び出すと、ドライバーは、OS の以前のすべてのパケットの読み取りが完了したことを担うことができます。 ハードウェアに十分なデータがキャプチャした場合、ドライバー可能性がありますすぐに次の完全なパケット WaveRT バッファーへのバーストし、もう一度バッファー イベントを設定します。 (OS がデータを迅速に読み取るいない) 場合、キャプチャ オーバーフローの場合、オーディオ ドライバーの削除またはオーディオ データの一部を上書きする可能性があります。 オーディオ ドライバーを削除または最も古いデータをまず上書き、オーディオ ドライバーの場合でも、OS にデータを読み取ることがないことができますが、その内部のパケット カウンターを進みが継続します。

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
<td align="left"><p>Windows 10 以降の Windows オペレーティング システムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSPROPERTY\_RTAUDIO\_SETWRITEPACKET**](ksproperty-rtaudio-setwritepacket.md)

[UsePositionLock](usepositionlock.md)

 

 






