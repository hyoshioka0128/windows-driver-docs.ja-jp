---
title: KSPROPERTY\_RTAUDIO\_SETWRITEPACKET
description: KSPROPERTY\_RTAUDIO\_SETWRITEPACKET は、OS に WaveRT バッファーに有効なデータによって書き込まれたことをドライバーに通知します。
ms.assetid: 2827D6BC-B669-4AAC-967C-99B068DCC29B
keywords:
- KSPROPERTY_RTAUDIO_SETWRITEPACKET Audio Devices
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_SETWRITEPACKET
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 12/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7e1692f2ceb2d01781eeb12f85511c5c89eb75a6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354379"
---
# <a name="kspropertyrtaudiosetwritepacket"></a>KSPROPERTY\_RTAUDIO\_SETWRITEPACKET


KSPROPERTY\_RTAUDIO\_SETWRITEPACKET は、OS に WaveRT バッファーに有効なデータによって書き込まれたことをドライバーに通知します。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

|取得|設定|対象|プロパティ記述子の型|プロパティ値の型|
|--- |--- |--- |--- |--- |
|X|〇|Pin|[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))|[KSRTAUDIO_SETWRITEPACKET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_setwritepacket_info)|


プロパティ記述子 (インスタンス データ) が、 [ **KSPROPERTY** ](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))構造体。 要求を送信する前に、クライアントは、パケットの数、パケットの長さ、およびその他の情報を含む値を持つ構造体を読み込みます。

プロパティの値は型の構造体[ **KSRTAUDIO\_SETWRITEPACKET\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_setwritepacket_info)します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_RTAUDIO\_SETWRITEPACKET プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

この KSPROPERTY がサポートされている場合、ドライバーがハードウェアの転送を最適化するために、提供された情報を使用できます必要に応じて。 など、OS が別のパケットのドライバーを通知するためにもう一度このルーチンを呼び出さない場合、指定されたパケットの最後の転送を停止するには、DMA 転送、またはプログラム ハードウェア ドライバーを最適化できます。 これは、アンダー フロー、循環バッファーを繰り返しするのではなく、たとえば可聴のギャップの概要の音の効果を軽減できます。 ただし、ドライバーは、その内部のパケット カウンターを増やし、リアルタイムの標準料金での通知イベントを通知する義務がまだは。

OS を指定した場合を除く、 *KSSTREAM\_ヘッダー\_OPTIONSF\_ENDOFSTREAM*フラグ、パケット サイズは、WaveRT バッファー サイズで割った値に渡される NotificationCount [**KSPROPERTY\_RTAUDIO\_バッファー\_WITH\_通知**](ksproperty-rtaudio-buffer-with-notification.md)します。

ハードウェアの機能に応じて場合、 *KSSTREAM\_ヘッダー\_OPTIONSF\_ENDOFSTREAM*フラグを指定すると、ドライバーには、サイレント状態の塗りつぶし、EOS に続く WaveRT バッファーの一部が可能性があります場合は、ハードウェアのパケットは、EOS 位置を超えるデータを転送します。

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


[**KSPROPERTY\_RTAUDIO\_GETREADPACKET**](ksproperty-rtaudio-getreadpacket.md)

[UsePositionLock](usepositionlock.md)

 

 






