---
title: KSPROPERTY\_RTAUDIO\_PACKETCOUNT
description: KSPROPERTY\_RTAUDIO\_PACKETCOUNT はハードウェアに WaveRT バッファーから完全に転送パケットの数を (1 から始まる) を返します。
ms.assetid: 904896DE-D135-43B6-AA1F-F49D0748952D
keywords:
- KSPROPERTY_RTAUDIO_PACKETCOUNT オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_PACKETCOUNT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 06/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: c726f41ff11389ee6ef7669809f16a52c9783929
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391646"
---
# <a name="kspropertyrtaudiopacketcount"></a>KSPROPERTY\_RTAUDIO\_PACKETCOUNT


KSPROPERTY\_RTAUDIO\_PACKETCOUNT はハードウェアに WaveRT バッファーから完全に転送パケットの数を (1 から始まる) を返します。

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
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/ulong" data-raw-source="[&lt;strong&gt;ULONG&lt;/strong&gt;](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/ulong)"><strong>ULONG</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンス データ) が、 [ **KSPROPERTY** ](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))構造体。 要求を送信する前に、クライアントは、ハードウェアに WaveRT バッファーから完全に転送パケットの数を (1 から始まる) の構造体を読み込みます。

プロパティの値は、ULONG 型の変数です。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_RTAUDIO\_PACKETCOUNT プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

OS は、パケットの数から WaveRT バッファーに書き込みますが、パケットのストリームの位置を派生できます。 OS は、WaveRT バッファーに書き込むには、次のパケットの WaveRT バッファーの位置を派生させることもできます。 WaveRT ドライバーでは、ドライバーは、WaveRT バッファーの各パケットからデータを転送するように、1 つの通知イベントを通知します。 そのためイベントだけでは、WaveRT バッファー内のパケットが転送されているを示すことはできません。 通常の運用でこれに問題がないが、アンダー フローの場合の修正がより簡単に、OS が次に書き込む、パケットを決定するパケット数を照会することによって実現します。

返された PacketCount では、ハードウェアに WaveRT バッファーから完全に転送パケットの数を (1 から始まる) を示します。 ここから、OS は現在転送中パケットの 0 から始まる数を決定し、そのパケット事前書き込まれることを確認できます。 たとえば、パケットの数が 5 の場合は、5 つのパケットが完全に転送されます。 0 ~ 4 のパケットが完全に転送します。 パケット 5 が進行中はそのため、OS が 6 のパケットを書き込む必要があります。 WaveRT バッファーの通知の数が 2 の場合は、し、パケット 6 になる WaveRT バッファー内のオフセット 0 (6 モジュロ 2 がパケット サイズが 0 0、および 0 の時間であるため)。

OS は、いつでもこのプロパティを取得する可能性があります。 ただし、一般にこのプロパティは定期的にまたは取得ドライバーには、データ フローのエラーが返された後に (ステータス\_データ\_遅れて\_エラー、状態\_データ\_オーバーラン) には SetWritePacket() からドライバーを使用した再同期します。

ドライバーがパケットの数を 0 にリセット ストリームが KSSTATE で\_を停止します。

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


[KSPROPSETID\_RTAudio](kspropsetid-rtaudio.md)

 

 






