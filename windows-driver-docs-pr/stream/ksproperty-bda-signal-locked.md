---
title: KSK プロパティ\_BDA\_シグナル\_ロックされています
description: クライアントは、KSK プロパティ\_BDA\_SIGNAL\_LOCKED を使用して、シグナルをロックできるかどうかを判断します。
ms.assetid: 98023f83-2e90-4649-8e85-3e7b7f26b01d
keywords:
- KSPROPERTY_BDA_SIGNAL_LOCKED ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SIGNAL_LOCKED
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7364834dfb4bff30719f77da94509c33f459e417
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838066"
---
# <a name="ksproperty_bda_signal_locked"></a>KSK プロパティ\_BDA\_シグナル\_ロックされています


クライアントは、KSK プロパティ\_BDA\_SIGNAL\_LOCKED を使用して、シグナルをロックできるかどうかを判断します。

## <span id="ddk_ksproperty_bda_signal_locked_ks"></span><span id="DDK_KSPROPERTY_BDA_SIGNAL_LOCKED_KS"></span>


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
<td><p>ピン留めまたはフィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

KSP の**NodeId**メンバー\_node は、コントロールノードの識別子を指定します。または、pin を指定するために−1に設定されています。

戻り値は、シグナルをロックできるかどうかを示します。 シグナルをロックできる場合は**TRUE** 、それ以外の場合は**FALSE**を返します。

RF チューナーノードが**TRUE**を返した場合、通常、フェーズロックループ (pll) ロックが示されます。

Demodulator ノードが**TRUE**を返した場合、少なくとも20% の信号品質が示されます。

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

[**KSK プロパティ\_BDA\_シグナル\_品質**](ksproperty-bda-signal-quality.md)

 

 






