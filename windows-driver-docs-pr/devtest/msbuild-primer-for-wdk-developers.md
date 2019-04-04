---
title: WDK の開発者向けの MSBuild 入門
description: このセクションで Build.exe と NMake.exe に精通する WDK 開発者に基本的な MSBuild 用語を紹介します。 このセクションでは、単純な MSBuild プロジェクトの構築が表示されます。
ms.assetid: EA223DF3-71FF-442F-B3E8-56C3B57F7B67
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4745f3c158ecc2732ce373e305795edc9ca9178
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550682"
---
# <a name="msbuild-primer-for-wdk-developers"></a>WDK の開発者向けの MSBuild 入門


このセクションで Build.exe と NMake.exe に精通する WDK 開発者に基本的な MSBuild 用語を紹介します。 このセクションでは、単純な MSBuild プロジェクトの構築が表示されます。

## <a name="span-idnmakeconceptsrelevanttomsbuildspanspan-idnmakeconceptsrelevanttomsbuildspanspan-idnmakeconceptsrelevanttomsbuildspannmake-concepts-relevant-to-msbuild"></a><span id="Nmake_concepts_relevant_to_MSBuild"></span><span id="nmake_concepts_relevant_to_msbuild"></span><span id="NMAKE_CONCEPTS_RELEVANT_TO_MSBUILD"></span>Nmake の概念に関連する MSBuild


Build.exe と (WDK 8) の前に、WDK の以前のバージョンを使用する場合、おそらくに慣れて用語と概念 NMake.exe を使用します。

-   **コマンド**-コマンド ライン ツールを呼び出します。
-   **ターゲット**-名前付きの一連のコマンドについて説明します。
-   **依存関係**-その他のターゲットに依存しているターゲットについて説明します。
-   Nmake が make で呼び出される指定された 1 つまたは複数のターゲットを持つファイル。 すべての依存関係を再帰的にし、ターゲットの後実行コマンド。
-   Nmake ファイルには、ビルド構造体の堅牢な管理のためには、その他の make ファイルを含めることができます。
-   Nmake では、コマンドのパラメーターの代わりに使用する名前付きの変数の作成もサポートしています。
-   (Nmake の) には、現在のディレクトリまたはパスの名前で、Make.exe 自体には、たとえば、割り当てられている自動変数もサポートしています。
-   ターゲットは、1 つのビルド中に 2 回は実行されません。 実行されると、ターゲットがその作業を完了するいると見なされます、再実行されず、ビルドでの後続のターゲットが依存している場合でも。

## <a name="span-idmsbuildconceptsspanspan-idmsbuildconceptsspanspan-idmsbuildconceptsspanmsbuild-concepts"></a><span id="MSBuild_concepts_"></span><span id="msbuild_concepts_"></span><span id="MSBUILD_CONCEPTS_"></span>MSBuild の概念


-   C++ プロジェクトのメインの MSBuild ファイルの拡張子は、.vcxproj です。
-   コマンドが変わって*タスク*、コマンド ライン プロセスの呼び出しだけではありません。 代わりに、タスクは、ビルド操作をアトミックに実行する MSBuild を使用できる実行可能コードの単位。 タスクの完全な一覧を参照してください[MSBuild タスクに固有 Visual c]( https://go.microsoft.com/fwlink/p/?linkid=236121).。
-   MSBuild では、その共通言語ランタイム (CLR) アセンブリからのタスクのインポート、 **UsingTask**要素として次の例を示します。
    ```
    <UsingTask TaskName="TaskName" AssemblyName="AssemblyName" />
    ```

-   ターゲットは、特定の順序でタスクをグループ化しより小さな単位に分割するビルド プロセスを許可します。
-   A **PropertyGroup**プロパティ人が読みやすい形式を使用して定義することができます。 次の例は、 **PropertyGroup**形式。
    ```
    <PropertyGroup>
      <ProductVersion>9.0.30729</ProductVersion>
    </PropertyGroup>
    ```

-   **項目**、オブジェクト指向のバリアントは、**プロパティ**します。 プロパティの形式には、名前と値が、項目の形式は、オブジェクトが複数の属性を持つ名前とオブジェクトです。 **項目**オブジェクトの配列であります。
-   **プロパティ**形式で参照される **$ (project)** 形式の項目は参照中に **@(name)** します。
-   **ItemGroup**のコレクションである**項目。**
-   **Itemgroup**一覧は、通常のすべてのコンパイルされるファイル。 ファイルのコレクションを使用してタスクに渡されます、 **@(itemname)** 表記します。 参照してください[MSBuild 項目](https://go.microsoft.com/fwlink/p/?linkid=236146)使用の詳細について**項目。**
-   MSBuild はさまざまな[組み込みプロパティ](https://go.microsoft.com/fwlink/p/?linkid=236149)をプロジェクト ファイルで参照することもできます。
-   MSBuild とビルド タスクの詳細については、[MSBuild の概念](https://go.microsoft.com/fwlink/p/?linkid=236157)と[MSBuild リファレンス](https://go.microsoft.com/fwlink/p/?linkid=236161)を参照してください。

 

 





