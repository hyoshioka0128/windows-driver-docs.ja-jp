---
title: KSK プロパティ\_BDA\_スペクトル\_反転
description: クライアントは、demodulator ノードのスペクトル反転の設定を制御するために、KSK プロパティ\_BDA\_スペクトル\_反転を使用します。
ms.assetid: a51dee0b-4a45-4159-978b-27ff6e2333e2
keywords:
- KSPROPERTY_BDA_SPECTRAL_INVERSION ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SPECTRAL_INVERSION
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b39cd4647aee73b9c784e1966388957bf4adcc39
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843601"
---
# <a name="ksproperty_bda_spectral_inversion"></a>KSK プロパティ\_BDA\_スペクトル\_反転


クライアントは、demodulator ノードのスペクトル反転の設定を制御するために、KSK プロパティ\_BDA\_スペクトル\_反転を使用します。

## <span id="ddk_ksproperty_bda_spectral_inversion_ks"></span><span id="DDK_KSPROPERTY_BDA_SPECTRAL_INVERSION_KS"></span>


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
<td><p>SpectralInversion</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

SpectralInversion 列挙型から返された値は、スペクトル反転の設定を識別します。

KSP の**NodeId**メンバー\_node は、demodulator ノードの識別子を指定します。

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

[**SpectralInversion**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568154(v=vs.85))

 

 






