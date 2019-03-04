---
ms.assetid: C5CD87E3-26C0-48AA-B75E-1EFFB0B5519D
title: 既にあるソース ファイルからのドライバーの作成
description: WDK は Microsoft Visual Studio と統合され、Visual Studio ソリューションとプロジェクトをビルドする場合と同じコンパイラとビルド ツールを使います。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2418493c531c514011d5312d7567e02d7d8b392
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518653"
---
# <a name="creating-a-driver-from-existing-source-files"></a>既にあるソース ファイルからのドライバーの作成

WDK は Microsoft Visual Studio と統合され、Visual Studio ソリューションとプロジェクトをビルドする場合と同じコンパイラとビルド ツールを使います。 Windows Driver Kit (WDK) 8 より前のバージョンの WDK で使われていた Windows ビルド ユーティリティ (Build.exe) は、[MSBuild](https://go.microsoft.com/fwlink/p/?linkid=262804) で置き換えられました。

以前のバージョンの WDK で作成されたドライバーを変換するには、提供されている Windows ドライバー テンプレートのいずれかを使って、Visual Studio で新しい Windows ドライバー ソリューションを作成します。 ドライバー モデルのテンプレートを使って作業を始めると、プロジェクトの構造が適切に設定され、適切なプラットフォーム ツールセットが選ばれます。 その後、ソリューションにソース ファイルを追加できます。 テンプレートの選択については、「[新しいデバイス ファンクション ドライバーの作成](creating-a-new-driver.md)」、「[新しいフィルター ドライバーの作成](creating-a-new-filter-driver.md)」、または「[新しいソフトウェア ドライバーの作成](creating-a-new-software-driver.md)」をご覧ください。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [WDK と Visual Studio のビルド環境](https://msdn.microsoft.com/Library/Windows/Hardware/Hh454286)
* [ProjectUpgradeTool](https://msdn.microsoft.com/Library/Windows/Hardware/Dn265174)
* [MSBuild](https://go.microsoft.com/fwlink/p/?linkid=262804)
* [チュートリアル: MSBuild の使用](https://go.microsoft.com/fwlink/p/?linkid=262807)
* [新しいデバイス ファンクション ドライバーの作成](creating-a-new-driver.md)
* [新しいフィルター ドライバーの作成](creating-a-new-filter-driver.md)
* [新しいソフトウェア ドライバーの作成](creating-a-new-software-driver.md)
 

 






