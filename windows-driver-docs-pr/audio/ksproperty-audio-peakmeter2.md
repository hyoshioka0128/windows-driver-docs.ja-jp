---
title: KSK プロパティ\_AUDIO\_PEAKMETER2
description: Windows 8 では、最後\_に\_peakmeter ノードがリセットされてから peakmeter ノード (KSNODETYPE\_peakmeter) で発生した最大オーディオ信号レベルを報告する ksk property AUDIO PEAKMETER2 プロパティが導入されています。
ms.assetid: 0A59A482-476D-412C-8D15-D821357C355B
keywords:
- KSPROPERTY_AUDIO_PEAKMETER2 オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_PEAKMETER2
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 04/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: bf6041ef504e1bf7c074eec21bd47ab8da61da6a
ms.sourcegitcommit: 8f27122409dea11ef0635afbbe5788a648066a1a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81772730"
---
# <a name="ksproperty_audio_peakmeter2"></a>KSK プロパティ\_AUDIO\_PEAKMETER2

Windows 8 では、最後\_に\_peakmeter ノードがリセットされてから peakmeter ノード (KSNODETYPE\_peakmeter) で発生した最大オーディオ信号レベルを報告する ksk property AUDIO PEAKMETER2 プロパティが導入されました。

## <span id="ddk_ksproperty_audio_peakmeter2_ks"></span><span id="DDK_KSPROPERTY_AUDIO_PEAKMETER2_KS"></span>


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

KSK PROPERTY\_AUDIO\_PEAKMETER2 property 要求は、正常\_に完了したことを示すステータス成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。 次の表は、考えられるエラー状態コードを示しています。

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

KSK プロパティ\_audio\_PEAKMETER2 プロパティは、 [**ksk プロパティ\_オーディオ\_peakmeter**](ksproperty-audio-peakmeter.md)プロパティとほぼ同じです。 KSK プロパティ\_AUDIO\_PEAKMETER2 プロパティは、pin トポロジのハードウェア使用状況を改善するために、Windows 8 で導入されました。 従来の KSK プロパティ\_オーディオ\_peakmeter プロパティは非推奨とされ、使用できなくなりました。

SignedMinimum は (0x8000 では\_なく) long MIN に設定する必要があります。また、signedminimum は、(ではなく) long\_MAX に設定する必要があります。 また、ピークメーターの値はこのスケールに対して相対的で、スケールは振幅が線形であることに注意してください。

たとえば、負の値と正の値を持つ波形が-1 と + 1 でそれぞれ (-1 から + 1 のスケールにある)、ピークメーターの値が長い\_場合は、特定の時間枠の最大の波形値が正確に報告されます。 反対に、ピーク時のメーターの値をゼロ (0) にして、すべての波形の値がゼロである無音状態を報告する必要があります。 ただし、ピーク値*がゼロ (* 0) と長い\_最大値の波形の場合、報告される波形値は元の値から直線的に減少します。

したがって、-0.5 と + 0.5 (-1 から + 1 のスケール) の間で発生する波形の場合は、ピークメーターの値を LONG\_MAX/2 に設定する必要があります。

KS オーディオフィルターは、このプロパティ要求を同期的に処理します。 要求が成功すると、peakmeter がリセットされ、累積ピーク値がゼロに初期化されます。 要求が成功しなかった場合、peakmeter は変更されません。

システムは、IRQL の\_パッシブ\_\_\_レベルで、ksproperty AUDIO\_PEAKMETER2 プロパティに対する IOCTL KS プロパティ要求を送信します。

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

[**KSK プロパティ\_オーディオ\_PEAKMETER**](ksproperty-audio-peakmeter.md)
