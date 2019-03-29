---
title: プリプロセッサ ディレクティブ
description: プリプロセッサ ディレクティブ
ms.assetid: 5731b159-c6f9-47a8-8eaa-a1b0b6c12132
keywords:
- GPD ファイル エントリ WDK Unidrv、プリプロセッサ ディレクティブ
- WDK GPD ファイルのプリプロセッサ ディレクティブ
- GPD ファイル セクションの解析
- プリプロセッサ シンボル WDK GPD ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4d8a855c0cfc79cfd2ce46480ce8ff6c2fcaf01
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464100"
---
# <a name="preprocessor-directives"></a>プリプロセッサ ディレクティブ





GPD ファイルは、GPD ファイル内のセクションの条件付きの解析を制御するために使用できる、プリプロセッサ ディレクティブを含めることができます。 次の表では、GPD ファイルで使用できるプリプロセッサ ディレクティブについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PreprocessorDirective</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em><strong>定義</strong>:<em>SymbolName</em></p></td>
<td><p>シンボルを定義します。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>未定義</strong>:<em>シンボル</em></p></td>
<td><p>以前に定義されたシンボルを削除します。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>Ifdef</strong> :<em>SymbolName</em></p></td>
<td><p>GPD ファイル エントリのブロックの先頭を示します。</p>
<p>このディレクティブと、次のエントリ ファイル、GPD の指定されたシンボルが定義されている場合 *<strong>Ifdef</strong>、*<strong>Elseifdef</strong>、*<strong>Else</strong>、または *<strong>Endif</strong>ディレクティブが GPD パーサーによって処理されます。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>Elseifdef</strong> :<em>シンボル</em></p></td>
<td><p>指定されたシンボルが定義されているし、前でシンボルが指定された場合<em> <strong>Ifdef</strong>または *<strong>Elseifdef</strong>ディレクティブは未定義の場合、このディレクティブと、次の GPD ファイルのエントリ *<strong>Ifdef</strong>、*<strong>Elseifdef</strong>、*<strong>Else</strong>、または *<strong>Endif</strong>ディレクティブが GPD パーサーによって処理されます。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>Else</strong> :</p></td>
<td><p>前に、シンボルが指定されている場合<em> <strong>Ifdef</strong>または *<strong>Elseifdef</strong>ディレクティブは未定義の場合、このディレクティブと、次の GPD ファイルのエントリ *<strong>Ifdef</strong>または *<strong>Endif</strong>ディレクティブが GPD パーサーによって処理されます。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>Endif</strong> :</p></td>
<td><p>GPD ファイル エントリのブロックの終了を示します。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>含める</strong>:"<em>FileName</em>"</p></td>
<td><p>追加の GPD ファイルの名前を指定します。 参照してください<a href="using-multiple-gpd-files-in-a-minidriver.md" data-raw-source="[Using Multiple GPD Files in a Minidriver](using-multiple-gpd-files-in-a-minidriver.md)">、ミニドライバーにファイルを複数 GPD を使用して</a>します。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>SetPPPrefix</strong> :<em>PrefixString</em></p></td>
<td><p>プリプロセッサ ディレクティブを先頭に付加するプレフィックス文字列を変更します。 参照してください、<strong>プリプロセッサ ディレクティブのプレフィックスを変更する</strong>セクション。</p></td>
</tr>
</tbody>
</table>

 

条件付きプリプロセッサ ディレクティブは入れ子にすることができます。 各入れ子のレベルでの条件付きプリプロセッサ ディレクティブを使用して順序を指定のとおりです。

\***Ifdef**:*Symbol1* GPD ファイル セクション

\***Elseifdef**:*Symbol2* GPD ファイル セクション

\***Elseifdef**:*Symbol3* GPD ファイル セクション

\***Elseifdef**:*Symbol4* GPD ファイル セクション

...

\***Else**:GPD ファイル セクション

\***Endif**:

各\* **Ifdef**ディレクティブの使用、 \* **Endif**が必要です。 \* **Elseifdef**と\* **Else**ディレクティブは省略可能です。 各 GPD ファイルのセクションでは、GPD ファイルのエントリと、必要に応じて、条件付きプリプロセッサ ディレクティブの入れ子になったシーケンスに含めることができます。

使用して定義されているすべてのシンボル\***定義**を使用して明示的に未定義まで定義\***定義を解除**します。

