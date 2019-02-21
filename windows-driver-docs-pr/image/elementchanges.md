---
title: ElementChanges 要素
description: 必要な ElementChanges 要素には、ScannerDescription、ScannerConfiguration、DefaultScanTicket、およびベンダー拡張要素への変更が含まれています。
ms.assetid: d6f1d188-beb6-4ea3-a362-de64d8d8dacb
keywords:
- ElementChanges 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ElementChanges
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67a3307002c9315605924a70c2837265ad0af3a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530480"
---
# <a name="elementchanges-element"></a>ElementChanges 要素


必要な**ElementChanges**要素にはへの変更が含まれています、 [ **ScannerDescription**](scannerdescription.md)、 [ **ScannerConfiguration**](scannerconfiguration.md)、 [ **DefaultScanTicket**](defaultscanticket.md)、およびベンダー拡張要素。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ElementChanges>
  child elements
</wscn:ElementChanges>
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
<td><p><a href="defaultscanticket.md" data-raw-source="[&lt;strong&gt;DefaultScanTicket&lt;/strong&gt;](defaultscanticket.md)"><strong>DefaultScanTicket</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scannerconfiguration.md" data-raw-source="[&lt;strong&gt;ScannerConfiguration&lt;/strong&gt;](scannerconfiguration.md)"><strong>ScannerConfiguration</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scannerdescription.md" data-raw-source="[&lt;strong&gt;ScannerDescription&lt;/strong&gt;](scannerdescription.md)"><strong>ScannerDescription</strong></a></p></td>
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
<td><p><a href="scannerelementschangeevent.md" data-raw-source="[&lt;strong&gt;ScannerElementsChangeEvent&lt;/strong&gt;](scannerelementschangeevent.md)"><strong>ScannerElementsChangeEvent</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

WSD スキャン サービスを含める必要があります、 **ElementChanges**要素を生成するとき、 [ **ScannerElementsChangeEvent** ](scannerelementschangeevent.md)要素。 各子要素**ElementChanges**すべての必須の子要素を含める必要があります。 オプションの要素が返された XML から不足している場合は、WSD スキャン サービスをクライアントに示すは、サービスにその要素がサポートしていません。

## <a name="see-also"></a>関連項目


[**DefaultScanTicket**](defaultscanticket.md)

[**ScannerConfiguration**](scannerconfiguration.md)

[**ScannerDescription**](scannerdescription.md)

[**ScannerElementsChangeEvent**](scannerelementschangeevent.md)

 

 






