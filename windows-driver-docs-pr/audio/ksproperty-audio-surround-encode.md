---
title: KSK プロパティ\_AUDIO\_サラウンド\_エンコード
description: KSK プロパティ\_AUDIO\_サラウンド\_ENCODE プロパティは、フィルターのサラウンドエンコーダーが有効か無効かを指定します。 サラウンドエンコーダーノード (KSNODETYPE\_PROLOGIC\_ENCODER) は、Dolby サラウンド Pro Logic encoding を実行します。
ms.assetid: 249ee13f-a986-4cb1-906f-55062274df45
keywords:
- KSPROPERTY_AUDIO_SURROUND_ENCODE オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_SURROUND_ENCODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfe0420cf6e77e541b8f4fa770b6b2a9b7485829
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832911"
---
# <a name="ksproperty_audio_surround_encode"></a>KSK プロパティ\_AUDIO\_サラウンド\_エンコード


KSK プロパティ\_AUDIO\_サラウンド\_ENCODE プロパティは、フィルターのサラウンドエンコーダーが有効か無効かを指定します。 サラウンドエンコーダーノード ([**KSNODETYPE\_prologic\_encoder**](ksnodetype-prologic-encoder.md)) は、Dolby サラウンド Pro logic encoding を実行します。

## <span id="ddk_ksproperty_audio_surround_encode_ks"></span><span id="DDK_KSPROPERTY_AUDIO_SURROUND_ENCODE_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>型</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) はブール型で、サラウンドエンコーダーノードが有効かどうかを示します。 値が**TRUE**の場合は、サラウンドエンコーダーノードが有効であることを示します。 **FALSE**は、無効であることを示します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_サラウンド\_ENCODE プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

Microsoft Windows XP 以降では、 [KMixer システムドライバー](https://docs.microsoft.com/windows-hardware/drivers/audio/kernel-mode-wdm-audio-components#kmixer-system-driver)は、\_AUDIO プロパティ\_サラウンド\_ENCODE プロパティをサポートしています。

この設定を有効にした場合、サラウンドエンコーダーノードは、4チャネルの入力ストリーム (左、右、中央、および背面のスピーカーのチャネルを含む) を、サラウンドエンコードされたステレオ出力ストリームにエンコードします。 この出力ストリームは、たとえば、 [**KSNODETYPE\_PROLOGIC\_デコーダー**](ksnodetype-prologic-decoder.md)ノードによってデコードできます。 また、オーディオデバイスのアナログステレオ出力を使用して再生することもできます。これは、左、右、中央、およびバックスピーカーに直接ドライブを配置する外部のサラウンドデコーダーに接続できます。

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


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_PROLOGIC\_エンコーダー**](ksnodetype-prologic-encoder.md)

[**KSNODETYPE\_PROLOGIC\_デコーダー**](ksnodetype-prologic-decoder.md)

 

 






