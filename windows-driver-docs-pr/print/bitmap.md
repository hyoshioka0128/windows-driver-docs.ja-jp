---
title: Bitmap 要素
description: 省略可能なビットマップ要素は、メッセージ ボックスの本文テキストの左側のビットマップ イメージの表示に使用されます。
ms.assetid: 6dd1a82f-7a9e-4ed6-9d0d-76e025331d2c
keywords:
- 要素の印刷デバイスをビットマップします。
topic_type:
- apiref
api_name:
- bitmap
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c46cf501af5e680636000845abbfed33c5e8d92d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384974"
---
# <a name="bitmap-element"></a>Bitmap 要素


省略可能な**ビットマップ**要素を使用してメッセージ ボックスの本文テキストの左側のビットマップ イメージを表示します。

**ビットマップ**で要素が定義されている、 *asyncui* この URI に、名前空間: http://schemas.microsoft.com/2003/print/asyncui/v1/request します。 (このリソースできない場合がありますのいくつかの言語および国。)

<a name="usage"></a>使用方法
-----

```xml
<bitmap
  bitmapID = "xs:string"
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
<td><p><strong>bitmapID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>〇</p></td>
<td><p></p>
<p>メッセージ ボックスに表示するビットマップ イメージを指定する必須の属性。 属性の値は、リソース DLL でのイメージの場所を指定します。 ビットマップ イメージが指定できる任意のサイズまたは書式設定します。メッセージ ボックスは、それに対応するサイズ変更されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>ResourceDll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>メッセージ ボックスに表示するビットマップ イメージが含まれている dll を指定する省略可能な属性。 この DLL は、プリンター ドライバーの依存ファイルである必要があり、ドライバーのリソース フォルダー (たとえば、%systemroot%\system32\spool\drivers\w32x86\3) に存在する必要があります。</p></td>
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
<td><p><a href="messageboxui.md" data-raw-source="[&lt;strong&gt;messageBoxUI&lt;/strong&gt;](messageboxui.md)"><strong>messageBoxUI</strong></a></p></td>
<td><p></p>
<p>クライアント コンピューターのメッセージ ボックスを表示するために使用する省略可能な要素です。</p></td>
</tr>
</tbody>
</table>

<a name="examples"></a>例
--------

次のコード例を使用する方法を示しています、**ビットマップ**要素。

```xml
<?xml version="1.0" ?>
   <asyncPrintUIRequest xmlns="http://schemas.microsoft.com/2003/print/asyncui/v1/request">
    <v1>
      <requestOpen>
        <messageBoxUI>
          <title stringID="1234" resourceDll="IHV.dll" />
          <bitmap bitmapID="100" resourceDll="IHV.dll" />
          <body stringID="100" resourceDll="IHV.dll">
            <parameter stringID="5" />
            <parameter stringID="1002" resourceDll="IHV.dll" />
          </body>
        </messageBoxUI>
      </requestOpen>
    </v1>
  </asyncPrintUIRequest>
```

## <a name="see-also"></a>関連項目

[**messageBoxUI**](messageboxui.md)
