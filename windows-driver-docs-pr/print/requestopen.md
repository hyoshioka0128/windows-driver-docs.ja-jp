---
title: requestOpen 要素
description: クライアント コンピューターのイベント通知メッセージを requestOpen 要素が使用されます。
ms.assetid: c1797295-9aca-4986-bd9d-482bb7049942
keywords:
- requestOpen 要素印刷デバイス
topic_type:
- apiref
api_name:
- requestOpen
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2fd86abbcfd958661da4b3e3ced547837ffa93b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550215"
---
# <a name="requestopen-element"></a>requestOpen 要素


**RequestOpen**要素は、クライアント コンピューターのイベント通知メッセージを使用します。

**RequestOpen**で要素が定義されている、 *asyncui*この URI に、名前空間:http://schemas.microsoft.com/2003/print/asyncui/v1/requestします。 (このリソースできない場合がありますのいくつかの言語および国。)

<a name="usage"></a>使用方法
-----

```xml
<requestOpen>
  child elements
</requestOpen>
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
<td><p><a href="balloonui.md" data-raw-source="[&lt;strong&gt;balloonUI&lt;/strong&gt;](balloonui.md)"><strong>balloonUI</strong></a></p></td>
<td><p></p>
<p>クライアント コンピューターでメッセージ バルーンの表示に使用される省略可能な要素です。</p></td>
</tr>
<tr class="even">
<td><p><a href="customui.md" data-raw-source="[&lt;strong&gt;customUI&lt;/strong&gt;](customui.md)"><strong>customUI</strong></a></p></td>
<td><p></p>
<p>クライアント コンピューターに表示されるカスタム ユーザー インターフェイスを指定する省略可能な要素です。</p></td>
</tr>
<tr class="odd">
<td><p><a href="messageboxui.md" data-raw-source="[&lt;strong&gt;messageBoxUI&lt;/strong&gt;](messageboxui.md)"><strong>messageBoxUI</strong></a></p></td>
<td><p></p>
<p>クライアント コンピューターのメッセージ ボックスを表示するために使用する省略可能な要素です。</p></td>
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
<td><p><a href="asyncprintuirequest.md" data-raw-source="[&lt;strong&gt;asyncPrintUIRequest&lt;/strong&gt;](asyncprintuirequest.md)"><strong>asyncPrintUIRequest</strong></a></p></td>
<td><p></p>
<p>クライアント コンピューターでメッセージを作成するプリンター ドライバーによって発行された要求を記述する必須要素。</p></td>
</tr>
</tbody>
</table>

<a name="examples"></a>例
--------

次のコード例では、イベント通知メッセージが開きます。

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

## <a name="see-also"></a>関連項目

[asyncPrintUIRequest](asyncprintuirequest.md)

[balloonUI](balloonui.md)

[customUI](customui.md)

[messageBoxUI](messageboxui.md)

[requestClose](requestclose.md)
