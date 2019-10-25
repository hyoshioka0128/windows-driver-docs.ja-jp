---
ms.assetid: 960368D6-5E24-46B6-83DA-0525065E5FFB
title: ドライバー パッケージ プロジェクトのドライバーの検証ツール プロパティ
description: ドライバー検証ツールは、ドライバーのテストの効果を高める、実行時検証ツールです。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42f53baf932735ec28168f437aeebad78c69eeac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839611"
---
# <a name="driver-verifier-properties-for-driver-package-projects"></a>ドライバー パッケージ プロジェクトのドライバーの検証ツール プロパティ

[ドライバー検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)は、ドライバーのテストの効果を高める、実行時検証ツールです。 ドライバーの検証ツールを有効化して構成し、ドライバーをテスト用に展開するときにすべてのテスト コンピューター上で実行されるようにすることができます。

リモート テスト コンピューターでドライバーの検証ツールを有効にする場合は、常にテスト コンピューターとのカーネル モード デバッグ接続をセットアップする必要があります。 ターゲット コンピューターの構成と、デバッグ ケーブルの設定について詳しくは、「[Windows のデバッグの概要](https://docs.microsoft.com/windows-hardware/drivers/debugger/getting-started-with-windows-debugging)」をご覧ください。

## <a name="span-idsetting_driver_verifier_properties_for_driver_package_projectsspanspan-idsetting_driver_verifier_properties_for_driver_package_projectsspanspan-idsetting_driver_verifier_properties_for_driver_package_projectsspansetting-driver-verifier-properties-for-driver-package-projects"></a><span id="Setting_Driver_Verifier_properties_for_driver_package_projects"></span><span id="setting_driver_verifier_properties_for_driver_package_projects"></span><span id="SETTING_DRIVER_VERIFIER_PROPERTIES_FOR_DRIVER_PACKAGE_PROJECTS"></span>ドライバー パッケージ プロジェクトのドライバー検証ツール プロパティの設定


1.  ドライバー パッケージのプロパティ ページを開きます。 ソリューション エクスプローラーでドライバー パッケージ プロジェクトを右クリックし、 **[プロパティ]** をクリックします。
2.  ドライバー パッケージのプロパティ ページで、 **[構成プロパティ]** 、 **[Driver Install]** (ドライバーのインストール)、 **[Driver Verification]** (ドライバーの検証) の順にクリックします。
3.  **[Enable Driver Verification]** (ドライバーの検証を有効にする) をオンにします。 このオプションがオンになっている場合は、テスト コンピューターで検証するドライバーと使用する[ドライバー検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)を選ぶことができます。

## <a name="span-idproject_configuration_and_platformspanspan-idproject_configuration_and_platformspanspan-idproject_configuration_and_platformspanproject-configuration-and-platform"></a><span id="Project_Configuration_and_Platform"></span><span id="project_configuration_and_platform"></span><span id="PROJECT_CONFIGURATION_AND_PLATFORM"></span>プロジェクト構成とプラットフォーム


構成一覧とプラットフォーム一覧を使うと、さまざまなプロジェクト構成とプラットフォームの組み合わせに、さまざまな展開の設定を適用できます。 たとえば、1 台のテスト コンピューターにはデバッグ用ビルドのための展開オプションのセットを使ってドライバーを展開し、別のテスト コンピューターにはリリース用ビルドのための展開オプションを使うことができます。

## <a name="span-idenable_driver_verifierspanspan-idenable_driver_verifierspanspan-idenable_driver_verifierspanenable-driver-verifier"></a><span id="Enable_Driver_Verifier"></span><span id="enable_driver_verifier"></span><span id="ENABLE_DRIVER_VERIFIER"></span>Enable Driver Verifier (ドライバーの検証ツールの有効化)


テスト コンピューター上でのドライバーの検証ツールの有効化は、コンピューターのすべてのドライバーを対象にしたり、ドライバー プロジェクトだけを対象にしたり、一覧で指定されたドライバーを対象にしたりすることができます。 たとえば、特定のデバイスのスタックにあるドライバーのセットに対して、ドライバー検証ツールを有効にしたい場合があります。

## <a name="span-idverify_driversspanspan-idverify_driversspanspan-idverify_driversspanverify-drivers"></a><span id="Verify_Drivers"></span><span id="verify_drivers"></span><span id="VERIFY_DRIVERS"></span>Verify Drivers (ドライバーの検証)


テスト コンピューター上のどのドライバーを検証するかを指定します。

<span id="All_Drivers"></span><span id="all_drivers"></span><span id="ALL_DRIVERS"></span>**All Drivers (すべてのドライバー)**  
ドライバーの検証ツールが、リモート テスト コンピューターにインストールされているすべてのドライバーを検証するように指定します。

<span id="Project_Output"></span><span id="project_output"></span><span id="PROJECT_OUTPUT"></span>**Project Output (プロジェクトの出力)**  
ドライバーの検証ツールが、リモート テスト コンピューターにインストールされているドライバー プロジェクトを検証するように指定します。 これは既定のオプションです。

<span id="Driver_List"></span><span id="driver_list"></span><span id="DRIVER_LIST"></span>**Driver List (ドライバーの一覧)**  
ドライバー検証ツールがリモート テスト コンピューター上で検証するドライバー、またはドライバーの一覧を指定します。 たとえば、特定のデバイスに関連付けられているすべてのドライバーの一覧を作ることができます。 ドライバーの指定は、バイナリ名で行います (たとえば Driver.sys)。 ドライバーの一覧は、セミコロンで区切ります。 ワイルドカード値 (たとえば、*n\*.sys*) は、サポートされていません。

## <a name="span-iddriver_verifier_standard_flagsspanspan-iddriver_verifier_standard_flagsspanspan-iddriver_verifier_standard_flagsspandriver-verifier-standard-flags"></a><span id="Driver_Verifier_Standard_Flags"></span><span id="driver_verifier_standard_flags"></span><span id="DRIVER_VERIFIER_STANDARD_FLAGS"></span>ドライバー検証ツールの標準フラグ


テスト コンピューター上で、ドライバー検証ツールの次のオプションを構成できます。

-   [DDI 準拠の検査](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking) (Windows 8)

    このオプションがアクティブになっていると、ドライバー検証ツールはドライバーとオペレーティング システムのカーネル インターフェイスとの適切なやり取りをチェックするデバイス ドライバー インターフェイス (DDI) ルールのセットを適用します。

-   [デッドロックの検出](https://docs.microsoft.com/windows-hardware/drivers/devtest/deadlock-detection)

    このオプションがアクティブになっていると、ドライバーの検証ツールはドライバーによるスピン ロック、ミューテックス、速いミューテックスの使用を監視します。 これによって、ある時点でドライバーのコードがデッドロックを引き起こす可能性があるかどうかが検出されます。

-   [DMA の検証](https://docs.microsoft.com/windows-hardware/drivers/devtest/dma-verification)

    このオプションがアクティブになっていると、ドライバーの検証ツールはドライバーによる DMA (ダイレクト メモリ アクセス) ルーチンの使用を監視します。 これによって、DMA バッファー、アダプター、マップ レジスタの不適切な使用が検出されます。

-   [強制 IRQL 検査](https://docs.microsoft.com/windows-hardware/drivers/devtest/force-irql-checking)

    このオプションがアクティブになっていると、ドライバーの検証ツールはページングが可能なコードを無効にして、ドライバーを極端にメモリ不足の状態にします。 ドライバーが不適切な IRQL で、またはスピン ロックを保持したままでページ メモリにアクセスしようとすると、ドライバーの検証ツールはこの動作を検出します。

-   [I/O の検証](https://docs.microsoft.com/windows-hardware/drivers/devtest/i-o-verification)

    このオプションがアクティブになっていると、ドライバーの検証ツールはドライバーの IRP (割り込み要求パケット) を特別なプールから割り当て、ドライバーの I/O 処理を監視します。 これによって、I/O ルーチンの不適切な使用や不整合な使用が検出されます。 ドライバーの検証ツールは、I/O マネージャーのルーチンの呼び出しも監視し、PnP (プラグ アンド プレイ) IRP、Power IRP、WMI IRP のストレス テストを実行します。

-   [その他の検査](https://docs.microsoft.com/windows-hardware/drivers/devtest/miscellaneous-checks)

    このオプションがアクティブになっていると、ドライバーの検証ツールはドライバーのクラッシュの一般的な原因 (解放したメモリの誤った処理など) を探します。

-   [プールのトラック](https://docs.microsoft.com/windows-hardware/drivers/devtest/pool-tracking)

    このオプションがアクティブになっていると、ドライバーの検証ツールは、ドライバーがアンロードされるときにすべてのメモリ割り当てが解放されたかどうかをチェックします。 これによってメモリ リークが明らかになります。

-   [セキュリティの検査](https://docs.microsoft.com/windows-hardware/drivers/devtest/security-checks)

    このオプションがアクティブになっていると、ドライバーの検証ツールはセキュリティの脆弱性につながるような一般的なエラー (カーネル モードのルーチンによるユーザー モードのアドレスの参照など) を探します。

-   [特別なプールの検査](https://docs.microsoft.com/windows-hardware/drivers/devtest/special-pool)

    このオプションがアクティブになっていると、ドライバーの検証ツールはほとんどのドライバーのメモリ要求を特別なプールから割り当てます。 この特別なプールでは、メモリ オーバーラン、メモリ アンダーラン、既に解放されたメモリへのアクセスが監視されます。

## <a name="span-iddriver_verifier_scenario_specific_settingsspanspan-iddriver_verifier_scenario_specific_settingsspanspan-iddriver_verifier_scenario_specific_settingsspandriver-verifier-scenario-specific-settings"></a><span id="Driver_Verifier_Scenario_Specific_Settings"></span><span id="driver_verifier_scenario_specific_settings"></span><span id="DRIVER_VERIFIER_SCENARIO_SPECIFIC_SETTINGS"></span>ドライバーの検証ツールのシナリオ固有の設定


-   [低リソースのシミュレーション](https://docs.microsoft.com/windows-hardware/drivers/devtest/low-resources-simulation)

    このオプションがアクティブになっていると、ドライバーの検証ツールはプール割り当て要求やその他のリソース要求をランダムに失敗させます。 システムでこれらの割り当てエラーを引き起こすことで、ドライバーの検証ツールはリソース不足の状況でのドライバーの能力をテストします。

-   [保留中の I/O 要求を強制する](https://docs.microsoft.com/windows-hardware/drivers/devtest/force-pending-i-o-requests)

    このオプションがアクティブになっていると、ドライバー検証ツールはランダムな [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) の呼び出しに STATUS\_PENDING を返すことによって、STATUS\_PENDING 戻り値へのドライバーの応答をテストします。

-   [IRP ログ](https://docs.microsoft.com/windows-hardware/drivers/devtest/irp-logging)

    このオプションがアクティブになっていると、ドライバー検証ツールはドライバーによる IRP の使用を監視し、IRP の使用のログを作成します。

-   [不変な MDL のスタック用検査](https://docs.microsoft.com/windows-hardware/drivers/devtest/invariant-mdl-checking-for-stack) (Windows 8)

    [[不変な MDL のスタック用検査]](https://docs.microsoft.com/windows-hardware/drivers/devtest/invariant-mdl-checking-for-stack) は、不変の MDL バッファーがドライバーでどのように処理されているかをドライバー スタック全体を対象に監視するオプションです。 不変の MDL バッファーに対する無効な改変が、ドライバーの検証ツールによって検出されます。 このオプションを使うには、少なくとも 1 つのドライバーで I/O の検証を有効にする必要があります。

-   [不変な MDL のドライバー用検査](https://docs.microsoft.com/windows-hardware/drivers/devtest/invariant-mdl-checking-for-driver) (Windows 8)

    [[不変な MDL のドライバー用検査]](https://docs.microsoft.com/windows-hardware/drivers/devtest/invariant-mdl-checking-for-driver) は、不変の MDL バッファーがドライバーでどのように処理されているかをドライバー単位で監視するオプションです。 不変の MDL バッファーに対する無効な改変が、このオプションによって検出されます。 このオプションを使うには、少なくとも 1 つのドライバーで I/O の検証を有効にする必要があります。

-   [Power Framework 遅延ファジー テスト](https://docs.microsoft.com/windows-hardware/drivers/devtest/concurrency-stress-test) (Windows 8)

    このオプションがアクティブになっていると、ドライバーの検証ツールはスレッド スケジュールをランダム化して、ドライバーの同時エラーを検出できるようにします。

-   [Stack Based Failure Injection (スタック ベースのエラー挿入)](https://docs.microsoft.com/windows-hardware/drivers/devtest/stack-based-failure-injection) (Windows 8)

    [[Stack Based Failure Injection (スタック ベースのエラー挿入]](https://docs.microsoft.com/windows-hardware/drivers/devtest/stack-based-failure-injection) オプションは、カーネル モードのドライバーにリソース エラーを挿入します。 このオプションは、特別なドライバーである KmAutoFail.sys と[ドライバー検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)を使って、ドライバーのエラー処理パスに入り込みます。

    **注**  [[Stack Based Failure Injection (スタック ベースのエラー挿入)]](https://docs.microsoft.com/windows-hardware/drivers/devtest/stack-based-failure-injection) と [[低リソースのシミュレーション]](https://docs.microsoft.com/windows-hardware/drivers/devtest/low-resources-simulation) を組み合わせることはできません。

     

## <a name="span-iddriver_verifier_options_that_require_i_o_verificationspanspan-iddriver_verifier_options_that_require_i_o_verificationspanspan-iddriver_verifier_options_that_require_i_o_verificationspandriver-verifier-options-that-require-io-verification"></a><span id="Driver_Verifier_options_that_require_I_O_Verification"></span><span id="driver_verifier_options_that_require_i_o_verification"></span><span id="DRIVER_VERIFIER_OPTIONS_THAT_REQUIRE_I_O_VERIFICATION"></span>I/O の検証を必要とするドライバーの検証ツールのオプション


先に [I/O の検証](https://docs.microsoft.com/windows-hardware/drivers/devtest/i-o-verification)を有効にする必要がある 4 つのオプションがあります。 I/O の検証が有効化されていない場合は、これらのオプションも有効になりません。

-   [保留中の I/O 要求を強制する](https://docs.microsoft.com/windows-hardware/drivers/devtest/force-pending-i-o-requests)
-   [IRP ログ](https://docs.microsoft.com/windows-hardware/drivers/devtest/irp-logging)
-   [不変な MDL のスタック用検査](https://docs.microsoft.com/windows-hardware/drivers/devtest/invariant-mdl-checking-for-stack)
-   [不変な MDL のドライバー用検査](https://docs.microsoft.com/windows-hardware/drivers/devtest/invariant-mdl-checking-for-driver)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [ドライバーの検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)
* [Visual Studio を使って実行時にドライバーをテストする方法](testing-a-driver-at-runtime.md)
* [テスト コンピューターへのドライバーの展開](deploying-a-driver-to-a-test-computer.md)
* [Windows のデバッグの概要](https://docs.microsoft.com/windows-hardware/drivers/debugger/getting-started-with-windows-debugging)
 

 






