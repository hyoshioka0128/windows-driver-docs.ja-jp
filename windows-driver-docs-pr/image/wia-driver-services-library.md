---
title: WIA ドライバー サービス ライブラリ
ms.assetid: c179483b-74c3-4788-aa04-20cec0e0eb3a
description: WIA ミニドライバーが特定のタスクを実行するときにアシスタンスを呼び出すことができます関数を含む WIA ドライバー サービス ライブラリについて説明します
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c966aa0a8563ae0ab2b62a38a39a6660642b51c
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349435"
---
# <a name="wia-driver-services-library"></a>WIA ドライバー サービス ライブラリ


WIA ドライバー サービスのライブラリには、次のタスクの実行についての支援、WIA ミニドライバーを呼び出すことができる関数が含まれています。

-   [構築して、項目のツリーを維持](#ddk-building-and-maintaining-an-item-tree-si)
-   [エラーのログ記録とトレース メッセージ](#ddk-logging-error-and-trace-messages-si)
-   [読み取りと、アイテムのプロパティを格納します。](#ddk-reading-and-storing-an-item-s-properties-si)
-   [更新およびデータを転送します。](#ddk-updating-and-transferring-data-si)

WIA ミニドライバーからこれらの関数のほとんどを呼び出してその[IWiaMiniDrv インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff545027)メソッドに応じて。 ただし、各 WIA ミニドライバーを呼び出す必要があります、 [ **wiasCreateDrvItem** ](https://msdn.microsoft.com/library/windows/hardware/ff549160)で機能、 [ **IWiaMiniDrv::drvInitializeWia** ](https://msdn.microsoft.com/library/windows/hardware/ff544986)メソッドドライバーの項目を作成します。 呼び出しが成功した、 **wiasCreateDrvItem**関数を作成、 **IWiaDrvItem**ミニドライバーの項目のツリーで使用されている項目オブジェクト。 いくつか[IWiaDrvItem インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff543896)メソッドは、型のパラメーターを持つ**IWiaDrvItem**など、 [ **IWiaDrvItem::AddItemToFolder** ](https://msdn.microsoft.com/library/windows/hardware/ff543856)、 [ **IWiaDrvItem::GetFirstChildItem**](https://msdn.microsoft.com/library/windows/hardware/ff543878)、 [ **IWiaDrvItem::GetNextSiblingItem**](https://msdn.microsoft.com/library/windows/hardware/ff543889)、および[ **IWiaDrvItem::GetParentItem**](https://msdn.microsoft.com/library/windows/hardware/ff543892)します。 また、 [ **wiasGetDrvItem** ](https://msdn.microsoft.com/library/windows/hardware/ff549243)関数には、この型のパラメーター。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549156" data-raw-source="[&lt;strong&gt;wiasCreateChildAppItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549156)"><strong>wiasCreateChildAppItem</strong></a></p></td>
<td><p>新しいアプリケーション項目を作成し、(親) の指定した項目の子として挿入します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549160" data-raw-source="[&lt;strong&gt;wiasCreateDrvItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549160)"><strong>wiasCreateDrvItem</strong></a></p></td>
<td><p>作成、 <strong>IWiaDrvItem</strong>オブジェクト。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549224" data-raw-source="[&lt;strong&gt;wiasGetChildrenContexts&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549224)"><strong>wiasGetChildrenContexts</strong></a></p></td>
<td><p>現在の項目の子に属しているアイテムのコンテキストの配列を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549233" data-raw-source="[&lt;strong&gt;wiasGetContextFromName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549233)"><strong>wiasGetContextFromName</strong></a></p></td>
<td><p>アイテムの名前のアイテムのコンテキストを取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549243" data-raw-source="[&lt;strong&gt;wiasGetDrvItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549243)"><strong>wiasGetDrvItem</strong></a></p></td>
<td><p>ドライバーの項目を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549264" data-raw-source="[&lt;strong&gt;wiasGetRootItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549264)"><strong>wiasGetRootItem</strong></a></p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549163" data-raw-source="[&lt;strong&gt;wiasCreateLogInstance&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549163)"><strong>wiasCreateLogInstance</strong></a></p></td>
<td><p>ログ オブジェクトのインスタンスを作成します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549170" data-raw-source="[&lt;strong&gt;wiasDebugError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549170)"><strong>wiasDebugError</strong></a></p></td>
<td><p>デバイス マネージャーのデバッグ コンソールでのデバッグ エラー文字列を出力します。 出力の色が赤では常にします。 この関数は、互換性のためだけに提供されます。 使用する Microsoft Windows xp では、推奨は<a href="https://msdn.microsoft.com/library/windows/hardware/ff549580" data-raw-source="[&lt;strong&gt;WIAS_LERROR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549580)"> <strong>WIAS_LERROR</strong> </a>代わりにします。</p>
<p>Windows Vista で使用する推奨が<a href="https://msdn.microsoft.com/library/windows/hardware/ff549565" data-raw-source="[&lt;strong&gt;WIAS_ERROR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549565)"> <strong>WIAS_ERROR</strong> </a>代わりにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549178" data-raw-source="[&lt;strong&gt;wiasDebugTrace&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549178)"><strong>wiasDebugTrace</strong></a></p></td>
<td><p>デバイス マネージャーのデバッグ コンソールでのデバッグ トレース文字列を出力します。 この関数は、互換性のためだけに提供されます。 使用する Microsoft Windows xp では、推奨は<a href="https://msdn.microsoft.com/library/windows/hardware/ff549600" data-raw-source="[&lt;strong&gt;WIAS_LTRACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549600)"> <strong>WIAS_LTRACE</strong> </a>代わりにします。</p>
<p>Windows Vista で使用する推奨が<a href="https://msdn.microsoft.com/library/windows/hardware/ff549619" data-raw-source="[&lt;strong&gt;WIA_TRACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549619)"> <strong>WIA_TRACE</strong> </a>代わりにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549190" data-raw-source="[&lt;strong&gt;wiasFormatArgs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549190)"><strong>wiasFormatArgs</strong></a></p></td>
<td><p>ログ記録用のパッケージ化された文字列に引数リストを書式設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549287" data-raw-source="[&lt;strong&gt;wiasPrintDebugHResult&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549287)"><strong>wiasPrintDebugHResult</strong></a></p></td>
<td><p>デバイス マネージャーのデバッグ コンソールで、HRESULT の文字列を出力します。 この関数は、互換性のためだけに提供されます。 古い Windows xp 以降と、現在サポートされていません。 使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff549589" data-raw-source="[&lt;strong&gt;WIAS_LHRESULT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549589)"> <strong>WIAS_LHRESULT</strong> </a>代わりにします。</p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549167" data-raw-source="[&lt;strong&gt;wiasCreatePropContext&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549167)"><strong>wiasCreatePropContext</strong></a></p></td>
<td><p>アイテムのプロパティの変更を示すプロパティのコンテキストを割り当てます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549195" data-raw-source="[&lt;strong&gt;wiasFreePropContext&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549195)"><strong>wiasFreePropContext</strong></a></p></td>
<td><p>によって占有されているメモリを解放する<a href="https://msdn.microsoft.com/library/windows/hardware/ff552749" data-raw-source="[&lt;strong&gt;WIA_PROPERTY_CONTEXT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552749)"> <strong>WIA_PROPERTY_CONTEXT</strong> </a>構造体。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549200" data-raw-source="[&lt;strong&gt;wiasGetChangedValueFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549200)"><strong>wiasGetChangedValueFloat</strong></a></p></td>
<td><p>アプリケーションで浮動小数点値を持つプロパティが変更されたかどうかを判断します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549211" data-raw-source="[&lt;strong&gt;wiasGetChangedValueGuid&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549211)"><strong>wiasGetChangedValueGuid</strong></a></p></td>
<td><p>アプリケーションが GUID 値を持つプロパティが変更されたかどうかを判断します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549214" data-raw-source="[&lt;strong&gt;wiasGetChangedValueLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549214)"><strong>wiasGetChangedValueLong</strong></a></p></td>
<td><p>長整数値を持つプロパティがアプリケーションによって変更されたかどうかを判断します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549219" data-raw-source="[&lt;strong&gt;wiasGetChangedValueStr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549219)"><strong>wiasGetChangedValueStr</strong></a></p></td>
<td><p>アプリケーションで文字列値を持つプロパティが変更されたかどうかを判断します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549255" data-raw-source="[&lt;strong&gt;wiasGetItemType&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549255)"><strong>wiasGetItemType</strong></a></p></td>
<td><p>ルートまたは子項目を示します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549257" data-raw-source="[&lt;strong&gt;wiasGetPropertyAttributes&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549257)"><strong>wiasGetPropertyAttributes</strong></a></p></td>
<td><p>アクセス フラグと一連のプロパティの有効な値を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549271" data-raw-source="[&lt;strong&gt;wiasIsPropChanged&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549271)"><strong>wiasIsPropChanged</strong></a></p></td>
<td><p>指定したプロパティは、アプリケーションによって変更されたかどうかをテストします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549300" data-raw-source="[&lt;strong&gt;wiasReadMultiple&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549300)"><strong>wiasReadMultiple</strong></a></p></td>
<td><p>WIA 項目から複数のプロパティを読み取ります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549308" data-raw-source="[&lt;strong&gt;wiasReadPropBin&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549308)"><strong>wiasReadPropBin</strong></a></p></td>
<td><p>WIA 項目から 1 つのバイナリ プロパティを読み取ります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549320" data-raw-source="[&lt;strong&gt;wiasReadPropFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549320)"><strong>wiasReadPropFloat</strong></a></p></td>
<td><p>WIA 項目から浮動小数点のプロパティ値を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549325" data-raw-source="[&lt;strong&gt;wiasReadPropGuid&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549325)"><strong>wiasReadPropGuid</strong></a></p></td>
<td><p>WIA 項目からプロパティの GUID 値を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549330" data-raw-source="[&lt;strong&gt;wiasReadPropLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549330)"><strong>wiasReadPropLong</strong></a></p></td>
<td><p>WIA 項目から長整数のプロパティ値を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549341" data-raw-source="[&lt;strong&gt;wiasReadPropStr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549341)"><strong>wiasReadPropStr</strong></a></p></td>
<td><p>WIA 項目からの文字列プロパティの値を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549358" data-raw-source="[&lt;strong&gt;wiasSetItemPropAttribs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549358)"><strong>wiasSetItemPropAttribs</strong></a></p></td>
<td><p>アクセス フラグと項目の一連のプロパティの有効な値を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549369" data-raw-source="[&lt;strong&gt;wiasSetItemPropNames&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549369)"><strong>wiasSetItemPropNames</strong></a></p></td>
<td><p>項目のプロパティをプロパティ名を書き込みます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549374" data-raw-source="[&lt;strong&gt;wiasSetPropChanged&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549374)"><strong>wiasSetPropChanged</strong></a></p></td>
<td><p>プロパティが変更されていることを示すプロパティのコンテキストを変更します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549381" data-raw-source="[&lt;strong&gt;wiasSetPropertyAttributes&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549381)"><strong>wiasSetPropertyAttributes</strong></a></p></td>
<td><p>アクセス フラグとアイテムのプロパティのプロパティ値を設定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549390" data-raw-source="[&lt;strong&gt;wiasSetValidFlag&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549390)"><strong>wiasSetValidFlag</strong></a></p></td>
<td><p>WIA_PROP_FLAG プロパティの有効な値を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549399" data-raw-source="[&lt;strong&gt;wiasSetValidListFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549399)"><strong>wiasSetValidListFloat</strong></a></p></td>
<td><p>型のサブ VT_R4 WIA_PROP_LIST プロパティの有効な値を設定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549409" data-raw-source="[&lt;strong&gt;wiasSetValidListGuid&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549409)"><strong>wiasSetValidListGuid</strong></a></p></td>
<td><p>サブタイプ VT_CLSID の WIA_PROP_LIST プロパティの有効な値を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549414" data-raw-source="[&lt;strong&gt;wiasSetValidListLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549414)"><strong>wiasSetValidListLong</strong></a></p></td>
<td><p>型のサブ VT_I4 WIA_PROP_LIST プロパティの有効な値を設定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549421" data-raw-source="[&lt;strong&gt;wiasSetValidListStr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549421)"><strong>wiasSetValidListStr</strong></a></p></td>
<td><p>型のサブ VT_BSTR WIA_PROP_LIST プロパティの有効な値を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549425" data-raw-source="[&lt;strong&gt;wiasSetValidRangeFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549425)"><strong>wiasSetValidRangeFloat</strong></a></p></td>
<td><p>サブタイプ VT_R4 の WIA_PROP_RANGE プロパティの有効な値の範囲を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549434" data-raw-source="[&lt;strong&gt;wiasSetValidRangeLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549434)"><strong>wiasSetValidRangeLong</strong></a></p></td>
<td><p>サブタイプ VT_I4 の WIA_PROP_RANGE プロパティの有効な値の範囲を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549448" data-raw-source="[&lt;strong&gt;wiasUpdateValidFormat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549448)"><strong>wiasUpdateValidFormat</strong></a></p></td>
<td><p>現在のミニドライバーのプロパティのコンテキストの有効な形式を更新します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549454" data-raw-source="[&lt;strong&gt;wiasValidateItemProperties&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549454)"><strong>wiasValidateItemProperties</strong></a></p></td>
<td><p>現在、有効な値に対して単純なアイテムのプロパティの一覧を検証します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549475" data-raw-source="[&lt;strong&gt;wiasWriteMultiple&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549475)"><strong>wiasWriteMultiple</strong></a></p></td>
<td><p>(さまざまな種類のプロパティがある可能性があります)、WIA 項目には、複数のプロパティ値を書き込みます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549500" data-raw-source="[&lt;strong&gt;wiasWritePropBin&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549500)"><strong>wiasWritePropBin</strong></a></p></td>
<td><p>WIA 項目に 1 つのバイナリ プロパティの値を書き込みます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549507" data-raw-source="[&lt;strong&gt;wiasWritePropFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549507)"><strong>wiasWritePropFloat</strong></a></p></td>
<td><p>WIA 項目には、浮動小数点のプロパティ値を書き込みます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549512" data-raw-source="[&lt;strong&gt;wiasWritePropGuid&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549512)"><strong>wiasWritePropGuid</strong></a></p></td>
<td><p>WIA 項目に GUID プロパティ値を書き込みます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549515" data-raw-source="[&lt;strong&gt;wiasWritePropLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549515)"><strong>wiasWritePropLong</strong></a></p></td>
<td><p>WIA 項目には、長整数のプロパティ値を書き込みます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549525" data-raw-source="[&lt;strong&gt;wiasWritePropStr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549525)"><strong>wiasWritePropStr</strong></a></p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549185" data-raw-source="[&lt;strong&gt;wiasDownSampleBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549185)"><strong>wiasDownSampleBuffer</strong></a></p></td>
<td><p>バッファーのピクセル データのダウン サンプルにこれを指定されたサイズ。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549249" data-raw-source="[&lt;strong&gt;wiasGetImageInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549249)"><strong>wiasGetImageInformation</strong></a></p></td>
<td><p>アイテムのコンテキスト情報が転送を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549282" data-raw-source="[&lt;strong&gt;wiasParseEndorserString&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549282)"><strong>wiasParseEndorserString</strong></a></p></td>
<td><p>WIA がサービス定義、および文字列内のベンダー定義トークン、トークンに関連付けられている値に置き換えて、裏書き文字列を解析します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549351" data-raw-source="[&lt;strong&gt;wiasSendEndOfPage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549351)"><strong>wiasSendEndOfPage</strong></a></p></td>
<td><p>データ転送では、現在の合計ページ数を送信中に、クライアント コールバック ルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549441" data-raw-source="[&lt;strong&gt;wiasUpdateScanRect&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549441)"><strong>wiasUpdateScanRect</strong></a></p></td>
<td><p>スキャン デバイスのスキャンの領域のサイズを更新します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549473" data-raw-source="[&lt;strong&gt;wiasWriteBufToFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549473)"><strong>wiasWriteBufToFile</strong></a></p></td>
<td><p>画像ファイルへの一時的なページのバッファーの内容を書き込みます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549484" data-raw-source="[&lt;strong&gt;wiasWritePageBufToFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549484)"><strong>wiasWritePageBufToFile</strong></a></p></td>
<td><p>画像ファイルへの一時的なページのバッファーの内容を書き込みます。 複数ページの TIFF ファイルにページを作成するのにには、この関数を使用します。</p></td>
</tr>
</tbody>
</table>

 

 

 




