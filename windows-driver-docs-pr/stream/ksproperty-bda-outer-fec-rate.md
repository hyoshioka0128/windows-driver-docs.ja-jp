---
title: KSPROPERTY\_BDA\_OUTER\_FEC\_率
description: クライアントを使用して、KSPROPERTY\_BDA\_OUTER\_FEC\_バイナリ畳み込みスキームを制御する際の速度が外側の転送エラーの修正に対して復調器ノードの種類を (FEC) を使用します。
ms.assetid: 0bf1819d-5361-4ab2-b337-e0dd393f5b9b
keywords:
- KSPROPERTY_BDA_OUTER_FEC_RATE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_OUTER_FEC_RATE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d94f1e68a4f297b8dbeda993221daf6b35f61645
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368150"
---
# <a name="kspropertybdaouterfecrate"></a>KSPROPERTY\_BDA\_OUTER\_FEC\_率


クライアントを使用して、KSPROPERTY\_BDA\_OUTER\_FEC\_バイナリ畳み込みスキームを制御する際の速度が外側の転送エラーの修正に対して復調器ノードの種類を (FEC) を使用します。

## <span id="ddk_ksproperty_bda_outer_fec_rate_ks"></span><span id="DDK_KSPROPERTY_BDA_OUTER_FEC_RATE_KS"></span>


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
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>フィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>BinaryConvolutionCodeRate</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

BinaryConvolutionCodeRate 列挙型から返される値は、バイナリの畳み込みスキームを識別します。

**NodeId** KSP のメンバー\_ノード復調器ノードの識別子を指定します。

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
<td>Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**BinaryConvolutionCodeRate**](https://docs.microsoft.com/previous-versions/windows/desktop/mstv/binaryconvolutioncoderate)

[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

 

 






