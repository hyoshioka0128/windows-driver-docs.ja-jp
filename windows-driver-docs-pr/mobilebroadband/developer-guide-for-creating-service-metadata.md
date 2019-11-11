---
title: サービス メタデータの作成に関する開発者向けガイド
description: サービス メタデータの作成に関する開発者向けガイド
ms.assetid: 2d250bce-2dd2-4bd8-aa0f-432dde7783e1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28de135945016ac249a7a0a19951dcb822b72b3a
ms.sourcegitcommit: 724404f7baf0f7f9a8bd3fd3eaf41c09f45a9e60
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445359"
---
# <a name="developer-guide-for-creating-service-metadata"></a>サービス メタデータの作成に関する開発者向けガイド

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]


このガイドでは、以前の Sysdev (<https://sysdev.microsoft.com>) と呼ばれる、Windows デベロッパーセンターハードウェアダッシュボードでサービスメタデータパッケージを作成する手順について説明します。 モバイルブロードバンドアプリをハードウェアデバイスに接続するには、サービスメタデータが必要です。 ユーザーがモバイルブロードバンドデバイスをコンピューターに接続すると、関連付けられているサービスメタデータがダウンロードされ、モバイルブロードバンドアプリが自動的にダウンロードされます。

サービスメタデータを活用して、Windows と緊密に統合されたエクスペリエンスを作成することができます。 サービスメタデータパッケージを使用すると、アイコンやオペレーター名などのブランド情報を含めたり、SIM ハードウェアや個人用ホットスポットにアクセスするための設定とアクセス許可を構成したり、モバイルブロードバンドアプリをプロビジョニングしてモバイルブロードバンドで動作することができます。ドライブ.

**注:**  
モバイルブロードバンドアプリが自動的にインストールされている場合でも、ユーザーは手動でスタート画面にピン留めする必要があります。



## <a name="span-idgetting_startedspanspan-idgetting_startedspanspan-idgetting_startedspangetting-started"></a><span id="Getting_started"></span><span id="getting_started"></span><span id="GETTING_STARTED"></span>はじめに


サービスメタデータパッケージを正常に作成するには、このセクションに記載されている手順を完了する必要があります。

### <a name="span-idregister_your_company_with_the_windows_dev_center_hardware_dashboardspanspan-idregister_your_company_with_the_windows_dev_center_hardware_dashboardspanspan-idregister_your_company_with_the_windows_dev_center_hardware_dashboardspanregister-your-company-with-the-windows-dev-center-hardware-dashboard"></a><span id="Register_your_company_with_the_Windows_Dev_Center_hardware_dashboard"></span><span id="register_your_company_with_the_windows_dev_center_hardware_dashboard"></span><span id="REGISTER_YOUR_COMPANY_WITH_THE_WINDOWS_DEV_CENTER_HARDWARE_DASHBOARD"></span>Windows デベロッパーセンターのハードウェアダッシュボードを使用して会社を登録する

-   会社には、Windows デベロッパーセンターハードウェアダッシュボードにアクティブなアカウントがあります。 会社が Windows デベロッパーセンターのハードウェアダッシュボードにアカウントを持っていない場合は、新しいアカウントを作成し、ユーザーアカウントを会社に追加することができます。 詳細については、Windows デベロッパーセンターのハードウェアダッシュボードヘルプの「[管理](https://docs.microsoft.com/windows-hardware/drivers/dashboard/administration)」を参照してください。

-   会社は、パッケージに署名するための VeriSign コード署名証明書を持っています。

### <a name="span-idservice_metadata_wizard_access_and_service_identifiers_registrationspanspan-idservice_metadata_wizard_access_and_service_identifiers_registrationspanspan-idservice_metadata_wizard_access_and_service_identifiers_registrationspanservice-metadata-wizard-access-and-service-identifiers-registration"></a><span id="Service_Metadata_wizard_access_and_service_identifiers_registration"></span><span id="service_metadata_wizard_access_and_service_identifiers_registration"></span><span id="SERVICE_METADATA_WIZARD_ACCESS_AND_SERVICE_IDENTIFIERS_REGISTRATION"></span>サービスメタデータウィザードのアクセスとサービス識別子の登録

MNOs と MVNOs は、サービスメタデータパッケージを作成する前に、次の手順を完了する必要があります。

-   サービスメタデータウィザードへのアクセスの要求

-   サービス id を登録する

上記の手順を完了するには、次の情報を含む sysdev@microsoft.com に電子メールを送信する必要があります。

-   Windows デベロッパーセンターハードウェアダッシュボードに登録したときに使用された組織名。

-   モバイルネットワークオペレーターとモバイル仮想ネットワークオペレーターのどちらであるか。

-   サービスメタデータパッケージを作成する必要がある理由を web サイトで確認できます。

必要に応じて、次のサービス識別子を含めます。

-   GSM プロバイダー Id の一覧

-   GSM プロバイダー名の一覧

-   CDMA Sid の一覧

-   CDMA プロバイダー名の一覧

要求を受け取った24時間の受信確認メールを受信する必要があります。 ただし、要求の処理には最大5営業日かかることがあります。 競合がある場合は、追加情報を求める電子メールをお送りします。

### <a name="span-idmobile_broadband_appspanspan-idmobile_broadband_appspanspan-idmobile_broadband_appspanmobile-broadband-app"></a><span id="Mobile_broadband_app"></span><span id="mobile_broadband_app"></span><span id="MOBILE_BROADBAND_APP"></span>モバイルブロードバンドアプリ

サービスメタデータパッケージを作成する前に、モバイルブロードバンドアプリが開発され、Microsoft Store に関連付けられていることを確認します。 このアプリは、プランの購入、データの使用状況、ヘルプ、サポートなどの主要なエクスペリエンスを提供すると共に、オペレーターから付加価値のあるサービスを強調表示する必要があります。 モバイルブロードバンドアプリの作成の詳細については、次のリンクを参照してください。

-   [モバイルブロードバンド WinRT API の概要](mobile-broadband-winrt-api-overview.md)

-   [携帯電話会社のハードウェアの概要](mobile-operator-hardware-overview.md)

-   [UWP モバイルブロードバンドアプリ](uwp-mobile-broadband-apps.md)

**注:**  
サービスメタデータがテストされ、外部で公開する準備が整うまで、モバイルブロードバンドアプリを Microsoft Store に発行する必要はありません。 サービスメタデータパッケージがプレビューモードのテストに合格した後にのみ、アプリを Microsoft Store に発行することをお勧めします。



## <a name="span-idcreating_service_metadata_packagesspanspan-idcreating_service_metadata_packagesspanspan-idcreating_service_metadata_packagesspancreating-service-metadata-packages"></a><span id="Creating_service_metadata_packages"></span><span id="creating_service_metadata_packages"></span><span id="CREATING_SERVICE_METADATA_PACKAGES"></span>サービスメタデータパッケージの作成


サービスメタデータパッケージの作成は、Windows デベロッパーセンターハードウェアダッシュボードで使用できるサービスメタデータウィザードから開始します。 サービスメタデータウィザードの詳細については、「[手順 2-サービスメタデータパッケージの作成](#2-create-the-service-metadata-package)」を参照してください。 サービスメタデータウィザードを使用して、既存のサービスメタデータパッケージを作成または編集できます。 ウィザードを実行して値を入力すると、ウィザードによって検証が行われ、エラーまたは警告が通知されます。 この検証には、不足または不適切なフィールド、サービス識別子の所有権、Microsoft Store 内のモバイルブロードバンドアプリの有無などの確認が含まれます。

最終的な確認ページが表示され、送信する準備ができたら、**開発者**モードまたは**プレビュー**モードでパッケージを提出することができます。

-   **開発者モード**サービスメタデータパッケージを作成し、オフラインのテスト目的で使用することが目的である場合に、初期段階で使用されます。 このモードでは、パッケージは署名されず、検証のために手動でダウンロードしてテストコンピューターにインストールする必要があります。 このモードは、デバイスで動作するサービスメタデータパッケージを迅速かつ迅速に作成および検証する方法として表示できます。

-   **プレビューモード**パッケージが正しく作成され、エンドツーエンドテスト用の送信準備が整っていると確信できる場合に使用します。 このモードでは、パッケージは Windows デベロッパーセンターハードウェアダッシュボードによって署名され、テストコンピューターが正しくプロビジョニングされていれば、テストコンピューターに自動的にダウンロードされます。

プレビューテストを完了し、パッケージがすべてのシナリオで動作することを確認したら、パッケージをライブに発行できます。

次の図は、ワークフローについて説明しています。

![サービスメタデータパッケージの作成](images/mbae-sxs81-createpackageworkflow.png)

新しいサービスメタデータパッケージを作成するには、「[サービスメタデータパッケージを作成するための手順](#steps-for-creating-a-service-metadata-package)」を参照してください。

既存のサービスメタデータパッケージを編集するには、「[サービスメタデータパッケージを編集する手順](#steps-for-editing-a-service-metadata-package)」を参照してください。

## <a name="steps-for-creating-a-service-metadata-package"></a>サービスメタデータパッケージを作成する手順


Windows デベロッパーセンターハードウェアダッシュボードでサービスメタデータパッケージを作成するには、次の手順に従います。

-   [1-サービスメタデータパッケージに必要な情報を収集します。](#1-gather-the-required-information-for-the-service-metadata-package)

-   [2-サービスメタデータパッケージを作成する](#2-create-the-service-metadata-package)

-   [3-Microsoft Store デバイスアプリにストアマニフェストファイルを挿入する](#3-insert-the-store-manifest-file-into-the-microsoft-store-device-app)

-   [4-サービスメタデータパッケージをテストする](#4-test-the-service-metadata-package)

-   [5-サービスメタデータパッケージを発行する](#5-publish-the-service-metadata-package)

### <a name="1-gather-the-required-information-for-the-service-metadata-package"></a>1-サービスメタデータパッケージに必要な情報を収集します。

このトピックの手順2のサービスメタデータウィザードの手順を実行すると、デバイスに関連付けたいモバイルブロードバンドアプリプロジェクトの package.appxmanifest ファイルに格納されているいくつかの情報が必要になります。 次の手順に従って情報を収集し、このトピックの手順2で使用できるようにします。

**注意**  
この手順の値を収集する前に、モバイルブロードバンドアプリが Microsoft Store に関連付けられている必要があります。 モバイルブロードバンドアプリを関連付けると、パッケージマニフェストファイルの値が、Microsoft Store 開発者アカウントの情報を使用するように更新されます。 ただし、モバイルブロードバンドアプリを Microsoft Store に発行する必要はありません。 サービスメタデータパッケージを発行する準備が整うまで、ローカルの開発環境にとどまります。



**UWP デバイスアプリ情報を収集するには**

1.  Visual Studio 2013 を使用して、モバイルブロードバンドアプリプロジェクトを開きます。

2.  右側のウィンドウで、 **package.appxmanifest**ファイルを右クリックし、 **[コードの表示]** をクリックします。

3.  Package.appxmanifest ファイルから次の属性を収集します。

    -   **Id**要素から、サービスメタデータウィザードの **[パッケージ名]** フィールドには**name**属性が使用されます。

    -   **Id**要素からは、サービスメタデータウィザードの **[発行元]** フィールドに **[パブリッシャー]** 属性が使用されます。

    -   **Applications**要素から、**アプリケーション**の子要素の**Id**属性がサービスメタデータウィザードの **[アプリ Id]** フィールドに使用されます。

4.  Package.appxmanifest ファイルを閉じます。

![コードビューの package.appxmanifest ファイル](images/mbae-sxs-appxmanifest.png)

また、次の手順を実行して、Visual Studio 2013 を使用せずにこれを完了することもできます。

**Visual Studio 2013 を使用せずにモバイルブロードバンドアプリ情報を収集するには**

1.  モバイルブロードバンドアプリの package.appxmanifest ファイルに移動します。

2.  ファイルを右クリックし、[ファイルを**開くアプリケーション**の選択] をクリックします。

3.  **[このアプリケーションをすべての package.appxmanifest ファイルに使用する]** チェックボックスをオフにし、 **[その他のオプション]** をクリックして、 **[メモ帳]** をクリックします。

4.  Package.appxmanifest ファイルから次の属性を収集します。

    -   **Id**要素から、サービスメタデータウィザードの **[パッケージ名]** フィールドには**name**属性が使用されます。

    -   **Id**要素からは、サービスメタデータウィザードの **[発行元]** フィールドに **[パブリッシャー]** 属性が使用されます。

    -   **Applications**要素から、**アプリケーション**の子要素の**Id**属性がサービスメタデータウィザードの **[アプリ Id]** フィールドに使用されます。

5.  Package.appxmanifest ファイルを保存して閉じます。

### <a name="2-create-the-service-metadata-package"></a>2-サービスメタデータパッケージを作成する

サービスメタデータは、Windows デベロッパーセンターハードウェアダッシュボードのサービスメタデータウィザードを使用して作成されます。

**サービスメタデータパッケージを作成するには**

1.  <https://sysdev.microsoft.com> に移動します。

2.  **[デバイスメタデータ]** 見出しの下にある **[モバイルブロードバンドエクスペリエンスの作成]** をクリックします。

    ![これは、ダッシュボードのランディングページです。](images/mbae-sxs81-dashboard.png)

3.  **[サービス情報]** ページで、次のフィールドを入力し、 **[次へ]** をクリックします。

    -   **Windows ネットワークの選択 UI で使用するネットワークの名前**(Windows 接続マネージャーで顧客に表示されるネットワークの名前) を入力します。

    -   **サービス番号を入力**します。これは、プロビジョニングメタデータの "carrier ID" フィールドと一致する必要がある GUID です。 GUID を作成するには、Visual Studio 2013 を使用します。 GUID を作成する方法の詳細については、「 [guid の作成 (guidgen.exe)](https://go.microsoft.com/fwlink/p/?linkid=330070)」を参照してください。

    -   **Windows ネットワークの選択 UI に表示されるアイコンをアップロード**します。 **[参照]** をクリックし、windows 接続マネージャーで顧客に表示されるアイコンを選択します。

    -   **アプリに Windows notification イベントハンドラーを入力します (以下の権利チェックが必要な場合を除きます)** 。これは、モバイルブロードバンドアプリに登録されている通知ハンドラーです。

    -   **ユーザーがモバイルブロードバンド接続 (個人用ホットスポット) を共有できるようにしますか?** -可能なオプションは**常に [許可**]、[**権利チェックのみを許可する] (Windows 通知イベントハンドラーが必要)** 、 **[許可しない]** です。 既定のオプションでは、常にを許可します。

    -   **SIMs で PIN のロック解除を実行するためにシステム管理者特権を必要としますか?** – SIM カードの固定を解除するためにシステム管理者特権を必要とする場合は、 **[はい]** をクリックします。

    ![ウィザードの [サービス情報] ステップ](images/mbae-sxs81-serviceinfostep.png)

4.  **[ハードウェア情報]** ページで、エクスペリエンスを識別するために使用する必要がある情報を選択します。 チェックボックスをオンにすると、適切なネットワーク範囲を追加できます。 生成された ID は、適切なサブスクライバーが識別されるように、Windows APN データベースに存在する必要があります。 APN データベースの詳細については、「 [Cosa/apn データベースの送信](cosa-apn-database-submission.md)」を参照してください。

    -   国際モバイル加入者 Id (IMSI) を使用する GSM プロバイダーの場合は、 **gsm**の見出しの下にある**imsi**チェックボックスをオンにします。 **[プロバイダー id]** ボックスに、GSM サービスプロバイダー id を入力します。 **[Imsi/ICCID 範囲]** 見出しの下に範囲を入力し、 **[追加]** をクリックします。

    -   統合回線カード識別子 (ICCID) を使用する GSM プロバイダーの場合は、 **gsm**の見出しの下にある **[SIM ICC ID]** チェックボックスをオンにします。 **[プロバイダー ID と ICC id の範囲を入力]** してください の見出しの下に範囲を入力し、 **[追加]** をクリックします。

    -   ホームプロバイダー名を使用する GSM プロバイダーの場合は、 **[gsm]** 見出しの下にある **[ホームプロバイダー名]** チェックボックスをオンにします。 **[ホームプロバイダー名を入力するか、プロバイダー id (MCC + MNC) を入力]** してください という見出しの下に、プロバイダー id とプロバイダー名を入力し、 **[追加]** をクリックします。

    -   SID を使用する CDMA プロバイダーの場合は、 **Cdma**の見出しの下にある **[sid]** チェックボックスをオンにします。 [ **Sid を入力**してください] ボックスに、CDMA sid を入力します。

    -   プロバイダー名を使用する CDMA プロバイダーの場合は、 **[Cdma]** 見出しの下にある **[プロバイダー名]** チェックボックスをオンにします。 **[プロバイダー名の入力]** ボックスに、cdma サービスプロバイダー名を入力します。

    -   **[次へ]** をクリックします。

    ![これは、ウィザードの [ハードウェア情報] 手順です。](images/mbae-sxs81-hardwareinfostep.png)

5.  **[アプリ情報]** ページで、このトピックの手順1で収集した情報を入力します。 特権アプリをさらに追加する場合は、**追加** をクリックし、最大 7 をクリックします。 すべての特権アプリを入力したら、 **[次へ]** をクリックします。

    ![これは、ウィザードの [アプリ情報] 手順です。](images/mbae-sxs81-appinfostep.png)

6.  **[確認]** ページで、情報が正しいことを確認します。 **[開発者モード]** または **[プレビューモード]** オプションを選択し、 **[送信]** をクリックします。

    -   **開発者モード**–パッケージは署名されていないため、手動でダウンロードしてすべてのコンピューターにインストールする必要があります。 このオプションは、オフライン開発用にパッケージを保存する場合に使います。

    -   **プレビューモード**–パッケージは署名され、適切なレジストリ設定が構成されているコンピューターをテストするために、Microsoft から自動的にダウンロードされます。 プレビューモードでは、モバイルブロードバンドアプリが Microsoft Store に発行されているかどうかは確認されません。

    ![これは、ウィザードの [確認] 手順です。](images/mbae-sxs81-confirm.png)

### <a name="3-insert-the-store-manifest-file-into-the-microsoft-store-device-app"></a>3-Microsoft Store デバイスアプリにストアマニフェストファイルを挿入する

ストアマニフェストファイルは、UWP デバイスアプリに含まれている必要があります。 サービスメタデータパッケージからストアマニフェストファイルをダウンロードし、モバイルブロードバンドアプリプロジェクトに挿入するには、次の手順に従います。

**ストアマニフェストファイルを挿入する**

1.  Windows デベロッパーセンターのハードウェアダッシュボードで、サービスメタデータパッケージの エクスペリエンスの管理 ページの サービスメタデータパッケージ をクリックし、 **StoreManifest** をクリックしてストアマニフェストファイルをダウンロードします。

    ![ストアマニフェストファイルをダウンロードする](images/mbae-sxs81-storemanifest.png)

2.  Visual Studio 2013 を使用して、モバイルブロードバンドアプリプロジェクトを開きます。

3.  プロジェクトを右クリックし、 **[追加]** をクリックして、 **[既存の項目]** をクリックします。

4.  ダウンロードしたストアマニフェストファイルを参照し、 **[追加]** をクリックします。

5.  モバイルブロードバンドアプリを再コンパイルし、Microsoft Store に再度発行します。

### <a name="4-test-the-service-metadata-package"></a>4-サービスメタデータパッケージをテストする

サービスメタデータパッケージをテストするには、モバイルブロードバンドデバイスとサービスメタデータパッケージファイルが必要です。 テストシステムを構成し、サービスメタデータパッケージをインストールする手順は、パッケージのモードによって異なります。

### <a name="span-idtest_a_service_metadata_package_in_developer_modespanspan-idtest_a_service_metadata_package_in_developer_modespanspan-idtest_a_service_metadata_package_in_developer_modespantest-a-service-metadata-package-in-developer-mode"></a><span id="Test_a_service_metadata_package_in_developer_mode"></span><span id="test_a_service_metadata_package_in_developer_mode"></span><span id="TEST_A_SERVICE_METADATA_PACKAGE_IN_DEVELOPER_MODE"></span>開発者モードでのサービスメタデータパッケージのテスト

シナリオを正しく動作させるには、パッケージを手動でダウンロードして適切な場所にインストールする必要があります。 開発者モードのパッケージには、新しいパッケージを作成したか既存のパッケージを作成したかに応じて、2つの異なるエントリポイントからアクセスする必要があります。

新しいパッケージを作成した場合は、Windows デベロッパーセンターのハードウェアダッシュボードで **[エクスペリエンスの管理]** をクリックし、関連付けられていない **[開発パッケージ]** (**エクスペリエンスの管理**テーブルの最初のエントリ) をクリックします。 次の図に例を示します。

![サービスメタデータパッケージのダウンロード](images/mbae-sxs81-managedevpackages.png)

既にエクスペリエンスに関連付けられている既存のサービスメタデータパッケージを編集した場合は、 **[エクスペリエンスの管理]** テーブルからエクスペリエンスを選択すると、 **[メタデータパッケージ]** テーブルに developer mode パッケージが表示されます。 **[MBAE Zip パッケージの編集]** をクリックしてダウンロードします。

![サービスメタデータパッケージのダウンロード](images/mbae-sxs81-manageassociatedpackages.png)

サービスメタデータパッケージをダウンロードした後、サービスメタデータパッケージが署名されていないため、テスト署名を有効にする必要があります。 テスト署名を有効にするには、管理者特権のコマンドプロンプトから**bcdedit – set testsigning オンを実行**し、コンピューターを再起動します。

テスト署名を有効にした後、サービスメタデータパッケージから devicemetadata-ms ファイルを次の場所に \*コピーします: **% Programdata%\\Microsoft\\Windows\\DeviceMetadataStore\\** <em>culture</em>。ここで、 *culture*はコンピューターの現在のカルチャコードです。

### <a name="span-idtest_a_service_metadata_package_in_preview_modespanspan-idtest_a_service_metadata_package_in_preview_modespanspan-idtest_a_service_metadata_package_in_preview_modespantest-a-service-metadata-package-in-preview-mode"></a><span id="Test_a_service_metadata_package_in_preview_mode"></span><span id="test_a_service_metadata_package_in_preview_mode"></span><span id="TEST_A_SERVICE_METADATA_PACKAGE_IN_PREVIEW_MODE"></span>プレビューモードでのサービスメタデータパッケージのテスト

サービスメタデータパッケージがプレビューモードの場合は、テストコンピューターにプレビューキーレジストリエントリを作成する必要があります。 Preview Key レジストリエントリの構成の詳細については、「[プレビューパッケージの作成](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)」を参照してください。

**注:**  
プレビューモードのサービスメタデータパッケージをテストするために、テスト署名を有効にする必要はありません。



プレビューキーのレジストリエントリが作成されたら、モバイルブロードバンドデバイスに接続し、[ネットワーク] の一覧に表示されていることを確認します。 そうでない場合は、[トラブルシューティング](#troubleshooting)のセクションで詳細を確認してください。

### <a name="span-idclear_the_existing_service_metadataspanspan-idclear_the_existing_service_metadataspanspan-idclear_the_existing_service_metadataspanclear-the-existing-service-metadata"></a><span id="Clear_the_existing_service_metadata"></span><span id="clear_the_existing_service_metadata"></span><span id="CLEAR_THE_EXISTING_SERVICE_METADATA"></span>既存のサービスメタデータをクリアする

サービスメタデータが PC にインストールされている場合、メタデータに含まれる値は、レジストリ、メタデータキャッシュ、メタデータストア、WWAN プロファイル、開発ノードなどのさまざまな場所に格納されます。 これにより、同じまたは異なるメタデータパッケージを使用して複数のテストを繰り返すことが困難になる場合があります。 サービスメタデータが正しくインストールされていることを確認するには、既存のサービスメタデータをクリアする必要があります。 すべてのトレースを削除する PowerShell スクリプトを実行するようにテストコンピューターを設定することにより、既存のサービスメタデータを消去できます。 まず、テストコンピューターで環境を設定する必要があります。

**注:**  
これは、Windows RT デバイスでは機能しません。 「Windows RT を実行しているデバイスのサービスメタデータを消去するには」の手順に従います。



**サービスメタデータを消去するための環境を設定するには**

1.  Psexec (<https://go.microsoft.com/fwlink/p/?linkid=330071>) をダウンロードし、フォルダーに抽出します。

2.  Windows Driver Kit Windows 8.1 (<https://go.microsoft.com/fwlink/?LinkId=330072>) をダウンロードしてインストールします。

3.  WDK ファイルがインストールされている場所に移動します。 既定の場所は、 **C:\\Program Files (x86)\\Windows kit\\8.1\\Tools**です。 テストコンピューターで x86 が実行されている場合は、x86 フォルダーから psexec と同じフォルダーに devcon をコピーします。 テストコンピューターで x64 が実行されている場合は、x64 フォルダーから devcon をコピーします。

4.  次のスクリプトを、MetadataRemovalScript と PsExec と同じフォルダーに保存します。

    **注:**  
    **[保存の種類]** ボックスで、ファイルを保存する前に [**すべてのファイル (\*\*)** ] を選択してください。




```PowerShell
# DEVICE SHOULD BE CONNECTED TO MACHINE

Write-Host "Launching devcon to remove MBAE software device nodes devcon.exe remove @SWD\MBAE\*"
$DevconParameters = ' remove @SWD\MBAE\* '
try
{
   Start-Process devcon.exe -ArgumentList $DevconParameters
}
catch
{
   $Error[0] # Dump details about the last error
   Write-Host "Error running devcon.exe " $DevconParameters
   exit
}

Write-Host "Removing MB Profiles"
$mbprcmd = "mbn sh pr i=*"
$mddelprcmd = "mbn del pr i=* name="

$cmdout = $mbprcmd | netsh | Out-String

$tokens = $cmdout.Split( [String[]] ("`r`n"), [StringSplitOptions]::RemoveEmptyEntries)

if($tokens.Length -gt 3)
{
   for($i=3;$i -lt $tokens.Length-1;$i++)
   {
      $x = $mddelprcmd + '"' + $tokens[$i].trim() +'"'
      Write-Host "Deleting Profile Cmd :" $x
      $x | netsh
   }
}

Write-Host ""
Write-Host "Disabling ALL Mobile Broadband Adapters"
$MBAdapters = Get-Netadapter -Name "Mobile Broadband*"

foreach($MBAdapter in $MBAdapters)
{
   Write-Host "Disabling MB Adapter :"$MBAdapter.Name
   Disable-NetAdapter -Name $MBAdapter.Name -Confirm:$false
}

Write-Host "Stopping Device Setup Manager Service"
Stop-Service DsmSvc

Write-Host "Removing MBAE metadata packages in store"
#Find Package Ids
$MBAEPackageRegKeyHive = "HKLM:\SOFTWARE\Microsoft\WwanSvc\MobileBroadbandAccounts\Accounts\"
if(Test-Path $MBAEPackageRegKeyHive)
{
    $DevMetadataStorePath = join-path -Path $Env:ProgramData -ChildPath "Microsoft\Windows\DeviceMetadataStore"

    $PackageIds = Get-ChildItem $MBAEPackageRegKeyHive | ForEach-Object {Get-ItemProperty $_.pspath} | where-object {$_.MetadataPackageId} | Foreach-Object {$_.MetadataPackageId}
    foreach($PackageId in $PackageIds)
    {
        $PackageStoreFile = $PackageId + ".devicemetadata-ms"        
        $PackageStorePath = Get-ChildItem $DevMetadataStorePath -Recurse -Filter $PackageStoreFile
        if($PackageStorePath -ne $null)
        {
            Write-Host "Deleting Device Metadata Store @" $PackageStorePath.FullName
            Remove-Item -Force $PackageStorePath.FullName
        }
    }
}

Write-Host "Removing all metadata from cache"
$DevMetadataCachePath = join-path -Path $Env:ProgramData -ChildPath "Microsoft\Windows\DeviceMetadataCache\*"
if(Test-Path $DevMetadataCachePath)
{
   Write-Host "Delete All Metadata Packages under "$DevMetadataCachePath
   Remove-Item -Recurse -Force $DevMetadataCachePath
}

Write-Host "Cleanup MBAE registry keys"
$MBAERegKeyPath = "HKLM:\SOFTWARE\Microsoft\WwanSvc\MobileBroadbandAccounts\*"
if(Test-Path $MBAERegKeyPath)
{
    Write-Host "Found MBAE reg keys - deleting"   
    Remove-Item -Path $MBAERegKeyPath -Recurse
}

Write-Host "Enabling all MB Adapters, press any key to continue"
$keypress = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyUp")

$MBAdapters = Get-Netadapter -Name "Mobile Broadband*"

foreach($MBAdapter in $MBAdapters)
{
   Write-Host "Enabling MB Adapter :"$MBAdapter.Name
   Enable-NetAdapter -Name $MBAdapter.Name -Confirm:$false
}


Write-Host "END of Script"

# DEVICE SHOULD BE CONNECTED TO MACHINE

Write-Host "Launching devcon to remove MBAE software device nodes devcon.exe remove @SWD\MBAE\*"
$DevconParameters = ' remove @SWD\MBAE\* '
try
{
    Start-Process devcon.exe -ArgumentList $DevconParameters    
}
catch
{
    $Error[0] # Dump details about the last error
    Write-Host "Error running devcon.exe " $DevconParameters
    exit
}

Write-Host "Removing MB Profiles"
$mbprcmd = "mbn sh pr i=*"
$mddelprcmd = "mbn del pr i=* name="

$cmdout = $mbprcmd | netsh | Out-String

$tokens = $cmdout.Split( [String[]] ("`r`n"), [StringSplitOptions]::RemoveEmptyEntries)

if($tokens.Length -gt 3)
{
    for($i=3;$i -lt $tokens.Length-1;$i++)
    {
        $x = $mddelprcmd + '"' + $tokens[$i].trim() +'"'
        Write-Host "Deleting Profile Cmd :" $x
        $x | netsh
    }
}

Write-Host ""
Write-Host "Please remove the MB device from the system and press any key to continue"
$keypress = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown")


Write-Host "Removing MBAE metadata packages in cache and store"
#Find Package Ids
$MBAEPackageRegKeyHive = "HKLM:\SOFTWARE\Microsoft\WwanSvc\MobileBroadbandAccounts\Accounts\"
if(Test-Path $MBAEPackageRegKeyHive)
{
    $DevMetadataCachePath = join-path -Path $Env:ProgramData -ChildPath "Microsoft\Windows\DeviceMetadataCache"
    $DevMetadataStorePath = join-path -Path $Env:ProgramData -ChildPath "Microsoft\Windows\DeviceMetadataStore"

    $PackageIds = Get-ChildItem $MBAEPackageRegKeyHive | ForEach-Object {Get-ItemProperty $_.pspath} | where-object {$_.MetadataPackageId} | Foreach-Object {$_.MetadataPackageId}
    foreach($PackageId in $PackageIds)
    {
        $PackageCacheFolder = Get-ChildItem $DevMetadataCachePath -Recurse -Filter $PackageId
        if($PackageCacheFolder -ne $null)
        {
            Write-Host "Deleting Device Metadata Cache @" $PackageCacheFolder.FullName
            Remove-Item -Recurse -Force $PackageCacheFolder.FullName
        }
        $PackageStoreFile = $PackageId + ".devicemetadata-ms"        
        $PackageStorePath = Get-ChildItem $DevMetadataStorePath -Recurse -Filter $PackageStoreFile
        if($PackageStorePath -ne $null)
        {
            Write-Host "Deleting Device Metadata Store @" $PackageStorePath.FullName
            Remove-Item -Force $PackageStorePath.FullName
        }
    }
}

Write-Host "Cleanup MBAE registry keys"
$MBAERegKeyPath = "HKLM:\SOFTWARE\Microsoft\WwanSvc\MobileBroadbandAccounts\*"
if(Test-Path $MBAERegKeyPath)
{
    Write-Host "Found MBAE reg keys - deleting"   
    Remove-Item -Path $MBAERegKeyPath -Recurse
}


Write-Host "END"
```


環境がセットアップされたら、既存のサービスメタデータを消去するたびに、次の手順を実行します。

**サービスメタデータを消去するには**

1.  モバイルブロードバンドデバイスがテストコンピューターに接続されていることを確認します。

2.  管理者特権でのコマンドプロンプトで、psexec を展開したフォルダーに移動し、 **psexec/s/i powershell**を実行します。

3.  PowerShell コマンドプロンプトで、psexec を抽出したフォルダーに移動します。

4.  「 **Set-set-executionpolicy 無制限**」と入力し、enter キーを押します。

5.  「 **Y** 」と入力し、「」と入力します。

6.  **\\MetadataRemovalScript**を入力し、enter キーを押します。

7.  メッセージが表示されたら、モバイルブロードバンドデバイスを削除し、enter キーを押します。

8.  テストコンピューターからサービスメタデータを消去するたびに、この手順を繰り返します。

**Windows RT を実行しているデバイスのサービスメタデータを消去するには**

1. ソフトウェアデバイスノードを削除します。

   1.  デバイスマネージャーで、 **[表示]** をクリックし、非表示の **[デバイスの表示]** をクリックします。

   2.  [ソフトウェアデバイス] を展開します。

   3.  次のデバイスノードを右クリックし、 **[アンインストール]** をクリックします。 **windows. Devices. Smsdevice**と**Windows. network operators. MobileBroadbandAccount**

2. すべてのインターフェイスからすべてのモバイルブロードバンドプロファイルを削除します。

   1. 管理者特権のコマンドプロンプトで、「 **netsh mbn 表示 (pro i =\\** 」と入力し*

   2. 各プロファイルについて、「 **netsh mbn delete profile name = "ここにプロファイル名" i =\\*」** と入力し、enter キーを押します。

3. すべてのモバイルブロードバンドアダプターを無効にします。

   1.  デバイスマネージャーで、 **[ネットワークアダプター]** を展開します。

   2.  各モバイルブロードバンドデバイスを右クリックし、 **[無効にする]** をクリックします。

4. 管理者特権のコマンドプロンプトで、「 **sc stop dsmsvc** 」と入力して DSM サービスを停止し、enter キーを押します。

5. サービスメタデータパッケージを含むフォルダーを、 **% Programdata%\\Microsoft\\Windows\\DeviceMetadataStore**から削除することで、デバイスメタデータストアからサービスメタデータパッケージを削除します。 サービスメタデータパッケージを特定するには、MobileBroadbandInfo ファイルを検索します。

6. すべての WWAN SVC MBAE レジストリエントリを削除します。

   1.  レジストリエディターで、次のレジストリエントリとすべての子エントリを削除します。 HKEY\_ローカル\_マシン\\ソフトウェア\\Microsoft\\WwanSvc\\MobileBroadbandAccounts。

   2.  レジストリエントリを削除するためのアクセス権がない場合は、フルコントロールアクセス許可を自分に付与する必要があります。

7. すべてのモバイルブロードバンドアダプターを有効にします。

   1.  デバイスマネージャーで、 **[ネットワークアダプター]** を展開します。

   2.  各モバイルブロードバンドデバイスを右クリックし、 **[有効]** をクリックします。

### <a name="5-publish-the-service-metadata-package"></a>5-サービスメタデータパッケージを発行する

サービスメタデータパッケージが正常に動作することを確認したら、最後の手順としてパッケージを解放します。 次に示すように、 **[リリース]** ボタンをクリックして、特定のエクスペリエンスにアタッチされているパッケージを選択することにより、パッケージを解放できます。

![サービスメタデータパッケージをリリースする](images/mbae-sxs81-releasetolive.jpg)

## <a name="steps-for-editing-a-service-metadata-package"></a>サービスメタデータパッケージを編集する手順


サービスメタデータパッケージを編集するには、Windows デベロッパーセンターハードウェアダッシュボードの [エクスペリエンスの管理] ページを使用します。

![[エクスペリエンスの管理] ページ](images/mbae-sxs81-manageexperience.png)

## <a name="troubleshooting"></a>[トラブルシューティング]


[ネットワーク] の一覧を開き、モバイルブロードバンドネットワークを探します。 サービスメタデータパッケージ**Serviceinfo .xml**ファイルで使用した名前とアイコンを使用してネットワークが表示されている場合は、パッケージが正しく解析されます。 同じ名前とアイコンを持つサービスメタデータパッケージを更新する場合、または約1分後に名前またはアイコンがリストに表示されない場合は、次の手順に従って追加の手順を実行する必要があります。

-   メタデータの更新を強制する

-   メタデータキャッシュを確認する

-   レジストリを確認する

-   WWAN ログを確認する

### <a name="span-idforcemdrefspanspan-idforcemdrefspanforce-a-metadata-refresh"></a><span id="forcemdref"></span><span id="FORCEMDREF"></span>メタデータの更新を強制する

メタデータとモバイルブロードバンドアプリシステムの一部はネットワークアクセスに依存していますが、これは失敗し、コンピューターが不整合な状態のままになる可能性があります。 このような場合は、サービスメタデータがインストールされていないか、モバイルブロードバンドアプリがインストールされていない状況が発生する可能性があります。 システムは定期的に状況を修復しようとしますが、電力を節約するために、再試行は非常にまれです (1 日に数回だけ)。 次の再試行を待つのではなく、手動で強制的に更新を強制することができます。 これを行うには、次の手順を実行します。

1.  デスクトップの**コントロールパネル**を開きます。

2.  [**デバイスとプリンター] を**開きます。

3.  **[表示]** メニューの **[最新]** の状態に更新 をクリックするか、 **F5**キーを押します。 この操作により、メタデータが再解析され、バックグラウンドイベントが再登録されます。

**重要**  
サービスメタデータパッケージが既に正常に解析されている場合、システムはこの更新をメタデータの更新として扱います。 この場合、メタデータパッケージのファイル名には別の GUID が、 **Packageinfo .xml**の[LastModifiedDate](lastmodifieddate.md)要素に更新されたタイムスタンプが含まれている必要があります。



### <a name="span-idcheckmdcachespanspan-idcheckmdcachespancheck-the-metadata-cache"></a><span id="checkmdcache"></span><span id="CHECKMDCACHE"></span>メタデータキャッシュを確認する

メタデータの更新で問題が解決しなかった場合は、サービスメタデータパッケージが有効であること、および正しいハードウェア Id があることを確認してください。 これを行うには、次の手順を実行します。

1. **% Programdata%\\Microsoft\\Windows\\DeviceMetadataCache\\dmrccache\\** <em>culture</em>に移動します。ここで、 *culture*はテストコンピューターの現在のカルチャのカルチャコード (たとえば、**en-us**または**es**)。

2. メタデータパッケージと同じ名前のフォルダーを探します ( **devicemetadata**拡張子は使用しません)。 このディレクトリが存在しない場合は、次の4つのいずれかを意味します。

   -   サービスメタデータパッケージが破損しています。

   -   サービスメタデータパッケージに正しいハードウェア Id がありません。

   -   モバイルブロードバンドデバイスは、メタデータをダウンロードできる状態ではなく、サービスメタデータパッケージをコピーする前にデバイスに接続している状態でもありません。

   -   メタデータパッケージのデジタル署名を確認しているときに問題が発生しました。 これは通常、テストコンピューターでテスト署名が有効になっていないことが原因で発生します。

パッケージが破損していないことと、サービスメタデータパッケージをコピーした後にモバイルブロードバンドデバイスに最初に接続したことが確実である場合は、IMSI の範囲を確認します。 非常に簡単に入力できるのは、数が多すぎる、または、数が少なすぎるか、または少なくなっています。 これらの項目を確認または修正した後も問題が解決しない場合は、レジストリを確認する必要があります。

### <a name="span-idcheckregspanspan-idcheckregspancheck-the-registry"></a><span id="checkreg"></span><span id="CHECKREG"></span>レジストリを確認する

**警告**  
本当に必要な場合を除き、アプリケーションに属していないレジストリデータは編集しないでください。 レジストリにエラーがある場合は、システムが正常に機能しない可能性があります。 そうでない場合は、どのような状況でも、 **MobileBroadbandAccounts**レジストリキーを削除します。 Windows では再作成されず、機能が無効になります。



レジストリを確認するには、次の手順を実行します。

1.  レジストリ エディターを開きます。

2.  **HKLM\\SOFTWARE\\Microsoft\\WwanSvc\\MobileBroadbandAccounts**にアクセスします。

3.  このレジストリキー内で、 **Accounts**、 **Networkinterfacebindings**、 **Data**の3つのキーを探します。 既定では、これらのキーは存在しません。モバイルブロードバンドデバイスの挿入、電源オン、または接続が初めて行われるときに、自動的に作成されます。

4.  **アカウント**または**networkinterfacebindings**キーが存在せず、既にモバイルブロードバンドアダプターに接続されているか、オンになっている場合は、WWAN ログを確認します。

5.  これらのキーの一部またはすべてが存在する場合は、**ツリー**ビューで **[アカウント]** キーを展開します。 Guid に類似した名前を持つ1つ以上のレジストリキーが、その中に存在する必要があります。 レジストリツリーのエントリは、次に示すレジストリツリーのようになります。

    ![解析されたアカウントのレジストリエントリ](images/fig2-registryentries-for-parsedmobilebroadbandaccount.png)

    レジストリキーが上の図のように見える場合 (値の名前は、アカウントが GSM または CDMA ネットワーク上にあるかどうかによって多少異なります)、[ネットワーク] の一覧にアイコンが表示されない場合は、イベントログを確認する必要があります。

    レジストリエントリが次の図のようになっている場合は、サービスメタデータパッケージがデバイスメタデータストアにコピーされる前にモバイルブロードバンドアダプターが挿入された、サービスメタデータパッケージが破損している、またはハードウェア Id が正しくないことを示します. メタデータパッケージをメタデータストアにコピーする前にデバイスに接続している、または電源をオンにした状況を解決するには、「メタデータの更新を強制する」の手順を実行します。 それ以外の場合は、「WWAN ログの確認」の手順に従います。

    ![未解析アカウントのレジストリエントリ](images/fig1-registryentries-for-unparsedmobilebroadbandaccount.png)

### <a name="span-idcheckwwanlogsspanspan-idcheckwwanlogsspancheck-the-wwan-logs"></a><span id="checkwwanlogs"></span><span id="CHECKWWANLOGS"></span>WWAN ログを確認する

**HKLM\\ソフトウェア\\Microsoft\\WwanSvc\\MobileBroadbandAccounts**の下に**アカウント**または**networkinterfacebindings**のレジストリキーがない場合、または完全に設定されていないエントリがある場合は、WWAN ログを確認する必要があります。 次の手順を実行すると、コンピューターが既知の状態にリセットされます。

1.  モバイルブロードバンドデバイスを取り外します (デバイスが埋め込まれている場合は、**デバイスマネージャー**で無効にします)。

2.  次のレジストリキーを削除します。

    -   **HKLM\\ソフトウェア\\Microsoft\\WwanSvc\\MobileBroadbandAccounts\\アカウント**

    -   **HKLM\\ソフトウェア\\Microsoft\\WwanSvc\\MobileBroadbandAccounts\\NetworkInterfaceBindings**

    **警告**  
    それ以外の状況では、 **HKLM\\ソフトウェア\\Microsoft\\WwanSvc\\MobileBroadbandAccounts\\** レジストリキーを削除します。 Windows では再作成されず、機能が無効になります。



ログには、アカウント管理の WWAN サービスエントリログエントリとパーサータスクエントリという2種類のエントリがあります。 最初の型は、ネットワークハードウェアの問題によって発生する問題をデバッグするのに役立ちます。2つ目の型は、メタデータの解析に関する問題をデバッグするのに役立ちます。

正常に処理されたネットワークのアカウント管理の WWAN サービスエントリのログエントリは、次のようになります。

```syntax
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:26.567 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Account updater started for network interface {7a0a0dce-0a51-471a-8c16-6e767cd0b861. 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:26.567 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Getting home provider ID from hardware device for network interface {7A0A0DCE-0A51-471A-8C16-6E767CD0B861}.  Provider ID is "234567". 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:26.567 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Getting home provider name from hardware device for network interface {7A0A0DCE-0A51-471A-8C16-6E767CD0B861}.  Provider name is "MS GSM". 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:26.586 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Network identity not recognized, assigning new network account ID. 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:26.597 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Devnode create/update started. 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:26.617 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Devnode create/update finished. 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:26.617 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Data store create/update started. 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:26.707 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Data store create/update finished. 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:26.707 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Account updater finished for network interface {7a0a0dce-0a51-471a-8c16-6e767cd0b861}.
```

これらのエントリは、ログで**アカウント管理**を検索することで見つけることができます。 この場合、最も重要なエントリは、**データストアの作成/更新が開始**され、**データストアの作成/更新が完了**したことです。 これらのエントリが存在し、エラーメッセージがない場合は、ハードウェアが正常に動作しています。 (ここで参照されるデータストアには、「レジストリの確認」で説明されているレジストリキーが含まれています)。

これに対し、SIM が削除されたデバイスでは、通常、エントリは次のようになります。

```syntax
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Account updater started for network interface {7a0a0dce-0a51-471a-8c16-6e767cd0b861}. 
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Detected removal of SIM from device bound to network interface {7A0A0DCE-0A51-471A-8C16-6E767CD0B861}. 
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Devnode create/update started. 
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Devnode create/update finished. 
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Account updater finished for network interface {7a0a0dce-0a51-471a-8c16-6e767cd0b861}. 
```

**注:**  
後者の例では、**データストアの作成/更新が開始**されたエントリや、**データストアの作成/更新が完了**したエントリはありません。 SIM に格納されている情報はアカウント管理プロセスにとって重要であるため、SIM がないデバイスには、関連するメタデータは必要ありません。



ハードウェアが正常に処理されていても、[ネットワーク] の一覧にロゴまたは名前が表示されない場合は、メタデータパッケージに問題がある可能性があります。 これは、ログ内のパーサータスクエントリを使用して調査できます。 これらのエントリを検索するには、「**パーサー-タスク**」を検索します。 正常に解析されたログエントリは、通常、次のようになります。

```syntax
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.007 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Parser task started. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.030 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Parsing metadata for device container with id "{972238E7-36F4-11E1-BC81-00155DE96B01}" for culture "en-US". 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.297 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Starting parse of mobile broadband service information file. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.297 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Metadata package contains no data for culture "en-US". Using fallback data. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.356 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Finished parse of mobile broadband service information file. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.356 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Starting update of stored network account information. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.377 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]The mobile broadband account now contains service provider information. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.378 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Finished update of stored network account information. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.378 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Applying WWAN profiles for service provider Contoso GSM. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.378 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Starting creation and/or update of WWAN profiles. 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:32.512 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: Profile Update Notification received 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:32.519 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: Complete Scanning 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:32.519 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: WWAN Interface information 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:32.586 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: Profile Update Notification received 
[0]02CC.0CD0::‎2012‎-‎01‎-‎04 09:22:32.651 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: Profile Update Notification received 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.659 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Finished creation and/or update of WWAN profiles. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.659 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]WWAN profiles applied successfully for service provider Contoso GSM. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.659 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Adding trusted provisioning certificates for service provider Contoso GSM. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:32.659 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Starting setting of trusted certificates for network provisioning. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:33.016 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Finished setting of trusted certificates for network provisioning. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:33.016 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Trusted provisioning certificates added successfully for service provider Contoso GSM. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:33.017 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Parser task finished. 
[0]0DA8.0A2C::‎2012‎-‎01‎-‎04 09:22:33.017 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]MbaeParserTask completed successfully. 
```

これらのログは、MobileBroadbandInfo ファイルが正しく解析されたこと、パーサータスクが、プロファイルを正常に更新した WWAN サービスのログと共に適用したこと、およびパーサータスクによって信頼されたを設定したことを示してい**ます。** **MobileBroadbandInfo**に記載されている証明書をプロビジョニングします。

プロセスのいずれかの部分が失敗した場合、そのエラーはログに記録されます。 たとえば、デジタル署名の確認がサービスプロバイダーアイコンファイルで失敗した場合、通常、ログエントリは次のようになります。

```syntax
[0]0F24.0C70::‎2012‎-‎01‎-‎04 10:09:49.271 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Parser task started. 
[0]0F24.0C70::‎2012‎-‎01‎-‎04 10:09:49.288 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Parsing metadata for device container with id "{97223B34-36F4-11E1-BC81-00155DE96B01}" for culture "en-US". 
[0]0F24.0C70::‎2012‎-‎01‎-‎04 10:09:49.483 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Starting parse of mobile broadband service information file. 
[0]0F24.0C70::‎2012‎-‎01‎-‎04 10:09:49.483 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Metadata package contains no data for culture "en-US". Using fallback data. 
[0]0F24.0C70::‎2012‎-‎01‎-‎04 10:09:49.547 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Finished parse of mobile broadband service information file. 
[0]0F24.0C70::‎2012‎-‎01‎-‎04 10:09:49.547 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Starting update of stored network account information. 
[0]0F24.0C70::‎2012‎-‎01‎-‎04 10:09:49.688 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Digital signature verification failed for file "c:\programdata\microsoft\windows\devicemetadatacache\dmrccache\en-us\B68264FF-E4D1-49B1-AB5F-2B9C1C16EF5D\ServiceInformation\ContosoBroadband.ico". 
[0]0F24.0C70::‎2012‎-‎01‎-‎04 10:09:49.690 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Finished update of stored network account information. 
[0]0F24.0C70::‎2012‎-‎01‎-‎04 10:09:49.692 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]Parser task finished. 
[0]0F24.0C70::‎2012‎-‎01‎-‎04 10:09:49.692 [Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]MbaeParserTask did not complete successfully.  Error is 0x80070306: One or more errors occurred while processing the request. 
```

パーサータスクが複数回実行される場合は正常であるため、複数の `[Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]` ログエントリが表示されることがあります。 この場合、エントリのセットは通常同じです。同じでない場合は、断続的な問題を示している可能性があります。

## <a name="span-idadditional_resourcesspanspan-idadditional_resourcesspanspan-idadditional_resourcesspanadditional-resources"></a><span id="Additional_resources"></span><span id="additional_resources"></span><span id="ADDITIONAL_RESOURCES"></span>その他のリソース


Windows 8.1 と Windows 10 のモバイルブロードバンドの詳細については、次のリンクを使用してください。

-   [モバイルブロードバンドの概要](overview-of-mobile-broadband.md)

-   [APN データベースの概要](apn-database-overview.md)

-   [サービスメタデータ](service-metadata.md)









