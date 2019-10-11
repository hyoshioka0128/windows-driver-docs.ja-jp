---
title: プリプロセッサ ディレクティブ
description: プリプロセッサ ディレクティブ
ms.assetid: 5731b159-c6f9-47a8-8eaa-a1b0b6c12132
keywords:
- GPD file エントリ WDK Unidrv、プリプロセッサディレクティブ
- プリプロセッサディレクティブ WDK GPD ファイル
- GPD file セクションの解析
- プリプロセッサシンボル WDK GPD ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03efd7c8167ff423e5ff445b39fbebc886e16c74
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038105"
---
# <a name="preprocessor-directives"></a>プリプロセッサ ディレクティブ





GPD ファイルにはプリプロセッサディレクティブを含めることができます。このディレクティブを使用して、GPD ファイル内のセクションの条件付き解析を制御できます。 次の表では、GPD ファイルで使用できるプリプロセッサディレクティブについて説明します。

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
<td><p></em><strong>Undefine-1:<em>SymbolName</em></p></td>
<td><p>以前に定義したシンボルを削除します。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>Ifdef</strong> :<em>SymbolName</em></p></td>
<td><p>GPD file エントリのブロックの先頭を示します。</p>
<p>指定されたシンボルが定義されている場合、このディレクティブと次の *<strong>Ifdef</strong>、*<strong>Elseifdef</strong>、*<strong>Else</strong>、または *<strong>Endif</strong>ディレクティブの間の GPD ファイルのエントリは、GPD パーサーによって処理されます。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>Elseifdef @ no__t-1:<em>SymbolName</em></p></td>
<td><p>指定されたシンボルが定義されていて、前の <em><strong>Ifdef</strong>または *<strong>Elseifdef</strong>ディレクティブで指定されたシンボルが未定義の場合、このディレクティブと次の *<strong>ifdef</strong>の間の GPD ファイルエントリ、*<strong>Elseifdef</strong>、*<strong>Else</strong>、、または *<strong>Endif</strong>ディレクティブは、GPD パーサーによって処理されます。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>Else @ no__t:</p></td>
<td><p>前の <em><strong>Ifdef</strong>または *<strong>Elseifdef</strong>ディレクティブで指定されたシンボルが定義されていない場合、このディレクティブと次の *<strong>ifdef</strong>または *<strong>Endif</strong>ディレクティブの間にある GPD ファイルのエントリは、GPD パーサーによって処理されます。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>Endif @ no__t:</p></td>
<td><p>GPD file エントリのブロックの末尾を示します。</p></td>
</tr>
<tr class="odd">
<td><p><em> に<strong>含ま</strong>れます。"<em>FileName</em>"</p></td>
<td><p>追加の GPD ファイルの名前を指定します。 「<a href="using-multiple-gpd-files-in-a-minidriver.md" data-raw-source="[Using Multiple GPD Files in a Minidriver](using-multiple-gpd-files-in-a-minidriver.md)">ミニドライバーでの複数の GPD ファイルの使用」を</a>参照してください。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>SetPPPrefix @ no__t-1:<em>PrefixString</em></p></td>
<td><p>プリプロセッサディレクティブに付加されたプレフィックス文字列を変更します。 「<strong>プリプロセッサディレクティブプレフィックスの変更</strong>」セクションを参照してください。</p></td>
</tr>
</tbody>
</table>

 

条件付きプリプロセッサディレクティブは入れ子にすることができます。 各入れ子レベルでは、条件付きプリプロセッサディレクティブを使用する順序は次のとおりです。

\***Ifdef**:*Symbol1*GPD file セクション

\***Elseifdef**:*Symbol2*GPD file セクション

\***Elseifdef**:*Symbol3*GPD file セクション

\***Elseifdef**:*Symbol4*GPD file セクション

...

\***Else**:GPD file セクション

\***Endif**:

使用する \***Ifdef**ディレクティブごとに、\***Endif**が必要です。 @No__t-0**Elseifdef**ディレクティブと \***Else**ディレクティブは省略可能です。 各 GPD file セクションには、GPD ファイルエントリ、および必要に応じて、条件付きプリプロセッサディレクティブの入れ子になったシーケンスを含めることができます。

@No__t-0 の**定義**を使用して定義されたすべてのシンボルは、@no__t の**未定義**を使用して明示的に未定義になるまで定義されたままです

