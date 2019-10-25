---
title: KSK プロパティ\_AUDIO\_3D\_インターフェイス
description: KSK プロパティ\_AUDIO\_3D\_インターフェイスプロパティは、サウンドバッファー内のデータを処理するために使用する3D アルゴリズムを指定します。
ms.assetid: 76c56e61-23ef-43ad-b66b-2412fd247b6e
keywords:
- KSPROPERTY_AUDIO_3D_INTERFACE オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_3D_INTERFACE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f40ff187306401a7357351063eff2de5b6377d1c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831127"
---
# <a name="ksproperty_audio_3d_interface"></a>KSK プロパティ\_AUDIO\_3D\_インターフェイス


KSK プロパティ\_AUDIO\_3D\_インターフェイスプロパティは、サウンドバッファー内のデータを処理するために使用する3D アルゴリズムを指定します。

## <span id="ddk_ksproperty_audio_3d_interface_ks"></span><span id="DDK_KSPROPERTY_AUDIO_3D_INTERFACE_KS"></span>


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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>GUID</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、3D アルゴリズムを指定する GUID です。 この値には、ヘッダーファイル Dsound の次の Guid のいずれかを指定できます。

-   DS3DALG\_既定値

-   DS3DALG\_\_仮想化なし

-   DS3DALG\_HRTF\_FULL

-   DS3DALG\_HRTF\_ライト

これらの Guid の詳細については、Microsoft Windows SDK のドキュメントの DSBUFFERDESC 構造体の**guid3dAlgorithm**メンバーの説明を参照してください。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_3D\_インターフェイスプロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

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

[**KSNODETYPE\_3D\_効果**](ksnodetype-3d-effects.md)

 

 






