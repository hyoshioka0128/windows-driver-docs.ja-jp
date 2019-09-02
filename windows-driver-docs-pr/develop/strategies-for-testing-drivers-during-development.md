---
ms.assetid: 3AF1C7EA-A7E0-47C4-A8D0-BB8D432F7EA0
title: ドライバー コードとドライバー パッケージのテストに関する推奨事項。
description: テストを開始するタイミング。 ドライバーの要件がある場合はすぐに、テスト ケースの設計を開始して、重要な要件が実装されていることをテストできます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2273cafe071233a29c0af92a2728a78c2be8c7f9
ms.sourcegitcommit: 2231d322eb4e9597ad7f537a4aa82b83422bd46a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70020630"
---
# <a name="tips-for-testing-drivers-during-development"></a>開発中のドライバーのテストに関するヒント

**テストを開始するタイミング。** ドライバーの要件がある場合はすぐに、テスト ケースの設計を開始して、重要な要件が実装されていることをテストできます。 これまでの調査から、コード内に欠陥が存在する時間が長ければ長いほど、コード内の欠陥の発見と修正にかかるコストは大きくなります。 開発サイクルの初期段階で欠陥を発見して修正できれば、コードがリリースおよび配布された後に欠陥を発見した場合に比べて、かかるコストも被害も小さくてすみます。 テスト ケースを早めに作成することは、設計上の問題の発見にも役立ちます。

## <a name="span-idsuggestions_for_testing_driversspanspan-idsuggestions_for_testing_driversspansuggestions-for-testing-during-development"></a><span id="suggestions_for_testing_drivers"></span><span id="SUGGESTIONS_FOR_TESTING_DRIVERS"></span>開発中のテストに関する提案


ドライバー コードとドライバー パッケージのテストに、次の提案を使ってください。

**コンパイル時にバグを見つけやすくするには:**

-   関数の役割型を使って、ドライバー提供のコールバック関数とディスパッチ ルーチンを宣言します。 これにより、コード分析と検証ツールの精度が向上し、テスト時間の効率もよくなります。 ドライバー提供の関数を宣言する方法について詳しくは、「[関数の役割型の宣言の使用](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-function-role-type-declarations)」をご覧ください。

