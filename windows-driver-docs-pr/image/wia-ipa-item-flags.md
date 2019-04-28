---
title: WIA\_IPA\_項目\_フラグ
description: WIA\_IPA\_項目\_フラグ プロパティには、WIA 項目の内容を示すフラグが含まれています。
ms.assetid: ee25fb38-eafa-49a9-83ab-4f99bc25f4e9
keywords:
- WIA_IPA_ITEM_FLAGS イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPA_ITEM_FLAGS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56dde9f5e26f242ef54a2cb0d2805d7808661405
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369506"
---
# <a name="wiaipaitemflags"></a>WIA\_IPA\_項目\_フラグ


WIA\_IPA\_項目\_フラグ プロパティには、WIA 項目の内容を示すフラグが含まれています。

## <span id="ddk_wia_ipa_item_flags_si"></span><span id="DDK_WIA_IPA_ITEM_FLAGS_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

WIA 項目のフラグは、内のものと同じ、 *lObjectFlags*のパラメーター、 [ **wiasCreateDrvItem** ](https://msdn.microsoft.com/library/windows/hardware/ff549160)ユーティリティ関数のサービスを提供します。 WIA サービスを作成して維持、WIA\_IPA\_項目\_FLAGS プロパティ。

アプリケーションは、WIA を読み取ります\_IPA\_項目\_WIA 項目の説明を決定するフラグ値にフラグを設定します。

次の表が Windows Vista およびそれ以降のバージョンのオペレーティング システムで廃止されていますが、Microsoft Windows XP を備えた有効なフラグについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>WiaItemTypeAnalyze</strong></p></td>
<td><p>WIA 項目をサポートする、 <strong>IWiaItem::AnalyzeItem</strong>メソッドは、Microsoft Windows SDK ドキュメントで説明します。 この項目には、リージョンまたは decomposepages を検出できます自動子アイテムの生成もサポートしています。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeBurst</strong></p></td>
<td><p>フォルダーのみです。 <strong>WiaItemTypeBurst</strong>継続時間シーケンスでこのフォルダー内のイメージを実行したことを示します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeHasAttachments</strong></p></td>
<td><p>WIA 項目を添付ファイルをサポートし、現在の添付ファイルが含まれています。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeHPanorama</strong></p></td>
<td><p>水平方向のパノラマ画像を表す WIA 項目。 このフラグは設定されている項目でのみ有効です、 <strong>WiaItemTypeFolder</strong>フラグを設定します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeTwainCapabilityPassThrough</strong></p></td>
<td><p><strong>WiaItemTypeTwainCapabilityPassThrough</strong> WIA デバイスが TWAIN 互換性レイヤーから TWAIN 機能データを受信できることを示します。 このフラグが設定されている場合、TWAIN 互換レイヤーに対応していない、TWAIN 機能は WIA ドライバーに渡すされます。 このフラグは、WIA ドライバーのルート項目に対してのみ有効です。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeVideo</strong></p></td>
<td><p>WIA 項目ストリーミング ビデオをサポートします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeVPanorama</strong></p></td>
<td><p>縦方向のパノラマ画像を表す WIA 項目。 <strong>WiaItemTypeVPanorama</strong>も設定されている項目に対してのみ有効ですが、 <strong>WiaItemTypeFolder</strong>フラグを設定します。</p></td>
</tr>
</tbody>
</table>

 

次の表では、Windows Vista、Windows XP、および以降のオペレーティング システムで有効なフラグについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>WiaItemTypeAudio</strong></p></td>
<td><p>オーディオ サポート WIA 項目。 <strong>WiaItemTypeAudio</strong>も設定されている項目に対してのみ有効ですが、 <strong>WiaItemTypeFile</strong>フラグを設定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeDeleted</strong></p></td>
<td><p>削除とマークされたが削除されているが存在しない、または無効なコンテンツが含まれて WIA 項目。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeDevice</strong></p></td>
<td><p>接続されたデバイスを表す WIA 項目。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeDisconnected</strong></p></td>
<td><p>切断されたデバイスを表す WIA 項目。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeFile</strong></p></td>
<td><p>WIA 項目がファイル転送をサポートします。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeFolder</strong></p></td>
<td><p>フォルダーは、WIA 項目。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeFree</strong></p></td>
<td><p>初期化されていないか、削除された WIA 項目。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeGenerated</strong></p></td>
<td><p>WIA ドライバーまたはアプリケーションによって生成された項目。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeImage</strong></p></td>
<td><p>イメージ ファイルは、WIA 項目。 <strong>WiaItemTypeImage</strong>も設定されている項目に対してのみ有効ですが、 <strong>WiaItemTypeFile</strong>フラグを設定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeRoot</strong></p></td>
<td><p>デバイスでサポートする機能のすべての項目の親である、WIA ドライバーのルート項目 WIA アイテム。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeStorage</strong></p></td>
<td><p><strong>WiaItemTypeImage</strong>フォルダー項目の追加の記憶域を示します。 WIA ドライバーでは、イメージとフォルダーの観点からそれらの項目を指定します。 WIA プロパティが存在しません (残りの記憶域スペース、書き込み速度、メディアの種類など) の記憶域の項目の特性を記述します。 この情報を公開するベンダー固有のプロパティを追加することができます。 これらのプロパティは、アプリケーションまたは拡張子が認識できるように記述するにのみアクセスできます。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeTransfer</strong></p></td>
<td><p>WIA 項目データを転送するために使用できます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeTwainCapabilityPassThrough</strong></p></td>
<td><p>WIA TWAIN 互換レイヤーから TWAIN 機能データを受信できるデバイス。 場合<strong>WiaItemTypeTwainCapabilityPassThrough</strong>が設定されて、TWAIN 互換レイヤーに対応していない、TWAIN 機能は、WIA ドライバーに渡されます。 このフラグは、WIA ドライバーのルート項目に対してのみ有効です。</p></td>
</tr>
</tbody>
</table>

 

次の表では、Windows Vista および以降のバージョンのオペレーティング システムのみで有効なフラグについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>WiaItemTypeDocument</strong></p></td>
<td><p><strong><em>WiaItemTypeDocument</em></strong>  <em>は廃止され、使用する必要があります。</em></p>
<p>WIA 項目は、ドキュメントのいずれかでドキュメント ファイルの形式、 <a href="wia-ipa-format.md" data-raw-source="[&lt;strong&gt;WIA_IPA_FORMAT&lt;/strong&gt;](wia-ipa-format.md)"> <strong>WIA_IPA_FORMAT</strong> </a>プロパティが含まれています。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeProgrammableDataSource</strong></p></td>
<td><p>WIA 項目はプログラミング可能なデータ ソースし、に基づく定義済みの構成規則のセットに依存して、 <a href="wia-ipa-item-category.md" data-raw-source="[&lt;strong&gt;WIA_IPA_ITEM_CATEGORY&lt;/strong&gt;](wia-ipa-item-category.md)"> <strong>WIA_IPA_ITEM_CATEGORY</strong> </a>プロパティ。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeMask</strong></p></td>
<td><p>他のすべてのフラグ マスクでは、フラグの値を定義します。 このフラグは、単独で、項目の種類ではありません。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeRemoved</strong></p></td>
<td><p>WIA 項目が項目のツリーから削除されました。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeRoot</strong></p></td>
<td><p>WIA 項目は、すべてのデバイスでサポートされる機能の項目の親である WIA ドライバーのルート項目です。</p></td>
</tr>
</tbody>
</table>

 

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
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_IPA\_形式**](wia-ipa-format.md)

[**WIA\_IPA\_項目\_カテゴリ**](wia-ipa-item-category.md)

[**wiasCreateDrvItem**](https://msdn.microsoft.com/library/windows/hardware/ff549160)

 

 






