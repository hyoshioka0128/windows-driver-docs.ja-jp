---
title: ScanIdentifier 要素
description: 必要な ScanIdentifier 要素には、スキャナーを ScanAvailableEvent イベントを通じて提供するデバイス固有の文字列が含まれています。
ms.assetid: 77116871-63dc-4388-9b36-a553219ddcf7
keywords:
- ScanIdentifier 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScanIdentifier
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4140becbe6f6162c9e5d0307d40955f2090f243d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557983"
---
# <a name="scanidentifier-element"></a>ScanIdentifier 要素


必要な**ScanIdentifier**要素にはを通じて、スキャナーを提供するデバイス固有の文字列が含まれています、 [ **ScanAvailableEvent** ](scanavailableevent.md)イベント。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScanIdentifier>
  text
</wscn:ScanIdentifier>
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
<td><p><a href="createscanjobrequest.md" data-raw-source="[&lt;strong&gt;CreateScanJobRequest&lt;/strong&gt;](createscanjobrequest.md)"><strong>CreateScanJobRequest</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scanavailableevent.md" data-raw-source="[&lt;strong&gt;ScanAvailableEvent&lt;/strong&gt;](scanavailableevent.md)"><strong>ScanAvailableEvent</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

クライアントが送信できる、 **ScanIdentifier**要素の WSD スキャン サービスを[ **CreateScanJobRequest** ](createscanjobrequest.md)操作の要素。 WSD スキャン サービスが使用できる**ScanIdentifier**ユーザーが、変換先を選択した後、正しいクライアントが、スキャンを要求することを確認します。

**ScanIdentifier**値が一意である必要がありますすべて[ **ScanAvailableEvent** ](scanavailableevent.md)インスタンス。

## <a name="see-also"></a>関連項目


[**CreateScanJobRequest**](createscanjobrequest.md)

[**ScanAvailableEvent**](scanavailableevent.md)

 

 






