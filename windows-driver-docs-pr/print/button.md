---
title: button 要素
description: 必須ボタン要素は、クライアントコンピューターに表示されるメッセージボックスのボタンの特性を指定します。
ms.assetid: 3e210599-9412-4eea-a024-338e39852199
keywords:
- ボタン要素の印刷デバイス
topic_type:
- apiref
api_name:
- button
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 511debe97b341575154d14fc1f4ab40ffdb8bc2a
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652863"
---
# <a name="button-element"></a>button 要素


必須**ボタン**要素は、クライアントコンピューターに表示されるメッセージボックスのボタンの特性を指定します。

**Button**要素は、この URI: [https://schemas.microsoft.com/2003/print/asyncui/v1/request](https://schemas.microsoft.com/2003/print/asyncui/v1/request)の*asyncui*名前空間で定義されています。 (このリソースは、一部の言語および国では使用できません。)

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
<th>備わっている</th>
<th>タスクバーの検索ボックスに</th>
<th>必須かどうか</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>buttonID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>[はい]</p></td>
<td><p></p>
<p>ユーザーがボタンをクリックしたときにプリンタードライバーに返される文字列を指定する必須の属性です。 この属性は、次のいずれかの値をとります。</p>
IDOK "OK" という名前のボタンがメッセージボックスに表示されます。 ユーザーがボタンをクリックすると、メッセージボックスに "IDOK" という文字列が返されます。
IDCANCEL [キャンセル] という名前のボタンがメッセージボックスに表示されます。 ユーザーがボタンをクリックすると、メッセージボックスに "IDCANCEL" という文字列が返されます。</td>
</tr>
<tr class="even">
<td><p><strong>resourceDll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>必須ではない</p></td>
<td><p></p>
<p>ボタンに表示するテキストを含むリソース DLL を指定する省略可能な属性です。 この DLL は、プリンタドライバの依存ファイルである必要があり、ドライバリソースフォルダに存在する必要があります (たとえば、%SYSTEMROOT%\system32\spool\drivers\w32x86\3)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>stringID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>[はい]</p></td>
<td><p></p>
<p>ボタンに表示するテキストを指定する必須の属性です。 属性値は、リソース DLL 内のテキスト文字列の場所を指定します。</p></td>
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
<td><p><a href="buttons.md" data-raw-source="[&lt;strong&gt;buttons&lt;/strong&gt;](buttons.md)"><strong>83'7b</strong></a></p></td>
<td><p></p>
<p>クライアントコンピューターのイベント通知メッセージボックスに表示される1つ以上のボタンを指定する必須の要素。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

ボタンは、メッセージボックスの下部に表示されます。

<a name="examples"></a>例
--------

次のコード例は、 **button**要素を使用して、 **[OK]** ボタンと **[キャンセル**] ボタンを相互に表示する方法を示しています。

```xml
<?xml version="1.0" ?>
  <asyncPrintUIRequest
    xmlns="https://schemas.microsoft.com/2003/print/asyncui/v1/request">
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

## <a name="see-also"></a>「

[buttons](buttons.md)
