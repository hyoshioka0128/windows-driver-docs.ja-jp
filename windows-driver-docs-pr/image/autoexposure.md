---
title: AutoExposure 要素
description: 必要な AutoExposure 要素では、WSD スキャン サービスが、ドキュメントの公開設定を自動的に決定する必要がありますを指定します。
ms.assetid: ccc2b246-cfa1-4d79-b968-7b4bbaad17ee
keywords:
- AutoExposure 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn AutoExposure
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecfd7d6adfa3eea0602ad04e93ef464e973c1eb9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571912"
---
# <a name="autoexposure-element"></a>AutoExposure 要素


必要な**AutoExposure**要素の WSD スキャン サービスが、ドキュメントの公開設定を自動的に決定する必要がありますを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:AutoExposure>
  text
</wscn:AutoExposure>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 ブール値 false、0 にする必要がある、1 または true です。**falsetrue**

## <a name="child-elements"></a>子要素


子要素はありません。

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
<td><p><a href="exposure.md" data-raw-source="[&lt;strong&gt;Exposure&lt;/strong&gt;](exposure.md)"><strong>公開</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>コメント
-------

ときのブール値、 **AutoExposure**要素が 1 または**true**、スキャン デバイスは白にドキュメントの背景を軽減するイメージの処理の方法を使用します。

値が 0 または**false**デバイスの各公開設定の既定の設定を使用する必要があります。

## <a name="see-also"></a>関連項目


[**公開**](exposure.md)

 

 






