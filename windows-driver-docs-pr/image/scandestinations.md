---
title: ScanDestinations 要素
description: 必要な ScanDestinations 要素は、すべてのクライアントがスキャン デバイスを登録するスキャンの変換先のコレクションです。
ms.assetid: 50f87269-4d95-4653-ba93-aa752bdc9168
keywords:
- ScanDestinations 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScanDestinations
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f05c61058b070b9ababa8112169b6a3f407fc377
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549070"
---
# <a name="scandestinations-element"></a>ScanDestinations 要素


必要な**ScanDestinations**要素は、すべてのクライアントがスキャン デバイスを登録するスキャンの変換先のコレクション。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScanDestinations>
  child elements
</wscn:ScanDestinations>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

なし

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
<td><p><a href="scandestination.md" data-raw-source="[&lt;strong&gt;ScanDestination&lt;/strong&gt;](scandestination.md)"><strong>ScanDestination</strong></a></p></td>
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
<td><p>&lt;wse: サブスクライブ&gt;</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

クライアントが送信する必要があります、 **ScanDestinations**内の要素、  **&lt;wse: サブスクライブ&gt;** WSD スキャンを 1 つまたは複数のスキャン変換先を登録する要求操作の要素サービス。 WSD スキャン サービスからのスキャンのチケット情報を取得する前にクライアントのセットアップ中に、クライアントが定期受信します。  **&lt;Wse: サブスクライブ&gt;** 要素は、仕様で定義されています。

**ScanDestinations**要素は、クライアントを一度に複数の一意のスキャン変換先に登録する柔軟性を提供します。

## <a name="see-also"></a>関連項目


[**ScanDestination**](scandestination.md)

 

 






