---
title: KSK プロパティ\_BDA\_内部\_FEC\_レート
description: クライアントは、KSK プロパティ\_BDA\_内部\_FEC\_率を使用して、demodulator ノードの内部前方エラー修正 (FEC) 型に使用されるバイナリ畳み込み方式を制御します。
ms.assetid: d5bf0ce0-d383-431f-85de-3d00f4831619
keywords:
- KSPROPERTY_BDA_INNER_FEC_RATE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_INNER_FEC_RATE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98b84bfac03807315a6494cac496cc613cbca7e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842140"
---
# <a name="ksproperty_bda_inner_fec_rate"></a>KSK プロパティ\_BDA\_内部\_FEC\_レート


クライアントは、KSK プロパティ\_BDA\_内部\_FEC\_率を使用して、demodulator ノードの内部前方エラー修正 (FEC) 型に使用されるバイナリ畳み込み方式を制御します。

## <span id="ddk_ksproperty_bda_inner_fec_rate_ks"></span><span id="DDK_KSPROPERTY_BDA_INNER_FEC_RATE_KS"></span>


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
<td><p>BinaryConvolutionCodeRate</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

BinaryConvolutionCodeRate 列挙型から返された値は、バイナリの畳み込みスキームを識別します。

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


[**BinaryConvolutionCodeRate**](https://docs.microsoft.com/previous-versions/windows/desktop/mstv/binaryconvolutioncoderate)

[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 






