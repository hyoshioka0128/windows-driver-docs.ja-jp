---
title: bitmap 要素
description: オプションの bitmap 要素は、メッセージボックス内の本文の左側にビットマップイメージを表示するために使用されます。
ms.assetid: 6dd1a82f-7a9e-4ed6-9d0d-76e025331d2c
keywords:
- ビットマップ要素の印刷デバイス
topic_type:
- apiref
api_name:
- bitmap
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3db726107f7fa07f0ebf0fe8858ecda69091cc7
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652867"
---
# <a name="bitmap-element"></a>bitmap 要素

オプションの**bitmap**要素は、メッセージボックス内の本文の左側にビットマップイメージを表示するために使用されます。

**Bitmap**要素は、この URI: https://schemas.microsoft.com/2003/print/asyncui/v1/request の*asyncui*名前空間で定義されています。 (このリソースは、一部の言語および国では使用できません。)

## <a name="usage"></a>使用方法

```xml
<bitmap
  bitmapID = "xs:string"
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
<td><p><strong>bitmapID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>[はい]</p></td>
<td><p></p>
<p>メッセージボックスに表示するビットマップイメージを指定する必須の属性です。 属性値は、リソース DLL 内のイメージの場所を指定します。 ビットマップイメージは任意のサイズまたは形式にすることができます。メッセージボックスは、それに合わせてサイズが変更されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>resourceDll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>必須ではない</p></td>
<td><p></p>
<p>メッセージボックスに表示するビットマップイメージを含むリソース DLL を指定する、省略可能な属性です。 この DLL は、プリンタドライバの依存ファイルである必要があり、ドライバリソースフォルダに存在する必要があります (たとえば、%SYSTEMROOT%\system32\spool\drivers\w32x86\3)。</p></td>
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
<p>クライアントコンピューターにメッセージボックスを表示するために使用される省略可能な要素。</p></td>
</tr>
</tbody>
</table>

## <a name="examples"></a>例

**Bitmap**要素の使用方法を次のコード例に示します。

```xml
<?xml version="1.0" ?>
   <asyncPrintUIRequest xmlns="https://schemas.microsoft.com/2003/print/asyncui/v1/request">
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

## <a name="see-also"></a>「

[**messageBoxUI**](messageboxui.md)
