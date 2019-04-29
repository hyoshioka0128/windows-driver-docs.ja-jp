---
title: INF ファイル プラットフォーム拡張機能および x64 ベースのシステム
description: INF ファイル プラットフォーム拡張機能および x64 ベースのシステム
ms.assetid: 062c58f7-3519-4835-9597-ab6be5ff5fe8
keywords:
- x64 INF ファイル プラットフォーム拡張機能 WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ac311ac10eb3a2188309d0382392bd3a7401ef6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391995"
---
# <a name="inf-file-platform-extensions-and-x64-based-systems"></a>INF ファイル プラットフォーム拡張機能および x64 ベースのシステム


### <a href="" id="platform-extensions-and-x64-based-systems--windows-xp-and-later-"></a> プラットフォームの拡張機能と x64 ベース システム (Windows XP 以降)

Windows Server 2003 Service Pack 1 (SP1) と、後で、 **.ntamd64**プラットフォーム拡張機能が必要です、 [ **INF モデル セクション**](inf-models-section.md)します。 **.Ntamd64**または **.nt**プラットフォーム拡張機能をサポートするその他のすべてのセクションで、プラットフォームの拡張機能は省略可能です。

省略可能なプラットフォーム拡張機能をサポートするセクションでは、Windows は、次のように処理するには、どのセクションを選択します。

1. Windows をチェック、<em>セクション名</em>**.ntamd64**セクションし、1 つが存在する場合はそれを処理します。 Windows をチェック、 **.ntamd64**いずれかで処理されている INF ファイルの拡張子には、INF ファイルが含まれている (に含まれている INF ファイルは、 **Include**エントリ)。

2. 場合、<em>セクション名</em>**.ntamd64**チェック Windows にセクションが存在しない、<em>セクション名</em>**.nt** INF ファイル、またはそのいずれかのセクションINF ファイルが含まれています。 Windows の処理、存在する場合、<em>セクション名</em>**.nt**セクション。

3. 場合、<em>セクション名</em>**.nt**セクションが存在しないか、Windows の処理、*セクション名*セクション プラットフォーム拡張機能が含まれていません。

### <a href="" id="testing-installation-on-x64-based-systems--windows-server-2003-sp1-and"></a> X64 ベース システムのインストールのテスト (Windows Server 2003 SP1 以降)

テストのみを目的として、要件を[ **INF モデル セクション**](inf-models-section.md)名に含める、 **.ntamd64**拡張を抑制することができます。 この要件を抑制するサブキーの下では、次のレジストリ値エントリを作成**HKLM\\ソフトウェア\\Microsoft\\Windows\\CurrentVersion\\セットアップ**し、このエントリを 1 つに設定します。

```ini
DisableDecoratedModelsRequirement:REG_DWORD
```

設定した後、 **DisableDecoratedModelsRequirement**エントリを 1 つの値、システムを再起動し、デバイスをインストールします。

プラットフォーム拡張機能の要件を復元するには、削除、 **DisableDecoratedModelsRequirement**エントリの値または 0 に設定し、システムを再起動します。

### <a href="" id="creating-inf-files-for-x64-based-systems--windows-xp-and-later-"></a> X64 ベース システム用の INF ファイルを作成する (Windows XP 以降)

一般に、オペレーティング システムのバージョンに基づくデバイスのインストール環境間で区別する、1 つの INF ファイルを使用することはできません。 たとえば、ファイルやデバイスをサポートするレジストリ設定は、x64 ベースのオペレーティング システムのバージョン間で異なる場合、バージョンごとに、オペレーティング システムに固有の INF ファイルを作成する必要があります。

ただし、デバイスに、オペレーティング システムに固有のインストールが必要としない場合は、Windows XP を実行する x64 ベース システム用の 1 つのオペレーティング システム INF ファイルを作成できます以降。

ため、Windows Server 2003 SP1 後を必要と、 **.ntamd64**プラットフォーム拡張機能、 [ **INF モデル セクション**](inf-models-section.md) 、名前が、その他のセクションでは、この拡張機能を必要としません。含める名前、作成して、x64 ベース システム用のクロスプラット フォーム システム INF ファイルを維持するためには、最も簡単な方法は、 **.ntamd64**拡張機能の名前にのみ*モデル*セクション。

このようなクロスプラット フォーム システム INF ファイルを作成するには、次の操作を行います。

1. 」の説明に従って、すべての INF ファイルで必要とされる汎用のエントリを含む有効な INF ファイルを作成する[INF ファイルの一般的なガイドライン](general-guidelines-for-inf-files.md)します。

2. 含める、INF**製造元**セクションが含まれる、*製造元識別子*を指定する、 [ **INF モデル セクション**](inf-models-section.md)名デバイス用を指定します、 **.ntamd64**プラットフォーム拡張機能。 たとえば、次**製造元**セクションでは、INF を指定*モデル*Abc デバイス"AbcModelSection"のセクション名、および **.ntamd64**プラットフォーム拡張機能。

   ```ini
   [Manufacturer]
   ; The manufacturer-identifier for the Abc device.
   %ManufacturerName%=AbcModelSection,ntamd64
   ```

3. 含める、<em>モデル</em>**.ntamd64**セクションの名前に一致する、*モデル*によって指定されるセクション名、*製造元識別子*で、**製造元**セクション。 次の AbcModelSection など<strong>.ntamd64</strong>セクションが含まれています、Abc デバイスには、*デバイスの説明*を指定する、*インストール セクション名*の"AbcInstallSection。"

   ```ini
   [AbcModelSection.ntamd64]
   %AbcDeviceName%=AbcInstallSection,Abc-hw-id
   ```

4. 含める、 *DDInstall*セクションの名前に一致する、*インストール セクション名*で指定された、*モデル*セクション。 たとえば、*デバイス説明*AbcModelSection のセクションでは、Abc デバイスの場合は、次の AbcInstallSection セクションを指定します。

   ```ini
   [AbcInstallSection]
   ; Install section entries go here.
   ...
   ```

5. 例では、デバイスのインストールに必要なその他のデバイス固有セクションが含まれて、 **.ntamd64**プラットフォーム拡張機能は、これらのセクションの名前。 INF ファイルのセクションとディレクティブの詳細については、次を参照してください。 [INF セクションの概要](summary-of-inf-sections.md)と[INF ディレクティブの概要](summary-of-inf-directives.md)します。

すべてのプラットフォームの種類の 1 つのオペレーティング システム INF を作成する方法については、次を参照してください。[クロスプラット フォーム対応の INF ファイル](cross-platform-inf-files.md)します。

 

 





