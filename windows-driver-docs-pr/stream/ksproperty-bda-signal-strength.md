---
title: KSPROPERTY\_BDA\_信号\_強度
description: クライアントを使用して、KSPROPERTY\_BDA\_信号\_mDb (デシベル (DB) の 1/1000) の信号の運送業者の強度を決める強度。
ms.assetid: b8b71135-cc0b-4a59-940a-dd766cab3305
keywords:
- KSPROPERTY_BDA_SIGNAL_STRENGTH ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SIGNAL_STRENGTH
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 021cc083e16b63839d82ecaefec14029742dd3e7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361110"
---
# <a name="kspropertybdasignalstrength"></a>KSPROPERTY\_BDA\_信号\_強度


クライアントを使用して、KSPROPERTY\_BDA\_信号\_mDb (デシベル (DB) の 1/1000) の信号の運送業者の強度を決める強度。

## <span id="ddk_ksproperty_bda_signal_strength_ks"></span><span id="DDK_KSPROPERTY_BDA_SIGNAL_STRENGTH_KS"></span>


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
<td><p>Pin またはフィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**NodeId** KSP のメンバー\_ノードの管理ノードの識別子を指定しますまたは、暗証番号 (pin) を指定する − 1 に設定されています。

返される値は、mDb の信号の運送業者の強度を指定します。

0 の強度は標準強度のブロードキャスト ネットワークの特定の種類が必要です。 Subnominal 長所は、正の mDb として報告されます。 超名目上の長所は、負の mDb として報告されます。

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


[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

 

 






