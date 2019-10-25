---
title: WIA\_IPA\_項目\_フラグ
description: WIA\_IPA\_ITEM\_FLAGS プロパティには、WIA 項目の説明フラグが含まれています。
ms.assetid: ee25fb38-eafa-49a9-83ab-4f99bc25f4e9
keywords:
- WIA_IPA_ITEM_FLAGS イメージングデバイス
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
ms.openlocfilehash: 5831b399849d5f8e32fbdab76352980e2a291122
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840692"
---
# <a name="wia_ipa_item_flags"></a>WIA\_IPA\_項目\_フラグ


WIA\_IPA\_ITEM\_FLAGS プロパティには、WIA 項目の説明フラグが含まれています。

## <span id="ddk_wia_ipa_item_flags_si"></span><span id="DDK_WIA_IPA_ITEM_FLAGS_SI"></span>


プロパティの型: VT\_I4

有効な値: WIA\_PROP\_NONE

アクセス権: 読み取り専用

<a name="remarks"></a>注釈
-------

WIA 項目フラグは、 [**wiasCreateDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem) service ユーティリティ関数の*lObjectFlags*パラメーターと同じです。 Wia サービスは、WIA\_IPA\_ITEM\_FLAGS プロパティを作成し、管理します。

アプリケーションは、wia\_IPA\_項目\_フラグを読み取り、WIA 項目の説明フラグの値を決定します。

次の表では、Windows Vista 以降のバージョンのオペレーティングシステムでは互換性のために残されているが、Microsoft Windows XP では有効なフラグについて説明します。

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
<td><p><strong>Iwiaitem:: Analyze eitem</strong>メソッドをサポートする WIA 項目。この方法については、Microsoft Windows SDK のドキュメントを参照してください。 この項目は、地域または decomposepages を検出するのに役立つ、子項目の自動生成もサポートしています。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeBurst</strong></p></td>
<td><p>フォルダーの場合のみ。 <strong>Wiaitemtypeburst</strong>は、このフォルダー内のイメージが連続する時間シーケンスで取得されたことを示します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeHasAttachments</strong></p></td>
<td><p>添付ファイルをサポートし、現在添付ファイルが含まれている WIA 項目。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeHPanorama</strong></p></td>
<td><p>水平パノラマ画像を表す WIA 項目。 このフラグは、 <strong>Wiaitemtypefolder</strong>フラグが設定されている項目に対してのみ有効です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeTwainCapabilityPassThrough</strong></p></td>
<td><p><strong>WiaItemTypeTwainCapabilityPassThrough</strong>は、WIA デバイスが twain 互換レイヤーから twain 機能データを受け取ることができることを示しています。 このフラグが設定されている場合、TWAIN 互換性レイヤーで認識されない TWAIN 機能は、WIA ドライバーに渡されます。 このフラグは、WIA ドライバーのルート項目に対してのみ有効です。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeVideo</strong></p></td>
<td><p>ストリーミングビデオをサポートする WIA 項目。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeVPanorama</strong></p></td>
<td><p>垂直パノラマ画像を表す WIA 項目。 <strong>Wiaitemtypevpanorama</strong>は、 <strong>Wiaitemtypefolder</strong>フラグが設定されている項目に対してのみ有効です。</p></td>
</tr>
</tbody>
</table>

 

次の表では、Windows Vista、Windows XP、およびそれ以降のオペレーティングシステムで有効なフラグについて説明します。

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
<td><p>オーディオをサポートする WIA 項目。 <strong>Wiaitemtypeaudio</strong>は、 <strong>Wiaitemtypeaudio</strong>フラグが設定されている項目に対してのみ有効です。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeDeleted</strong></p></td>
<td><p>削除対象としてマークされている WIA 項目が削除されたか、存在しないか、または無効なコンテンツが含まれています。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeDevice</strong></p></td>
<td><p>接続されているデバイスを表す WIA 項目。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeDisconnected</strong></p></td>
<td><p>切断されたデバイスを表す WIA 項目。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeFile</strong></p></td>
<td><p>ファイル転送をサポートする WIA 項目。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeFolder</strong></p></td>
<td><p>フォルダーである WIA 項目。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeFree</strong></p></td>
<td><p>初期化されていないか、削除された WIA 項目。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeGenerated</strong></p></td>
<td><p>アプリケーションまたはドライバーによって生成された WIA 項目。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeImage</strong></p></td>
<td><p>画像ファイルである WIA 項目。 <strong>Wiaitemtypeimage</strong>は、 <strong>Wiaitemtypeimage</strong>フラグが設定されている項目に対してのみ有効です。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeRoot</strong></p></td>
<td><p>Wia ドライバーのルート項目である WIA 項目。これは、デバイスがサポートしているすべての機能項目の親です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeStorage</strong></p></td>
<td><p><strong>Wiaitemtypeimage</strong>は、フォルダー項目の追加の記憶域を示します。 WIA ドライバーは、イメージとフォルダーの観点から項目を指定します。 ストレージ項目の特性 (残りの記憶域スペース、書き込み速度、メディアの種類など) を説明する WIA プロパティは存在しません。 この情報を公開するベンダー固有のプロパティを追加できます。 これらのプロパティは、ユーザーが認識するために作成したアプリケーションまたは拡張機能にのみアクセスできます。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeTransfer</strong></p></td>
<td><p>データの転送に使用できる WIA 項目。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeTwainCapabilityPassThrough</strong></p></td>
<td><p>Twain 互換性レイヤーから TWAIN 機能データを受け取ることができる WIA デバイス。 <strong>WiaItemTypeTwainCapabilityPassThrough</strong>が設定されている場合、twain 互換性レイヤーで認識されない twain 機能は、WIA ドライバーに渡されます。 このフラグは、WIA ドライバーのルート項目に対してのみ有効です。</p></td>
</tr>
</tbody>
</table>

 

次の表では、Windows Vista 以降のバージョンのオペレーティングシステムでのみ有効なフラグについて説明します。

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
<td><p><strong><em>Wiaitemtypedocument</em></strong> <em>は互換性のために残されているため、使用しない</em>でください。</p>
<p>WIA 項目は、 <a href="wia-ipa-format.md" data-raw-source="[&lt;strong&gt;WIA_IPA_FORMAT&lt;/strong&gt;](wia-ipa-format.md)"><strong>WIA_IPA_FORMAT</strong></a>プロパティに含まれるドキュメント形式の1つのドキュメントファイルです。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeProgrammableDataSource</strong></p></td>
<td><p>WIA 項目は、プログラミング可能なデータソースであり、 <a href="wia-ipa-item-category.md" data-raw-source="[&lt;strong&gt;WIA_IPA_ITEM_CATEGORY&lt;/strong&gt;](wia-ipa-item-category.md)"><strong>WIA_IPA_ITEM_CATEGORY</strong></a>プロパティに基づいて定義済みの構成規則のセットに従います。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeMask</strong></p></td>
<td><p>他のすべての定義済みフラグ値のフラグマスク。 このフラグは、単独では項目の種類ではありません。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeRemoved</strong></p></td>
<td><p>項目ツリーから WIA 項目が削除されました。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeRoot</strong></p></td>
<td><p>WIA 項目は、デバイスがサポートしているすべての機能項目の親である WIA ドライバーのルート項目です。</p></td>
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
<td>Wiadef (Wiadef を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_IPA\_形式**](wia-ipa-format.md)

[**WIA\_IPA\_項目\_カテゴリ**](wia-ipa-item-category.md)

[**wiasCreateDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)

 

 






