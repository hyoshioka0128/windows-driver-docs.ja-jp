---
title: messageBoxUI 要素
description: 省略可能な messageBoxUI 要素は、クライアント コンピューターのメッセージ ボックスを表示に使用されます。
ms.assetid: 83fe67fe-72b0-42e2-864e-242b7b9989d9
keywords:
- messageBoxUI 要素印刷デバイス
topic_type:
- apiref
api_name:
- messageBoxUI
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 070b4cd8840d777e49b035e5858a819244da0c24
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375206"
---
# <a name="messageboxui-element"></a>messageBoxUI 要素


省略可能な**messageBoxUI**要素を使用して、クライアント コンピューターのメッセージ ボックスを表示します。

**MessageBoxUI**で要素が定義されている、 *asyncui*この URI に、名前空間:http://schemas.microsoft.com/2003/print/asyncui/v1/requestします。 (このリソースできない場合がありますのいくつかの言語および国。)

<a name="usage"></a>使用方法
-----

```xml
<messageBoxUI>
  child elements
</messageBoxUI>
```

<a name="attributes"></a>属性
----------

属性はありません。

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
<td><p><a href="bitmap.md" data-raw-source="[&lt;strong&gt;bitmap&lt;/strong&gt;](bitmap.md)"><strong>ビットマップ</strong></a></p></td>
<td><p></p>
<p>ビットマップ イメージをメッセージ ボックスの本文テキストの左側に表示するために使用する省略可能な要素です。</p></td>
</tr>
<tr class="even">
<td><p><a href="body.md" data-raw-source="[&lt;strong&gt;body&lt;/strong&gt;](body.md)"><strong>body</strong></a></p></td>
<td><p></p>
<p>テキストを提供する必須要素は、イベントの通知メッセージに表示されます。 このテキストは、プリンターのイベントの特定の詳細、ユーザーを提供する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="buttons.md" data-raw-source="[&lt;strong&gt;buttons&lt;/strong&gt;](buttons.md)"><strong>ボタン</strong></a></p></td>
<td><p></p>
<p>1 つまたは複数のボタンを指定する必須要素は、クライアント コンピューターの通知のメッセージ ボックスで表示、イベント。</p></td>
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

参照してください[**ボタン**](button.md)を配置する方法を示すコード例については、 **[ok]** ボタンと**キャンセル**メッセージ ボックス ボタンをクリックします。 参照してください、**例**メッセージ ボックス ボタン クリックをキャプチャする方法の詳細についてはします。

<a name="examples"></a>例
--------

次のコード例は、プリンター ドライバーに通知する方法を示していますが、 **OK**メッセージ ボックスにボタンがクリックされました。

```xml
<?xml version="1.0" ?> 
  <asyncPrintUIResponse xmlns="http://schemas.microsoft.com/2003/print/asyncui/v1/response">
    <v1>
      <requestClose>
        <messageBoxUI>
          <buttonID>IDOK</buttonID>
        </messageBoxUI >
      </requestClose>
    </v1>
  </asyncPrintUIResponse>
```

## <a name="see-also"></a>関連項目

[bitmap](bitmap.md)

[body](body.md)

[ボタン](button.md)

[ボタン](buttons.md)

[requestOpen](requestopen.md)

[title](title.md)
