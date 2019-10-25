---
title: KSK プロパティ\_BDA\_転送\_モード
description: クライアントは、KSK プロパティ\_BDA\_伝送\_モードを使用して、ブロードキャスト信号の送信方法を demodulator ノードの設定を制御します。
ms.assetid: 8d49a45f-031f-445f-ae2e-d98223a7d524
keywords:
- KSPROPERTY_BDA_TRANSMISSION_MODE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_TRANSMISSION_MODE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20e742d0c4dc53e66df89e238b19cadff0623f28
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843593"
---
# <a name="ksproperty_bda_transmission_mode"></a>KSK プロパティ\_BDA\_転送\_モード


クライアントは、KSK プロパティ\_BDA\_伝送\_モードを使用して、ブロードキャスト信号の送信方法を demodulator ノードの設定を制御します。

## <span id="ddk_ksproperty_bda_transmission_mode_ks"></span><span id="DDK_KSPROPERTY_BDA_TRANSMISSION_MODE_KS"></span>


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
<td><p>TransmissionMode</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

TransmissionMode 列挙型から返された値は、ブロードキャストシグナルの送信方法の設定を識別します。

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

[**TransmissionMode**](https://docs.microsoft.com/previous-versions/windows/desktop/mstv/transmissionmode)

 

 