\* **Include**ディレクティブでは、追加の GPD ファイルの名前を指定できます。 詳細については、次を参照してください。[複数 GPD ファイルで、ミニドライバーを使用して](using-multiple-gpd-files-in-a-minidriver.md)します。

なお、 \*IgnoreBlock GPD エントリには影響しません、プリプロセッサ ディレクティブ GPD パーサーの前に、プリプロセッサが実行されるためです。

### <a href="" id="ddk-changing-the-preprocessor-directive-prefix-gg"></a>プリプロセッサ ディレクティブのプレフィックスを変更します。

\* **SetPPPrefix**ディレクティブでは、プリプロセッサ ディレクティブで使用されるプレフィックスを変更できます。 つまり、アスタリスクを置換するこのディレクティブを使用することができます (\*) 文字、プリプロセッサ ディレクティブが別の文字または文字列の先頭に付加します。

たとえば、次のように、GPD ファイルには、次のディレクティブが含まれている場合。

```cpp
*SetPPPrefix: #SpecialPrefix#
```

プリプロセッサ ディレクティブで始まるの検索を中止プリプロセッサ**\\*** し、以降のディレクティブの代わりに検索**\#SpecialPrefix\#**. 次の順序は、プリプロセッサのプレフィックスを一時的に変更 **\#SpecialPrefix\#**、しに、復元 * *\\* * *。

```cpp
*SetPPPrefix: #SpecialPrefix#
#SpecialPrefix#Ifdef: WINNT_50
#SpecialPrefix#Include: "ExtraGPD.gpd"
#SpecialPrefix#Endif:
#SpecialPrefix#SetPPPrefix: *
```

この機能の主な目的は、GPD ファイルが Windows 2000 と互換性があるオペレーティング システムの今後のバージョン用に記述できるようにします。 たとえば、オペレーティング システムの将来のバージョンの GPD ファイルは、Windows 2000 でサポートされているアスタリスク プレフィックス付きプリプロセッサ ディレクティブと競合する GPD ファイルのエントリを含めることができます。 プレフィックスを変更すると、将来のオペレーティング システムのバージョン用に記述された GPD ファイルを Windows 2000 では使用もできます。 例は、次のように構築された可能性があります。

```cpp
*Ifdef: WINNT_70
    *SetPPPrefix: #SpecialPrefix#
    *% Do special, OS-specific processing of
    *% GPD file entries that might conflict with
    *% asterisk-prefixed preprocessor directives.
    #SpecialPrefix#SetPPPrefix: *
*Endif:
```

この手法は、プリプロセッサを検索するプレフィックスをのみ変更に注意してください。 アスタリスクは、パーサーで認識されるキーワードを前に必ず必要があります。

### <a href="" id="ddk-predefined-preprocessor-symbols-gg"></a>定義済みプリプロセッサ シンボル

Microsoft では、次のプリプロセッサ シンボルを定義します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>シンボル</th>
<th>定義されている場所</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WINNT_51</p></td>
<td><p>Windows XP のプリプロセッサ GPD</p></td>
<td><p>環境では、Windows XP です。</p></td>
</tr>
<tr class="even">
<td><p>WINNT_50</p></td>
<td><p>Windows XP および Windows 2000 のプリプロセッサ GPD</p></td>
<td><p>環境では、Windows 2000 です。</p></td>
</tr>
<tr class="odd">
<td><p>WINNT_40</p></td>
<td><p>Windows XP、Windows 2000、および Windows NT 4.0 GPD プリプロセッサ</p></td>
<td><p>環境は、Windows NT 4.0 です。</p></td>
</tr>
<tr class="even">
<td><p>PARSER_VER_1.0</p></td>
<td><p>Windows NT 4.0、Windows 2000、Windows XP 用 GPD プリプロセッサ</p></td>
<td><p>GPD パーサーのバージョン 1.0</p></td>
</tr>
</tbody>
</table>

 

WINNT\_40、WINNT\_50、および WINNT\_51 シンボルは Windows NT 4.0、Windows 2000、Windows XP と互換性のある GPD ファイルを作成するために役立ちます。 かどうか、たとえば、Windows XP は、Windows 2000 ではサポートされていないプリンター機能をサポートしで区切られた GPD ファイル セクション内でその機能を指定できます\* **Ifdef**:WINNT\_51 と\* **Endif**ディレクティブ。

 

 




