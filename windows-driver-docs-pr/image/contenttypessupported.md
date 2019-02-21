---
title: ContentTypesSupported 要素
description: 必要な ContentTypesSupported 要素には、スキャナーをサポートする別のドキュメント コンテンツの種類を説明するキーワードの一覧が含まれています。
ms.assetid: f7ed2ba9-8cd9-486c-9bb0-3eb2c925450a
keywords:
- ContentTypesSupported 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ContentTypesSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 029bb0269a265bdb49c536d68eddb61bb1c93d0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535897"
---
# <a name="contenttypessupported-element"></a>ContentTypesSupported 要素


必要な**ContentTypesSupported**要素には、スキャナーをサポートする別のドキュメント コンテンツの種類を説明するキーワードの一覧が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ContentTypesSupported>
  child elements
</wscn:ContentTypesSupported>
```

<a name="attributes"></a>属性
----------

属性はありません。

## <a name="child-elements"></a>子要素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="contenttypevalue.md" data-raw-source="[&lt;strong&gt;ContentTypeValue&lt;/strong&gt;](contenttypevalue.md)"><strong>ContentTypeValue</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="devicesettings.md" data-raw-source="[&lt;strong&gt;DeviceSettings&lt;/strong&gt;](devicesettings.md)"><strong>DeviceSettings</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

各[ **ContentTypeValue** ](contenttypevalue.md)に記載されている要素を**ContentTypesSupported**要素が、元のドキュメントの主な特徴について説明します。 クライアントでは、1 つのコンテンツの種類を取得します。 その[ **ScanTicket** ](scanticket.md)スキャンを開始するときに、この一覧から。

## <a name="see-also"></a>関連項目


[**ScanTicket**](scanticket.md)

 

 






