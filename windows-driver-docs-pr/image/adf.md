---
title: ADF 要素
description: 省略可能な ADF 要素には、スキャナーに関連付けられている自動ドキュメント フィーダー (ADF) の機能について説明します。
ms.assetid: 2c9114c3-0c6e-4404-a1ee-fd8d63c6e8eb
keywords:
- ADF 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ADF
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04aac63bfc0dee8260860181214aaf3baedf1e6c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550259"
---
# <a name="adf-element"></a>ADF 要素


省略可能な**ADF**要素が、スキャナーに関連付けられている自動ドキュメント フィーダー (ADF) の機能について説明します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ADF>
  child elements
</wscn:ADF>
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
<td><p><a href="adfback.md" data-raw-source="[&lt;strong&gt;ADFBack&lt;/strong&gt;](adfback.md)"><strong>ADFBack</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="adffront.md" data-raw-source="[&lt;strong&gt;ADFFront&lt;/strong&gt;](adffront.md)"><strong>ADFFront</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="adfsupportsduplex.md" data-raw-source="[&lt;strong&gt;ADFSupportsDuplex&lt;/strong&gt;](adfsupportsduplex.md)"><strong>ADFSupportsDuplex</strong></a></p></td>
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
<td><p><a href="scannerconfiguration.md" data-raw-source="[&lt;strong&gt;ScannerConfiguration&lt;/strong&gt;](scannerconfiguration.md)"><strong>ScannerConfiguration</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

WSD スキャン サービスがすべての構成情報を提供する必要があります、ADF スキャン デバイスの場合は、 **ADF**子要素。

## <a name="see-also"></a>関連項目


[**ADFBack**](adfback.md)

[**ADFFront**](adffront.md)

[**ADFSupportsDuplex**](adfsupportsduplex.md)

[**ScannerConfiguration**](scannerconfiguration.md)

 

 






