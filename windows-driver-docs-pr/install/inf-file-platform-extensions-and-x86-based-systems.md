---
title: INF ファイル プラットフォーム拡張機能および x86 ベースのシステム
description: INF ファイル プラットフォーム拡張機能および x86 ベースのシステム
ms.assetid: d0e1c6ba-32c4-413d-b0d9-620e3617a62b
keywords:
- x86 INF ファイルプラットフォーム拡張機能 (WDK)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 782ad30f4a755c4bd6119a1fb54a18c438b17f44
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223146"
---
# <a name="inf-file-platform-extensions-and-x86-based-systems"></a>INF ファイル プラットフォーム拡張機能および x86 ベースのシステム


次の表は、windows 2000 以降のバージョンの Windows を実行している x86 ベースのシステム用のプラットフォーム拡張機能の Windows サポートをまとめたものです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">プラットフォーム拡張機能</th>
<th align="left">プラットフォーム拡張機能のサポート (Windows 2000 以降)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>.ntamd64</strong></p></td>
<td align="left"><p>サポートされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.ntia64</strong></p></td>
<td align="left"><p>サポートされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>。 ntarm</strong></p></td>
<td align="left"><p>サポートされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.ntarm64</strong></p></td>
<td align="left"><p>サポートされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>.ntx86</strong></p></td>
<td align="left"><p>拡張機能をサポートするセクションでは省略可能です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>. nt</strong></p></td>
<td align="left"><p>拡張機能をサポートするセクションでは省略可能です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>(プラットフォーム拡張機能なし)</p></td>
<td align="left"><p>すべてのセクションで既定でサポートされています。</p></td>
</tr>
</tbody>
</table>

 

X86 ベースのシステムでプラットフォーム拡張機能を使用する方法の詳細については、次のセクションを参照してください。

[プラットフォーム拡張機能と x86 ベースシステム (Windows 2000 以降)](#platform-extensions-and-x86-based-systems--windows-2000-and-later-)

[X86 ベースのシステム用の INF ファイルの作成 (Windows 2000 以降)](#creating-inf-files-for-x86-based-systems--windows-2000-and-later-)

### <a name="platform-extensions-and-x86-based-systems"></a><a href="" id="platform-extensions-and-x86-based-systems--windows-2000-and-later-"></a>プラットフォーム拡張機能と x86 ベースシステム

Windows XP 以降のバージョンの Windows では、*モデル*セクション名とプラットフォーム拡張機能をサポートする他のセクションの名前に対して、省略可能な**nt**または**ntx86**プラットフォーム拡張機能がサポートされています。

Windows 2000 は、 [**INF*モデル*セクション**](inf-models-section.md)名のプラットフォーム拡張機能をサポートしていませんが、プラットフォーム拡張機能をサポートする他のセクションの名前には、省略可能な**nt**または**ntx86**プラットフォーム拡張機能をサポートしています。

オプションのプラットフォーム拡張機能をサポートするセクションでは、次のように、処理するセクションが Windows によって選択されます。

1. Windows<em>では</em>**ntx86**セクションがチェックされ、存在する場合は処理されます。 Windows は、処理されている INF ファイルと、含まれているすべての INF ファイル (つまり、**インクルード**エントリに含まれているすべての inf ファイル) で、 **ntx86**拡張子があるかどうかを確認します。

2. **Ntx86**セクションが存在しない場合、WINDOWS は inf ファイルまたは含まれている inf ファイルに<em>セクション名</em>**. nt**セクションがあるかどうかを確認<em>します。</em> 存在する場合、Windows は<em>セクション-name</em>**. nt**セクションを処理します。

3. <em>セクション名</em>**. nt**セクションが存在しない場合、Windows はプラットフォーム拡張機能を含まない*セクション名*セクションを処理します。

### <a name="creating-inf-files-for-x86-based-systems"></a><a href="" id="creating-inf-files-for-x86-based-systems--windows-2000-and-later-"></a>X86 ベースのシステム用の INF ファイルの作成

一般に、オペレーティングシステムのバージョンに基づいたデバイスのインストールを区別する単一の INF ファイルを使用することはできません。 たとえば、デバイスをサポートするファイルまたはレジストリ設定が、x86 ベースのオペレーティングシステムのバージョンによって異なる場合は、バージョンごとにオペレーティングシステム固有の INF ファイルを作成する必要があります。

ただし、デバイスでオペレーティングシステム固有のインストールを必要としない場合は、Windows 2000 以降のバージョンの Windows を実行する x86 ベースのシステム用に、単一のオペレーティングシステムのシステム INF ファイルを作成できます。

**Nt**および**ntx86**プラットフォーム拡張機能は省略可能であるため、x86 ベースのシステム用のオペレーティングシステム以外のシステム INF ファイルを作成して維持するための最も簡単な方法は、セクション名でプラットフォーム拡張機能を使用しないことです。

Windows 2000 以降のバージョンの Windows を実行する x86 ベースのシステム用の単一のオペレーティングシステム INF ファイルを作成するには、次の手順を実行します。

1.  「 [Inf ファイルの一般的なガイドライン](general-guidelines-for-inf-files.md)」で説明されているように、すべての inf ファイルで必要とされる汎用エントリを含む有効な inf ファイルを作成します。

2.  デバイスの [*モデル*] セクションの名前を指定する*製造元の識別子*を含む INF **manufacturer**セクションを含めますが、省略可能な**nt**または**ntx86**プラットフォーム拡張機能は指定しません。 たとえば、次の**製造元**のセクションでは、Abc デバイスに対して "AbcModelSection" という*モデル*セクション名を指定しています。

    ```inf
    [Manufacturer]
    ; The manufacturer-identifier for the Abc device.
    %ManufacturerName%=AbcModelSection
    ```

3.  **製造元のセクションで***製造元の識別子*によって指定された*モデル*セクション名と一致する名前を持つ*モデル*セクションを含めます。 たとえば、Abc デバイスの次の AbcModelSection セクションには、"AbcInstallSection" の*インストールセクション名*を指定する*デバイスの説明*が含まれています。

    ```inf
    [AbcModelSection]
    %AbcDeviceName%=AbcInstallSection,Abc-hw-id
    ```

4.  [*モデル*] セクションで指定された*インストールセクション名*と一致する名前を持つ*ddinstall*セクションを含めます。 たとえば、AbcModelSection セクションの*デバイスの説明*では、Abc デバイスの次の AbcInstallSection セクションを指定しています。 Windows では、windows 2000 以降のバージョンの Windows を実行している x86 ベースのシステムに Abc デバイスをインストールするために、このセクションを処理します。

    ```inf
    [AbcInstallSection]
    ; Install section entries go here.
    ...
    ```

5.  デバイスをインストールするために必要なその他のデバイス固有のセクションを含めますが、これらのセクションの名前には、 **nt**または**ntx86**プラットフォーム拡張機能を含めないでください。 Windows では、windows 2000 以降のバージョンの Windows を実行している x86 ベースのシステムに Abc デバイスをインストールするために、これらのセクションを処理します。

INF ファイルのセクションとディレクティブの詳細については、「 [Inf セクションの概要](summary-of-inf-sections.md)」および「 [Inf ディレクティブの概要](summary-of-inf-directives.md)」を参照してください。

すべてのプラットフォームの種類に対して単一のクロスプラットフォーム INF ファイルを作成する方法の詳細については、「[クロスプラットフォーム Inf ファイル](cross-platform-inf-files.md)」を参照してください。

 

 





