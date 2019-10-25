---
title: KSK プロパティ\_AUDIO\_コーラス\_レベル
description: KSK プロパティ\_AUDIO\_コーラス\_LEVEL プロパティは、コーラスレベルを指定します。 これは、コーラスノード (KSNODETYPE\_コーラス) のプロパティです。
ms.assetid: 80541b2c-0fb3-4306-8ed2-e524b5a4c113
keywords:
- KSPROPERTY_AUDIO_CHORUS_LEVEL オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_CHORUS_LEVEL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45e489ea8cdce5f994827e4ae5d9fdf862eac3f5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831062"
---
# <a name="ksproperty_audio_chorus_level"></a>KSK プロパティ\_AUDIO\_コーラス\_レベル


KSK プロパティ\_AUDIO\_コーラス\_LEVEL プロパティは、コーラスレベルを指定します。 これは、コーラスノード ([**KSNODETYPE\_コーラス**](ksnodetype-chorus.md)) のプロパティです。

## <span id="ddk_ksproperty_audio_chorus_level_ks"></span><span id="DDK_KSPROPERTY_AUDIO_CHORUS_LEVEL_KS"></span>


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
<th align="left">[購入]</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[はい]</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は ULONG 型で、コーラスレベルを指定します。 コーラスレベルの値は、0 ~ 100\*(65536-1/65536)% の線形範囲に従います。

-   値0x00010000 は100% を表します。

-   値0xFFFFFFFF は 100\*(65536-1/65536) パーセントを表します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_コーラス\_LEVEL プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティは、コーラスエコーのボリュームレベルを取得および設定するために使用されます。

コーラスは、わずかな遅延で元のサウンドをエコーし、エコーの遅延をわずかに modulating することによって作成される音声ダブルの効果です。 詳細については、Microsoft Windows SDK のドキュメントの**Idirectsoundfxchorus**インターフェイスの説明を参照してください。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSNODETYPE\_コーラス**](ksnodetype-chorus.md)

[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

 

 






