---
title: KSPROPERTY\_RTAUDIO\_バッファー
description: KSPROPERTY\_RTAUDIO\_バッファー プロパティは、ドライバーによって割り当てられた循環バッファーのオーディオ データを指定します。次の表では、このプロパティの機能をまとめたものです。
ms.assetid: e2c78849-1a34-446c-9f44-012f36ddafa5
keywords:
- KSPROPERTY_RTAUDIO_BUFFER オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_BUFFER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4aff71afda39ff3646c3277d6f29f23d970e96b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332686"
---
# <a name="kspropertyrtaudiobuffer"></a>KSPROPERTY\_RTAUDIO\_バッファー


KSPROPERTY\_RTAUDIO\_バッファー プロパティは、ドライバーによって割り当てられた循環バッファーのオーディオ データを指定します。

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
<td align="left"><p><a href="ksrtaudio-buffer-property.md" data-raw-source="[&lt;strong&gt;KSRTAUDIO_BUFFER_PROPERTY&lt;/strong&gt;](ksrtaudio-buffer-property.md)"><strong>KSRTAUDIO_BUFFER_PROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537493" data-raw-source="[&lt;strong&gt;KSRTAUDIO_BUFFER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537493)"><strong>KSRTAUDIO_BUFFER</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンス データ) から成る、KSRTAUDIO\_バッファー\_プロパティ構造を含む、 [ **KSPROPERTY** ](https://msdn.microsoft.com/library/windows/hardware/ff564262)の他のメンバーと構造体。 クライアントは、構造体に、要求されたバッファー サイズを書き込みます。 としてベース アドレスを指定する必要があります、クライアントは、特定のベース アドレスを使用する必要はない場合、 **NULL**します。

プロパティの値 (データの操作) は型 KSRTAUDIO の構造体\_バッファー。 ドライバーは、実際のバッファー サイズ、ベース アドレスは、割り当て済み循環バッファーのメモリ バリアのフラグと、この構造体を格納します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_RTAUDIO\_バッファー プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。 次の表では、可能性のあるエラー状態コードの一部を示します。

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
<td align="left"><p>デバイス準備ができていません</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ベース アドレスは、循環バッファーの先頭にある仮想メモリ アドレスです。 クライアントは、このアドレスにバッファーに直接アクセスできます。 バッファーが仮想メモリ内で連続しています。 物理メモリ内で連続してバッファーを作成するかどうかは、ドライバーに委ね意思決定します。

クライアントをプロパティ記述子のベース アドレスを設定する必要があります**NULL**します。 ドライバーは、割り当てられたバッファーの仮想アドレスにプロパティ値のベース アドレスを設定します。

通常、オーディオ ハードウェアでは、いずれかを開始し、サンプルの境界の終了または他の種類のハードウェアに依存する配置の制約を満たしているオーディオ バッファーが必要です。 十分なメモリを使用できる場合、バッファーの実際のサイズは (増減) を最も近いサンプルまたは他のハードウェアに制約がある境界に丸められたもの、要求されたサイズにします。 実際のサイズが少なくとも; 要求されたサイズである必要があります。それ以外の場合、オーディオ セッション API (WASAPI) オーディオ エンジンは、バッファーを使用しないし、ストリームの作成は失敗します。

場合、KSPROPERTY\_RTAUDIO\_バッファー プロパティの要求が成功すると、型 KSRTAUDIO の構造体であるプロパティ値\_バッファー、ドライバーによって割り当てられたバッファーのサイズとアドレスが含まれています。

このプロパティを介して割り当てられたバッファーを解放、暗証番号 (pin) を自動的に終了します。

呼び出す必要があるイベント通知を実行する場合に、 [ **KSPROPERTY\_RTAUDIO\_バッファー\_WITH\_通知**](ksproperty-rtaudio-buffer-with-notification.md) KSPROPERTYではなく\_RTAUDIO\_バッファー。

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
<td align="left"><p>Windows Vista 以降の Windows オペレーティング システムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSRTAUDIO\_バッファー**](https://msdn.microsoft.com/library/windows/hardware/ff537493)

[**KSRTAUDIO\_バッファー\_プロパティ**](ksrtaudio-buffer-property.md)

[**KSPROPERTY\_RTAUDIO\_BUFFER\_WITH\_NOTIFICATION**](ksproperty-rtaudio-buffer-with-notification.md)

 

 






