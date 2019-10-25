---
title: KSK プロパティ\_BDA\_RF\_チューナー\_頻度
description: クライアントは、KSK プロパティ\_BDA\_RF\_チューナー\_FREQUENCY と共に、KSK プロパティ\_BDA\_RF\_チューナー\_FREQUENCY\_を使用して、チューナーノードの周波数設定を制御します。
ms.assetid: 0bcecf33-06d5-4b07-8602-da97db5c1306
keywords:
- KSPROPERTY_BDA_RF_TUNER_FREQUENCY ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_RF_TUNER_FREQUENCY
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43ae1820760974f980b1a18c10e7bd8907671095
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838076"
---
# <a name="ksproperty_bda_rf_tuner_frequency"></a>KSK プロパティ\_BDA\_RF\_チューナー\_頻度


クライアントは、KSK プロパティ\_BDA\_RF\_チューナー\_FREQUENCY と共に、KSK プロパティ\_BDA\_RF\_チューナー\_FREQUENCY\_を使用して、チューナーノードの周波数設定を制御します。

## <span id="ddk_ksproperty_bda_rf_tuner_frequency_ks"></span><span id="DDK_KSPROPERTY_BDA_RF_TUNER_FREQUENCY_KS"></span>


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

プロパティ値は、設定する基本頻度を指定します。

KSK プロパティ\_BDA\_RF\_チューナー\_FREQUENCY プロパティを次のように指定します。

-   BDA\_FREQUENCY\_\_設定されていません (− 1) は、頻度が設定されていないことを示します。

-   BDA\_FREQUENCY\_\_定義されていません (0) は、頻度が定義されていないことを示します。

KSK プロパティ\_BDA\_RF\_チューナー\_頻度\_乗数プロパティによって、BDA\_FREQUENCY\_の乗数が指定されている場合\_設定 (− 1) または BDA\_FREQUENCY\_乗数\_\_定義されていません (0)。次に、KSK プロパティ\_BDA\_RF\_チューナー\_FREQUENCY プロパティは、キロヘルツ (kHz) 単位で頻度を指定します。 さらに、frequency 乗数プロパティのミニドライバーのセットハンドラー ([*Kstrsetpropertyhandler*](https://docs.microsoft.com/previous-versions/ff567200(v=vs.85))) が呼び出されていない場合、ミニドライバーは、指定された頻度が KHz (1Hz x 1000) 単位で表されることを判断する必要があります。 実際には、既定の乗数値は1000です。 詳細については、「 [BDA チューナーノードの周波数プロパティへのアクセス](https://docs.microsoft.com/windows-hardware/drivers/stream/accessing-frequency-properties-of-a-bda-tuner-node)」を参照してください。

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

[**KSK プロパティ\_BDA\_RF\_チューナー\_頻度\_乗数**](ksproperty-bda-rf-tuner-frequency-multiplier.md)

 

 






