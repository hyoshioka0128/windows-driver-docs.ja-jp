---
title: title 要素
description: 必須の title 要素は、イベント通知メッセージのタイトルに表示されるテキストを提供します。
ms.assetid: 60583593-9fe9-4c3c-ab86-3e7c37a8e199
keywords:
- タイトル要素の印刷デバイス
topic_type:
- apiref
api_name:
- title
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24b08ea498cd15e95e8bc9fc0efae63058cb9e8e
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652958"
---
# <a name="title-element"></a>title 要素

必須の**title**要素は、イベント通知メッセージのタイトルに表示されるテキストを提供します。

**Title**要素は、この URI: [https://schemas.microsoft.com/2003/print/asyncui/v1/request](https://schemas.microsoft.com/2003/print/asyncui/v1/request)の*asyncui*名前空間で定義されています。 (このリソースは、一部の言語および国では使用できません。)

## <a name="usage"></a>使用方法

```xml
<title
  stringID = "xs:string"
  resourceDll = "xs:string"/>
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
<td><p><strong>resourceDll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>必須ではない</p></td>
<td><p></p>
<p>イベント通知メッセージに表示するタイトルテキストを含むリソース DLL を指定する、省略可能な属性です。 この DLL は、プリンタドライバの依存ファイルである必要があり、ドライバリソースフォルダに存在する必要があります (たとえば、%SYSTEMROOT%\system32\spool\drivers\w32x86\3)。</p></td>
</tr>
<tr class="even">
<td><p><strong>stringID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>[はい]</p></td>
<td><p></p>
<p>イベント通知メッセージのタイトルに表示するテキストを指定する必須の属性です。 属性値は、リソース DLL 内のテキスト文字列の場所を指定します。</p></td>
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
<p>クライアントコンピューターにメッセージバルーンを表示するために使用される省略可能な要素。</p></td>
</tr>
</tbody>
</table>

## <a name="remarks"></a>注釈

属性**Resourcedll**が指定されていない場合、Microsoft が提供するユーザーインターフェイス dll Prnntfy からタイトルテキストが生成されます。

リソース DLL から読み込まれた本文のテキストには、パーセンテージ (%) を含めることができます。[**parameter**](parameter.md)子要素で指定されたテキスト文字列に置き換えられる文字。

## <a name="examples"></a>例

**Title 要素を**使用して、タイトルに使用されるテキストが含まれているリソース DLL 内の文字列の場所 (この例では stringid = "1234") を示すコード例を次に示します。

```cpp
<?xml version="1.0" ?>
   <asyncPrintUIRequest
    xmlns="https://schemas.microsoft.com/2003/print/asyncui/v1/request">
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

## <a name="see-also"></a>「

[balloonUI](balloonui.md)

[parameter](parameter.md)
