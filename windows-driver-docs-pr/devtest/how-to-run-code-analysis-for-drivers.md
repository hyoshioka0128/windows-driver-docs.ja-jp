---
title: ドライバーのコード分析を実行する方法
description: コード Analysis for Drivers は、ソース コードの障害に関する情報を提供します。 コード分析を手動で実行して、自動的には各ビルドでもコード分析を実行することができます。
ms.assetid: BDD4EC2C-FB23-44BE-9A52-F98774AC7268
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 599989326f7f09eef7aead3f351d84ae796a1351
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579393"
---
# <a name="how-to-run-code-analysis-for-drivers"></a>ドライバーのコード分析を実行する方法


コード Analysis for Drivers は、ソース コードの障害に関する情報を提供します。 コード分析を手動で実行して、自動的には各ビルドでもコード分析を実行することができます。

このトピックの内容:

-   [コード分析の実行](#running-code-analysis)
-   [コード分析の結果を表示します。](#viewing-the-code-analysis-results)
-   [レポート上の欠陥の非表示にします。](#suppressing-the-report-of-defects)
-   [警告 C6262 カーネル モード ドライバー用のスタックの使用制限を変更します。](#changing-stack-usage-limits-for-warning-c6262-for-kernel-mode-drivers)
-   [関連トピック](#related-topics)

## <a name="running-code-analysis"></a>コード分析の実行


**コード分析を手動でドライバーのソース コードを実行するには**

1.  Visual Studio では、ドライバーのプロジェクト ファイルまたはソリューションを選択し、プロジェクト構成と分析プラットフォームを選択します。
2.  **[分析]** メニューまたは **[ビルド]** メニューの **[ソリューションでコード分析を実行]** をクリックします。

**ビルドのたびに自動的にドライバーのソース コードでコード分析を実行するには**

1.  Visual Studio で、ドライバーのプロジェクトまたはソリューションを右クリックして**ソリューション エクスプ ローラー**クリック**プロパティ**します。
2.  プロジェクトのプロパティ ダイアログ ボックスで、次のようにクリックします。**コード分析**します。
3.  **C と C++ のプロパティのコード分析** ページで、(たとえば、Windows 8 および Win32) 分析するプロジェクト構成とプラットフォームを選択します。
4.  選択**ビルド時に C/C++ のコード分析を有効にする**します。
5.  規則のセットを選択**Microsoft ドライバー推奨規則**します。 これは、既定規則のドライバーのセットです。
6.  **ビルド** メニューのをクリックして**ソリューションのビルド**します。

## <a name="viewing-the-code-analysis-results"></a>コード分析の結果を表示します。


ソース コードでの欠陥の検出可能であれば、**コード分析結果**ウィンドウ、障害が発生したソース ファイルでコード分析の警告番号と行番号が表示されます。

**障害を表示するには**

1.  **コード分析結果**ウィンドウで、行番号と、問題の説明に表示されます をクリックして、**コード分析結果**ウィンドウ。

    コード ウィンドウでは、ソース コードを表示し、障害が発生することを示します。

2.  特定の警告に関する詳細についてでの警告をクリックします。、**コード分析結果**ウィンドウ。

**ビルドに関連付けられているコード分析ログ ファイルを表示するには**

1.  ビルド構成とプラットフォームのためのディレクトリに移動します (たとえば、 \\Windows7Release\\x64)。
2.  推奨の規則を使用する場合、ログ ファイルは、vc と呼ばれます。\*codeanalysis.xml します。 Windows Server 2012 用のドライバーを作成する場合、このファイルは、ドライバー検証ログの作成に使用されます。

## <a name="suppressing-the-report-of-defects"></a>レポート上の欠陥の非表示にします。


場合によっては、特定の警告メッセージのレポートを抑制したい場合があります。たとえば、次のように、警告が主に情報であり、エラーの原因がわかっている場合です。

**警告メッセージを抑制するには**

1.  報告された問題のインスタンスを削除する行番号を選択しで警告、**コード分析結果**ウィンドウ。
2.  警告の説明に展開されている、次のようにクリックします。**アクション** &gt; **メッセージの非表示** &gt; **ソース**します。

    Suppress 指定子と pragma 警告ディレクティブの直後に続くコード行にのみ警告を抑制します、\#プラグマ警告ステートメント。

    ```
    #pragma warning(suppress: 6014)
    ```

## <a name="changing-stack-usage-limits-for-warning-c6262-for-kernel-mode-drivers"></a>警告 C6262 カーネル モード ドライバー用のスタックの使用制限を変更します。


ユーザー モードとカーネル モードのコードでは、スタック領域は限られており、し、ページ スタックのコミットに失敗したスタック オーバーフロー例外が発生します。 高スタックの使用は、特にカーネル モードでの問題を使用可能な合計のスタック領域は 12 KB のみためです。 カーネル モード コードは積極的にスタックの使用を制限します。

コード分析ツールの警告を発行する[C6262](https://go.microsoft.com/fwlink/p/?linkid=321750)関数で 1 KB を超えるスタック領域がローカルで使用する場合。 リソースが消費される可能性のある関数を調査する場合は、カスタマイズまたはで使用されるスタックのしきい値制限を低く[C6262](https://go.microsoft.com/fwlink/p/?linkid=321750)します。 スタックのしきい値の制限を低くとコード分析ツールがより多くの問題を検索可能性があることができます。 それらスタック使用量の問題に対処できます。 たとえば、他の関数がリソースを使用しているかどうかに 400 バイトは、しきい値を下げることです。

**C6262 stacksize の制限をカスタマイズするには**

1. メモ帳または別のテキスト エディターで、カーネル モード ドライバー (またはコンポーネント) の Visual Studio プロジェクト ファイル (.vcxproj) を開きます。
2. 新しい追加**&lt;ItemDefinitionGroup&gt;** コンパイラ **&lt;ClCompile&gt;** します。
3. 追加、 **&lt;PREfastAdditionalOptions&gt;** 要素、 **stacksize**<em>&lt;バイト&gt;</em>します。 既定値は**stacksize1024**します。
   ```XML
     <ItemDefinitionGroup>
       <ClCompile>



      <!-- Change stack depth for C6262 from 1024 to 400 -->
      <PREfastAdditionalOptions>stacksize400</PREfastAdditionalOptions>

    </ClCompile>
  </ItemDefinitionGroup>


```


4.  プロジェクト ファイルを保存します。 Visual Studio を始めて、更新されたドライバー プロジェクトを読み込むコード分析を実行できます。

    1 KB の既定値に戻すには、プロジェクト ファイルに加えた変更を元に戻すか、スタック サイズの値を変更**stacksize1024**します。

## <a name="related-topics"></a>関連トピック


[Code Analysis for Drivers の警告](prefast-for-drivers-warnings.md)










