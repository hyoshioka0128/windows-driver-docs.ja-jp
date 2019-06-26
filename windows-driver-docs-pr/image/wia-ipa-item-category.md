---
title: WIA\_IPA\_項目\_カテゴリ
description: WIA\_IPA\_項目\_WIA 項目のグループ化されたカテゴリがカテゴリのプロパティに含まれています。
ms.assetid: 0dde5e1c-ac30-4129-96fb-89ce1950c29b
keywords:
- WIA_IPA_ITEM_CATEGORY イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPA_ITEM_CATEGORY
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec2f70c600199b6c0ae0872c705c3b41d6a5f07e
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391432"
---
# <a name="wiaipaitemcategory"></a>WIA\_IPA\_項目\_カテゴリ


WIA\_IPA\_項目\_WIA 項目のグループ化されたカテゴリがカテゴリのプロパティに含まれています。

## <span id="ddk_wia_ipa_item_category_si"></span><span id="DDK_WIA_IPA_ITEM_CATEGORY_SI"></span>


プロパティの種類:VT\_CLSID

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>コメント
-------

WIA ミニドライバーは、作成し、このプロパティを保持します。

WIA には、次のカテゴリを定義します。

<span id="WIA_CATEGORY_BARCODE_READER"></span><span id="wia_category_barcode_reader"></span>WIA\_カテゴリ\_バーコード\_リーダー  
プログラミング可能なデータ ソース、バーコードのメタデータのダウンロードを有効になっている転送では、バーコード リーダー項目。

<span id="WIA_CATEGORY_ENDORSER"></span><span id="wia_category_endorser"></span>WIA\_カテゴリ\_裏書き  
プログラミング可能なデータの保証のカテゴリが imprinting と保証するには、両方を表す項目をソースし、アップロードおよびデータ コンテンツの印刷動作保証済みのダウンロードを有効に転送することができます。

<span id="WIA_CATEGORY_FEEDER"></span><span id="wia_category_feeder"></span>WIA\_カテゴリ\_フィーダー  
標準の規則が続くし、ドキュメント フィーダーをサポートするために必要な WIA プロパティを持つ、プログラミング可能なデータ ソースであるフィーダー項目を指定します。

<span id="WIA_CATEGORY_FEEDER_BACK"></span><span id="wia_category_feeder_back"></span>WIA\_カテゴリ\_フィーダー\_戻る  
双方向の基本フィーダー項目の背面にあるデータ ソースを記述するプログラミング可能なデータ ソース アイテム (WIA\_カテゴリ\_フィーダー)。

<span id="WIA_CATEGORY_FEEDER_FRONT"></span><span id="wia_category_feeder_front"></span>WIA\_カテゴリ\_フィーダー\_フロント  
双方向の基本フィーダー項目の前面にあるデータ ソースを記述するプログラミング可能なデータ ソース アイテム (WIA\_カテゴリ\_フィーダー)。

<span id="WIA_CATEGORY_FILM"></span><span id="wia_category_film"></span>WIA\_カテゴリ\_フィルム  
標準の規則が続くし、ユニットのフィルム スキャンをサポートするために必要な WIA プロパティを持つ、プログラミング可能なデータ ソースであるフィルム項目を指定します。

<span id="WIA_CATEGORY_FINISHED_FILE"></span><span id="wia_category_finished_file"></span>WIA\_カテゴリ\_FINISHED\_ファイル  
*いない*プログラミング可能なデータ ソース。 デバイスは、完成したファイル形式で、または完了したファイル形式の項目を格納するフォルダー項目でのデータを提供します。

<span id="WIA_CATEGORY_FLATBED"></span><span id="wia_category_flatbed"></span>WIA\_カテゴリ\_ベッド  
フラット ベッドの項目を標準の規則が続くし、フラット ベッド プラテン スキャンをサポートするために必要な WIA プロパティを持つ、プログラミング可能なデータ ソースです。

<span id="WIA_CATEGORY_FOLDER"></span><span id="wia_category_folder"></span>WIA\_カテゴリ\_フォルダー  
フォルダー ストレージの項目を (プログラミング可能なデータ ソースではなく) その他のフォルダーの項目を含むやファイルを終了します。

<span id="WIA_CATEGORY_IMPRINTER"></span><span id="wia_category_imprinter"></span>WIA\_カテゴリ\_・ インプリント ・  
プログラミング可能なデータの imprinting カテゴリ imprinting と保証するには、両方を表す項目のソースし、アップロードおよびデータ コンテンツの印刷動作保証済みのダウンロードを有効に転送することができます。

