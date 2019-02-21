---
title: インストールされている (TCP/IP)
description: TCP/IP がインストールされているコンス トラクターには、MIB テーブルの行の ID (OID) と、参照値の一覧のオブジェクトが含まれています。
ms.assetid: 4e14d8c1-7c66-4035-845d-f3f92dad8c4f
keywords:
- インストールされているコンス トラクター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc940e2b3b5d5f40cf0ddd587281c3782a976de2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549269"
---
# <a name="installed-tcpip"></a>インストールされている (TCP/IP)


TCP/IP がインストールされているコンス トラクターには、MIB テーブルの行の ID (OID) と、参照値の一覧のオブジェクトが含まれています。 参照値のいずれかに存在するかどうか、行、このアルゴリズムを返します**TRUE**します。 プリンターの構成に関連するほとんどのクエリでは、特定の値が、プリンターの MIB に格納されているし、ブール型の結果を返すがあるかどうかを判断する必要があります。 インストールされているコンス トラクターは、Tcpbidi.xsd で定義されます。

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
<td><p><strong>deviceIndex</strong></p></td>
<td><p>(省略可能)フラグを設定するには、A と<strong>TRUE</strong>は、関連付けられているアルゴリズムが指定した OID; で、デバイスのインデックスを含める必要がありますと<strong>FALSE</strong>OID に末尾のゼロが追加されます。 既定値は<strong>FALSE</strong>します。 詳細については、のページで、メモを参照してください。<a href="value.md" data-raw-source="[Value](value.md)">値</a>します。</p></td>
</tr>
<tr class="even">
<td><p><strong>drvPrinterEvent</strong></p></td>
<td><p>(省略可能)ポート モニターが、ドライバーに通知を送信するかどうかを示すブール値。 A <strong>TRUE</strong>値では、ドライバーをポート モニターが通知を送信することを示します<strong>FALSE</strong>ポート モニター ドライバーに、通知が送信しないことを示します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>name</strong></p></td>
<td><p>スキーマの値の名前。</p></td>
</tr>
<tr class="even">
<td><p><strong>Oid</strong></p></td>
<td><p>OID、MIB テーブルの行。</p></td>
</tr>
<tr class="odd">
<td><p><strong>refreshInterval</strong></p></td>
<td><p>ポーリング間隔を秒単位の値。 既定値は、600 秒です。</p></td>
</tr>
</tbody>
</table>

 

### <a name="code-example"></a>コード例

次のコード例では、検索アルゴリズムは、1.3.6.1.2.1.43.13.4.1.9 から MIB テーブルの行を取得します。&lt; **deviceIndex**&gt;します。 クエリが返すかどうか、このテーブルの行には、3 または 4 のいずれかが含まれています、 **TRUE**。 それ以外の場合、クエリを返します**FALSE**します。

```cpp
<Property name="DuplexUnit">
  <Installed name="Installed" oid="1.3.6.1.2.1.43.13.4.1.9" deviceIndex="true">
    <Lookup value="3"/>
    <Lookup value="4"/>
  </Installed>
</Property>
```

前の例は、次のクエリ結果します。

```cpp
\Printer.Configuration.DuplexUnit:Installed
```

 

 




