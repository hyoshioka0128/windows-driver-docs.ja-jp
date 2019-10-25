---
title: KSK プロパティ\_BDA\_RF\_チューナー\_トランスポンダー
description: クライアントは、KSK プロパティ\_BDA\_RF\_チューナー\_トランスポンダーを使用して、適切なトランスポンダー番号のチューナーノードに通知します。
ms.assetid: 00445260-a317-4341-baab-d1391f6748e4
keywords:
- KSPROPERTY_BDA_RF_TUNER_TRANSPONDER ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_RF_TUNER_TRANSPONDER
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01e97e0544dfd6907e929b3dafbdc97dfe2a3e89
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838080"
---
# <a name="ksproperty_bda_rf_tuner_transponder"></a>KSK プロパティ\_BDA\_RF\_チューナー\_トランスポンダー


クライアントは、KSK プロパティ\_BDA\_RF\_チューナー\_トランスポンダーを使用して、適切なトランスポンダー番号のチューナーノードに通知します。

## <span id="ddk_ksproperty_bda_rf_tuner_transponder_ks"></span><span id="DDK_KSPROPERTY_BDA_RF_TUNER_TRANSPONDER_KS"></span>


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

プロパティ値は、設定するトランスポンダー番号を指定します。

一部のチューニングスペースには、ハードウェアに埋め込まれた頻度を取得する方法に関するすべての情報が含まれています。 これらのチューニングスペースは、トランスポンダー番号を指定します。 このプロパティは、このトランスポンダー番号のチューナーノードに通知します。 その後、チューナーハードウェアによって、中間周波数を取得するために必要なチューニング特性が自動的に決定されます。 この場合、KSPROPSETID\_BdaFrequencyFilter プロパティセットの他のプロパティは、−1に設定されます。

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

 

 






