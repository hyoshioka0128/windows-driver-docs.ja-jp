---
title: asyncPrintUIRequest 要素
description: 必須の asyncPrintUIRequest 要素は、クライアントコンピューターでメッセージを作成するためにプリンタードライバーによって発行される要求を記述します。
ms.assetid: 992e3c97-b148-4802-be48-3067adb6dd0d
keywords:
- asyncPrintUIRequest 要素の印刷デバイス
topic_type:
- apiref
api_name:
- asyncPrintUIRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55b88c74c27bba4f9fb1426129609cb39b24ecb3
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652936"
---
# <a name="asyncprintuirequest-element"></a>asyncPrintUIRequest 要素

必須の**asyncPrintUIRequest**要素は、クライアントコンピューターでメッセージを作成するためにプリンタードライバーによって発行される要求を記述します。

**AsyncPrintUIRequest**要素は、この URI: [https://schemas.microsoft.com/2003/print/asyncui/v1/request](https://schemas.microsoft.com/2003/print/asyncui/v1/request)の*asyncui*名前空間で定義されています。

## <a name="usage"></a>使用方法

```xml
<asyncPrintUIRequest>
  child elements
</asyncPrintUIRequest>
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
<td><p><a href="requestclose.md" data-raw-source="[&lt;strong&gt;requestClose&lt;/strong&gt;](requestclose.md)"><strong>requestClose</strong></a></p></td>
<td><p></p>
<p>クライアントコンピューターでイベント通知メッセージを閉じるために使用される省略可能な要素。</p></td>
</tr>
<tr class="even">
<td><p><a href="requestopen.md" data-raw-source="[&lt;strong&gt;requestOpen&lt;/strong&gt;](requestopen.md)"><strong>requestOpen</strong></a></p></td>
<td><p></p>
<p>クライアントコンピューターでイベント通知メッセージを開くために使用される要素。</p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素

親要素はありません。

## <a name="examples"></a>例

**AsyncPrintUIRequest**要素を使用する方法を次のコード例に示します。

```xml
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

[**requestClose**](requestclose.md)

[**requestOpen**](requestopen.md)
