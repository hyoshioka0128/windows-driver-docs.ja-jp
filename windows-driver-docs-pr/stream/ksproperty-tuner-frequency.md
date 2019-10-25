---
title: KSK プロパティ\_チューナー\_頻度
description: KSK プロパティ\_チューナー\_FREQUENCY プロパティは、チューナーの現在の周波数またはチャネルを設定または取得します。 このプロパティを実装する必要があります。
ms.assetid: ba6caf67-63c1-4a31-b93f-3b06b61244bf
keywords:
- KSPROPERTY_TUNER_FREQUENCY ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_FREQUENCY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: af918b665e2e2455679ddcb0f5eb501214719b87
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837918"
---
# <a name="ksproperty_tuner_frequency"></a>KSK プロパティ\_チューナー\_頻度


KSK プロパティ\_チューナー\_FREQUENCY プロパティは、チューナーの現在の周波数またはチャネルを設定または取得します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_tuner_frequency_ks"></span><span id="DDK_KSPROPERTY_TUNER_FREQUENCY_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_frequency_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_FREQUENCY_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_frequency_s)"><strong>KSPROPERTY_TUNER_FREQUENCY_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、チューナーの現在の周波数を指定する ULONG です。 この値はヘルツ (Hz) 単位で指定します。

<a name="remarks"></a>注釈
-------

KSK プロパティ\_チューナー\_FREQUENCY\_S 構造体の**frequency**メンバーは、現在のチューナー周波数を指定します。

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
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSK プロパティ\_チューナー\_頻度\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_frequency_s)

 

 






