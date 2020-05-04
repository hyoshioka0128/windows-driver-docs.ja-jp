---
title: INF ファイル プラットフォーム拡張機能および x64 ベースのシステム
description: INF ファイル プラットフォーム拡張機能および x64 ベースのシステム
ms.assetid: 062c58f7-3519-4835-9597-ab6be5ff5fe8
keywords:
- x64 INF ファイルプラットフォーム拡張機能、WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09b83744fb27bbe5692609f3c0e4e9cea5f90966
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223148"
---
# <a name="inf-file-platform-extensions-and-x64-based-systems"></a>INF ファイル プラットフォーム拡張機能および x64 ベースのシステム


### <a name="platform-extensions-and-x64-based-systems-windows-xp-and-later"></a><a href="" id="platform-extensions-and-x64-based-systems--windows-xp-and-later-"></a>プラットフォーム拡張機能と x64 ベースシステム (Windows XP 以降)

Windows Server 2003 Service Pack 1 (SP1) 以降では、 **ntamd64**プラットフォーム拡張機能が[**INF モデルセクション**](inf-models-section.md)に必要です。 プラットフォーム拡張機能をサポートするその他すべてのセクションでは、 **ntamd64**または**nt**プラットフォーム拡張機能は省略可能です。

オプションのプラットフォーム拡張機能をサポートするセクションでは、次のように、処理するセクションが Windows によって選択されます。

1. Windows<em>では</em>**ntamd64**セクションがチェックされ、存在する場合は処理されます。 Windows は、処理されている INF ファイルと、含まれているすべての INF ファイル (つまり、**インクルード**エントリに含まれているすべての inf ファイル) で、 **ntamd64**拡張子があるかどうかを確認します。

2. **Ntamd64**セクションが存在しない場合、WINDOWS は inf ファイルまたは含まれている inf ファイルに<em>セクション名</em>**. nt**セクションがあるかどうかを確認<em>します。</em> 存在する場合、Windows は<em>セクション-name</em>**. nt**セクションを処理します。

3. <em>セクション名</em>**. nt**セクションが存在しない場合、Windows はプラットフォーム拡張機能を含まない*セクション名*セクションを処理します。

### <a name="testing-installation-on-x64-based-systems-windows-server-2003-sp1-and-later"></a><a href="" id="testing-installation-on-x64-based-systems--windows-server-2003-sp1-and"></a>X64 ベースのシステムでのインストールのテスト (Windows Server 2003 SP1 以降)

テスト目的の場合のみ、 [**INF モデルセクション**](inf-models-section.md)名に **. ntamd64**拡張子が含まれているという要件を抑制できます。 この要件を抑制するには、サブキー **HKLM\\Software\\Microsoft\\Windows\\CurrentVersion\\Setup**の下に次のレジストリ値のエントリを作成し、この値を1に設定します。

```inf
DisableDecoratedModelsRequirement:REG_DWORD
```

**DisableDecoratedModelsRequirement** value エントリを1に設定したら、システムを再起動してから、デバイスをインストールします。

プラットフォーム拡張機能の要件を復元するには、 **DisableDecoratedModelsRequirement** value エントリを削除するか、ゼロに設定してから、システムを再起動します。

### <a name="creating-inf-files-for-x64-based-systems-windows-xp-and-later"></a><a href="" id="creating-inf-files-for-x64-based-systems--windows-xp-and-later-"></a>X64 ベースシステム用の INF ファイルの作成 (Windows XP 以降)

一般に、オペレーティングシステムのバージョンに基づいたデバイスのインストールを区別する単一の INF ファイルを使用することはできません。 たとえば、デバイスをサポートするファイルまたはレジストリ設定が x64 ベースのオペレーティングシステムのバージョンによって異なる場合は、バージョンごとにオペレーティングシステム固有の INF ファイルを作成する必要があります。

ただし、デバイスがオペレーティングシステム固有のインストールを必要としない場合は、Windows XP 以降を実行している x64 ベースのシステム用に1つのオペレーティングシステムのシステム INF ファイルを作成できます。

Windows Server 2003 SP1 以降では、 [**INF モデルセクション**](inf-models-section.md)名に**ntamd64**プラットフォーム拡張機能が必要ですが、他のセクション名にはこの拡張機能は必要ありません。そのため、x64 ベースシステム用のオペレーティングシステム以外のシステム INF ファイルを作成して維持するための最も簡単な方法は、[*モデル*の名前] セクションの**ntamd64**拡張子だけです。

このようなクロスオペレーティングシステムの INF ファイルを作成するには、次の手順を実行します。

1. 「 [Inf ファイルの一般的なガイドライン](general-guidelines-for-inf-files.md)」で説明されているように、すべての inf ファイルで必要とされる汎用エントリを含む有効な inf ファイルを作成します。

2. デバイスの[**Inf モデルセクション**](inf-models-section.md)名を指定し、 **ntamd64**プラットフォーム拡張機能を指定する*製造元識別子*を含む inf**製造元**セクションをインクルードします。 たとえば、次の**製造元**のセクションでは、Abc デバイスの場合は "AbcModelSection" という名前の INF*モデル*セクション名を指定し、 **ntamd64**プラットフォーム拡張機能を指定します。

   ```inf
   [Manufacturer]
   ; The manufacturer-identifier for the Abc device.
   %ManufacturerName%=AbcModelSection,ntamd64
   ```

3. **製造元のセクションで***製造元の識別子*で指定された*モデル*セクション名と一致する名前を持つ**ntamd64** <em>セクションをインクルードします。</em> たとえば、Abc デバイスの次の AbcModelSection<strong>ntamd64</strong>セクションには、"AbcInstallSection" という*インストールセクション*を指定する*デバイスの説明*が含まれています。

   ```inf
   [AbcModelSection.ntamd64]
   %AbcDeviceName%=AbcInstallSection,Abc-hw-id
   ```

4. [*モデル*] セクションで指定された*インストールセクション名*と一致する名前を持つ*ddinstall*セクションを含めます。 たとえば、AbcModelSection セクションの*デバイスの説明*では、Abc デバイスの次の AbcInstallSection セクションを指定しています。

   ```inf
   [AbcInstallSection]
   ; Install section entries go here.
   ...
   ```

5. デバイスのインストールに必要なその他のデバイス固有のセクションを含めますが、これらのセクションの名前には**ntamd64**プラットフォーム拡張機能を含めないでください。 INF ファイルのセクションとディレクティブの詳細については、「 [Inf セクションの概要](summary-of-inf-sections.md)」および「 [Inf ディレクティブの概要](summary-of-inf-directives.md)」を参照してください。

すべてのプラットフォームの種類に対して単一のクロスオペレーティングシステム INF を作成する方法については、「[クロスプラットフォーム Inf ファイル](cross-platform-inf-files.md)」を参照してください。

 

 





