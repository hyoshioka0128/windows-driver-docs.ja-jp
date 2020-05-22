---
title: WDK 開発者向け MSBuild 入門
description: このセクションでは、Build .exe と dism.exe に精通している WDK 開発者向けの基本的な MSBuild 用語をいくつか紹介します。 このセクションでは、単純な MSBuild プロジェクトの構築について説明します。
ms.assetid: EA223DF3-71FF-442F-B3E8-56C3B57F7B67
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78d1693eb029ff6640a5f84110a37facc68b37d1
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769630"
---
# <a name="msbuild-primer-for-wdk-developers"></a>WDK 開発者向け MSBuild 入門


このセクションでは、Build .exe と dism.exe に精通している WDK 開発者向けの基本的な MSBuild 用語をいくつか紹介します。 このセクションでは、単純な MSBuild プロジェクトの構築について説明します。

## <a name="span-idnmake_concepts_relevant_to_msbuildspanspan-idnmake_concepts_relevant_to_msbuildspanspan-idnmake_concepts_relevant_to_msbuildspannmake-concepts-relevant-to-msbuild"></a><span id="Nmake_concepts_relevant_to_MSBuild"></span><span id="nmake_concepts_relevant_to_msbuild"></span><span id="NMAKE_CONCEPTS_RELEVANT_TO_MSBUILD"></span>MSBuild に関連する Nmake の概念


以前のバージョンの WDK (WDK 8 より前のバージョン) を使用していた場合は、dism.exe が使用する用語と概念を理解していることがあります。

-   **コマンド**-コマンドラインツールを呼び出します。
-   **ターゲット**-コマンドの名前付きシーケンスについて説明します。
-   **依存関係**-他のターゲットに依存するターゲットについて説明します。
-   Nmake は、1つまたは複数のターゲットが指定された make ファイルで呼び出されます。 次に、すべての依存関係を再帰的に実行してから、ターゲットのコマンドを実行します。
-   Nmake ファイルには、ビルド構造を堅牢に管理するための他の make ファイルを含めることができます。
-   Nmake では、コマンドのパラメーターに置き換えられる名前付き変数の作成もサポートされています。
-   Nmake は、.exe 自体によって割り当てられた自動変数 (現在のディレクトリまたはパスの名前など) もサポートしています。
-   1つのビルドでターゲットが2回実行されることはありません。 実行後、ターゲットは作業を完了したと見なされ、ビルド内の後続のターゲットが依存している場合でも、再実行されません。

## <a name="span-idmsbuild_concepts_spanspan-idmsbuild_concepts_spanspan-idmsbuild_concepts_spanmsbuild-concepts"></a><span id="MSBuild_concepts_"></span><span id="msbuild_concepts_"></span><span id="MSBUILD_CONCEPTS_"></span>MSBuild の概念


-   C++ プロジェクトの MSBuild ファイルの主な拡張子は .vcxproj です。
-   コマンドは*タスク*と呼ばれるようになりました。コマンドラインプロセスを単に呼び出すだけではありません。 代わりに、タスクは、MSBuild がアトミックビルド操作を実行するために使用できる実行可能コードの単位です。 タスクの完全な一覧については、「 [Visual C++ に固有の MSBuild タスク](https://docs.microsoft.com/visualstudio/msbuild/msbuild-tasks-specific-to-visual-cpp)」を参照してください。
-   MSBuild は、次の例に示すように、 **UsingTask**要素を使用して共通言語ランタイム (CLR) アセンブリからタスクをインポートします。
    ```
    <UsingTask TaskName="TaskName" AssemblyName="AssemblyName" />
    ```

-   ターゲットは、タスクを特定の順序でグループ化し、ビルドプロセスをより小さな単位に分割できるようにします。
-   **PropertyGroup**を使用すると、わかりやすい形式でプロパティを定義できます。 次の例は、 **PropertyGroup**形式を示しています。
    ```
    <PropertyGroup>
      <ProductVersion>9.0.30729</ProductVersion>
    </PropertyGroup>
    ```

-   **項目**は、**プロパティ**のオブジェクト指向のバリアントです。 プロパティの形式は name/value ですが、item の形式は name/object で、オブジェクトには複数の属性があります。 **項目**はオブジェクトの配列です。
-   **プロパティ**は **$ (project)** という形式で参照されますが、項目は **@ (name)** という形式で参照されます。
-   **ItemGroup**は、項目のコレクションです **。**
-   **Itemgroups**は、通常、コンパイルするすべてのファイルを一覧にしたものです。 ファイルのコレクションは、 **@ (itemname)** 表記を使用してタスクに渡されます。 項目の使用方法の詳細については、「 [MSBuild 項目](https://docs.microsoft.com/visualstudio/msbuild/msbuild-items)」を参照してください **。**
-   MSBuild には、プロジェクトファイルで参照できる多くの[組み込みプロパティ](https://docs.microsoft.com/visualstudio/msbuild/msbuild-reserved-and-well-known-properties)が用意されています。
-   MSBuild とビルドタスクの詳細については、「 [msbuild の概念](https://docs.microsoft.com/visualstudio/msbuild/msbuild-concepts)と[msbuild リファレンス](https://docs.microsoft.com/visualstudio/msbuild/msbuild-reference)」を参照してください。

 

 





