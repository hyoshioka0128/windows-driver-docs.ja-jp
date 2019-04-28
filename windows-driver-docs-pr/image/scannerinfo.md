---
title: ScannerInfo 要素
description: 省略可能な ScannerInfo 要素には、スキャナーに関する説明情報を管理者割り当てられているいずれかが含まれています。
ms.assetid: 41d31209-8269-42ef-99f2-83818eb06f6b
keywords:
- ScannerInfo 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScannerInfo xml lang "..."
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 245bde98b14365c3a5e619447d2a751540070d8a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370062"
---
# <a name="scannerinfo-element"></a>ScannerInfo 要素


省略可能な**ScannerInfo**スキャナーに関する説明情報を割り当てられた管理上の任意の要素が含まれます。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScannerInfo xml:lang="..."
  lang = "xs:string">
  text
</wscn:ScannerInfo xml:lang="...">
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

スキャナーの説明情報を提供する文字列。

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

構成、 **ScannerInfo**要素の値は実装固有。 たとえば、スキャナーのローカルのコンソールまたはデバイスの web サーバーでは、この値を構成することができます。 スキャン デバイスを使用して複数のローカライズされた言語のサポートを有効にするには、この要素の複数のバージョンを返すことができます、 **xml:lang**属性。

<a name="examples"></a>例
--------

次のコード例では、ScannerInfo 要素を使用する方法を示します。

```xml
<wscn:ScannerInfo xml:lang="en-AU, en-CA, en-GB, en-US">
  Out of courtesy to others, please scan only
  small (1-5 page) jobs at this scanner.
</wscn:ScannerInfo>
```

## <a name="see-also"></a>関連項目

Description**](scannerdescription.md)
