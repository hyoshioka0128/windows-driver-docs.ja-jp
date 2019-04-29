---
title: JobToken 要素
description: 必要な JobToken 要素には、新しいスキャン ジョブのデバイスが作成したトークンが含まれています。
ms.assetid: 09446fc0-074a-4f54-93fa-55b4dd467fad
keywords:
- JobToken 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn JobToken
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d022c3307f292691c292c1a5eeea8e10178172d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384545"
---
# <a name="jobtoken-element"></a>JobToken 要素


必要な**JobToken**要素には、新しいスキャン ジョブのデバイスが作成したトークンが含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:JobToken>
  text
</wscn:JobToken>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 任意の有効な文字の文字列。

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
<td><p><a href="createscanjobresponse.md" data-raw-source="[&lt;strong&gt;CreateScanJobResponse&lt;/strong&gt;](createscanjobresponse.md)"><strong>CreateScanJobResponse</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="retrieveimagerequest.md" data-raw-source="[&lt;strong&gt;RetrieveImageRequest&lt;/strong&gt;](retrieveimagerequest.md)"><strong>RetrieveImageRequest</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**JobToken**要素を組み合わせて、 [ **JobId** ](jobid.md)を一意に特定のスキャン ジョブを表す要素。 **JobToken**でデバイスのスキャンに渡される、 [ **RetrieveImageRequest** ](retrieveimagerequest.md)スキャン要求元がスキャン ジョブを実際に作成されたことを確認するデバイスを有効にする要素を操作します。

## <a name="see-also"></a>関連項目


[**CreateScanJobResponse**](createscanjobresponse.md)

[**JobId**](jobid.md)

[**RetrieveImageRequest**](retrieveimagerequest.md)

 

 






