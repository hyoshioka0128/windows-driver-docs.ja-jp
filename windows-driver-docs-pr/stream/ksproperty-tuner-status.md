---
title: KSPROPERTY\_チューナー\_状態
description: KSPROPERTY\_チューナー\_STATUS プロパティは、現在の頻度を含め、チューニング処理に関する情報を取得、フェーズには、ループ (PLL) オフセット、および信号の強さがロックされています。 このプロパティを実装する必要があります。
ms.assetid: 8613cda2-f39b-4363-a1c7-ac91162b9fca
keywords:
- KSPROPERTY_TUNER_STATUS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_STATUS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 004e62b00873753c107155391de3c1c311f67274
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355956"
---
# <a name="kspropertytunerstatus"></a>KSPROPERTY\_チューナー\_状態


KSPROPERTY\_チューナー\_STATUS プロパティは、現在の頻度を含め、チューニング処理に関する情報を取得、フェーズには、ループ (PLL) オフセット、および信号の強さがロックされています。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_tuner_status_ks"></span><span id="DDK_KSPROPERTY_TUNER_STATUS_KS"></span>


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
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_status_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STATUS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_status_s)"><strong>KSPROPERTY_TUNER_STATUS_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_status_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STATUS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_status_s)"><strong>KSPROPERTY_TUNER_STATUS_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSPROPERTY\_チューナー\_状態\_構造を現在の頻度、PLL オフセット、および信号を指定する強度。

<a name="remarks"></a>注釈
-------

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
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_チューナー\_状態\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_status_s)

 

 






