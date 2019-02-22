---
title: ScannerLocation 要素
description: 省略可能な ScannerLocation 要素には、スキャナーの割り当てられた管理上の場所を指定します。
ms.assetid: 564a468d-7a4a-49c6-921a-5d8825c783fb
keywords:
- ScannerLocation 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScannerLocation xml lang "..."
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8107024dc1c0215a94a4a606062b6a7ed2c1cd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535727"
---
# <a name="scannerlocation-element"></a>ScannerLocation 要素


省略可能な**ScannerLocation**要素は、スキャナーの割り当てられた管理上の場所を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScannerLocation xml:lang="..."
  lang = "xs:string">
  text
</wscn:ScannerLocation xml:lang="...">
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

スキャナーの場所を指定する文字列。

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

構成、 **ScannerLocation**要素の値は実装固有。 たとえば、スキャナーのローカルのコンソールまたはデバイスの web サーバーでは、この値を構成することができます。 スキャン デバイスを使用して複数のローカライズされた言語のサポートを有効にするには、この要素の複数のバージョンを返すことができます、 **xml:lang**属性。

<a name="examples"></a>例
--------

次のコード例では、ScannerLocation 要素を使用する方法を示します。

```xml
<wscn:ScannerLocation xml:lang="en-AU, en-CA, en-GB, en-US">
  LA Campus - Building 1
</wscn:ScannerLocation>
```

## <a name="see-also"></a>関連項目

[**ScannerDescription**](scannerdescription.md)
