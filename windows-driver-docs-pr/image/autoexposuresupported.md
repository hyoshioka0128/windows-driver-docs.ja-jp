---
title: AutoExposureSupported 要素
description: 必要な AutoExposureSupported 要素では、デバイスのスキャンが露出のさまざまな設定の自動調整をサポートしているかどうかを指定します。
ms.assetid: 36ef003f-b049-4eb2-8fe3-53aa77db3065
keywords:
- AutoExposureSupported 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn AutoExposureSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07406e332e01fbce4353a3cbe36f89dfe0e2cc9f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573366"
---
# <a name="autoexposuresupported-element"></a>AutoExposureSupported 要素


必要な**AutoExposureSupported**要素は、デバイスのスキャンが露出のさまざまな設定の自動調整をサポートしているかどうかを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:AutoExposureSupported>
  text
</wscn:AutoExposureSupported>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 必要がありますは 0 を指定するブール値 false または true は 1 です。**falsetrue**

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
<td><p><a href="devicesettings.md" data-raw-source="[&lt;strong&gt;DeviceSettings&lt;/strong&gt;](devicesettings.md)"><strong>DeviceSettings</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>コメント
-------

[**公開**](exposure.md)

デバイスのスキャンは、さまざまな自動調整をサポートしている場合[**露出**](exposure.md) WSD スキャン サービスの設定は 1 を返す必要があります (**true**)、それ以外の 0 (を返す必要があります**false**)。

この要素に使用できる値を拡張することはできません。

## <a name="see-also"></a>関連項目


[**DeviceSettings**](devicesettings.md)

[**公開**](exposure.md)

 

 






