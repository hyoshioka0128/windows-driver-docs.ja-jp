---
title: balloonUI 要素
description: オプションの balloonUI 要素は、クライアントコンピューターにメッセージバルーンを表示するために使用されます。
ms.assetid: 8db15dcb-26ed-429e-ad4c-e5dc59f9bbca
keywords:
- balloonUI 要素の印刷デバイス
topic_type:
- apiref
api_name:
- balloonUI
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7003092cfca1e01f4e706536443c99da0eebc749
ms.sourcegitcommit: 3ee05aabaf9c5e14af56ce5f1dde588c2c7eb4ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74881906"
---
# <a name="balloonui-element"></a>balloonUI 要素

オプションの**balloonUI**要素は、クライアントコンピューターにメッセージバルーンを表示するために使用されます。

**BalloonUI**要素は、この URI: [http://schemas.microsoft.com/2003/print/asyncui/v1/request](https://schemas.microsoft.com/2003/print/asyncui/v1/request)の*asyncui*名前空間で定義されています (このリソースは一部の言語および国では使用できない可能性があります)。

## <a name="usage"></a>使用方法

```xml
<balloonUI
  iconID = "xs:string"
  resourceDll = "xs:string">
  child elements
</balloonUI>
```

## <a name="attributes"></a>属性

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>備わっている</th>
<th>タスクバーの検索ボックスに</th>
<th>必須かどうか</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>iconID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>必須ではない</p></td>
<td><p></p>
<p>イベント通知メッセージに表示するプリンターアイコンを指定する省略可能な属性です。 属性値は、リソース DLL 内のアイコンの場所を指定します。 アイコンのサイズは 32 x 32 ピクセルで、任意の色深度を使用する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><strong>resourceDll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>必須ではない</p></td>
<td><p></p>
<p>イベント通知メッセージに表示するプリンターアイコンを含むリソース DLL を指定する、省略可能な属性です。 この DLL は、プリンタドライバの依存ファイルである必要があり、ドライバリソースフォルダに存在する必要があります (たとえば、%SYSTEMROOT%\system32\spool\drivers\w32x86\3)。</p></td>
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
<p>イベント通知メッセージに表示されるテキストを提供する必須の要素。 このテキストは、プリンターイベントについてのユーザー固有の詳細を提供します。</p></td>
</tr>
<tr class="even">
<td><p><a href="title.md" data-raw-source="[&lt;strong&gt;title&lt;/strong&gt;](title.md)"><strong>題</strong></a></p></td>
<td><p></p>
<p>イベント通知メッセージのタイトルに表示されるテキストを提供する必須の要素。</p></td>
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
<p>クライアントコンピューターでイベント通知メッセージを開くために使用される要素。</p></td>
</tr>
</tbody>
</table>

## <a name="remarks"></a>注釈

属性**iconID**と**resourcedll**が指定されていない場合は、一般的なプリンターアイコンがバルーンメッセージに表示されます。 カスタムプリンターアイコンを表示するには、両方の属性の値を指定します。

## <a name="examples"></a>例

次のコード例は、対話型のバルーンを使用して、 **CDATA**型のデータを DLL に渡す方法を示しています。

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

[**action**](action.md)

[**body**](body.md)

[**requestOpen**](requestopen.md)

[**題**](title.md)
