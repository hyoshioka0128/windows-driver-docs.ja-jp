---
title: ドライバーのコード分析を実行する方法
description: ドライバーのコード分析では、ソースコードの欠陥の可能性に関する情報が提供されます。 コード分析は手動で実行できます。また、各ビルドでコード分析を自動的に実行することもできます。
ms.assetid: BDD4EC2C-FB23-44BE-9A52-F98774AC7268
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e918f95f05f9123e20005aca4309841b26cab216
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769704"
---
# <a name="how-to-run-code-analysis-for-drivers"></a>ドライバーのコード分析を実行する方法

ドライバーのコード分析では、ソースコードの欠陥の可能性に関する情報が提供されます。 コード分析は手動で実行できます。また、各ビルドでコード分析を自動的に実行することもできます。

このトピックの内容:

* [コード分析の実行](#running-code-analysis)
* [コード分析の結果の表示](#viewing-the-code-analysis-results)
* [欠陥の報告の抑制](#suppressing-the-report-of-defects)
* [カーネルモードドライバーの警告 C6262 のスタック使用制限を変更する](#changing-stack-usage-limits-for-warning-c6262-for-kernel-mode-drivers)
* [関連項目](#related-topics)

## <a name="running-code-analysis"></a>コード分析の実行

### <a name="to-run-code-analysis-on-driver-source-code-manually"></a>ドライバーのソースコードに対して手動でコード分析を実行するには

1. Visual Studio で、ドライバープロジェクトファイルまたはソリューションを選択し、分析するプロジェクト構成とプラットフォームを選択します。
2. **[分析]** メニューまたは **[ビルド]** メニューの **[ソリューションでコード分析を実行]** をクリックします。

### <a name="to-run-code-analysis-on-driver-source-code-automatically-with-each-build"></a>各ビルドで自動的にドライバーソースコードのコード分析を実行するには

1. Visual Studio で、**ソリューションエクスプローラー**のドライバープロジェクトまたはソリューションを右クリックし、[**プロパティ**] をクリックします。
2. プロジェクトの [プロパティ] ダイアログボックスで、[**コード分析**] をクリックします。
3. [ **C/c + + のコード分析のプロパティ**] ページで、分析するプロジェクトの構成とプラットフォーム (Windows 8 や Win32 など) を選択します。
4. [**ビルド時に C/c + + のコード分析を有効にする**] を選択します。
5. [規則セット] で、[ **Microsoft ドライバーの推奨規則**] を選択します。 これは、ドライバーの既定の規則セットです。
6. [**ビルド**] メニューの [**ソリューションのビルド**] をクリックします。

## <a name="viewing-the-code-analysis-results"></a>コード分析の結果の表示

ソースコードに問題が見つかった場合は、[**コード分析の結果**] ウィンドウに、障害が発生したソースファイルのコード分析の警告番号と行番号が表示されます。

### <a name="to-view-defects"></a>欠陥を表示するには

1. [**コード分析の結果**] ウィンドウで行番号をクリックすると、[**コード分析の結果**] ウィンドウに欠陥の説明が表示されます。

   コードウィンドウにソースコードが表示され、障害が発生した場所が示されます。

2. 特定の警告の詳細を確認するには、[**コード分析の結果**] ウィンドウで警告をクリックします。

### <a name="to-view-the-code-analysis-log-file-associated-with-a-build"></a>ビルドに関連付けられているコード分析ログファイルを表示するには

1. ビルド構成とプラットフォーム (など) のディレクトリに移動 `\\Windows7Release\\x64` します。
2. 推奨される規則を使用すると、ログファイルが呼び出され `vc.\*codeanalysis.xml` ます。 Windows Server 2012 用のドライバーを作成する場合は、このファイルを使用してドライバー検証ログを作成します。

## <a name="suppressing-the-report-of-defects"></a>欠陥の報告の抑制

場合によっては、特定の警告メッセージのレポートを非表示にすることが必要になることがあります。たとえば、警告が主に情報案内で、エラーの原因がわかっているとします。

### <a name="to-suppress-warning-messages"></a>警告メッセージを非表示にするには

1. 報告された欠陥のインスタンスを削除するには、[**コード分析の結果**] ウィンドウで行番号と警告を選択します。
2. 警告の展開された説明で、[**アクション**] [ &gt; **Suppress Message** &gt; **送信元の**メッセージを非表示にする] をクリックします。

   抑制指定子を持つプラグマ警告ディレクティブを使用すると、プラグマの warning ステートメントの直後にあるコード行に対してのみ警告が表示されなく \# なります。

    ```command
    #pragma warning(suppress: 6014)
    ```

## <a name="changing-stack-usage-limits-for-warning-c6262-for-kernel-mode-drivers"></a>カーネルモードドライバーの警告 C6262 のスタック使用制限を変更する

ユーザーモードとカーネルモードのコードでは、スタック領域が制限され、スタックのページをコミットできないとスタックオーバーフロー例外が発生します。 使用可能な合計スタック領域は 12 KB であるため、高いスタックの使用は特にカーネルモードの問題です。 カーネルモードのコードでは、スタックの使用を積極的に制限する必要があります。

関数で 1 KB を超えるスタック領域がローカルで使用されている場合、コード分析ツールは警告[C6262](https://docs.microsoft.com/cpp/code-quality/c6262)を発行します。 リソースを集中的に使用する可能性がある関数を調査する場合は、 [C6262](https://docs.microsoft.com/cpp/code-quality/c6262)によって使用されるスタックしきい値の制限をカスタマイズまたは下げることができます。 スタックしきい値の制限を低くすると、コード分析ツールにより多くの問題が検出される可能性があります。 その後、これらのスタック使用の問題に対処することを選択できます。 たとえば、しきい値を400バイトに下げて、他の関数がリソースを使用しているかどうかを確認することができます。

### <a name="to-customize-the-stacksize-limit-for-c6262"></a>C6262 の stacksize limit をカスタマイズするには

1. カーネルモードドライバー (またはコンポーネント) の Visual Studio プロジェクトファイル (.vcxproj) をメモ帳またはその他のテキストエディターで開きます。
2. コンパイラ** \< clcompile \> **の新しい** \< itemdefinitiongroup \> **を追加します。
3. ** \< Prefastadditionaloptions \> **要素を追加し、 **stacksize \< バイト \> **を設定します。 既定値は**stacksize1024**です。

```XML
     <ItemDefinitionGroup>
       <ClCompile>


      <!-- Change stack depth for C6262 from 1024 to 400 -->
      <PREfastAdditionalOptions>stacksize400</PREfastAdditionalOptions>

    </ClCompile>
  </ItemDefinitionGroup>
```

4. プロジェクト ファイルを保存します。 Visual Studio を起動し、更新されたドライバープロジェクトを読み込んで、コード分析を実行します。

   既定値の 1 KB に戻すには、プロジェクトファイルに対して行った変更を元に戻すか、スタックサイズの値を**stacksize1024**に変更します。

## <a name="related-topics"></a>関連トピック

[ドライバーのコード分析の警告](prefast-for-drivers-warnings.md)
