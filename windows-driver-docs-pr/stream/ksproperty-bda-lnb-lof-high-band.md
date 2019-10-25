---
title: KSK プロパティ\_BDA\_LNB\_LOF\_高\_帯域
description: クライアントは、KSK プロパティ\_BDA\_LNB\_LOF\_を使用して、高\_帯域の周波数を変化させるために低騒音ブロック (LNB) デバイスによって使用されるローカルオシレーター周波数 (LOF) について RF チューナーノードに通知します。シグナル.
ms.assetid: 77ee5ad8-330e-47a6-8fdb-6a4f9b3eef1d
keywords:
- KSPROPERTY_BDA_LNB_LOF_HIGH_BAND ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_LNB_LOF_HIGH_BAND
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2927983b196fb2488d520c2676b12ebafd4dba04
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845555"
---
# <a name="ksproperty_bda_lnb_lof_high_band"></a>KSK プロパティ\_BDA\_LNB\_LOF\_高\_帯域


クライアントは、KSK プロパティ\_BDA\_LNB\_LOF\_を使用して、高\_帯域の周波数を変化させるために低騒音ブロック (LNB) デバイスによって使用されるローカルオシレーター周波数 (LOF) について RF チューナーノードに通知します。シグナル.

## <span id="ddk_ksproperty_bda_lnb_lof_high_band_ks"></span><span id="DDK_KSPROPERTY_BDA_LNB_LOF_HIGH_BAND_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

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
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>フィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSP の**NodeId**メンバー\_node は、RF チューナーノードの識別子を指定します。

プロパティ値は、高帯域信号用に LNB によって使用される LOF を指定します。

LNB は、衛星アンテナによって反射される RF 信号を収集し、ハイバンドの LOF 量によって RF 信号の周波数をシフトし、結果の信号を RF チューナーに送信します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Bdamedia (Bdamedia を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 






