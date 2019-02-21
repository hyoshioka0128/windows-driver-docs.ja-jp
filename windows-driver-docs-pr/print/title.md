---
title: Title 要素
description: 必要な title 要素は、イベント通知メッセージのタイトルに表示されるテキストを提供します。
ms.assetid: 60583593-9fe9-4c3c-ab86-3e7c37a8e199
keywords:
- 要素の印刷デバイスをタイトルします。
topic_type:
- apiref
api_name:
- title
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: acbf9669af62899138560270cc89345eeeb869b3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557463"
---
# <a name="title-element"></a>Title 要素


必要な**タイトル**要素は、イベント通知メッセージのタイトルに表示されるテキストを提供します。

**タイトル**で要素が定義されている、 *asyncui*この URI に、名前空間:http://schemas.microsoft.com/2003/print/asyncui/v1/requestします。 (このリソースできない場合がありますのいくつかの言語および国。)

<a name="usage"></a>使用方法
-----

```xml
<title
  stringID = "xs:string"
  resourceDll = "xs:string"/>
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
<p>リソース イベントの通知メッセージを表示するタイトル テキストを含む DLL を指定する省略可能な属性。 この DLL は、プリンター ドライバーの依存ファイルである必要があり、ドライバーのリソース フォルダー (たとえば、%systemroot%\system32\spool\drivers\w32x86\3) に存在する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><strong>stringID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>〇</p></td>
<td><p></p>
<p>イベント通知メッセージのタイトルに表示するテキストを指定する必須の属性。 属性の値は、リソース DLL でのテキスト文字列の場所を指定します。</p></td>
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
<td><p><a href="balloonui.md" data-raw-source="[&lt;strong&gt;balloonUI&lt;/strong&gt;](balloonui.md)"><strong>balloonUI</strong></a></p></td>
<td><p></p>
<p>クライアント コンピューターでメッセージ バルーンの表示に使用される省略可能な要素です。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

場合、属性**resourceDll**が指定されていない、Microsoft 提供のユーザー インターフェイスの DLL Prnntfy.dll からタイトルのテキストが生成されます。

リソース DLL から読み込まれた本文が割合 (%) を含めることができます。指定されたテキスト文字列で置き換えられる文字、 [**パラメーター** ](parameter.md)子要素。

<a name="examples"></a>例
--------

次のコード例を使用する方法を示しています、**タイトル**をリソース DLL の場所の文字列を示す要素 (この例では、stringID =「1234」) タイトルに使用するテキストを格納しています。

```cpp
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

## <a name="see-also"></a>関連項目

[balloonUI](balloonui.md)

[パラメーター](parameter.md)
