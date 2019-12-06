---
title: parameter 要素
description: 省略可能な parameter 要素は、イベント通知メッセージのテキストでパーセント () 文字を置き換えるテキスト文字列を指定します。
ms.assetid: 6a43af7d-da00-4038-b1a8-a076d07c4c1a
keywords:
- パラメーター要素の印刷デバイス
topic_type:
- apiref
api_name:
- parameter
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6063785012286e73387a5011fb0c8e0543857edd
ms.sourcegitcommit: 3ee05aabaf9c5e14af56ce5f1dde588c2c7eb4ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74881910"
---
# <a name="parameter-element"></a>parameter 要素

省略可能な**parameter**要素は、パーセント (%) の代わりに使用するテキスト文字列を指定します。イベント通知メッセージのテキスト内の文字。

**Parameter**要素は、この URI: [http://schemas.microsoft.com/2003/print/asyncui/v1/request](https://schemas.microsoft.com/2003/print/asyncui/v1/request)の*asyncui*名前空間で定義されています。 (このリソースは、一部の言語および国では使用できません。)

## <a name="usage"></a>使用方法

```xml
<parameter
  stringID = "xs:string"
  resourceDll = "xs:string"
  type = "xs:string"/>
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
<p>イベント通知メッセージに表示するテキストを含むリソース DLL を指定する、省略可能な属性です。 この DLL は、プリンタドライバの依存ファイルである必要があり、ドライバリソースフォルダに存在する必要があります (たとえば、%SYSTEMROOT%\system32\spool\drivers\w32x86\3)。</p></td>
</tr>
<tr class="even">
<td><p><strong>stringID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>[はい]</p></td>
<td><p></p>
<p>パーセント (%) の場所に表示するテキストを指定する必須の属性です。イベント通知メッセージのテキスト内の文字。 属性値は、リソース DLL 内のテキスト文字列の場所を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>type</strong></p></td>
<td><p>xs:string</p></td>
<td><p>必須ではない</p></td>
<td><p></p>
<p>プリンターまたはドキュメントの名前を指定する省略可能な属性です。 この属性には、次の値のいずれかを指定できます。 DocumentThe されるドキュメントの名前。プリンター名。コントロールパネルの [プリンターと Fax] フォルダーに表示されるプリンターの名前。たとえば、"Fabrikam 5000 on \ プリント" または "Printer in 階ベッドルーム" のように指定します。</p></td>
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
<p>イベント通知メッセージに表示されるテキストを提供する必須の要素。 このテキストは、プリンターイベントについてのユーザー固有の詳細を提供します。</p></td>
</tr>
<tr class="even">
<td><p><a href="title.md" data-raw-source="[&lt;strong&gt;title&lt;/strong&gt;](title.md)"><strong>題</strong></a></p></td>
<td><p></p>
<p>必須の title 要素は、イベント通知メッセージのタイトルに表示されるテキストを提供します。</p></td>
</tr>
</tbody>
</table>

## <a name="remarks"></a>注釈

リソース DLL から読み込まれるテキストには、パーセンテージ (%) を含めることができます。**parameter**要素によって指定されたテキスト文字列に置き換えられる文字。

## <a name="examples"></a>例

次のコード例は、**パラメーター**要素を使用して、完全なイベント通知メッセージを生成する方法を示しています。

この例では、 **Stringid**値によって次の値が指定されています。

- ドライバーリソース DLL 内のユーザーインターフェイス文字列100は、"プリンターは %1 インクを超えています。%2 を開いてインクカートリッジを交換してください。 "

- Microsoft が提供するユーザーインターフェイス DLL のユーザーインターフェイス文字列5は、"黄色" です。

- ドライバーリソース DLL のユーザーインターフェイス文字列1002は、"サイドアクセスドア B" です。

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

上記の XML コードでは、イベント通知メッセージに次の本文 (stringID = "100") が表示されます: "プリンターは黄色のインクが不足しています。サイドアクセスドア B を開いてインクカートリッジを交換してください。 "

## <a name="see-also"></a>関連項目

[body](body.md)

[title](title.md)
