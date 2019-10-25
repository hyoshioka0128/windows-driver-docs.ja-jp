---
title: KSK プロパティ\_RTAUDIO\_GETREADPACKET
description: KSK プロパティ\_RTAUDIO\_GETREADPACKET は、キャプチャされたオーディオパケットに関する情報を返します。
ms.assetid: BA52CDCE-0178-4C90-A82C-15800DD3709E
keywords:
- KSPROPERTY_RTAUDIO_GETREADPACKET オーディオデバイス
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
ms.openlocfilehash: ed12673544f73943fc14ae1b77a3b466cea74498
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830684"
---
# <a name="ksproperty_rtaudio_getreadpacket"></a>KSK プロパティ\_RTAUDIO\_GETREADPACKET


KSK プロパティ\_RTAUDIO\_GETREADPACKET は、キャプチャされたオーディオパケットに関する情報を返します。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

 
|[購入]|設定|対象|プロパティ記述子の型|プロパティ値の型|
|--- |--- |--- |--- |--- |
|[はい]|必須ではない|Pin|[KSPROPERTY](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))|[KSRTAUDIO_GETREADPACKET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_getreadpacket_info)|


プロパティ記述子 (インスタンスデータ) は、 [**Ksk プロパティ**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))構造体です。 クライアントは、要求を送信する前に、パケット番号、パケット長、およびその他の情報を示す値を使用して構造体を読み込みます。

プロパティ値は、 [**Ksrtaudio\_GETREADPACKET\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_getreadpacket_info)型の変数です。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

RTAUDIO\_GETREADPACKET プロパティ要求\_KSK プロパティは、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

状態\_デバイス\_準備ができていませ\_ん-新しいデータが利用できない場合、ドライバーはこのエラーを返します。

<a name="remarks"></a>注釈
-------

WaveRT バッファーからキャプチャされたオーディオデータを読み取る前に、OS はこのルーチンを呼び出して、使用可能なデータに関する情報を取得します。

パケット番号は、ストリーム内のパケットを識別します。 ストリームが KSSTATE\_STOP の場合、この値は0にリセットされます。 この数値は、キャプチャされたバッファーごとに進められます。 パケット番号からは、OS は WaveRT バッファー内のパケットの場所を取得できます。また、ストリームの開始を基準としてパケットのストリームの位置を派生させることもできます。

パケットサイズは、 [ **\_通知を使用して、Ksk プロパティ\_RTAUDIO\_\_buffer**](ksproperty-rtaudio-buffer-with-notification.md)に渡される notificationcount で割った、walastbuffer のサイズです。 OS は、いつでもこのルーチンを呼び出すことができます。 通常の操作では、ドライバーによってバッファー通知イベントが設定された後、または以前の呼び出しがより詳細なデータに対して true を返すと、OS はこのルーチンを呼び出します。 OS がこのルーチンを呼び出すと、ドライバーは OS が以前のすべてのパケットの読み取りを終了したと見なします。 ハードウェアに十分なデータがキャプチャされている場合、ドライバーは次の完全なパケットをすぐに WaveRT バッファーにバーストし、バッファーイベントを再度設定します。 キャプチャオーバーフローの場合 (OS がデータを十分に読み取ることができない場合)、オーディオドライバーは一部のオーディオデータを破棄または上書きする可能性があります。 オーディオドライバーは、古いデータを最初に削除するか上書きします。そのため、データが読み取られていない場合でも、オーディオドライバーは内部パケットカウンターをさらに進めることができます。

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
<td align="left"><p>Windows 10 以降の Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSK プロパティ\_RTAUDIO\_SETWRITEPACKET**](ksproperty-rtaudio-setwritepacket.md)

[UsePositionLock](usepositionlock.md)

 

 