@No__t-0**Include**ディレクティブを使用すると、追加の GPD ファイルの名前を指定できます。 詳細については、「[ミニドライバーでの複数の GPD ファイルの使用](using-multiple-gpd-files-in-a-minidriver.md)」を参照してください。

プリプロセッサは GPD パーサーの前に実行されるため、@no__t 0IgnoreBlock GPD エントリはプリプロセッサディレクティブには影響しないことに注意してください。

### <a href="" id="ddk-changing-the-preprocessor-directive-prefix-gg"></a>プリプロセッサディレクティブのプレフィックスを変更する

@No__t-0**Setppprefix**ディレクティブを使用すると、プリプロセッサディレクティブで使用されるプレフィックスを変更できます。 つまり、このディレクティブを使用すると、プリプロセッサディレクティブの前にあるアスタリスク (\*) 文字を別の文字または文字列に置き換えることができます。

たとえば、GPD ファイルに次のディレクティブが含まれているとします。

```cpp
*SetPPPrefix: #SpecialPrefix#
```

次に、プリプロセッサは **\*** で始まるプリプロセッサディレクティブの検索を停止し、代わりに **\#特別なプレフィックス @ no__t から**始まるディレクティブを検索します。 次のシーケンスは、プリプロセッサプリフィックスを一時的に **\#no__t-2**に変更し、その後 **\*** に復元します。

```cpp
*SetPPPrefix: #SpecialPrefix#
#SpecialPrefix#Ifdef: WINNT_50
#SpecialPrefix#Include: "ExtraGPD.gpd"
#SpecialPrefix#Endif:
#SpecialPrefix#SetPPPrefix: *
```

この機能の主な目的は、将来のオペレーティングシステムのバージョン用に記述された GPD ファイルに Windows 2000 との互換性を持たせることです。 たとえば、将来のバージョンのオペレーティングシステム用の GPD ファイルに、Windows 2000 でサポートされているアスタリスクプレフィックスが付いたプリプロセッサディレクティブと競合する GPD ファイルエントリを含めることができるとします。 プレフィックスを変更することにより、将来のオペレーティングシステムのバージョン用に記述された GPD ファイルを Windows 2000 で使用することもできます。 例として、次のようなものがあります。

```cpp
*Ifdef: WINNT_70
    *SetPPPrefix: #SpecialPrefix#
    *% Do special, OS-specific processing of
    *% GPD file entries that might conflict with
    *% asterisk-prefixed preprocessor directives.
    #SpecialPrefix#SetPPPrefix: *
*Endif:
```

この手法では、プリプロセッサが検索するプレフィックスのみが変更されることに注意してください。 パーサーによって認識されるキーワードの前には、常にアスタリスクが付いている必要があります。

### <a href="" id="ddk-predefined-preprocessor-symbols-gg"></a>定義済みプリプロセッサシンボル

Microsoft では、次のプリプロセッサシンボルを定義しています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>シンボル</th>
<th>定義された場所</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WINNT_51</p></td>
<td><p>Windows XP 用 GPD プリプロセッサ</p></td>
<td><p>環境は Windows XP です。</p></td>
</tr>
<tr class="even">
<td><p>WINNT_50</p></td>
<td><p>Windows XP および Windows 2000 用 GPD プリプロセッサ</p></td>
<td><p>環境は Windows 2000 です。</p></td>
</tr>
<tr class="odd">
<td><p>WINNT_40</p></td>
<td><p>GPD プリプロセッサ for Windows XP、Windows 2000、および Windows NT 4.0</p></td>
<td><p>環境は Windows NT 4.0 です。</p></td>
</tr>
<tr class="even">
<td><p>PARSER_VER_ 1.0</p></td>
<td><p>GPD プリプロセッサ for Windows NT 4.0、Windows 2000、および Windows XP</p></td>
<td><p>GPD パーサーバージョン1.0</p></td>
</tr>
</tbody>
</table>

 

WINNT @ no__t-040、WINNT @ no__t-150、および WINNT @ no__t-251 シンボルは、Windows NT 4.0、Windows 2000、および Windows XP と互換性のある GPD ファイルを作成する場合に便利です。 たとえば、Windows XP で Windows 2000 でサポートされていないプリンター機能がサポートされている場合、\***Ifdef**によって制限された GPD file セクション内でその機能を指定できます。WINNT @ no__t-051 と \***Endif**ディレクティブ。

 

 




