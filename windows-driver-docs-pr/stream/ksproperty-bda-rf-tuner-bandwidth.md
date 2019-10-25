---
title: KSK プロパティ\_BDA\_RF\_チューナー\_帯域幅
description: クライアントは、KSK プロパティ\_BDA\_RF\_チューナー\_帯域幅を使用して、チューナーノードの帯域幅設定を制御します。
ms.assetid: 34feb05d-c1dc-4ce1-86bf-d7d33920befd
keywords:
- KSPROPERTY_BDA_RF_TUNER_BANDWIDTH ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_RF_TUNER_BANDWIDTH
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 412eac5587fa0da8c8c8018d203d4af33ef14ad0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838085"
---
# <a name="ksproperty_bda_rf_tuner_bandwidth"></a>KSK プロパティ\_BDA\_RF\_チューナー\_帯域幅


クライアントは、KSK プロパティ\_BDA\_RF\_チューナー\_帯域幅を使用して、チューナーノードの帯域幅設定を制御します。

## <span id="ddk_ksproperty_bda_rf_tuner_bandwidth_ks"></span><span id="DDK_KSPROPERTY_BDA_RF_TUNER_BANDWIDTH_KS"></span>


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
<th>セット</th>
<th>的を絞る</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>filter</p></td>
<td><p>KSP_NODE</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

KSP の**NodeId**メンバー\_node は、チューナーノードの識別子を指定します。

プロパティ値は、設定する帯域幅を指定します。 帯域幅は、相互に関連するシグナルまたはグループの送信に使用される周波数の範囲です。 つまり、一度に送信できる情報の量です。

KSK プロパティ\_BDA\_RF\_チューナー\_帯域幅プロパティを次のように指定します。

-   BDA\_チャン\_帯域幅\_\_設定されていません (− 1) は、帯域幅が設定されていないことを示します。

-   BDA\_チャン\_帯域幅\_\_定義されていません (0) 帯域幅が定義されていないことを示します。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Bdamedia (Bdamedia を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 






