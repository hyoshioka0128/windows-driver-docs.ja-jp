---
title: WIA ドライバー サービス ライブラリ
ms.assetid: c179483b-74c3-4788-aa04-20cec0e0eb3a
description: 特定のタスクの実行を支援するために、WIA ミニドライバーが呼び出すことができる関数を含む WIA ドライバーサービスライブラリについて説明します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aeb92a1e769e43bf3a2fe3fba91accf3699bbac8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840704"
---
# <a name="wia-driver-services-library"></a>WIA ドライバー サービス ライブラリ


WIA ドライバーサービスライブラリには、WIA ミニドライバーが次のタスクの実行を支援するために呼び出すことができる機能が含まれています。

-   [項目ツリーのビルドと保守](#ddk-building-and-maintaining-an-item-tree-si)
-   [エラーメッセージとトレースメッセージのログ記録](#ddk-logging-error-and-trace-messages-si)
-   [項目のプロパティの読み取りと格納](#ddk-reading-and-storing-an-item-s-properties-si)
-   [データの更新と転送](#ddk-updating-and-transferring-data-si)

WIA ミニドライバーは、必要に応じて、これらの関数のほとんどを[IWiaMiniDrv インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)メソッドから呼び出します。 ただし、各 WIA ミニドライバーは、 [**IWiaMiniDrv::D rvinitializewia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)メソッドの[**wiasCreateDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)関数を呼び出してドライバー項目を作成する必要があります。 **WiasCreateDrvItem**関数の呼び出しが成功するたびに、ミニドライバーの項目ツリーで使用される**IWiaDrvItem** item オブジェクトが作成されます。 いくつかの[IWiaDrvItem インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem)メソッドには、 [**IWiaDrvItem:: AddItemToFolder**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-additemtofolder)、 [**IWiaDrvItem:: GetFirstChildItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getfirstchilditem)、 [**IWiaDrvItem:: GetNextSiblingItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getnextsiblingitem)を[**含む IWiaDrvItem 型のパラメーターがあります。IWiaDrvItem:: GetParentItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getparentitem)。 また、 [**wiasGetDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetdrvitem)関数には、この型のパラメーターがあります。

ドライバーサービスライブラリには、次の機能が用意されています。

## <a href="" id="ddk-building-and-maintaining-an-item-tree-si"></a>項目ツリーのビルドと保守


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatechildappitem" data-raw-source="[&lt;strong&gt;wiasCreateChildAppItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatechildappitem)"><strong>wiasCreateChildAppItem</strong></a></p></td>
<td><p>新しいアプリケーション項目を作成し、指定した (親) 項目の子として挿入します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem" data-raw-source="[&lt;strong&gt;wiasCreateDrvItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)"><strong>wiasCreateDrvItem</strong></a></p></td>
<td><p><strong>IWiaDrvItem</strong>オブジェクトを作成します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchildrencontexts" data-raw-source="[&lt;strong&gt;wiasGetChildrenContexts&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchildrencontexts)"><strong>wiasGetChildrenContexts</strong></a></p></td>
<td><p>現在の項目の子に属している項目コンテキストの配列を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetcontextfromname" data-raw-source="[&lt;strong&gt;wiasGetContextFromName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetcontextfromname)"><strong>wiasGetContextFromName</strong></a></p></td>
<td><p>項目名の項目コンテキストを取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetdrvitem" data-raw-source="[&lt;strong&gt;wiasGetDrvItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetdrvitem)"><strong>wiasGetDrvItem</strong></a></p></td>
<td><p>ドライバー項目を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetrootitem" data-raw-source="[&lt;strong&gt;wiasGetRootItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetrootitem)"><strong>wiasGetRootItem</strong></a></p></td>
<td><p>指定された WIA 項目のルート項目コンテキストを取得します。</p></td>
</tr>
</tbody>
</table>

 

## <a href="" id="ddk-logging-error-and-trace-messages-si"></a>エラーメッセージとトレースメッセージのログ記録


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreateloginstance" data-raw-source="[&lt;strong&gt;wiasCreateLogInstance&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreateloginstance)"><strong>wiasCreateLogInstance</strong></a></p></td>
<td><p>ログオブジェクトのインスタンスを作成します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasdebugerror" data-raw-source="[&lt;strong&gt;wiasDebugError&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasdebugerror)"><strong>wiasDebugError</strong></a></p></td>
<td><p>デバッグエラー文字列をデバイスマネージャーデバッグコンソールに出力します。 出力色は常に赤です。 この関数は、互換性のためだけに用意されています。 Microsoft Windows XP では、代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_lerror" data-raw-source="[&lt;strong&gt;WIAS_LERROR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_lerror)"><strong>WIAS_LERROR</strong></a>を使用することをお勧めします。</p>
<p>Windows Vista では、代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_error" data-raw-source="[&lt;strong&gt;WIAS_ERROR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_error)"><strong>WIAS_ERROR</strong></a>を使用することをお勧めします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasdebugtrace" data-raw-source="[&lt;strong&gt;wiasDebugTrace&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasdebugtrace)"><strong>wiasDebugTrace</strong></a></p></td>
<td><p>デバッグトレース文字列をデバイスマネージャーデバッグコンソールに出力します。 この関数は、互換性のためだけに用意されています。 Microsoft Windows XP では、代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_ltrace" data-raw-source="[&lt;strong&gt;WIAS_LTRACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_ltrace)"><strong>WIAS_LTRACE</strong></a>を使用することをお勧めします。</p>
<p>Windows Vista では、代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_trace" data-raw-source="[&lt;strong&gt;WIA_TRACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_trace)"><strong>WIA_TRACE</strong></a>を使用することをお勧めします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasformatargs" data-raw-source="[&lt;strong&gt;wiasFormatArgs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasformatargs)"><strong>wiasFormatArgs</strong></a></p></td>
<td><p>引数リストを、ログ記録用のパッケージ化された文字列に書式設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasprintdebughresult" data-raw-source="[&lt;strong&gt;wiasPrintDebugHResult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasprintdebughresult)"><strong>wiasPrintDebugHResult</strong></a></p></td>
<td><p>デバイスマネージャーデバッグコンソールに HRESULT 文字列を出力します。 この関数は、互換性のためだけに用意されています。 Windows XP 以降では廃止されており、サポートされなくなりました。 代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_lhresult" data-raw-source="[&lt;strong&gt;WIAS_LHRESULT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_lhresult)"><strong>WIAS_LHRESULT</strong></a>を使用してください。</p></td>
</tr>
</tbody>
</table>

 

## <a href="" id="ddk-reading-and-storing-an-item-s-properties-si"></a>項目のプロパティの読み取りと格納


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatepropcontext" data-raw-source="[&lt;strong&gt;wiasCreatePropContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatepropcontext)"><strong>wiasCreatePropContext</strong></a></p></td>
<td><p>項目のどのプロパティが変更されているかを示すプロパティコンテキストを割り当てます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasfreepropcontext" data-raw-source="[&lt;strong&gt;wiasFreePropContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasfreepropcontext)"><strong>wiasFreePropContext</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_context" data-raw-source="[&lt;strong&gt;WIA_PROPERTY_CONTEXT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_context)"><strong>WIA_PROPERTY_CONTEXT</strong></a>構造体によって占有されているメモリを解放します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat" data-raw-source="[&lt;strong&gt;wiasGetChangedValueFloat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat)"><strong>wiasGetChangedValueFloat</strong></a></p></td>
<td><p>浮動小数点値を持つプロパティがアプリケーションによって変更されたかどうかを判断します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvalueguid" data-raw-source="[&lt;strong&gt;wiasGetChangedValueGuid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvalueguid)"><strong>Wiasgetのすべての属性</strong></a></p></td>
<td><p>GUID 値を持つプロパティがアプリケーションによって変更されたかどうかを判断します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluelong" data-raw-source="[&lt;strong&gt;wiasGetChangedValueLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluelong)"><strong>wiasGetChangedValueLong</strong></a></p></td>
<td><p>長整数値を持つプロパティがアプリケーションによって変更されたかどうかを判断します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluestr" data-raw-source="[&lt;strong&gt;wiasGetChangedValueStr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluestr)"><strong>wiasGetChangedValueStr</strong></a></p></td>
<td><p>文字列値を持つプロパティがアプリケーションによって変更されたかどうかを判断します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetitemtype" data-raw-source="[&lt;strong&gt;wiasGetItemType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetitemtype)"><strong>wiasGetItemType</strong></a></p></td>
<td><p>ルートまたは子項目を示します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetpropertyattributes" data-raw-source="[&lt;strong&gt;wiasGetPropertyAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetpropertyattributes)"><strong>wiasGetPropertyAttributes</strong></a></p></td>
<td><p>一連のプロパティのアクセスフラグと有効な値を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasispropchanged" data-raw-source="[&lt;strong&gt;wiasIsPropChanged&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasispropchanged)"><strong>wiasIsPropChanged</strong></a></p></td>
<td><p>指定されたプロパティがアプリケーションによって変更されたかどうかをテストします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadmultiple" data-raw-source="[&lt;strong&gt;wiasReadMultiple&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadmultiple)"><strong>wiasReadMultiple</strong></a></p></td>
<td><p>複数のプロパティを WIA 項目から読み取ります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropbin" data-raw-source="[&lt;strong&gt;wiasReadPropBin&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropbin)"><strong>wiasReadPropBin</strong></a></p></td>
<td><p>1つのバイナリプロパティを WIA 項目から読み取ります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropfloat" data-raw-source="[&lt;strong&gt;wiasReadPropFloat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropfloat)"><strong>wiasReadPropFloat</strong></a></p></td>
<td><p>WIA 項目から浮動小数点プロパティ値を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropguid" data-raw-source="[&lt;strong&gt;wiasReadPropGuid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropguid)"><strong>wiasReadPropGuid</strong></a></p></td>
<td><p>WIA 項目から GUID プロパティ値を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadproplong" data-raw-source="[&lt;strong&gt;wiasReadPropLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadproplong)"><strong>wiasReadPropLong p)</strong></a></p></td>
<td><p>WIA 項目から長整数型のプロパティ値を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropstr" data-raw-source="[&lt;strong&gt;wiasReadPropStr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadpropstr)"><strong>wiasReadPropStr</strong></a></p></td>
<td><p>WIA 項目から文字列プロパティ値を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetitempropattribs" data-raw-source="[&lt;strong&gt;wiasSetItemPropAttribs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetitempropattribs)"><strong>wiasSetItemPropAttribs</strong></a></p></td>
<td><p>項目のプロパティセットのアクセスフラグと有効な値を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetitempropnames" data-raw-source="[&lt;strong&gt;wiasSetItemPropNames&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetitempropnames)"><strong>wiasSetItemPropNames</strong></a></p></td>
<td><p>プロパティ名を項目プロパティに書き込みます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetpropchanged" data-raw-source="[&lt;strong&gt;wiasSetPropChanged&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetpropchanged)"><strong>wiasSetPropChanged</strong></a></p></td>
<td><p>プロパティが変更されていることを示すために、プロパティコンテキストを変更します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetpropertyattributes" data-raw-source="[&lt;strong&gt;wiasSetPropertyAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetpropertyattributes)"><strong>wiasSetPropertyAttributes</strong></a></p></td>
<td><p>項目のプロパティのアクセスフラグとプロパティ値を設定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidflag" data-raw-source="[&lt;strong&gt;wiasSetValidFlag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidflag)"><strong>wiasSetValidFlag</strong></a></p></td>
<td><p>WIA_PROP_FLAG プロパティの有効な値を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidlistfloat" data-raw-source="[&lt;strong&gt;wiasSetValidListFloat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidlistfloat)"><strong>wiasSetValidListFloat</strong></a></p></td>
<td><p>VT_R4 型の WIA_PROP_LIST プロパティに有効な値を設定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidlistguid" data-raw-source="[&lt;strong&gt;wiasSetValidListGuid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidlistguid)"><strong>wiasSetValidListGuid</strong></a></p></td>
<td><p>Subtype VT_CLSID の WIA_PROP_LIST プロパティに有効な値を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidlistlong" data-raw-source="[&lt;strong&gt;wiasSetValidListLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidlistlong)"><strong>wiasSetValidListLong</strong></a></p></td>
<td><p>VT_I4 型の WIA_PROP_LIST プロパティに有効な値を設定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidliststr" data-raw-source="[&lt;strong&gt;wiasSetValidListStr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidliststr)"><strong>wiasSetValidListStr</strong></a></p></td>
<td><p>VT_BSTR 型の WIA_PROP_LIST プロパティに有効な値を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidrangefloat" data-raw-source="[&lt;strong&gt;wiasSetValidRangeFloat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidrangefloat)"><strong>wiasSetValidRangeFloat</strong></a></p></td>
<td><p>Subtype VT_R4 の WIA_PROP_RANGE プロパティに有効な値の範囲を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidrangelong" data-raw-source="[&lt;strong&gt;wiasSetValidRangeLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassetvalidrangelong)"><strong>wiasSetValidRangeLong</strong></a></p></td>
<td><p>Subtype VT_I4 の WIA_PROP_RANGE プロパティに有効な値の範囲を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasupdatevalidformat" data-raw-source="[&lt;strong&gt;wiasUpdateValidFormat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasupdatevalidformat)"><strong>wiasUpdateValidFormat</strong></a></p></td>
<td><p>現在のミニドライバーのプロパティコンテキストの有効な形式を更新します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasvalidateitemproperties" data-raw-source="[&lt;strong&gt;wiasValidateItemProperties&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasvalidateitemproperties)"><strong>wiasValidateItemProperties</strong></a></p></td>
<td><p>単純な項目のプロパティのリストを現在の有効な値と照合して検証します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritemultiple" data-raw-source="[&lt;strong&gt;wiasWriteMultiple&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritemultiple)"><strong>wiasWriteMultiple</strong></a></p></td>
<td><p>複数のプロパティ値を WIA 項目に書き込みます (プロパティの型は異なる場合があります)。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropbin" data-raw-source="[&lt;strong&gt;wiasWritePropBin&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropbin)"><strong>wiasWritePropBin</strong></a></p></td>
<td><p>1つのバイナリプロパティ値を WIA 項目に書き込みます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropfloat" data-raw-source="[&lt;strong&gt;wiasWritePropFloat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropfloat)"><strong>wiasWritePropFloat</strong></a></p></td>
<td><p>浮動小数点プロパティ値を WIA 項目に書き込みます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropguid" data-raw-source="[&lt;strong&gt;wiasWritePropGuid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropguid)"><strong>wiasWritePropGuid</strong></a></p></td>
<td><p>WIA 項目に GUID プロパティ値を書き込みます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswriteproplong" data-raw-source="[&lt;strong&gt;wiasWritePropLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswriteproplong)"><strong>wiasWritePropLong p)</strong></a></p></td>
<td><p>Long 整数プロパティ値を WIA 項目に書き込みます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropstr" data-raw-source="[&lt;strong&gt;wiasWritePropStr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepropstr)"><strong>wiasWritePropStr</strong></a></p></td>
<td><p>文字列プロパティ値を WIA 項目に書き込みます。</p></td>
</tr>
</tbody>
</table>

 

## <a href="" id="ddk-updating-and-transferring-data-si"></a>データの更新と転送


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasdownsamplebuffer" data-raw-source="[&lt;strong&gt;wiasDownSampleBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasdownsamplebuffer)"><strong>wiasDownSampleBuffer</strong></a></p></td>
<td><p>は、ピクセルデータのバッファーを取得し、指定されたサイズに downsamples します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetimageinformation" data-raw-source="[&lt;strong&gt;wiasGetImageInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetimageinformation)"><strong>wiasGetImageInformation</strong></a></p></td>
<td><p>項目から転送コンテキスト情報を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasparseendorserstring" data-raw-source="[&lt;strong&gt;wiasParseEndorserString&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasparseendorserstring)"><strong>wiasParseEndorserString</strong></a></p></td>
<td><p>文字列内の WIA サービスで定義されたトークンとベンダーが定義したトークンを、トークンに関連付けられている値に置き換えて、裏書き文字列を解析します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassendendofpage" data-raw-source="[&lt;strong&gt;wiasSendEndOfPage&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassendendofpage)"><strong>wiasSendEndOfPage</strong></a></p></td>
<td><p>データ転送中に、現在の合計ページ数を送信するクライアントコールバックルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasupdatescanrect" data-raw-source="[&lt;strong&gt;wiasUpdateScanRect&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasupdatescanrect)"><strong>Wiasアップデート Canrect</strong></a></p></td>
<td><p>スキャンデバイスのスキャン領域のサイズを更新します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritebuftofile" data-raw-source="[&lt;strong&gt;wiasWriteBufToFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritebuftofile)"><strong>wiasWriteBufToFile</strong></a></p></td>
<td><p>一時ページバッファーの内容をイメージファイルに書き込みます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepagebuftofile" data-raw-source="[&lt;strong&gt;wiasWritePageBufToFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepagebuftofile)"><strong>wiasWritePageBufToFile</strong></a></p></td>
<td><p>一時ページバッファーの内容をイメージファイルに書き込みます。 マルチページ TIFF ファイルにページを書き込むには、この関数を使用します。</p></td>
</tr>
</tbody>
</table>

 

 

 




