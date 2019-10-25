---
title: KSK プロパティ\_DVDSUBPIC\_パレット
description: KSK プロパティ\_DVDSUBPIC\_パレットプロパティは、サブピクチャストリームで使用するカラーパレットを指定します。
ms.assetid: 9dafb956-4adf-45ec-b997-8ed35991f7d8
keywords:
- KSPROPERTY_DVDSUBPIC_PALETTE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDSUBPIC_PALETTE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb65bbc1d054938ab882147671409cb3d7adf7fd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827076"
---
# <a name="ksproperty_dvdsubpic_palette"></a>KSK プロパティ\_DVDSUBPIC\_パレット


KSK プロパティ\_DVDSUBPIC\_パレットプロパティは、サブピクチャストリームで使用するカラーパレットを指定します。

## <span id="ddk_ksproperty_dvdsubpic_palette_ks"></span><span id="DDK_KSPROPERTY_DVDSUBPIC_PALETTE_KS"></span>


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
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sppal" data-raw-source="[&lt;strong&gt;KSPROPERTY_SPPAL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sppal)"><strong>KSPROPERTY_SPPAL</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、\_SPPAL 構造体の KSK プロパティです。これは、YUV カラー形式でのサブピクチャ表示に使用するカラーパレットを表します。

<a name="remarks"></a>注釈
-------

[**Ksk プロパティ\_SPPAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sppal)構造体には、16個の YUV 要素の配列が含まれています。 これらの要素は、サブピクチャコマンドストリーム内で要求された4ビットの色番号に対応します。

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


[**KSK プロパティ\_SPPAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sppal)

 

 






