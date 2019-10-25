---
title: KSK プロパティ\_トポロジ\_カテゴリ
description: KSK プロパティ\_TOPOLOGY\_CATEGORIES プロパティは、ドライバーがサポートする機能カテゴリの配列を照会します。
ms.assetid: 35a293a1-f8fe-44da-a50b-a4429e369567
keywords:
- KSPROPERTY_TOPOLOGY_CATEGORIES ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TOPOLOGY_CATEGORIES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d37380229e81651e903c7685beed1253bcdd3cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837929"
---
# <a name="ksproperty_topology_categories"></a>KSK プロパティ\_トポロジ\_カテゴリ


KSK プロパティ\_TOPOLOGY\_CATEGORIES プロパティは、ドライバーがサポートする機能カテゴリの配列を照会します。

## <span id="ddk_ksproperty_topology_categories_ks"></span><span id="DDK_KSPROPERTY_TOPOLOGY_CATEGORIES_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>の後に一連の guid が続きます。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、 [**Ksmultiple\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)構造体を返し、その後に、KS フィルターがサポートする可能性のある機能カテゴリを表す一連の guid を返します。 Microsoft では、 *ks*および*ksmedia. h*で標準カテゴリを提供しています。 次に、テクノロジ固有ではない機能カテゴリの一覧を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能カテゴリ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KSCATEGORY_BRIDGE</p></td>
<td><p>カーネルストリーミングサブシステムの外部へのブリッジ。</p></td>
</tr>
<tr class="even">
<td><p>KSCATEGORY_CAPTURE</p></td>
<td><p>変革.</p></td>
</tr>
<tr class="odd">
<td><p></p>
KSCATEGORY_ COMMUNICATIONSTRANSFORM</td>
<td><p>通信変換デバイス。</p></td>
</tr>
<tr class="even">
<td><p>KSCATEGORY_DATACOMPRESSOR</p></td>
<td><p>データストリームを圧縮します。</p></td>
</tr>
<tr class="odd">
<td><p>KSCATEGORY_DATADECOMPRESSOR</p></td>
<td><p>データストリームを圧縮解除します。</p></td>
</tr>
<tr class="even">
<td><p>KSCATEGORY_DATATRANSFORM</p></td>
<td><p>データストリームを変換します。</p></td>
</tr>
<tr class="odd">
<td><p>KSCATEGORY_FILESYSTEM</p></td>
<td><p>データストリームをファイルシステムに移動します。</p></td>
</tr>
<tr class="even">
<td><p>KSCATEGORY_INTERFACETRANSFORM</p></td>
<td><p>使用されているインターフェイスの型を変換します。</p></td>
</tr>
<tr class="odd">
<td><p>KSCATEGORY_MEDIUMTRANSFORM</p></td>
<td><p>使用されているメディアの種類を変換します。</p></td>
</tr>
<tr class="even">
<td><p>KSCATEGORY_MIXER</p></td>
<td><p>複数のデータストリームをミックスします。</p></td>
</tr>
<tr class="odd">
<td><p>KSCATEGORY_RENDER</p></td>
<td><p>レンダラ.</p></td>
</tr>
<tr class="even">
<td><p>KSCATEGORY_SPLITTER</p></td>
<td><p>データストリームを分割します。</p></td>
</tr>
</tbody>
</table>

 

トポロジカテゴリは、デバイスインターフェイスクラスに対応します。

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
<td>Ks (Ks を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSTOPOLOGY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstopology)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSMULTIPLE\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

 

 






