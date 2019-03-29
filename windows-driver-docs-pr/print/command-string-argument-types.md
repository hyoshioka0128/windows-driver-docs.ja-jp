---
title: コマンド文字列引数型
description: コマンド文字列引数型
ms.assetid: c7540c3f-265a-4fee-aca9-b8cc10b6be8f
keywords:
- プリンターが WDK Unidrv、文字列をコマンドします。
- コマンド文字列を WDK Unidrv
- WDK Unidrv 文字列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3601e71eb0892cbbd2314ed0fcbe533763e98261
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464322"
---
# <a name="command-string-argument-types"></a>コマンド文字列引数型





コマンド文字列で引数が含まれる場合は、各引数の型を指定する必要があります。 各引数の型指定は、パーセント記号の前に、1 つの文字です。

次の表では、すべての引数の型の指定子を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>引数の型指定子</th>
<th>結果として得られる値の説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>%&lt;<em>数字</em>&gt;d</p></td>
<td><p>負の場合は、マイナス記号を含む、10 進値を表す ASCII 文字列です。 <em>&lt;数字&gt;</em>は文字列の長さを示す省略可能な番号です。</p></td>
</tr>
<tr class="even">
<td><p>%&lt;<em>数字</em>&gt;D</p></td>
<td><p>など、正または負符号、ASCII 文字列の表す 10 進数の値します。 <em>&lt;数字&gt;</em>は文字列の長さを示す省略可能な番号です。</p></td>
</tr>
<tr class="odd">
<td><p>%c</p></td>
<td><p>バイナリ バイトです。</p></td>
</tr>
<tr class="even">
<td><p>%C</p></td>
<td><p>バイナリ バイトを ASCII「0」に追加します。</p></td>
</tr>
<tr class="odd">
<td><p>%f</p></td>
<td><p>「12.25」のように、右から 3 番目の文字として挿入小数点付きの 10 進数の値を表す符号なしの ASCII 文字列。</p></td>
</tr>
<tr class="even">
<td><p>%g</p></td>
<td><p>2 * ABS (<em>パラメーター</em>) + IS_NEGATIVE (<em>パラメーター</em>) 最上位桁を base 64 指定すると、最下位の数字です。 最上位桁 (0 ~ 63) は、254 を通じて 191 のバイト数で表されます。 その他のすべての桁は 63 126 からのバイト数で表されます。 "IS_NEGATIVE (<em>パラメーター</em>)"場合は 1<em>パラメーター</em>負、および、それ以外の場合は 0 です。</p></td>
</tr>
<tr class="odd">
<td><p>%l</p></td>
<td><p>バイナリ、ワード、最下位バイトまずします。</p></td>
</tr>
<tr class="even">
<td><p>%m</p></td>
<td><p>バイナリ、ワード、最上位バイトまずします。</p></td>
</tr>
<tr class="odd">
<td><p>%n</p></td>
<td><p>Canon 整数のエンコーディング。 最上位バイトから最下位バイトにエンコードされたバイナリ値です。 4 の最下位ビットは 001 としてエンコードされます<em>sbbbb</em>ここで、 <em>s</em> 、記号を表します (0 は負の値 1 が正の値)、および<em>b</em>整数の上位ビットを表します。 [次へ] の最上位 6 ビットが 01 としてエンコードされた<em>bbbbbb</em>します。 たとえば、254 (11111110) は、(01001111 00111110) として表されます。</p></td>
</tr>
<tr class="even">
<td><p>%q</p></td>
<td><p>QUME の 16 進数を表す ASCII 文字列です。 Toshiba/Qume デバイス。</p></td>
</tr>
<tr class="odd">
<td><p>%v</p></td>
<td><p>NEC VFU (垂直形式単位) のエンコーディングします。 指定した変数の値は 1/6 インチで除算します。 VFU データは、プリンターに送信回数の合計になります。</p></td>
</tr>
</tbody>
</table>

 

任意の引数に対して許容される値の範囲を指定できます。 これを行うには、一連の角かっこの内側に配置して、引数の最小値と最大値を含める ( \[、 \] )、すぐに次の引数の型指定子と値をコンマで区切っています。 たとえば、次のコマンドでは、LinefeedSpacing/2 の値の許容範囲として 0 ~ 255 を指定します。

```cpp
*Command:CmdSetLineSpacing{*Cmd:"<1B>3"%c[0,255]{(LinefeedSpacing/2)}}
```

 

 




