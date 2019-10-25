---
title: KSK プロパティ\_BDA\_\_PIN\_ID を制御しています
description: クライアントは、KSK プロパティ\_BDA\_使用して\_ピン\_ID を制御し、BDA テンプレート接続リスト内のノードの制御ピンを取得します。
ms.assetid: d40454a3-0938-4efb-8b06-06b599be8b20
keywords:
- KSPROPERTY_BDA_CONTROLLING_PIN_ID ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_CONTROLLING_PIN_ID
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecd8523aac5f65d37d29a0f5fc3167ea684f5673
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842148"
---
# <a name="ksproperty_bda_controlling_pin_id"></a>KSK プロパティ\_BDA\_\_PIN\_ID を制御しています


クライアントは、KSK プロパティ\_BDA\_使用して\_ピン\_ID を制御し、BDA テンプレート接続リスト内のノードの制御ピンを取得します。

## <span id="ddk_ksproperty_bda_controlling_pin_id_ks"></span><span id="DDK_KSPROPERTY_BDA_CONTROLLING_PIN_ID_KS"></span>


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
<td><p>必須ではない</p></td>
<td><p>フィルター</p></td>
<td><p>KSP_BDA_NODE_PIN</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

戻り値は、制御ピン ID を指定します。

ノードは、フィルター内の1つのピン (入力ピンまたは出力ピン) に関連付けられています。 ノードには、独自のファイルハンドルがないため、制御ピン経由でのみアクセスできます。 ネットワークプロバイダーは、このプロパティと KSP\_BDA\_ノード\_固定構造体を使用して、BDA テンプレート接続リスト (KSTOPOLOGY\_CONNECTION または BDA\_テンプレート内の各ノードの制御ピンを照会することができ\_接続配列)。

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


[**BdaPropertyGetControllingPinId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertygetcontrollingpinid)

[**BDA\_テンプレート\_接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdatypes/ns-bdatypes-_bda_template_connection)

[**KSP\_BDA\_ノード\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdamedia/ns-bdamedia-_ksp_bda_node_pin)

[**KSTOPOLOGY\_接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstopology_connection)

 

 






