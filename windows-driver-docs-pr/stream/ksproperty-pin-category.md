---
title: KSPROPERTY\_PIN\_カテゴリ
description: クライアントの使用、KSPROPERTY\_PIN\_暗証番号 (pin) の工場出荷時のカテゴリを取得するプロパティをカテゴリ。
ms.assetid: 6579408c-9ec5-4b09-9a63-815cec5bd5a3
keywords:
- KSPROPERTY_PIN_CATEGORY ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_CATEGORY
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16cc3d0efeae4ba220c547412ad0ebae82c87630
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353215"
---
# <a name="kspropertypincategory"></a>KSPROPERTY\_PIN\_カテゴリ


クライアントの使用、KSPROPERTY\_PIN\_暗証番号 (pin) の工場出荷時のカテゴリを取得するプロパティをカテゴリ。

## <span id="ddk_ksproperty_pin_category_ks"></span><span id="DDK_KSPROPERTY_PIN_CATEGORY_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p>GUID</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**PinId** KSP のメンバー\_暗証番号 (pin) の構造がカテゴリの GUID を取得するためのファクトリを暗証番号 (pin) を指定します。

KS フィルターを標準の機能を示すためにこのプロパティを使用して*カテゴリ*のピンをピン留めするファクトリをインスタンス化されます。

Stream ミニドライバーは、このプロパティを直接処理する必要はありません。ストリーム クラス ドライバーは、必要に応じて詳細情報を照会するストリーム要求のブロックを使用してこのプロパティを処理します。

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
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_暗証番号 (PIN)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)

 

 






