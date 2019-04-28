---
title: WDK と Visual Studio のビルド環境
description: WDK 8、Windows Driver Kit (WDK) 8.1 では、主要な変更を導入するドライバーをビルドするために使用します。
ms.assetid: B964CF3F-ACDB-41ED-8962-B7DDB957D7D3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e01ecc15c40dd9d9e6eeca1fd6cbc3f259026cc2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371532"
---
# <a name="wdk-and-visual-studio-build-environment"></a>WDK と Visual Studio のビルド環境


WDK 8、Windows Driver Kit (WDK) 8.1 では、主要な変更を導入するドライバーをビルドするために使用します。 WDK は、不要になった Build.exe を使用します。 ドライバー WDK ビルド環境では、MSBuild.exe を使用し、Visual Studio 開発環境に完全に統合します。 これは、ソース ファイル、makefile.inc、makefile.new およびその他が以前のバージョンの WDK に存在するファイルは使用されなくビルドを関連することを意味します。 これで、WDK を使用すると、作成、編集、ビルド、テスト、および Visual Studio でのドライバーを展開できます。 このドキュメントの目的は、WDK 8.1 と WDK 8 の概要での以前の Wdk に慣れているユーザーに役立つ情報を提供することです。

**注**  WDK 8.1 と Microsoft Visual Studio 2013 を使用するプロジェクトとソリューションの WDK 8 で作成されたをアップグレードする必要があります。 プロジェクトやソリューションを開く前に、[ProjectUpgradeTool](projectupgradetool.md) を実行してください。 ProjectUpgradeTool では、WDK 8.1 を使用して構築できるように、プロジェクトとソリューションを変換します。

 

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="msbuild-primer-for-wdk-developers.md" data-raw-source="[MSBuild primer for WDK developers](msbuild-primer-for-wdk-developers.md)">WDK の開発者向けの MSBuild 入門</a></p></td>
<td align="left"><p>このセクションで Build.exe と NMake.exe に精通する WDK 開発者に基本的な MSBuild 用語を紹介します。 このセクションでは、単純な MSBuild プロジェクトの構築が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdk-and-msbuild-overview.md" data-raw-source="[WDK and MSBuild overview](wdk-and-msbuild-overview.md)">WDK と MSBuild の概要</a></p></td>
<td align="left"><p>Visual Studio では、複数のプロジェクトを管理できます。 このセクションでは、WDK ビルド環境について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="platform-toolset.md" data-raw-source="[Platform Toolset](platform-toolset.md)">プラットフォーム ツールセット</a></p></td>
<td align="left"><p>Windows Driver Kit (WDK) では、ツール、およびドライバーの開発に固有のライブラリを提供する MSBuild プラットフォーム ツールセットの機能を利用します。 MSBuild プラットフォーム ツールセットの機能は、拡張可能です。 使用するプラットフォーム ツールセットの特定のバージョンと呼ばれる MSBuild プロパティによって制御される<strong>PlatformToolset</strong>します。 プロジェクトは、ツールとライブラリ間を設定して切り替えることができます、 <strong>PlatformToolset</strong>プロジェクト ファイルのプロパティ。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="windows-driver-specific-property-files.md" data-raw-source="[Windows driver-specific property files](windows-driver-specific-property-files.md)">Windows ドライバー固有のプロパティ ファイル</a></p></td>
<td align="left"><p>ドライバーのプロパティ シートでは、すべてのドライバー プロジェクトのビルドに MSBuild を使用するツールの既定の設定があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="windows-driver-targets.md" data-raw-source="[Windows driver targets](windows-driver-targets.md)">Windows ドライバーのターゲット</a></p></td>
<td align="left"><p>WindowsDriver.Common.targets、WindowsDriver.masm.targets、WindowsDriver.arm.targets ファイルは、ドライバーをビルドするために必要なターゲットを提供します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdk-build-output.md" data-raw-source="[WDK build output](wdk-build-output.md)">WDK ビルド出力</a></p></td>
<td align="left"><p>既定では、WDK は、中間ディレクトリを使用して<strong>$ (intdir)</strong>マクロを既定のビルド出力ディレクトリを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdk-tasks-for-msbuild.md" data-raw-source="[WDK tasks for MSBuild](wdk-tasks-for-msbuild.md)">MSBuild の WDK タスク</a></p></td>
<td align="left"><p>Windows Driver Kit (WDK) には、ビルド プロセスでよく使用されますが、Visual Studio では正常に配布されていないツールが含まれています。 これらのツールは、ドライバーまたはドライバー パッケージの署名には、ソフトウェアのトレースを実装するか、処理 (stampinf.exe、mc.exe、tracewpp.exe、binplace.exe など) は、リソースまたはメッセージのファイルをコンパイルに使用されます。 これらのコマンド ライン ツールは、ビルド プロセス中に実行できるようにする MSBuild タスク (ターゲットに含まれます) として公開する必要があります。 WDK は、ドライバーをビルドするときに、MSBuild タスクとしてこれらのツールを実行できるように、必要なコンポーネントを提供します。</p></td>
</tr>
</tbody>
</table>

 

 

 





