---
title: KSPROPERTY\_BDA\_RF\_チューナー\_帯域幅
description: クライアントを使用して、KSPROPERTY\_BDA\_RF\_チューナー\_チューナーのノードの帯域幅の設定を制御する帯域幅。
ms.assetid: 34feb05d-c1dc-4ce1-86bf-d7d33920befd
keywords:
- KSPROPERTY_BDA_RF_TUNER_BANDWIDTH ストリーミング メディア デバイス
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
ms.openlocfilehash: 3b5a343424a291448b09f95f65b926eda4392d05
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329978"
---
# <a name="kspropertybdarftunerbandwidth"></a>KSPROPERTY\_BDA\_RF\_チューナー\_帯域幅


クライアントを使用して、KSPROPERTY\_BDA\_RF\_チューナー\_チューナーのノードの帯域幅の設定を制御する帯域幅。

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
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

**NodeId** KSP のメンバー\_ノードは、チューナーのノードの識別子を指定します。

プロパティの値を設定する帯域幅を指定します。 帯域幅は、シグナルまたはグループを相互に関連する通知の送信に使用される周波数の範囲です。 つまり、一度に転送できる情報の量。

指定、KSPROPERTY\_BDA\_RF\_チューナー\_と帯域幅のプロパティ。

-   BDA\_CHAN\_BANDWITH\_いない\_セット (-1) では、帯域幅が設定されていないことを示します。

-   BDA\_CHAN\_BANDWITH\_いない\_定義 (0) では、帯域幅が定義されていないことを示します。

<a name="requirements"></a>必要条件
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


[**KSP\_ノード**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

 

 






