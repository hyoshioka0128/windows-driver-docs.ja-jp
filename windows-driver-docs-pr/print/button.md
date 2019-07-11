---
title: Button 要素
description: 必要なボタン要素は、クライアント コンピューターに表示されるメッセージ ボックスに、ボタンの特性を指定します。
ms.assetid: 3e210599-9412-4eea-a024-338e39852199
keywords:
- 要素の印刷デバイスをボタンします。
topic_type:
- apiref
api_name:
- button
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8abffb192f94b44696a93db9cb7c8e0e6a794be3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330348"
---
# <a name="button-element"></a>Button 要素


必要な**ボタン**要素は、クライアント コンピューターに表示されるメッセージ ボックスに、ボタンの特性を指定します。

**ボタン**で要素が定義されている、 *asyncui*この URI に、名前空間: [http://schemas.microsoft.com/2003/print/asyncui/v1/request](http://schemas.microsoft.com/2003/print/asyncui/v1/request )します。 (このリソースできない場合がありますのいくつかの言語および国。)

<a name="usage"></a>使用方法
-----

```xml
<button
  stringID = "xs:string"
  resourceDll = "xs:string"
  buttonID = "xs:string"/>
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
<td><p><strong>buttonID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>〇</p></td>
<td><p></p>
<p>ユーザーがボタンをクリックすると、プリンター ドライバーに返される文字列を指定する必須の属性。 この属性には、値は次のいずれかを実行できます。</p>
名前 [IDOK A] ボタンを表示して、メッセージ ボックスには"OK"されます。 ユーザーは、ボタンをクリックすると、メッセージ ボックスは"IDOK"文字列を返します。
名前"CANCEL"の [IDCANCEL A] ボタンがメッセージ ボックスに表示されます。 ユーザーは、ボタンをクリックすると、メッセージ ボックスは"IDCANCEL"文字列を返します。</td>
</tr>
<tr class="even">
<td><p><strong>ResourceDll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>リソースのボタンに表示するテキストを含んでいる DLL を指定する省略可能な属性。 この DLL は、プリンター ドライバーの依存ファイルである必要があり、ドライバーのリソース フォルダー (たとえば、%systemroot%\system32\spool\drivers\w32x86\3) に存在する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>stringID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>〇</p></td>
<td><p></p>
<p>ボタンを表示するテキストを指定する必須の属性。 属性の値は、リソース DLL でのテキスト文字列の場所を指定します。</p></td>
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
<td><p><a href="buttons.md" data-raw-source="[&lt;strong&gt;buttons&lt;/strong&gt;](buttons.md)"><strong>ボタン</strong></a></p></td>
<td><p></p>
<p>1 つまたは複数のボタンを指定する必須要素は、クライアント コンピューターの通知のメッセージ ボックスで表示、イベント。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

ボタンがメッセージ ボックスの下部に表示されます。

<a name="examples"></a>例
--------

次のコード例を使用する方法を示しています、**ボタン**を表示する要素**OK**と**キャンセル**互いの隣のボタン。

```xml
<?xml version="1.0" ?>
  <asyncPrintUIRequest
    xmlns="http://schemas.microsoft.com/2003/print/asyncui/v1/request">
    <v1>
      <requestOpen>
        <messageBoxUI>
          <title stringID="1234" resourceDll="IHV.dll" />
          <body stringID="100" resourceDll="IHV.dll">
            <parameter stringID="5" />
            <parameter stringID="1002" resourceDll="IHV.dll" />
          </body>
          <buttons>
            <button stringID="1" resourceDll="IHV.dll" buttonID="IDOK"/>
            <button stringID="2" resourceDll="IHV.dll" buttonID="IDCANCEL"/>
          </buttons>
        </messageBoxUI>
      </requestOpen>
    </v1>
  </asyncPrintUIRequest>
```

## <a name="see-also"></a>関連項目

[ボタン](buttons.md)