<span id="WIA_CATEGORY_MICR_READER"></span><span id="wia_category_micr_reader"></span>WIA\_カテゴリ\_MICR\_リーダー  
プログラミング可能なデータ ソース、MICR テキストのダウンロードを有効になっている転送では、(磁気インク文字認識) MICR リーダー項目。

<span id="WIA_CATEGORY_PATCH_CODE_READER"></span><span id="wia_category_patch_code_reader"></span>WIA\_カテゴリ\_PATCH\_コード\_リーダー  
プログラミング可能なデータ ソース、修正プログラム コードのメタデータのダウンロードを有効になっている転送では、修正プログラム コード リーダーの項目。

<span id="WIA_CATEGORY_ROOT"></span><span id="wia_category_root"></span>WIA\_カテゴリ\_ルート  
デバイスのルート項目。

<span id="WIA_CATEGORY_AUTO"></span><span id="wia_category_auto"></span>WIA\_カテゴリ\_自動  
Windows 7 以降では、[自動項目](https://docs.microsoft.com/windows-hardware/drivers/image/auto-item)WIA プロパティをサポートするために必要なは[スキャンの自動構成](https://docs.microsoft.com/windows-hardware/drivers/image/auto-configured-scanning)します。

上記のカテゴリは、WIA 項目を処理するかを使用する方法を定義します。 たとえば、項目が完成したファイルである場合は、データが静的で、デバイスに配置されていることを想定できます。 項目は、フィーダーを表している場合は、ドキュメント フィーダーの必要なプロパティが含まれると、ドキュメント フィーダー付きのように動作することを期待できます。 これらのカテゴリの詳細については、次を参照してください。 [WIA 項目カテゴリ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-item-categories)します。

次の表では、カテゴリとその項目のフラグ、WIA がグループ化を示します。 次の表では、すべての WIA を定義する WIA 項目フラグの完全な一覧は含まれません。 これらのフラグの完全な一覧を参照してください。 [ **WIA\_IPA\_項目\_フラグ**](wia-ipa-item-flags.md)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>WIA カテゴリ</th>
<th>WIA 項目のフラグ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_CATEGORY_BARCODE_READER</p></td>
<td><p>WiaItemTypeProgrammableDataSource</p>
<p><strong>必須</strong></p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeFile</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_ENDORSER</p></td>
<td><p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeImage</p>
<p><strong>省略可</strong></p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeFile</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FEEDER</p></td>
<td><p><strong>必須</strong></p>
<p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeFile</p>
<p><strong>省略可</strong></p>
<p>WiaItemTypeFolder</p>
<p>(ADF は、WIA_CATEGORY_FEEDER_FRONT と WIA_CATEGORY_FEEDER_BACK 項目が存在する場合にのみ、項目をルート)</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_FEEDER_BACK</p></td>
<td><p><strong>必須</strong></p>
<p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeFile</p>
<p><strong>省略可</strong></p>
<p>なし</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FEEDER_FRONT</p></td>
<td><p><strong>必須</strong></p>
<p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeFile</p>
<p><strong>省略可</strong></p>
<p>なし</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_FILM</p></td>
<td><p><strong>必須</strong></p>
<p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeFile</p>
<p>WiaItemTypeFolder</p>
<p><strong>省略可</strong></p>
<p>なし</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FINISHED_FILE</p></td>
<td><p><strong>必須</strong></p>
<p>WiaItemTypeFile</p>
<p>WiaItemTypeTransfer</p>
<p><strong>省略可</strong></p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeAudio</p>
<p>WiaItemTypeDeleted</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_FLATBED</p></td>
<td><p><strong>必須</strong></p>
<p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeFile</p>
<p><strong>省略可</strong></p>
<p>WiaItemTypeFolder</p>
<p>(FB ルート項目のみにスキャン リージョンの項目を複数サポートされます)</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FOLDER</p></td>
<td><p><strong>必須</strong></p>
<p>WiaItemTypeStorage</p>
<p>WiaItemTypeFolder</p>
<p><strong>省略可</strong></p>
<p>WiaItemTypeDeleted</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_IMPRINTER</p></td>
<td><p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeImage</p>
<p><strong>省略可</strong></p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeFile</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_MICR_READER</p></td>
<td><p>WiaItemTypeProgrammableDataSource</p>
<p><strong>必須</strong></p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeFile</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_PATCH_CODE_READER</p></td>
<td><p>WiaItemTypeProgrammableDataSource</p>
<p><strong>必須</strong></p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeFile</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_ROOT</p></td>
<td><p><strong>必須</strong></p>
<p>WiaItemTypeRoot</p>
<p>WiaItemTypeFolder</p>
<p><strong>省略可</strong></p>
<p>WiaItemTypeDevice</p>
<p>WiaItemTypeDisconnected</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_AUTO</p></td>
<td><p><strong>必須</strong></p>
<p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeFile</p>
<p><strong>省略可</strong></p>
<p><em>None</em></p></td>
</tr>
</tbody>
</table>

 

次の表では、カテゴリと、WIA プロパティと WIA 項目、WIA がグループ化を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>WIA カテゴリ</th>
<th>WIA プロパティ</th>
<th>WIA 項目</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_CATEGORY_FEEDER</p></td>
<td><p>フィーダー スキャナー コントロールのプロパティも含まれます。</p>
<p>イメージおよびドキュメントに固有のプロパティは、通常は含まれています。</p></td>
<td><p>ドキュメントのフロント エンドとバックエンドのページを表す子項目を含む、WIA フィーダー項目。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_FEEDER_BACK</p></td>
<td><p>フィーダー スキャナー コントロールのプロパティも含まれます。</p>
<p>イメージおよびドキュメントに固有のプロパティは、通常は含まれています。</p></td>
<td><p>バック ページのドキュメントを表す WIA フィーダー項目。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FEEDER_FRONT</p></td>
<td><p>フィーダー スキャナー コントロールのプロパティも含まれます。</p>
<p>イメージおよびドキュメントに固有のプロパティは、通常は含まれています。</p></td>
<td><p>ドキュメントの最初のページを表す WIA フィーダー項目。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_FILM</p></td>
<td><p>フィルム スキャナー コントロールのプロパティも含まれます。</p>
<p>イメージおよびドキュメントに固有のプロパティは、通常は含まれています。</p></td>
<td><p>スキャンの個々 のフレームを表す子項目を含む、WIA フィルム項目。</p>
<p>ただし、子項目を含めることはできません、 <strong>WiaItemTypeFolder</strong>フラグ。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FINISHED_FILE</p></td>
<td><p>プロパティは、報告されている項目の種類によって異なります。 たとえば、 <strong>WiaItemTypeImage</strong>ピクセルあたりのビット数など、いくつかの画像アイテム プロパティがあります。</p></td>
<td><p>完成したファイルの内容を表す子項目を含む、WIA ストレージ項目 (つまり、データがファイルなど<em>.jpg</em>、 <em>.htm</em>、および<em>.txt</em>ファイル)。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_FLATBED</p></td>
<td><p>フラット ベッド スキャナー コントロールのプロパティも含まれます。</p>
<p>イメージおよびドキュメントに固有のプロパティは、通常は含まれています。</p></td>
<td><p>スキャナーのフラット ベッドからプラテン上でスキャンが実行されているリージョンを表す子項目を含む、WIA ベッド項目。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FOLDER</p></td>
<td><p>プロパティには、フォルダーとデバイスの名前を付け、アクセス権、ドキュメントの処理、およびドキュメントの状態のものが含まれます。</p></td>
<td><p>記憶域ユニットを表す項目です。 ストレージのスキャナーは、のフォルダー スキャナーの少なくとも 1 つの項目が必要です。 この項目は、個々 のストレージの項目を表すサブフォルダー項目を指定できます。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_ROOT</p></td>
<td><p>プロパティには、デバイスの制御、名前、アクセス権、ドキュメントの処理、およびデバイスの種類のものが含まれます。</p></td>
<td><p>ルート項目のみです。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_AUTO</p></td>
<td><p>プロパティには、自動構成をスキャンするためのものが含まれます。 詳細については、次を参照してください。 <a href="https://docs.microsoft.com/windows-hardware/drivers/image/wia-properties-supported-by-an-auto-item" data-raw-source="[WIA Properties Supported by an Auto Item](https://docs.microsoft.com/windows-hardware/drivers/image/wia-properties-supported-by-an-auto-item)">WIA して自動アイテムのプロパティがサポートされている</a>します。</p></td>
<td><p>スキャナーのスキャン設定を自動構成を表す WIA 自動項目。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista およびそれ以降のバージョンのオペレーティング システムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_IPA\_項目\_フラグ**](wia-ipa-item-flags.md)

 

 






