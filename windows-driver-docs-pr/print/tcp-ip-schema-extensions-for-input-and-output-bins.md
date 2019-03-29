---
title: 入力ビンと出力ビンの TCP/IP スキーマ拡張
description: 入力ビンと出力ビンの TCP/IP スキーマ拡張
ms.assetid: 942325e8-588c-4171-91fa-366db6e2cb16
keywords:
- TCP/IP スキーマ拡張機能の WDK プリンター
- スキーマ拡張 WDK TCP/IP
- OutputBin コンストラクト
- InputBin コンストラクト
- 出力ビン WDK プリンター
- 入力ビン WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 720e096a4e2615098f74c011d0f813385dcddd47
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571825"
---
# <a name="tcpip-schema-extensions-for-input-and-output-bins"></a>入力ビンと出力ビンの TCP/IP スキーマ拡張


Bidi スキーマを拡張するために使用されて、Tcpbidi.xsd ファイル定義の 2 つの構造、InputBin OutputBin、特定のプリンターに関連する拡張機能を実装する入力と出力ビン。InputBin および OutputBin コンストラクトは両方では、次の使用可能な属性があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>name</strong></p></td>
<td><p>箱の bidi スキーマの名前。</p></td>
</tr>
<tr class="even">
<td><p><strong>mibName</strong></p></td>
<td><p>箱の MIB の名前。</p></td>
</tr>
<tr class="odd">
<td><p><strong>refreshInterval</strong></p></td>
<td><p>(省略可能)ポーリング間隔を秒単位の値。 既定値は、600 秒です。</p></td>
</tr>
</tbody>
</table>

 

### <a name="code-example"></a>コード例

コード例を次に示します、InputBin および OutputBin コンストラクトを使用して、2 つの入力ビンを識別する方法と、1 つの出力ビン。

```cpp
<Property name="Printer">
  <Property name="Layout">
    <Property name="InputBins">
      <InputBin name="TopBin"    mibName="TRAY 1"/>
      <InputBin name="BottomBin" mibName="TRAY 2"/>
    </Property>
  </Property>
  <Property name="Finishing">
    <Property name="OutputBins">
      <OutputBin name="TopBin" mibName="STANDARD BIN"/>
    </Property>
  </Property>
</Property>
```

このセクションには、次のトピックがあります。

[暗黙的な箱の拡張機能](implicit-bin-extensions.md)

[明示的な箱の拡張機能](explicit-bin-extensions.md)

[ドライバー固有のビン](driver-specific-bins.md)

 

 




