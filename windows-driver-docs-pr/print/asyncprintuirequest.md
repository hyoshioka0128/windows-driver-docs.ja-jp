---
title: asyncPrintUIRequest 要素
description: 必要な asyncPrintUIRequest 要素には、クライアント コンピューターでメッセージを作成するプリンター ドライバーによって発行された要求について説明します。
ms.assetid: 992e3c97-b148-4802-be48-3067adb6dd0d
keywords:
- asyncPrintUIRequest 要素印刷デバイス
topic_type:
- apiref
api_name:
- asyncPrintUIRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 023928b2266a5577ed1271ecf61daef6870e1692
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331210"
---
# <a name="asyncprintuirequest-element"></a>asyncPrintUIRequest 要素


必要な**asyncPrintUIRequest**要素には、クライアント コンピューターでメッセージを作成するプリンター ドライバーによって発行された要求がについて説明します。

**AsyncPrintUIRequest**で要素が定義されている、 *asyncui*この URI に、名前空間: http://schemas.microsoft.com/2003/print/asyncui/v1/request します。

<a name="usage"></a>使用方法
-----

```xml
<asyncPrintUIRequest>
  child elements
</asyncPrintUIRequest>
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
<td><p><a href="requestclose.md" data-raw-source="[&lt;strong&gt;requestClose&lt;/strong&gt;](requestclose.md)"><strong>requestClose</strong></a></p></td>
<td><p></p>
<p>クライアント コンピューターのイベント通知メッセージを閉じるに使用される省略可能な要素です。</p></td>
</tr>
<tr class="even">
<td><p><a href="requestopen.md" data-raw-source="[&lt;strong&gt;requestOpen&lt;/strong&gt;](requestopen.md)"><strong>requestOpen</strong></a></p></td>
<td><p></p>
<p>クライアント コンピューターのイベント通知メッセージを開くために使用する要素。</p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="examples"></a>例
--------

次のコード例を使用する方法を示しています、 **asyncPrintUIRequest**要素。

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


[**requestClose**](requestclose.md)

[**requestOpen**](requestopen.md)

 

 




