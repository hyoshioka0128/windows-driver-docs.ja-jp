---
title: requestOpen 要素
description: RequestOpen 要素は、クライアントコンピューターでイベント通知メッセージを開くために使用されます。
ms.assetid: c1797295-9aca-4986-bd9d-482bb7049942
keywords:
- requestOpen 要素の印刷デバイス
topic_type:
- apiref
api_name:
- requestOpen
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95525612525dafca7e74f4bbe7048ede388c1e95
ms.sourcegitcommit: 3ee05aabaf9c5e14af56ce5f1dde588c2c7eb4ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74881904"
---
# <a name="requestopen-element"></a>requestOpen 要素

**Requestopen**要素は、クライアントコンピューターでイベント通知メッセージを開くために使用されます。

**Requestopen**要素は、この URI: [http://schemas.microsoft.com/2003/print/asyncui/v1/request](https://schemas.microsoft.com/2003/print/asyncui/v1/request)の*asyncui*名前空間で定義されています。 (このリソースは、一部の言語および国では使用できません。)

## <a name="usage"></a>使用方法

```xml
<requestOpen>
  child elements
</requestOpen>
```

## <a name="attributes"></a>属性

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
<p>クライアントコンピューターにメッセージバルーンを表示するために使用される省略可能な要素。</p></td>
</tr>
<tr class="even">
<td><p><a href="customui.md" data-raw-source="[&lt;strong&gt;customUI&lt;/strong&gt;](customui.md)"><strong>customUI</strong></a></p></td>
<td><p></p>
<p>クライアントコンピューターに表示されるカスタムユーザーインターフェイスを指定する、省略可能な要素。</p></td>
</tr>
<tr class="odd">
<td><p><a href="messageboxui.md" data-raw-source="[&lt;strong&gt;messageBoxUI&lt;/strong&gt;](messageboxui.md)"><strong>messageBoxUI</strong></a></p></td>
<td><p></p>
<p>クライアントコンピューターにメッセージボックスを表示するために使用される省略可能な要素。</p></td>
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
<p>クライアントコンピューターでメッセージを作成するためにプリンタードライバーによって発行された要求を記述する必須の要素。</p></td>
</tr>
</tbody>
</table>

## <a name="examples"></a>例

次のコード例では、イベント通知メッセージを開きます。

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
