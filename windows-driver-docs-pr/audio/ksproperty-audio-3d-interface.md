---
title: KSPROPERTY\_オーディオ\_3D\_インターフェイス
description: KSPROPERTY\_オーディオ\_3D\_インターフェイスのプロパティをサウンド バッファー内のデータの処理に使用する 3D アルゴリズムを指定します。
ms.assetid: 76c56e61-23ef-43ad-b66b-2412fd247b6e
keywords:
- KSPROPERTY_AUDIO_3D_INTERFACE オーディオ デバイス
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
ms.openlocfilehash: d3da288b5783ea2e4b70c3f1111300e056111387
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358959"
---
# <a name="kspropertyaudio3dinterface"></a>KSPROPERTY\_オーディオ\_3D\_インターフェイス


KSPROPERTY\_オーディオ\_3D\_インターフェイスのプロパティをサウンド バッファー内のデータの処理に使用する 3D アルゴリズムを指定します。

## <span id="ddk_ksproperty_audio_3d_interface_ks"></span><span id="DDK_KSPROPERTY_AUDIO_3D_INTERFACE_KS"></span>


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
<td align="left"><p>〇</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>GUID</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、3 D のアルゴリズムを指定する GUID です。 この値は、ヘッダー ファイル Dsound.h から次の Guid のいずれかを指定できます。

-   DS3DALG\_既定

-   DS3DALG\_いいえ\_仮想化

-   DS3DALG\_HRTF\_FULL

-   DS3DALG\_HRTF\_ライト

これらの Guid の詳細については、の説明を参照して、 **guid3dAlgorithm** Microsoft Windows SDK ドキュメントで DSBUFFERDESC 構造体のメンバー。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_3D\_インターフェイス プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

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
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_3D\_効果**](ksnodetype-3d-effects.md)

 

 






