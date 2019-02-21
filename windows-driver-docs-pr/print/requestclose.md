---
title: requestClose 要素
description: 省略可能な requestClose 要素は、クライアント コンピューターのイベント通知メッセージを閉じるに使用されます。
ms.assetid: b2f21ab2-9205-483c-9f56-1c877edb7da2
keywords:
- 印刷デバイスの requestClose 要素
topic_type:
- apiref
api_name:
- requestClose
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: da1ed220d080383b7edcafcab9dd2dea67e9710d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532822"
---
# <a name="requestclose-element"></a>requestClose 要素


省略可能な**requestClose**要素を使用して、クライアント コンピューターのイベント通知メッセージを閉じます。

**RequestClose**で要素が定義されている、 *asyncui*この URI に、名前空間:http://schemas.microsoft.com/2003/print/asyncui/v1/requestします。 (このリソースできない場合がありますのいくつかの言語および国。)

<a name="usage"></a>使用方法
-----

```xml
<requestClose/>
```

<a name="attributes"></a>属性
----------

属性はありません。

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
<td><p><a href="asyncprintuirequest.md" data-raw-source="[&lt;strong&gt;asyncPrintUIRequest&lt;/strong&gt;](asyncprintuirequest.md)"><strong>asyncPrintUIRequest</strong></a></p></td>
<td><p></p>
<p>クライアント コンピューターでメッセージを作成するプリンター ドライバーによって発行された要求を記述する必須要素。</p></td>
</tr>
</tbody>
</table>

<a name="examples"></a>例
--------

次のコード例は、メッセージ ボックス ボタン クリックをキャプチャした後、イベント通知を閉じる方法を示しています、 **OK**ボタンをクリックします。

```cpp
<?xml version="1.0" ?>
   <asyncPrintUIResponse
    xmlns="http://schemas.microsoft.com/2003/print/asyncui/v1/response">
    <v1>
      <requestClose>
        <messageBoxUI>
          <buttonID>IDOK</buttonID>
        </messageBoxUI>
      </requestClose>
    </v1>
  </asyncPrintUIResponse>
```

## <a name="see-also"></a>関連項目

[asyncPrintUIRequest](asyncprintuirequest.md)

[requestOpen](requestopen.md)
