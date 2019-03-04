---
title: Enterprise WDK 10 の使用
description: 組織で WDK を使うためにコマンド ライン ベースの環境を設定する方法について説明します。
author: Dansimp
ms.date: 08/25/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76e22cf1f7bd128c0a60cd49fe1144b404c71b63
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518730"
---
# <a name="using-the-enterprise-wdk-10"></a>Enterprise WDK 10 の使用

Enterprise Windows Driver Kit (Enterprise WDK) は、使用前のインストールが一切不要なコマンド ライン ビルド環境です。  EWDK をダウンロードした後は、バージョン管理ソフトウェアで管理したり、必要に応じてファイルを zip 圧縮してコピーしたりすることができます。  Enterprise WDK で作成される .zip ファイルには、Visual Studio ベースのドライバー プロジェクトをビルドするために必要なコンパイラー、リンカー、ビルド ツール、ヘッダー、ライブラリがすべて含まれます。

Enterprise WDK には、ドライバーと基本的な Win32 ドライバー テスト アプリケーションを構築するために必要な要素が含まれています。  好みのコード エディターを使って、ソース コードとプロジェクト ファイルを変更できます。  Enterprise WDK はコマンドライン ベースであるため、IDE、ドライバー展開、ドライバー テストなど、Visual Studio に組み込まれている機能の一部を備えていません。 



## <a name="getting-started"></a>作業の開始

> [!NOTE] 
> Windows 10 バージョン 1709 以降、Enterprise WDK は ISO ベースです。  まず、ISO をダウンロードしてマウントした後、`LaunchBuildEnv` を実行します。

1.  次の場所から EWDK をダウンロードします: [WDK と EWDK のダウンロード](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)
2.  .zip ファイルを適切な名前のディレクトリ (d:\ewdk など) に展開します。
3.  管理者コマンド プロンプトから前の手順で展開したフォルダーに移動し、**LaunchBuildEnvcmd** を実行してビルド環境を作成します。 次に、例を示します。**D:\EWDK\LaunchBuildEnv**

ビルド環境を作成した後は、それを使ってファイルを操作したり、Visual Studio プロジェクトをビルドしたりできます。 次に例を示します。  
*   Cd *directory_containing_project_files*
*   Msbuild *projectname*.vsproj

プロジェクトとソリューションに関する基本的な MSBuild コマンド:
* Msbuild project.vcxproj /p:configuration=[release | debug] /p:platform=[arm | Win32 | x64]

デスクトップ ショートカットを作成するには:

%comspec% /k pushd `<drive\dir>` && LaunchBuildEnv.cmd

ここで、`<drive\dir>` はファイルの抽出先の場所です (例: d:\ewdk)。

%comspec% /k pushd "d:\ewdk" && LaunchBuildEnv.cmd


## <a name="see-also"></a>参照

[MSBuild リファレンス](https://msdn.microsoft.com/library/0k6kkbsd.aspx)
