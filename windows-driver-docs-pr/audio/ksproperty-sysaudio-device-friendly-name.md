---
title: KSPROPERTY\_SYSAUDIO\_デバイス\_フレンドリ\_名
description: KSPROPERTY\_SYSAUDIO\_デバイス\_フレンドリ\_NAME プロパティは、仮想のオーディオ デバイスのフレンドリ名を含む Unicode 文字列を取得します。
ms.assetid: 14e23bb3-f0af-486f-8e34-fe27b2db2849
keywords:
- KSPROPERTY_SYSAUDIO_DEVICE_FRIENDLY_NAME オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_DEVICE_FRIENDLY_NAME
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f939950cbfdb9ea471847276ee83bf73da08d60f
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391612"
---
# <a name="kspropertysysaudiodevicefriendlyname"></a>KSPROPERTY\_SYSAUDIO\_デバイス\_フレンドリ\_名


KSPROPERTY\_SYSAUDIO\_デバイス\_フレンドリ\_NAME プロパティは、仮想のオーディオ デバイスのフレンドリ名を含む Unicode 文字列を取得します。

## <span id="ddk_ksproperty_sysaudio_device_friendly_name_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_DEVICE_FRIENDLY_NAME_KS"></span>


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
<td align="left"><p>X</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a>+ ULONG</p></td>
<td align="left"><p>LPWSTR</p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンス データ) は、仮想のオーディオ デバイスを識別するデバイス ID を含む ULONG 変数を続けて KSPROPERTY 構造で構成されます。 SysAudio 列挙する場合*n*仮想のオーディオ デバイス (を参照してください[ **KSPROPERTY\_SYSAUDIO\_デバイス\_カウント**](ksproperty-sysaudio-device-count.md)) し、有効なデバイス Id の範囲は 0 ~ *n*-1。 デバイス ID の値は-1 を指定できますも、現在のデバイスを示すために使用すると、これは最後の仮想のオーディオ デバイスによって開かれます、 [ **KSPROPERTY\_SYSAUDIO\_デバイス\_インスタンス**](ksproperty-sysaudio-device-instance.md)または[ **KSPROPERTY\_SYSAUDIO\_インスタンス\_情報**](ksproperty-sysaudio-instance-info.md)要求のプロパティを設定します。

プロパティの値 (データの操作) では、デバイスのフレンドリ名を含む Unicode 文字の null で終わる文字列へのポインターです。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_SYSAUDIO\_デバイス\_フレンドリ\_プロパティの名前の要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSPROPERTY\_SYSAUDIO\_デバイス\_数**](ksproperty-sysaudio-device-count.md)

[**KSPROPERTY\_SYSAUDIO\_デバイス\_インスタンス**](ksproperty-sysaudio-device-instance.md)

[**KSPROPERTY\_SYSAUDIO\_インスタンス\_情報**](ksproperty-sysaudio-instance-info.md)

 

 






