---
title: Parameter 要素
description: 省略可能なパラメーター要素には、イベント通知メッセージのテキストにパーセント記号 () 文字の代わりに使用するテキスト文字列を指定します。
ms.assetid: 6a43af7d-da00-4038-b1a8-a076d07c4c1a
keywords:
- parameter 要素印刷デバイス
topic_type:
- apiref
api_name:
- parameter
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 820b1985308399f83af8cb2b23b594e5763aebe2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324242"
---
# <a name="parameter-element"></a>Parameter 要素


省略可能な**パラメーター**割合 (%) の代わりに使用するテキスト文字列を指定します。イベント通知メッセージのテキストの文字。

**パラメーター**で要素が定義されている、 *asyncui*この URI に、名前空間: http://schemas.microsoft.com/2003/print/asyncui/v1/request します。 (このリソースできない場合がありますのいくつかの言語および国。)

<a name="usage"></a>使用方法
-----

```xml
<parameter
  stringID = "xs:string"
  resourceDll = "xs:string"
  type = "xs:string"/>
```

<a name="attributes"></a>属性
----------

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>種類</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ResourceDll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>リソース イベントの通知メッセージを表示するテキストを含んでいる DLL を指定する省略可能な属性。 この DLL は、プリンター ドライバーの依存ファイルである必要があり、ドライバーのリソース フォルダー (たとえば、%systemroot%\system32\spool\drivers\w32x86\3) に存在する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><strong>stringID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>〇</p></td>
<td><p></p>
<p>割合 (%) の場所に表示するテキストを指定する必須の属性イベント通知メッセージのテキストの文字。 属性の値は、リソース DLL でのテキスト文字列の場所を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>type</strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>プリンターやドキュメントの名前を指定する省略可能な属性。 この属性は、印刷中のドキュメントの次の値: DocumentThe 名前のいずれかを実行できます。PrinterNameThe 名、プリンタと Fax に記載されているプリンターのコントロール パネル、たとえば、"Fabrikam 5000 \printserver で"フォルダーまたは「2 階の寝室のプリンター」。</p></td>
</tr>
</tbody>
</table>

## <a name="child-elements"></a>子要素


子要素はありません。

## <a name="parent-elements"></a>親要素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="body.md" data-raw-source="[&lt;strong&gt;body&lt;/strong&gt;](body.md)"><strong>body</strong></a></p></td>
<td><p></p>
<p>テキストを提供する必須要素は、イベントの通知メッセージに表示されます。 このテキストは、プリンターのイベントの特定の詳細、ユーザーを提供する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="title.md" data-raw-source="[&lt;strong&gt;title&lt;/strong&gt;](title.md)"><strong>title</strong></a></p></td>
<td><p></p>
<p>必要な title 要素は、イベント通知メッセージのタイトルに表示されるテキストを提供します。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

リソース DLL から読み込まれたテキストは割合 (%) を含めることができます。指定されたテキスト文字列で置き換えられる文字、**パラメーター**要素。

<a name="examples"></a>例
--------

次のコード例に示す方法、**パラメーター**要素を使用して、完了イベントの通知メッセージを生成します。

この例で、 **stringID**値は、次を指定します。

-   ドライバー リソース DLL 内のユーザー インターフェイス文字列 100 は"プリンターが; %1 のインクが不足ください %2 を開き、インク カートリッジを交換します。"
-   Microsoft 提供のユーザー インターフェイスの DLL でのユーザー インターフェイス文字列 5 は「黄」です。
-   ドライバー リソース DLL 内のユーザー インターフェイス文字列 1002 は、"側アクセス ドア B"です。

```xml
<?xml version="1.0" ?>
   <asyncPrintUIRequest
    xmlns="http://schemas.microsoft.com/2003/print/asyncui/v1/request">
    <v1>
      <requestOpen>
        <balloonUI iconID="1" resourceDll="IHV.dll">
          <title stringID="1234" resourceDll="IHV.dll" />
          <body stringID="100" resourceDll="IHV.dll">
            <parameter stringID="5" />
            <parameter stringID="1002" resourceDll="IHV.dll" />
          </body>
        </balloonUI>
      </requestOpen>
    </v1>
  </asyncPrintUIRequest>
```

上記の XML コードを次に本体テキスト (stringID =「100」)、イベント通知メッセージが表示されます。"プリンターが黄色のインクからくださいアクセス ドア B 開きインク カートリッジを交換します。"

## <a name="see-also"></a>関連項目

[body](body.md)

[title](title.md)
