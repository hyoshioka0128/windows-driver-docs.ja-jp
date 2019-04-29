---
title: INF ファイル プラットフォーム拡張機能および x86 ベースのシステム
description: INF ファイル プラットフォーム拡張機能および x86 ベースのシステム
ms.assetid: d0e1c6ba-32c4-413d-b0d9-620e3617a62b
keywords:
- x86 INF ファイル プラットフォーム拡張機能 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b100a09c2f2c2794963404030e95260e9727d6da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391991"
---
# <a name="inf-file-platform-extensions-and-x86-based-systems"></a>INF ファイル プラットフォーム拡張機能および x86 ベースのシステム


次の表は、Windows 2000 および以降のバージョンの Windows を実行する x86 ベース システム用のプラットフォームの拡張機能の Windows のサポートをまとめたものです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">プラットフォームの拡張機能</th>
<th align="left">プラットフォーム拡張機能のサポート (Windows 2000 以降)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>.ntamd64</strong></p></td>
<td align="left"><p>サポートされません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.ntia64</strong></p></td>
<td align="left"><p>サポートされません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>.ntarm</strong></p></td>
<td align="left"><p>サポートされません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.ntarm64</strong></p></td>
<td align="left"><p>サポートされません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>.ntx86</strong></p></td>
<td align="left"><p>拡張機能をサポートするセクションを省略可能です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.nt</strong></p></td>
<td align="left"><p>拡張機能をサポートするセクションを省略可能です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>(プラットフォーム拡張子なし)</p></td>
<td align="left"><p>既定ですべてのセクションではサポートされています。</p></td>
</tr>
</tbody>
</table>

 

X86 ベースのシステムでプラットフォーム拡張機能を使用する方法の詳細については、次のセクションを参照してください。

[プラットフォームの拡張機能と x86 ベースのシステム (Windows 2000 以降)](#platform-extensions-and-x86-based-systems--windows-2000-and-later-)

[X86 ベースのシステム (Windows 2000 以降) の INF ファイルの作成](#creating-inf-files-for-x86-based-systems--windows-2000-and-later-)

### <a href="" id="platform-extensions-and-x86-based-systems--windows-2000-and-later-"></a> プラットフォームの拡張機能とシステムの x86 ベース

Windows XP および Windows の以降のバージョンをサポートして、省略可能な **.nt**または **.ntx86**プラットフォーム拡張機能、*モデル*セクション名とをサポートするその他のセクションの名前プラットフォームの拡張機能。

Windows 2000 では、プラットフォーム拡張機能をサポートしません、 [ **INF*モデル*セクション**](inf-models-section.md)名は省略可能なサポート **.nt**または **.ntx86**プラットフォームの拡張機能プラットフォーム拡張機能をサポートするその他のセクションの名前にします。

省略可能なプラットフォーム拡張機能をサポートするセクションでは、Windows は、次のように処理するには、どのセクションを選択します。

1. Windows をチェック、<em>セクション名</em>**.ntx86**セクションし、1 つが存在する場合はそれを処理します。 Windows をチェック、 **.ntx86**いずれかで処理されている INF ファイルの拡張子には、INF ファイルが含まれている (に含まれている INF ファイルは、 **Include**エントリ)。

2. 場合、<em>セクション名</em>**.ntx86**チェック Windows にセクションが存在しない、<em>セクション名</em>**.nt** INF ファイル、またはそのいずれかのセクションINF ファイルが含まれています。 Windows の処理、存在する場合、<em>セクション名</em>**.nt**セクション。

3. 場合、<em>セクション名</em>**.nt**セクションが存在しないか、Windows の処理、*セクション名*セクション プラットフォーム拡張機能が含まれていません。

### <a href="" id="creating-inf-files-for-x86-based-systems--windows-2000-and-later-"></a> X86 ベースのシステムの INF ファイルの作成

一般に、オペレーティング システムのバージョンに基づくデバイスのインストール環境間で区別する、1 つの INF ファイルを使用することはできません。 たとえば、x86 ベースのオペレーティング システムのバージョン間でファイルやデバイスをサポートするレジストリ設定が異なる場合、バージョンごとに、オペレーティング システムに固有の INF ファイルを作成する必要があります。

ただし、デバイスにオペレーティング システムに固有のインストールが必要としない場合は、Windows 2000 および以降のバージョンの Windows を実行する x86 ベース システム用のクロスプラット フォームの 1 つのシステム INF ファイルを作成できます。

**.Nt**と **.ntx86**プラットフォーム拡張機能は省略可能、作成して、x86 ベース システム用のクロスプラット フォーム システム INF ファイルを維持するためには、最も簡単な方法では上プラットフォーム拡張機能を使用しないことセクション名。

Windows 2000 および以降のバージョンの Windows を実行する x86 ベース システム用の 1 つのオペレーティング システム INF ファイルを作成するには、次の操作を行います。

1.  」の説明に従って、すべての INF ファイルで必要とされる汎用のエントリを含む有効な INF ファイルを作成する[INF ファイルの一般的なガイドライン](general-guidelines-for-inf-files.md)します。

2.  INF を含める**製造元**セクションが含まれる、*製造元識別子*を指定する、*モデル*セクション、デバイス名が指定されていない、省略可能な **.nt**または **.ntx86**プラットフォーム拡張機能。 たとえば、次**製造元**セクションを指定します、*モデル*Abc デバイス"AbcModelSection"のセクション名。

    ```ini
    [Manufacturer]
    ; The manufacturer-identifier for the Abc device.
    %ManufacturerName%=AbcModelSection
    ```

3.  含める、*モデル*セクションの名前に一致する、*モデル*によって指定されるセクション名、*製造元識別子*で、**製造元**セクション。 たとえば、Abc デバイスの場合は、次の AbcModelSection セクションが含まれています、*デバイス説明*を指定する、*インストール セクション名*"AbcInstallSection"の。

    ```ini
    [AbcModelSection]
    %AbcDeviceName%=AbcInstallSection,Abc-hw-id
    ```

4.  含める、 *DDInstall*セクションの名前に一致する、*インストール セクション名*で指定された、*モデル*セクション。 たとえば、*デバイス説明*AbcModelSection のセクションでは、Abc デバイスの場合は、次の AbcInstallSection セクションを指定します。 Windows では、Windows 2000 以降のバージョンの Windows を実行する x86 ベースのシステムで、Abc デバイスをインストールするには、このセクションを処理します。

    ```ini
    [AbcInstallSection]
    ; Install section entries go here.
    ...
    ```

5.  例では、デバイスのインストールに必要なその他のデバイス固有セクションが含まれて、 **.nt**または **.ntx86**プラットフォーム拡張機能は、これらのセクションの名前。 Windows では、Windows 2000 以降のバージョンの Windows を実行する x86 ベースのシステムで、Abc デバイスをインストールするこれらのセクションを処理します。

INF ファイルのセクションとディレクティブの詳細については、次を参照してください。 [INF セクションの概要](summary-of-inf-sections.md)と[INF ディレクティブの概要](summary-of-inf-directives.md)します。

すべてのプラットフォームの種類のプラットフォームをまたぐ単一 INF ファイルを作成する方法については、次を参照してください。[クロスプラット フォーム対応の INF ファイル](cross-platform-inf-files.md)します。

 

 





