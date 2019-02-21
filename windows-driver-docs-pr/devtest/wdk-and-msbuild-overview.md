---
title: WDK と MSBuild の概要
description: Visual Studio では、複数のプロジェクトを管理できます。 このセクションでは、WDK ビルド環境について説明します。
ms.assetid: BABF3C72-05E9-4424-AAF9-68DFD48CEC32
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acd24d1284ab15fa62441deaa79b22aa9ce9ed7e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529649"
---
# <a name="wdk-and-msbuild-overview"></a>WDK と MSBuild の概要


Visual Studio では、複数のプロジェクトを管理できます。 このセクションでは、WDK ビルド環境について説明します。

Visual Studio ソリューションは、の 1 つのプロジェクトまたは複数のプロジェクトで構成できます: ドライバーのプロジェクトおよびドライバー以外のプロジェクトの両方。 すべてのプロジェクトでは、プラットフォーム ツールセットに関連付けられます。 プラットフォーム ツールセットは、拡張し、特定の種類のバイナリをビルドするには、指定されたターゲット アーキテクチャのビルド プロセスを変更します。 バイナリには、ドライバー、ライブラリ、または実行可能プログラムができます。

次の図は、MSBuild プラットフォームを使用して一般的なビルド プロセスを示しています。 図では、ドライバーのプロジェクト (MSBuild プロジェクト 1) はドライバーをビルドするのにドライバーのプラットフォーム ツールセットを使用します。 ドライバーのプロジェクトには、Windows カーネル モードとユーザー モードのヘッダーとライブラリを参照できます。 Windows DLL プロジェクト (MSBuild プロジェクト 2) は、DLL をビルドしますし、アプリケーションやユーザー モードのライブラリを構築、Windows SDK プラットフォーム ツールセットを使用します。 すべてのプラットフォーム ツールセットには、ターゲットの独自セットがあります。 これらのターゲットは、タスクを呼び出します。 これらのタスクでは、ビルド ツールを実行します。

C と C++ ネイティブ コード (ユーザー モードおよびカーネル モード) とマネージ コード、WDK インストール .NET Framework、Windows ヘッダー、ライブラリ (ユーザー モードまたはカーネル モード) とツール、.NET ツールと VC コンパイラ、CRT ヘッダー、およびライブラリ。 と共に、msbuild では、C と C++ プロジェクトをビルドできるように、コンパイラによって必要なすべてのコンポーネント インストールしなければなりません。

![visual studio のドライバー ソリューションの wdk と msbuild プラットフォームを示します。](images/build-platform-msbuild.png)

 

 





