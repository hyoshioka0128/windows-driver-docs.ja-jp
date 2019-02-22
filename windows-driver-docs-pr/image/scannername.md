---
title: ScannerName 要素
description: 必要な ScannerName 要素には、スキャナーの管理者に割り当てられているわかりやすい名前を指定します。
ms.assetid: 013a1cb8-4b59-4271-a7bd-eb8d741643e5
keywords:
- ScannerName 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScannerName xml lang "..."
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59349e620d90ac2187fc194b139a8d51ed9cfaed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538982"
---
# <a name="scannername-element"></a>ScannerName 要素


必要な**ScannerName**要素は、スキャナーの管理者に割り当てられているわかりやすい名前を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScannerName xml:lang="..."
  lang = "xs:string">
  text
</wscn:ScannerName xml:lang="...">
```

<a name="attributes"></a>属性
----------

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>種類</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>lang</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>(省略可能)文字列を指定する文字列の言語を識別する文字列。<em>文字列</em></p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>テキスト値
----------

スキャナーのわかりやすい名前を指定する文字列。

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
<td><p><a href="scannerdescription.md" data-raw-source="[&lt;strong&gt;ScannerDescription&lt;/strong&gt;](scannerdescription.md)"><strong>ScannerDescription</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

構成、 **ScannerName**要素の値は実装固有。 たとえば、スキャナーのローカルのコンソールまたはデバイスの web サーバーでは、この値を構成することができます。 デバイスが 1 つだけのホステッド サービス、そのフレンドリ名を持つかどうかと**ScannerName**要素が同じ値を持つ必要があります。 デバイスには、複数のホステッド サービスが含まれている場合**ScannerName**スキャナーを識別する必要があります。

スキャン デバイスを使用して複数のローカライズされた言語のサポートを有効にするには、この要素の複数のバージョンを返すことができます、 **xml:lang**属性。

<a name="examples"></a>例
--------

次のコード例では、ScannerName 要素を使用する方法を示します。

```xml
<wscn:ScannerName xml:lang="en-AU, en-CA, en-GB, en-US">
  Accounting Scanner in Copy Room 2
</wscn:ScannerName>
```

## <a name="see-also"></a>関連項目

[**ScannerDescription**](scannerdescription.md)