-   **[Level4 (/W4)] (レベル 4 (/W4))** の警告オプションを使ってコードをコンパイルします。 コンパイラに検出された警告を修正すると、ドライバー コードの品質が向上し、開発サイクルのより早い段階でその他の欠陥をなくすためにも役立ちます。
-   Microsoft Source Code Annotation Language (SAL) 2.0 を使って、コードに注釈を付けます。 注釈は、関数がパラメーターをどのように使うか (パラメーターをどのように想定するか) と関数の終了時に何が保証されるかを説明します。 注釈によっても、コード分析ツールの精度が向上します。 ドライバー固有の注釈について詳しくは、「[Windows ドライバーの SAL 2.0 注釈](https://docs.microsoft.com/windows-hardware/drivers/devtest/sal-2-annotations-for-windows-drivers)」をご覧ください。
-   ドライバーの開発中に、[ドライバーの検証用ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-verifying-drivers)を使います。 特定の検証ツールを使うタイミングのガイドラインについては、「[コード分析ツールと検証ツールを使ったドライバーの分析](analyzing-driver-quality-by-using-code-analysis-tools.md)」と「[確認ツールの概要](https://docs.microsoft.com/windows-hardware/drivers/devtest/survey-of-verification-tools)」をご覧ください。

**ドライバー パッケージをテストするには:**

-   開発プロセスの初期段階で INF ファイルとドライバー パッケージを作成して、テスト中に使います。

-   [ChkINF](https://docs.microsoft.com/windows-hardware/drivers/devtest/chkinf) ツールを使って INF ファイルの構造と構文を確認し、INF ファイルとその他のインストール関連の問題の診断に役立てます。

-   [  **Inf2Cat**](https://docs.microsoft.com/windows-hardware/drivers/devtest/inf2cat) ツールを ( **/nocat** オプションを指定して) 使用し、追加の INF ファイルの確認を行います。 **Inf2Cat** を使うと、INF で参照されているファイルが存在し、INF が想定するパッケージ ディレクトリに配置されていることを確認できます。

-   「[開発とテストにおけるドライバーの署名](https://docs.microsoft.com/windows-hardware/drivers/install/signing-drivers-during-development-and-test)」の説明に従って、ドライバーのインストールとテストを容易にするためドライバーに署名します。

-   WDK で提供される Device Fundamental テストの一部として含まれている **DriverInstall** テストを実行します。 「[Visual Studio を使って実行時にドライバーをテストする方法](testing-a-driver-at-runtime.md)」と「[Device Fundamental テストを選んで構成する方法](how-to-select-and-configure-the-device-fundamental-tests.md)」をご覧ください。 **DriverInstall** テストは、ドライバーがテスト コンピューターに展開された後に実行できます。 **DriverInstall** テストをドライバー テスト グループに追加できます。 **DriverInstall** テストは、All Tests\\Basic\\Device Fundamentals\\DriverInstall の下の **[Driver Test Categories (ドライバー テスト カテゴリ)]** に表示されます。 [  **IWDTFDriverPackageAction2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriverpackageaction/nn-wdtfdriverpackageaction-iwdtfdriverpackageaction2) インターフェイスを使って、独自のテストを作成することもできます。

-   デバイス マネージャーを使ってドライバーとデバイスに関するシステム情報を確認し、SetupAPI ログを参照して、[デバイス インストールの問題のトラブルシューティング](https://docs.microsoft.com/windows-hardware/drivers/install/troubleshooting-device-and-driver-installations)を行います。 SetupAPI ログには、デバイスまたはドライバーのインストール中に実行された一連の操作に関する情報が含まれています。

    Visual Studio と WDK を使って、ドライバーのテスト コンピューターへの展開時にドライバー パッケージのインストールのテストとトラブルシューティングを行うことができます。「[テスト コンピューターへのドライバーの展開](deploying-a-driver-to-a-test-computer.md)」をご覧ください。 [ドライバー パッケージ プロジェクトの展開プロパティ](deployment-properties-for-driver-projects.md)から、 **[Install and Verify] (インストールと確認)** オプションを選択します。 このオプションを選択して、 **[Default Driver Package Installation Task (possible reboot) (既定のドライバー パッケージ インストール タスク (再起動の可能性あり))]** または **[Default Printer Driver Package Installation Task (possible reboot) (既定のプリンター ドライバー パッケージ インストール タスク (再起動の可能性あり))]** を指定すると、テストはドライバーの INF ファイルを読み取って、ドライバーをインストールします。 次に、ドライバーが起動して動作していることを確認します。 テストが完了すると、インストール タスクの成功/失敗に関する詳細情報が提供されます。 結果は、 **[Driver Test Group Explorer (ドライバー テスト グループ エクスプローラー)]** の [Driver Test Groups (ドライバー テスト グループ)] &gt; [Driver Installation (ドライバーのインストール)] に表示されます。 タスク名は、 **[Default Driver Package Installation Task (既定のドライバー パッケージ インストール タスク)]** です。

**実行時にドライバーをテストするには:**

-   WDK に含まれている Device Fundamental テストを実行します。 「[Visual Studio を使って実行時にドライバーをテストする方法](testing-a-driver-at-runtime.md)」と「[Device Fundamental テストを選んで構成する方法](how-to-select-and-configure-the-device-fundamental-tests.md)」をご覧ください。

-   デバッガーを設定して、テスト結果のトラブルシューティングとデバッグを実行できるようにします。 詳しくは、「[Windows のデバッグの概要](https://docs.microsoft.com/windows-hardware/drivers/debugger/getting-started-with-windows-debugging)」をご覧ください。
 
-   展開に使うテスト コンピューターで、ドライバーの検証ツールを有効にします。「[ドライバー プロジェクトのドライバーの検証ツール プロパティ](driver-verifier-properties-for--driver-projects.md)」をご覧ください。 [[DDI 準拠の検査]](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking) オプションを選択します。 DDI 準拠の検査でドライバーが失敗した場合は、[静的ドライバー検証](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)ツールを実行して、失敗の原因となったルールを明確にします。 静的ドライバー検証ツールは、ソース ファイル内でバグの原因を見つけるのに役立ちます。
-   できる限り多くの異なるハードウェア構成で、ドライバーとデバイスをテストします。 さまざまなハードウェアを使うと、デバイス間の競合や、デバイス操作でのその他のエラーを見つけるのに役立ちます。 たとえば、プロセッサ アーキテクチャが異なる複数のコンピューターや、32 ビット バージョンと 64 ビット バージョンの Windows がそれぞれ動作するコンピューターで、ドライバーとデバイスをテストする必要があります。

-   [Windows のチェック ビルド](https://docs.microsoft.com/windows-hardware/drivers/devtest/checked-build-of-windows)を使って、ドライバーとデバイスをテストします。 Windows のチェック ビルド (またはチェック済みのオペレーティング システムと HAL のみ) でドライバーを実行すると、他のツールでのテストではわからないエラーを検出するのに役立ちます。 ドライバーの開発とテストでは、カーネル デバッガーと共にチェック ビルドを使った実行を標準の手法として含める必要があります。
-   マルチプロセッサ システムで、ドライバーとデバイスをテストします。 他では見つからない競合条件やその他のタイミングの問題が、マルチプロセッサ システムでは明らかになります。 「[Device Fundamental テストを選んで構成する方法](how-to-select-and-configure-the-device-fundamental-tests.md)」と「[複数のプロセッサ グループをサポートするためのテスト ドライバーのブート パラメーター](https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-parameters-to-test-drivers-for-multiple-processor-group-support)」をご覧ください。

-   特定のシステムとハードウェアの条件、特に周辺条件について、ドライバーとデバイスをテストします。 たとえば、"D3 hot (D3 ホット)" や "D3 cold (D3 コールド)" などの条件があります。 デバイスの電源状態 "D3 hot (D3 ホット)" (電源が失われていない) と "D3 cold (D3 コールド)" (電源がデバイスから削除されている) から、ドライバーとデバイスが適切に復帰することを確認します。 詳しくは、「[Device Fundamental テストを選んで構成する方法](how-to-select-and-configure-the-device-fundamental-tests.md)」をご覧ください。
