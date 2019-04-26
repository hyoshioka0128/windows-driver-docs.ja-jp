---
title: クロスプラットフォームの INF ファイル
description: クロスプラットフォームの INF ファイル
ms.assetid: 5f7e80d2-b8b5-4ce9-9e70-cacc51223deb
keywords:
- クロス プラットフォームの INF ファイル WDK
- INF ファイル WDK デバイス インストールでは、クロス プラットフォーム
- WDK、クロスプラット フォーム システム INF ファイルのオペレーティング システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee9118a88cd58d5a3219f906d879d34da5175083
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352077"
---
# <a name="cross-platform-inf-files"></a>クロスプラットフォームの INF ファイル


クロス プラットフォームの INF ファイルの最も簡単な方法では、この方法は最も簡単な作成および管理するため、各プラットフォームの種類に個別の INF ファイルを作成します。 プラットフォームに固有の INF ファイルを作成する方法の詳細については、次のトピックを参照してください。

[X64 ベース システム用の INF ファイルを作成する (Windows XP 以降)](inf-file-platform-extensions-and-x64-based-systems.md#creating-inf-files-for-x64-based-systems--windows-xp-and-later-)

[X86 ベースのシステム (Windows 2000 以降) の INF ファイルの作成](inf-file-platform-extensions-and-x86-based-systems.md#creating-inf-files-for-x86-based-systems--windows-2000-and-later-)

デバイスがオペレーティング システムに固有のインストール要件を持たない場合、1 つのオペレーティング システムとデバイスのクロスプラット フォーム対応の INF ファイルを作成できます。 たとえば、ファイルやデバイスをサポートするレジストリ設定は、特定のプラットフォーム オペレーティング システムのバージョンとの間が異なる場合、そのプラットフォームの種類のすべてのオペレーティング システムのバージョンでサポートされている 1 つの INF ファイル一般に、作成することはできません。

1 つのオペレーティング システムおよび Windows 2000 および以降のバージョンの Windows のクロスプラット フォーム対応の INF ファイルを作成するには、最も簡単な方法はとおりです。

-   使用して、 **.ntia64**プラットフォームの拡張機能のセクションでは、Itanium ベース システムのコンポーネントをインストールして使用するために必要な名前に **.ntamd64**はセクションの名前で、プラットフォームの拡張機能x64 ベース システムにコンポーネントをインストールする必要です。

-   **.Nt**と **.ntx86**プラットフォーム拡張機能をサポートするすべてのセクションで、プラットフォーム拡張機能は省略可能、使用しないでください、 **.nt**または **.ntx86**プラットフォーム拡張機能は、x86 ベースのシステムでコンポーネントをインストールするセクションの名前。

を 1 つのオペレーティング システムと Microsoft Windows 2000 および以降のバージョンの Windows のクロスプラット フォーム対応の INF ファイルを作成するには、次のプロセスを使用します。

-   使用して、 **.ntia64**プラットフォームの拡張機能のセクションでは、Itanium ベース システムのコンポーネントをインストールして使用するために必要な名前に **.ntamd64**はセクションの名前で、プラットフォームの拡張機能x64 ベース システムにコンポーネントをインストールする必要です。

1 つのオペレーティング システムとオペレーティング システムに固有の要件がないデバイスのクロスプラット フォーム対応の INF ファイルを作成するすべてのプラットフォームの種類をサポートしています、Windows 2000 と Windows の以降のバージョンをサポートする、次の操作します。

1. 」の説明に従って、すべての INF ファイルで必要とされる汎用のエントリを含む有効な INF ファイルを作成する[INF ファイルの一般的なガイドライン](general-guidelines-for-inf-files.md)します。

2. 含める、INF**製造元**セクションが含まれる、*製造元識別子*を指定する、*モデル*デバイスおよびプラットフォーム拡張機能のエントリのセクション名デバイスをサポートしているプラットフォームごとにします。 たとえば、次のセクションの製造元を指定します、*モデル*"AbcModelSection"およびプラットフォーム拡張機能のセクション名 **.ntia64**と **.ntamd64**します。 (指定しない、 **.ntx86**プラットフォーム拡張機能です)。

   ```cpp
   [Manufacturer]
   ; The manufacturer-identifier for the Abc device.
   %ManufacturerName%=AbcModelSection,ntia64,ntamd64
   ```

3. 含める、*モデル*セクションの名前を持つはプラットフォームの拡張機能が含まれません。 Windows 2000 以降、オペレーティング システムは、x86 ベースのシステムは、このセクションを処理します。 たとえば、AbcModelSection の次のセクションを指定します、*インストール セクション名*"AbcInstallSection"デバイスの Abc の。

   ```cpp
   [AbcModelSection]
   %AbcDeviceName%=AbcInstallSection,Abc-hw-id
   ```

4. 含める、<em>モデル</em>**.ntia64**セクション。 Windows Server 2003 SP1 と以降のバージョンが必要です、<em>モデル</em>**.ntia64** Itanium ベース システム用のセクション。 場合、<em>モデル</em>**.ntia64**セクションが存在する場合、Itanium ベース システム用に、このセクションで使用も Windows Server 2003 および Windows XP。 次の AbcModelSection など<strong>.ntia64</strong>セクションを指定します、*インストール セクション名*"AbcInstallSection.ntia64"デバイスの Abc の。

   ```cpp
   [AbcModelSection.ntia64]
   %AbcDeviceName%=AbcInstallSection.ntia64,Abc-hw-id
   ```

5. 含める、<em>モデル</em>**.ntamd64**セクション。 Windows Server 2003 SP1 と以降のバージョンが必要です、<em>モデル</em>**.ntamd64** x64 ベース システム用のセクション。 場合、<em>モデル</em>**.ntamd64**セクションが存在する、Windows Server 2003 および Windows XP x64 ベース システムこのセクションを使用しても。 次の AbcModelSection など<strong>.ntamd64</strong>セクションを指定します、*インストール セクション名*"AbcInstallSection.ntamd64"デバイスの Abc の。

   ```cpp
   AbcModelSectionName.ntamd64
   %AbcDeviceName%=AbcInstallSection.ntamd64,Abc-hw-id
   ```

6. 含める、 *DDInstall*セクションの名前が同じとして、*インストール セクション名*で指定された、*モデル*プラットフォーム拡張機能が含まれていないセクション。 たとえば、AbcModelSection セクションでは、AbcInstallSection の次のセクションを指定します。 Windows では、Windows 2000 またはそれ以降のバージョンの Windows を実行する x86 ベースのシステムで、Abc デバイスをインストールするには、このセクションを処理します。

   ```cpp
   [AbcInstallSection]
   ; Install section entries go here.
   ...
   ```

7. 含める、 <em>DDInstall</em>**.ntia64**名前が同じセクションとして、*インストール セクション名*で指定された、<em>モデル</em>**.ntia64**セクション。 AbcModelSection など<strong>.ntia64</strong>セクションでは、次の AbcInstallSection を指定します。<strong>.ntia64</strong>セクション。 Windows では、Windows XP または Windows の以降のバージョンを実行する Itanium ベース システムで、Abc デバイスをインストールするには、このセクションを処理します。

   ```cpp
   [AbcInstallSection.ntia64]
   ; Install section entries go here.
   ...
   ```

8. 含める、 <em>DDInstall</em>**.ntamd64**名前が同じセクションとして、*インストール セクション名*で指定された、<em>モデル</em>**.ntamd64**セクション。 AbcModelSection など<strong>.ntamd64</strong>セクションでは、次の AbcInstallSection を指定します。<strong>.ntamd64</strong>セクション。 Windows では、Windows XP または Windows の以降のバージョンを実行する x64 ベース システムで、Abc デバイスをインストールするには、このセクションを処理します。

   ```cpp
   [AbcInstallSection.ntamd64]
   ; Install section entries go here.
   ...
   ```

9. X86 ベースのインストールに必要な追加のデバイス固有のセクションが含まれます。 含めないでください、 **.ntx86**プラットフォーム拡張機能は、これらのセクションの名前。 Windows では、既定では、デバイスを Windows 2000 またはそれ以降のバージョンの Windows を実行する x86 ベースのシステムにインストールするこれらのセクションを処理します。

10. Windows XP または Windows の以降のバージョンを実行する Itanium ベース システム用に必要な追加のデバイス固有のセクションが含まれます。 含める、 **.ntia64**これらセクション名で拡張機能。

11. Windows XP または Windows の以降のバージョンを実行する x64 ベース システム用に必要な追加のデバイス固有のセクションが含まれます。 含める、 **.ntamd64**これらセクション名で拡張機能。

INF ファイルのセクションとディレクティブの詳細については、次を参照してください。 [INF セクションの概要](summary-of-inf-sections.md)と[INF ディレクティブの概要](summary-of-inf-directives.md)します。

 

 





