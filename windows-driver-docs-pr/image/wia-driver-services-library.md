---
title: WIA ドライバー サービス ライブラリ
ms.assetid: c179483b-74c3-4788-aa04-20cec0e0eb3a
description: WIA ミニドライバーが特定のタスクを実行するときにアシスタンスを呼び出すことができます関数を含む WIA ドライバー サービス ライブラリについて説明します
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ec4f2411140ffd27072ac9d481ae9dbf16600ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383754"
---
# <a name="wia-driver-services-library"></a>WIA ドライバー サービス ライブラリ


WIA ドライバー サービスのライブラリには、次のタスクの実行についての支援、WIA ミニドライバーを呼び出すことができる関数が含まれています。

-   [構築して、項目のツリーを維持](#ddk-building-and-maintaining-an-item-tree-si)
-   [エラーのログ記録とトレース メッセージ](#ddk-logging-error-and-trace-messages-si)
-   [読み取りと、アイテムのプロパティを格納します。](#ddk-reading-and-storing-an-item-s-properties-si)
-   [更新およびデータを転送します。](#ddk-updating-and-transferring-data-si)

WIA ミニドライバーからこれらの関数のほとんどを呼び出してその[IWiaMiniDrv インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)メソッドに応じて。 ただし、各 WIA ミニドライバーを呼び出す必要があります、 [ **wiasCreateDrvItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatedrvitem)で機能、 [ **IWiaMiniDrv::drvInitializeWia** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)メソッドドライバーの項目を作成します。 呼び出しが成功した、 **wiasCreateDrvItem**関数を作成、 **IWiaDrvItem**ミニドライバーの項目のツリーで使用されている項目オブジェクト。 いくつか[IWiaDrvItem インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem)メソッドは、型のパラメーターを持つ**IWiaDrvItem**など、 [ **IWiaDrvItem::AddItemToFolder** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-additemtofolder)、 [ **IWiaDrvItem::GetFirstChildItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getfirstchilditem)、 [ **IWiaDrvItem::GetNextSiblingItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getnextsiblingitem)、および[ **IWiaDrvItem::GetParentItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getparentitem)します。 また、 [ **wiasGetDrvItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetdrvitem)関数には、この型のパラメーター。

ドライバーのサービス ライブラリでは、次の機能を提供します。

## <a href="" id="ddk-building-and-maintaining-an-item-tree-si"></a>構築して、項目のツリーを維持


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatechildappitem" data-raw-source="[&lt;strong&gt;wiasCreateChildAppItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatechildappitem)"><strong>wiasCreateChildAppItem</strong></a></p></td>
<td><p>新しいアプリケーション項目を作成し、(親) の指定した項目の子として挿入します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatedrvitem" data-raw-source="[&lt;strong&gt;wiasCreateDrvItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatedrvitem)"><strong>wiasCreateDrvItem</strong></a></p></td>
<td><p>作成、 <strong>IWiaDrvItem</strong>オブジェクト。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchildrencontexts" data-raw-source="[&lt;strong&gt;wiasGetChildrenContexts&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchildrencontexts)"><strong>wiasGetChildrenContexts</strong></a></p></td>
<td><p>現在の項目の子に属しているアイテムのコンテキストの配列を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetcontextfromname" data-raw-source="[&lt;strong&gt;wiasGetContextFromName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetcontextfromname)"><strong>wiasGetContextFromName</strong></a></p></td>
<td><p>アイテムの名前のアイテムのコンテキストを取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetdrvitem" data-raw-source="[&lt;strong&gt;wiasGetDrvItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetdrvitem)"><strong>wiasGetDrvItem</strong></a></p></td>
<td><p>ドライバーの項目を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetrootitem" data-raw-source="[&lt;strong&gt;wiasGetRootItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetrootitem)"><strong>wiasGetRootItem</strong></a></p></td>
<td><p>指定した WIA 項目のルート項目のコンテキストを取得します。</p></td>
</tr>
</tbody>
</table>

 

## <a href="" id="ddk-logging-error-and-trace-messages-si"></a>エラーのログ記録とトレース メッセージ


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreateloginstance" data-raw-source="[&lt;strong&gt;wiasCreateLogInstance&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreateloginstance)"><strong>wiasCreateLogInstance</strong></a></p></td>
<td><p>ログ オブジェクトのインスタンスを作成します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasdebugerror" data-raw-source="[&lt;strong&gt;wiasDebugError&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasdebugerror)"><strong>wiasDebugError</strong></a></p></td>
<td><p>デバイス マネージャーのデバッグ コンソールでのデバッグ エラー文字列を出力します。 出力の色が赤では常にします。 この関数は、互換性のためだけに提供されます。 使用する Microsoft Windows xp では、推奨は<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_lerror" data-raw-source="[&lt;strong&gt;WIAS_LERROR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_lerror)"> <strong>WIAS_LERROR</strong> </a>代わりにします。</p>
<p>Windows Vista で使用する推奨が<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_error" data-raw-source="[&lt;strong&gt;WIAS_ERROR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_error)"> <strong>WIAS_ERROR</strong> </a>代わりにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasdebugtrace" data-raw-source="[&lt;strong&gt;wiasDebugTrace&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasdebugtrace)"><strong>wiasDebugTrace</strong></a></p></td>
<td><p>デバイス マネージャーのデバッグ コンソールでのデバッグ トレース文字列を出力します。 この関数は、互換性のためだけに提供されます。 使用する Microsoft Windows xp では、推奨は<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_ltrace" data-raw-source="[&lt;strong&gt;WIAS_LTRACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_ltrace)"> <strong>WIAS_LTRACE</strong> </a>代わりにします。</p>
<p>Windows Vista で使用する推奨が<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_trace" data-raw-source="[&lt;strong&gt;WIA_TRACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_trace)"> <strong>WIA_TRACE</strong> </a>代わりにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasformatargs" data-raw-source="[&lt;strong&gt;wiasFormatArgs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasformatargs)"><strong>wiasFormatArgs</strong></a></p></td>
<td><p>ログ記録用のパッケージ化された文字列に引数リストを書式設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasprintdebughresult" data-raw-source="[&lt;strong&gt;wiasPrintDebugHResult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasprintdebughresult)"><strong>wiasPrintDebugHResult</strong></a></p></td>
<td><p>デバイス マネージャーのデバッグ コンソールで、HRESULT の文字列を出力します。 この関数は、互換性のためだけに提供されます。 古い Windows xp 以降と、現在サポートされていません。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_lhresult" data-raw-source="[&lt;strong&gt;WIAS_LHRESULT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_lhresult)"> <strong>WIAS_LHRESULT</strong> </a>代わりにします。</p></td>
</tr>
</tbody>
</table>

 

## <a href="" id="ddk-reading-and-storing-an-item-s-properties-si"></a>読み取りと、アイテムのプロパティを格納します。


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatepropcontext" data-raw-source="[&lt;strong&gt;wiasCreatePropContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatepropcontext)"><strong>wiasCreatePropContext</strong></a></p></td>
<td><p>アイテムのプロパティの変更を示すプロパティのコンテキストを割り当てます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasfreepropcontext" data-raw-source="[&lt;strong&gt;wiasFreePropContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasfreepropcontext)"><strong>wiasFreePropContext</strong></a></p></td>
<td><p>によって占有されているメモリを解放する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/ns-wiamindr_lh-_wia_property_context" data-raw-source="[&lt;strong&gt;WIA_PROPERTY_CONTEXT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/ns-wiamindr_lh-_wia_property_context)"> <strong>WIA_PROPERTY_CONTEXT</strong> </a>構造体。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat" data-raw-source="[&lt;strong&gt;wiasGetChangedValueFloat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat)"><strong>wiasGetChangedValueFloat</strong></a></p></td>
<td><p>アプリケーションで浮動小数点値を持つプロパティが変更されたかどうかを判断します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvalueguid" data-raw-source="[&lt;strong&gt;wiasGetChangedValueGuid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvalueguid)"><strong>wiasGetChangedValueGuid</strong></a></p></td>
<td><p>アプリケーションが GUID 値を持つプロパティが変更されたかどうかを判断します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluelong" data-raw-source="[&lt;strong&gt;wiasGetChangedValueLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluelong)"><strong>wiasGetChangedValueLong</strong></a></p></td>
<td><p>長整数値を持つプロパティがアプリケーションによって変更されたかどうかを判断します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluestr" data-raw-source="[&lt;strong&gt;wiasGetChangedValueStr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluestr)"><strong>wiasGetChangedValueStr</strong></a></p></td>
<td><p>アプリケーションで文字列値を持つプロパティが変更されたかどうかを判断します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetitemtype" data-raw-source="[&lt;strong&gt;wiasGetItemType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetitemtype)"><strong>wiasGetItemType</strong></a></p></td>
<td><p>ルートまたは子項目を示します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetpropertyattributes" data-raw-source="[&lt;strong&gt;wiasGetPropertyAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetpropertyattributes)"><strong>wiasGetPropertyAttributes</strong></a></p></td>
<td><p>アクセス フラグと一連のプロパティの有効な値を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasispropchanged" data-raw-source="[&lt;strong&gt;wiasIsPropChanged&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasispropchanged)"><strong>wiasIsPropChanged</strong></a></p></td>
<td><p>指定したプロパティは、アプリケーションによって変更されたかどうかをテストします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadmultiple" data-raw-source="[&lt;strong&gt;wiasReadMultiple&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadmultiple)"><strong>wiasReadMultiple</strong></a></p></td>
<td><p>WIA 項目から複数のプロパティを読み取ります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadpropbin" data-raw-source="[&lt;strong&gt;wiasReadPropBin&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadpropbin)"><strong>wiasReadPropBin</strong></a></p></td>
<td><p>WIA 項目から 1 つのバイナリ プロパティを読み取ります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadpropfloat" data-raw-source="[&lt;strong&gt;wiasReadPropFloat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadpropfloat)"><strong>wiasReadPropFloat</strong></a></p></td>
<td><p>WIA 項目から浮動小数点のプロパティ値を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadpropguid" data-raw-source="[&lt;strong&gt;wiasReadPropGuid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadpropguid)"><strong>wiasReadPropGuid</strong></a></p></td>
<td><p>WIA 項目からプロパティの GUID 値を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadproplong" data-raw-source="[&lt;strong&gt;wiasReadPropLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadproplong)"><strong>wiasReadPropLong</strong></a></p></td>
<td><p>WIA 項目から長整数のプロパティ値を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadpropstr" data-raw-source="[&lt;strong&gt;wiasReadPropStr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadpropstr)"><strong>wiasReadPropStr</strong></a></p></td>
<td><p>WIA 項目からの文字列プロパティの値を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetitempropattribs" data-raw-source="[&lt;strong&gt;wiasSetItemPropAttribs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetitempropattribs)"><strong>wiasSetItemPropAttribs</strong></a></p></td>
<td><p>アクセス フラグと項目の一連のプロパティの有効な値を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetitempropnames" data-raw-source="[&lt;strong&gt;wiasSetItemPropNames&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetitempropnames)"><strong>wiasSetItemPropNames</strong></a></p></td>
<td><p>項目のプロパティをプロパティ名を書き込みます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetpropchanged" data-raw-source="[&lt;strong&gt;wiasSetPropChanged&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetpropchanged)"><strong>wiasSetPropChanged</strong></a></p></td>
<td><p>プロパティが変更されていることを示すプロパティのコンテキストを変更します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetpropertyattributes" data-raw-source="[&lt;strong&gt;wiasSetPropertyAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetpropertyattributes)"><strong>wiasSetPropertyAttributes</strong></a></p></td>
<td><p>アクセス フラグとアイテムのプロパティのプロパティ値を設定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidflag" data-raw-source="[&lt;strong&gt;wiasSetValidFlag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidflag)"><strong>wiasSetValidFlag</strong></a></p></td>
<td><p>WIA_PROP_FLAG プロパティの有効な値を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidlistfloat" data-raw-source="[&lt;strong&gt;wiasSetValidListFloat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidlistfloat)"><strong>wiasSetValidListFloat</strong></a></p></td>
<td><p>型のサブ VT_R4 WIA_PROP_LIST プロパティの有効な値を設定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidlistguid" data-raw-source="[&lt;strong&gt;wiasSetValidListGuid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidlistguid)"><strong>wiasSetValidListGuid</strong></a></p></td>
<td><p>サブタイプ VT_CLSID の WIA_PROP_LIST プロパティの有効な値を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidlistlong" data-raw-source="[&lt;strong&gt;wiasSetValidListLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidlistlong)"><strong>wiasSetValidListLong</strong></a></p></td>
<td><p>型のサブ VT_I4 WIA_PROP_LIST プロパティの有効な値を設定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidliststr" data-raw-source="[&lt;strong&gt;wiasSetValidListStr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidliststr)"><strong>wiasSetValidListStr</strong></a></p></td>
<td><p>型のサブ VT_BSTR WIA_PROP_LIST プロパティの有効な値を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidrangefloat" data-raw-source="[&lt;strong&gt;wiasSetValidRangeFloat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidrangefloat)"><strong>wiasSetValidRangeFloat</strong></a></p></td>
<td><p>サブタイプ VT_R4 の WIA_PROP_RANGE プロパティの有効な値の範囲を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidrangelong" data-raw-source="[&lt;strong&gt;wiasSetValidRangeLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassetvalidrangelong)"><strong>wiasSetValidRangeLong</strong></a></p></td>
<td><p>サブタイプ VT_I4 の WIA_PROP_RANGE プロパティの有効な値の範囲を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasupdatevalidformat" data-raw-source="[&lt;strong&gt;wiasUpdateValidFormat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasupdatevalidformat)"><strong>wiasUpdateValidFormat</strong></a></p></td>
<td><p>現在のミニドライバーのプロパティのコンテキストの有効な形式を更新します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasvalidateitemproperties" data-raw-source="[&lt;strong&gt;wiasValidateItemProperties&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasvalidateitemproperties)"><strong>wiasValidateItemProperties</strong></a></p></td>
<td><p>現在、有効な値に対して単純なアイテムのプロパティの一覧を検証します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritemultiple" data-raw-source="[&lt;strong&gt;wiasWriteMultiple&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritemultiple)"><strong>wiasWriteMultiple</strong></a></p></td>
<td><p>(さまざまな種類のプロパティがある可能性があります)、WIA 項目には、複数のプロパティ値を書き込みます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepropbin" data-raw-source="[&lt;strong&gt;wiasWritePropBin&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepropbin)"><strong>wiasWritePropBin</strong></a></p></td>
<td><p>WIA 項目に 1 つのバイナリ プロパティの値を書き込みます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepropfloat" data-raw-source="[&lt;strong&gt;wiasWritePropFloat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepropfloat)"><strong>wiasWritePropFloat</strong></a></p></td>
<td><p>WIA 項目には、浮動小数点のプロパティ値を書き込みます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepropguid" data-raw-source="[&lt;strong&gt;wiasWritePropGuid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepropguid)"><strong>wiasWritePropGuid</strong></a></p></td>
<td><p>WIA 項目に GUID プロパティ値を書き込みます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswriteproplong" data-raw-source="[&lt;strong&gt;wiasWritePropLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswriteproplong)"><strong>wiasWritePropLong</strong></a></p></td>
<td><p>WIA 項目には、長整数のプロパティ値を書き込みます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepropstr" data-raw-source="[&lt;strong&gt;wiasWritePropStr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepropstr)"><strong>wiasWritePropStr</strong></a></p></td>
<td><p>WIA 項目には、文字列プロパティの値を書き込みます。</p></td>
</tr>
</tbody>
</table>

 

## <a href="" id="ddk-updating-and-transferring-data-si"></a>更新およびデータを転送します。


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasdownsamplebuffer" data-raw-source="[&lt;strong&gt;wiasDownSampleBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasdownsamplebuffer)"><strong>wiasDownSampleBuffer</strong></a></p></td>
<td><p>バッファーのピクセル データのダウン サンプルにこれを指定されたサイズ。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetimageinformation" data-raw-source="[&lt;strong&gt;wiasGetImageInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetimageinformation)"><strong>wiasGetImageInformation</strong></a></p></td>
<td><p>アイテムのコンテキスト情報が転送を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasparseendorserstring" data-raw-source="[&lt;strong&gt;wiasParseEndorserString&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasparseendorserstring)"><strong>wiasParseEndorserString</strong></a></p></td>
<td><p>WIA がサービス定義、および文字列内のベンダー定義トークン、トークンに関連付けられている値に置き換えて、裏書き文字列を解析します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassendendofpage" data-raw-source="[&lt;strong&gt;wiasSendEndOfPage&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassendendofpage)"><strong>wiasSendEndOfPage</strong></a></p></td>
<td><p>データ転送では、現在の合計ページ数を送信中に、クライアント コールバック ルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasupdatescanrect" data-raw-source="[&lt;strong&gt;wiasUpdateScanRect&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasupdatescanrect)"><strong>wiasUpdateScanRect</strong></a></p></td>
<td><p>スキャン デバイスのスキャンの領域のサイズを更新します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritebuftofile" data-raw-source="[&lt;strong&gt;wiasWriteBufToFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritebuftofile)"><strong>wiasWriteBufToFile</strong></a></p></td>
<td><p>画像ファイルへの一時的なページのバッファーの内容を書き込みます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepagebuftofile" data-raw-source="[&lt;strong&gt;wiasWritePageBufToFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepagebuftofile)"><strong>wiasWritePageBufToFile</strong></a></p></td>
<td><p>画像ファイルへの一時的なページのバッファーの内容を書き込みます。 複数ページの TIFF ファイルにページを作成するのにには、この関数を使用します。</p></td>
</tr>
</tbody>
</table>

 

 

 




