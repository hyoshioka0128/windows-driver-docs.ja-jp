---
title: KSPROPERTY\_トポロジ\_カテゴリ
description: KSPROPERTY\_トポロジ\_ドライバーがサポートする機能のカテゴリの配列のカテゴリのプロパティのクエリ。
ms.assetid: 35a293a1-f8fe-44da-a50b-a4429e369567
keywords:
- KSPROPERTY_TOPOLOGY_CATEGORIES ストリーミング メディア デバイス
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
ms.openlocfilehash: e9a51b74be02ec2eb9829cfc6a4e8e5b4b29350b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559479"
---
# <a name="kspropertytopologycategories"></a>KSPROPERTY\_トポロジ\_カテゴリ


KSPROPERTY\_トポロジ\_ドライバーがサポートする機能のカテゴリの配列のカテゴリのプロパティのクエリ。

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
<td><p>X</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563441" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563441)"><strong>KSMULTIPLE_ITEM</strong></a>Guid のシーケンスと、その後</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティを返します、 [ **KSMULTIPLE\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff563441)シーケンス機能カテゴリ、KS フィルターでは、使用可能なを表す Guid の後に、構造体。 Microsoft は、標準のカテゴリを提供します。 *ks.h*と*ksmedia.h*します。 次はテクノロジ固有ではない機能のカテゴリの一覧です。

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
<td><p>サブシステムのストリーミング、カーネルの外側へのブリッジです。</p></td>
</tr>
<tr class="even">
<td><p>KSCATEGORY_CAPTURE</p></td>
<td><p>キャプチャします。</p></td>
</tr>
<tr class="odd">
<td><p></p>
KSCATEGORY_ COMMUNICATIONSTRANSFORM</td>
<td><p>通信変換デバイスです。</p></td>
</tr>
<tr class="even">
<td><p>KSCATEGORY_DATACOMPRESSOR</p></td>
<td><p>データ ストリームを圧縮します。</p></td>
</tr>
<tr class="odd">
<td><p>KSCATEGORY_DATADECOMPRESSOR</p></td>
<td><p>データ ストリームの圧縮を解除します。</p></td>
</tr>
<tr class="even">
<td><p>KSCATEGORY_DATATRANSFORM</p></td>
<td><p>データ ストリームを変換します。</p></td>
</tr>
<tr class="odd">
<td><p>KSCATEGORY_FILESYSTEM</p></td>
<td><p>データ ストリームは、ファイル システムの内外に移動します。</p></td>
</tr>
<tr class="even">
<td><p>KSCATEGORY_INTERFACETRANSFORM</p></td>
<td><p>使用されているインターフェイス型を変換します。</p></td>
</tr>
<tr class="odd">
<td><p>KSCATEGORY_MEDIUMTRANSFORM</p></td>
<td><p>使用されているメディアの種類を変換します。</p></td>
</tr>
<tr class="even">
<td><p>KSCATEGORY_MIXER</p></td>
<td><p>複数のデータ ストリームを合成します。</p></td>
</tr>
<tr class="odd">
<td><p>KSCATEGORY_RENDER</p></td>
<td><p>レンダラーです。</p></td>
</tr>
<tr class="even">
<td><p>KSCATEGORY_SPLITTER</p></td>
<td><p>データ ストリームを分割します。</p></td>
</tr>
</tbody>
</table>

 

トポロジのカテゴリは、デバイス インターフェイス クラスに対応します。

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
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSTOPOLOGY**](https://msdn.microsoft.com/library/windows/hardware/ff567146)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSMULTIPLE\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff563441)

 

 






