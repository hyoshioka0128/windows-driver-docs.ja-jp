---
title: KSK プロパティ\_BDA\_RF\_チューナー\_極性
description: クライアントは、KSK プロパティ\_BDA\_RF\_チューナー\_極性を使用して、チューナーノードの極性の設定を制御します。
ms.assetid: 6778b4ac-2444-4e27-ab80-5802dda09fdd
keywords:
- KSPROPERTY_BDA_RF_TUNER_POLARITY ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_RF_TUNER_POLARITY
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fec06fe32322fe9aef72c1ccd37fff09e90b8b8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838077"
---
# <a name="ksproperty_bda_rf_tuner_polarity"></a>KSK プロパティ\_BDA\_RF\_チューナー\_極性


クライアントは、KSK プロパティ\_BDA\_RF\_チューナー\_極性を使用して、チューナーノードの極性の設定を制御します。

## <span id="ddk_ksproperty_bda_rf_tuner_polarity_ks"></span><span id="DDK_KSPROPERTY_BDA_RF_TUNER_POLARITY_KS"></span>


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

KSP の**NodeId**メンバー\_node は、チューナーノードの識別子を指定します。

プロパティ値は、送信信号に設定する極性を指定します。

一部の転送 (特にサテライト転送) では、信号は polarized される可能性があります。 このプロパティは、送信されたシグナルの polarization をチューナーノードに通知します。 Polarization 列挙型には、シグナルの極性を指定する値が含まれます。

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

[**Polarization**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff567780(v=vs.85))

 

 






