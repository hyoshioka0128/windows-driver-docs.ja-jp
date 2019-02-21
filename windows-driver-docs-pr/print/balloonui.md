---
title: balloonUI 要素
description: 省略可能な balloonUI 要素は、クライアント コンピューターでメッセージ バルーンの表示に使用されます。
ms.assetid: 8db15dcb-26ed-429e-ad4c-e5dc59f9bbca
keywords:
- balloonUI 要素印刷デバイス
topic_type:
- apiref
api_name:
- balloonUI
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: db9fa4cc0554f0d6569eb9c8b35cfa95a8964db1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550726"
---
# <a name="balloonui-element"></a>balloonUI 要素


省略可能な**balloonUI**要素を使用して、クライアント コンピューターでメッセージ バルーンを表示します。

**BalloonUI**で要素が定義されている、 *asyncui*この URI に、名前空間:http://schemas.microsoft.com/2003/print/asyncui/v1/requestします。 (このリソースできない場合がありますのいくつかの言語および国。)

<a name="usage"></a>使用方法
-----

```xml
<balloonUI
  iconID = "xs:string"
  resourceDll = "xs:string">
  child elements
</balloonUI>
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
<td><p><strong>iconID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>イベントの通知メッセージを表示するプリンターのアイコンを指定する省略可能な属性。 属性の値は、リソース DLL で、アイコンの場所を指定します。 アイコンは、32 x 32 のピクセルのサイズ、色深度が任意である必要があります。</p></td>
</tr>
<tr class="even">
<td><p><strong>ResourceDll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>リソース イベントの通知メッセージを表示するプリンターのアイコンを含む DLL を指定する省略可能な属性。 この DLL は、プリンター ドライバーの依存ファイルである必要があり、ドライバーのリソース フォルダー (たとえば、%systemroot%\system32\spool\drivers\w32x86\3) に存在する必要があります。</p></td>
</tr>
</tbody>
</table>

## <a name="child-elements"></a>子要素


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
<p>イベント通知メッセージのタイトルに表示されるテキストを提供する必須要素。</p></td>
</tr>
</tbody>
</table>

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
<td><p><a href="requestopen.md" data-raw-source="[&lt;strong&gt;requestOpen&lt;/strong&gt;](requestopen.md)"><strong>requestOpen</strong></a></p></td>
<td><p></p>
<p>クライアント コンピューターのイベント通知メッセージを開くために使用する要素。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

場合、属性**iconID**と**resourceDll**が指定されていない、バルーン メッセージに汎用的なプリンターのアイコンが表示されます。 カスタムのプリンターのアイコンを表示するには、両方の属性の値を指定します。

<a name="examples"></a>例
--------

次のコード例は、対話型のバルーンを使用して渡す方法を示しています。 **CDATA** DLL へのデータを入力します。

```xml
<?xml version="1.0" ?> 
  <asyncPrintUIRequest xmlns="http://schemas.microsoft.com/2003/print/asyncui/v1/request">
    <v1>
      <requestOpen>
        <balloonUI iconID="1" resourceDll="IHV.dll">
          <title stringID="1234" resourceDll="IHV.dll" />
          <body stringID="100" resourceDll="IHV.dll">
            <parameter stringID="<5>" />
            <parameter stringID="1002" resourceDll="IHV.dll" />
          </body>
          <action dll="adc.dll" entrypoint="def" />
            IHV Data to pass into dll
            MUST BE CDATA
          </action>
        </balloonUI>
      </requestOpen>
    </v1>
  </asyncPrintUIRequest>
```

## <a name="see-also"></a>関連項目


[**アクション**](action.md)

[**body**](body.md)

[**requestOpen**](requestopen.md)

[**title**](title.md)

 

 




