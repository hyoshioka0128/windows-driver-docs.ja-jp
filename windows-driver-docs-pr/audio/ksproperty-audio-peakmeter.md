---
title: KSK プロパティ\_オーディオ\_PEAKMETER
description: KSK プロパティ\_オーディオ\_peakmeter プロパティは、peakmeter ノードが最後にリセットされたときから peakmeter ノード (KSNODETYPE\_peakmeter) で発生した最大オーディオ信号レベルを取得します。
ms.assetid: c8c2c9ed-61ea-4bbe-b376-c956f051416e
keywords:
- KSPROPERTY_AUDIO_PEAKMETER オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_PEAKMETER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 04/17/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2a041d558b9e14007ee660beeb2016a3ddf5362b
ms.sourcegitcommit: 8f27122409dea11ef0635afbbe5788a648066a1a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81772736"
---
# <a name="ksproperty_audio_peakmeter"></a>KSK プロパティ\_オーディオ\_PEAKMETER

KSK プロパティ\_オーディオ\_peakmeter プロパティは、peakmeter ノードが最後にリセットされたときから peakmeter ノード ([**KSNODETYPE\_peakmeter**](ksnodetype-peakmeter.md)) で発生した最大オーディオ信号レベルを取得します。

>>
> [!IMPORTANT]
> KSK プロパティ\_オーディオ\_peakmeter プロパティは償却されているため、使用しないでください。 代わりに、 [**\_ksproperty\_AUDIO PEAKMETER2**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-peakmeter2)を使用してください。  


## <span id="ddk_ksproperty_audio_peakmeter_ks"></span><span id="DDK_KSPROPERTY_AUDIO_PEAKMETER_KS"></span>


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
<th align="left">取得</th>
<th align="left">オン</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>はい</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>フィルターまたは Pin インスタンスを使用したノード</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></td>
<td align="left"><p>LONG</p></td>
</tr>
</tbody>
</table>

プロパティ値 (操作データ) は LONG 型で、ノードのピークサンプル値を指定します。 ピーク値が負の値の場合は、その絶対値が使用されます。


### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_オーディオ\_peakmeter プロパティ要求は、正常\_に完了したことを示すステータス成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。 次の表は、考えられるエラー状態コードを示しています。

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
<td align="left"><p>STATUS_NOT_IMPLEMENTED</p></td>
<td align="left"><p>KS フィルターは peakmeter の現在の値を返すことができません。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>解説
-------

KS オーディオフィルターは、このプロパティ要求を同期的に処理します。 要求が成功すると、peakmeter がリセットされ、累積ピーク値がゼロに初期化されます。 要求が成功しなかった場合、peakmeter は変更されません。

システムは、IRQL の\_パッシブ\_\_\_レベルで、KSPROPERTY オーディオ\_peakmeter プロパティの IOCTL KS プロパティ要求を送信します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目

[**KSNODEPROPERTY\_オーディオ\_チャネル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)

[**KSNODETYPE\_PEAKMETER**](ksnodetype-peakmeter.md)

[**KSK プロパティ\_AUDIO\_PEAKMETER2**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-peakmeter2)
