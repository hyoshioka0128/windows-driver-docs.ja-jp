---
ms.assetid: C5CD87E3-26C0-48AA-B75E-1EFFB0B5519D
title: 既にあるソース ファイルからのドライバーの作成
description: WDK は Microsoft Visual Studio と統合され、Visual Studio ソリューションとプロジェクトをビルドする場合と同じコンパイラとビルド ツールを使います。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e57e821e4a223107fa28d193eb68784f8eece76d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370806"
---
# <a name="creating-a-driver-from-existing-source-files"></a>既にあるソース ファイルからのドライバーの作成

WDK は Microsoft Visual Studio と統合され、Visual Studio ソリューションとプロジェクトをビルドする場合と同じコンパイラとビルド ツールを使います。 Windows Driver Kit (WDK) 8 より前のバージョンの WDK で使われていた Windows ビルド ユーティリティ (Build.exe) は、[MSBuild](https://go.microsoft.com/fwlink/p/?linkid=262804) で置き換えられました。

以前のバージョンの WDK で作成されたドライバーを変換するには、提供されている Windows ドライバー テンプレートのいずれかを使って、Visual Studio で新しい Windows ドライバー ソリューションを作成します。 ドライバー モデルのテンプレートを使って作業を始めると、プロジェクトの構造が適切に設定され、適切なプラットフォーム ツールセットが選ばれます。 その後、ソリューションにソース ファイルを追加できます。 テンプレートの選択については、「[新しいデバイス ファンクション ドライバーの作成](creating-a-new-driver.md)」、「[新しいフィルター ドライバーの作成](creating-a-new-filter-driver.md)」、または「[新しいソフトウェア ドライバーの作成](creating-a-new-software-driver.md)」をご覧ください。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [WDK と Visual Studio のビルド環境](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdk-and-visual-studio-build-environment)
* [ProjectUpgradeTool](https://docs.microsoft.com/windows-hardware/drivers/devtest/projectupgradetool)
* [MSBuild](https://go.microsoft.com/fwlink/p/?linkid=262804)
* [チュートリアル: MSBuild の使用](https://go.microsoft.com/fwlink/p/?linkid=262807)
* [新しいデバイス ファンクション ドライバーの作成](creating-a-new-driver.md)
* [新しいフィルター ドライバーの作成](creating-a-new-filter-driver.md)
* [新しいソフトウェア ドライバーの作成](creating-a-new-software-driver.md)
 

 






