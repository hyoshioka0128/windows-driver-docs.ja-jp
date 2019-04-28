---
title: ADFSupportsDuplex 要素
description: 必要な ADFSupportsDuplex 要素では、接続されている自動ドキュメント フィーダー (ADF) がメディアの両方の側のスキャンをサポートしているかどうかを指定します。
ms.assetid: 0e85243a-5b15-4b51-9608-c8036639c735
keywords:
- ADFSupportsDuplex 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ADFSupportsDuplex
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85e2fc11b83db7de19411f95922f59037bf37cd2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367072"
---
# <a name="adfsupportsduplex-element"></a>ADFSupportsDuplex 要素


必要な**ADFSupportsDuplex**要素は、接続されている自動ドキュメント フィーダー (ADF) がメディアの両方の側のスキャンをサポートしているかどうかを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ADFSupportsDuplex>
  text
</wscn:ADFSupportsDuplex>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 必要がありますは 0 を指定するブール値 false または true は 1 です。**false**または**は true。**

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
<td><p><a href="adf.md" data-raw-source="[&lt;strong&gt;ADF&lt;/strong&gt;](adf.md)"><strong>ADF</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

デバイスのスキャンに双方向のスキャンをサポートする ADF がある場合は、WSD スキャン サービスは 1 を返す必要があります (**true**)、それ以外の 0 を返す必要があります (**false**)。

この要素に使用できる値を拡張することはできません。

## <a name="see-also"></a>関連項目


[**ADF**](adf.md)

 

 






