---
title: KSK プロパティ\_AEC\_\_塗りつぶし\_有効にする
description: KSK プロパティ\_AEC\_ノイズ\_FILL\_ENABLE プロパティを使用して、バックグラウンドノイズの塗りつぶしを有効または無効にします。 これは、AEC ノードのオプションのプロパティです (KSNODETYPE\_音響\_ECHO\_CANCEL)。
ms.assetid: 7c0ed4ba-d25e-42b5-b213-fbe74040a453
keywords:
- KSPROPERTY_AEC_NOISE_FILL_ENABLE オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AEC_NOISE_FILL_ENABLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5123a84d26766142f9dbb90afe5b602921fe08c1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831136"
---
# <a name="ksproperty_aec_noise_fill_enable"></a>KSK プロパティ\_AEC\_\_塗りつぶし\_有効にする


KSK プロパティ\_AEC\_ノイズ\_FILL\_ENABLE プロパティを使用して、バックグラウンドノイズの塗りつぶしを有効または無効にします。 これは、AEC ノードのオプションのプロパティです ([**KSNODETYPE\_音響\_ECHO\_CANCEL**](ksnodetype-acoustic-echo-cancel.md))。

## <span id="ddk_ksproperty_aec_noise_fill_enable_ks"></span><span id="DDK_KSPROPERTY_AEC_NOISE_FILL_ENABLE_KS"></span>


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
<td align="left"><p>型</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) の型は BOOL です。 この値を**TRUE**に設定すると、バックグラウンドノイズの塗りつぶしが有効になります。 有効にすると、ノードはバックグラウンドノイズをキャプチャストリームに挿入します。 この値を**FALSE**に設定すると、バックグラウンドノイズの塗りつぶしが無効になります。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AEC の\_ノイズ\_\_FILL は、プロパティ要求が正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

AEC ノードは、完全なエコーのキャンセル後にキャプチャされたデータストリームがゼロに設定されたときに不自然な無音状態が発生しないようにするために、バックグラウンドの快適ノイズをキャプチャストリームに挿入します。

AEC ノードを含むフィルターが作成されるか、ノードがリセットされると、バックグラウンドノイズの入力は既定で無効になります。

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

[**KSNODETYPE\_音響\_ECHO\_キャンセル**](ksnodetype-acoustic-echo-cancel.md)

 

 






