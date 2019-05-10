---
title: サービス メタデータの作成に関する開発者向けガイド
description: サービス メタデータの作成に関する開発者向けガイド
ms.assetid: 2d250bce-2dd2-4bd8-aa0f-432dde7783e1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09df5432075549f14093fbeda9005d5faab7f774
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405171"
---
# <a name="developer-guide-for-creating-service-metadata"></a>サービス メタデータの作成に関する開発者向けガイド

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]


このガイドは Sysdev と呼ばれる以前、Windows デベロッパー センター ハードウェア ダッシュ ボードのサービス メタデータ パッケージを作成するプロセスを説明します (<http://sysdev.microsoft.com>)。 ハードウェア デバイスにモバイル ブロード バンドのアプリを接続するには、サービス メタデータが必要です。 ユーザーには、自分のコンピューターにモバイル ブロード バンド デバイスが接続されるためと関連付けられているサービスのメタデータをダウンロードするモバイル ブロード バンドのアプリを自動的にダウンロードし。

Windows と緊密に統合されたエクスペリエンスを作成するサービス メタデータを活用することができます。 サービス メタデータ パッケージのブランド アイコンなどの情報と、オペレーター名を含める、設定と SIM ハードウェアと個人用のホット スポットにアクセスするためのアクセス許可を構成することを許可して、モバイル ブロード バンドを使用するモバイル ブロード バンドのアプリのプロビジョニングデバイスです。

**注:**  
モバイル ブロード バンド アプリが自動的にインストールされているにもかかわらず、ユーザー必要がありますにピン留め Start 画面で、手動でします。



## <a name="span-idgettingstartedspanspan-idgettingstartedspanspan-idgettingstartedspangetting-started"></a><span id="Getting_started"></span><span id="getting_started"></span><span id="GETTING_STARTED"></span>作業の開始


正常にサービス メタデータ パッケージを作成するには、このセクションでは含まれている手順を行う必要があります。

### <a name="span-idregisteryourcompanywiththewindowsdevcenterhardwaredashboardspanspan-idregisteryourcompanywiththewindowsdevcenterhardwaredashboardspanspan-idregisteryourcompanywiththewindowsdevcenterhardwaredashboardspanregister-your-company-with-the-windows-dev-center-hardware-dashboard"></a><span id="Register_your_company_with_the_Windows_Dev_Center_hardware_dashboard"></span><span id="register_your_company_with_the_windows_dev_center_hardware_dashboard"></span><span id="REGISTER_YOUR_COMPANY_WITH_THE_WINDOWS_DEV_CENTER_HARDWARE_DASHBOARD"></span>Windows デベロッパー センター ハードウェア ダッシュ ボードで、会社を登録します。

-   会社では、Windows デベロッパー センター ハードウェア ダッシュ ボードで、アクティブなアカウントを持ちます。 会社が、Windows デベロッパー センター ハードウェア ダッシュ ボード上にアカウントを持たない場合は、新しいアカウントを作成し、あなたの会社にユーザー アカウントを追加します。 詳細については、次を参照してください。[管理](https://msdn.microsoft.com/library/windows/hardware/mt786447)、Windows デベロッパー センター ハードウェア ダッシュ ボードのヘルプ。

-   会社では、署名、パッケージの署名に証明書 VeriSign コードがあります。

### <a name="span-idservicemetadatawizardaccessandserviceidentifiersregistrationspanspan-idservicemetadatawizardaccessandserviceidentifiersregistrationspanspan-idservicemetadatawizardaccessandserviceidentifiersregistrationspanservice-metadata-wizard-access-and-service-identifiers-registration"></a><span id="Service_Metadata_wizard_access_and_service_identifiers_registration"></span><span id="service_metadata_wizard_access_and_service_identifiers_registration"></span><span id="SERVICE_METADATA_WIZARD_ACCESS_AND_SERVICE_IDENTIFIERS_REGISTRATION"></span>サービス メタデータ ウィザードへのアクセスとサービスの識別子の登録

MNOs と MVNOs は、サービス メタデータ パッケージを作成する前に、次の手順を完了する必要があります。

-   サービス メタデータのウィザードへのアクセスを要求します。

-   登録、サービスの id

上記の手順を完了するには電子メールを送信する必要がありますsysdev@microsoft.com次の情報を使用します。

-   Windows デベロッパー センター ハードウェア ダッシュ ボードに登録したときに使用される組織名。

-   かどうか、モバイル ネットワーク オペレーターまたはモバイルの仮想ネットワークの演算子であります。

-   Web サイトおよび理由でサービス メタデータ パッケージを作成する必要がある理由。

該当する場合は、次のサービス識別子が含まれます。

-   GSM プロバイダー Id の一覧

-   GSM プロバイダー名の一覧

-   CDMA Sid の一覧

-   CDMA プロバイダー名の一覧

要求を受信した 24 時間で、受信確認の電子メールを受信する必要があります。 ただし、要求を処理する最大 5 営業日かかる可能性があります。 競合がある場合お知らせする追加情報を求める電子メール。

### <a name="span-idmobilebroadbandappspanspan-idmobilebroadbandappspanspan-idmobilebroadbandappspanmobile-broadband-app"></a><span id="Mobile_broadband_app"></span><span id="mobile_broadband_app"></span><span id="MOBILE_BROADBAND_APP"></span>モバイル ブロード バンド アプリ

サービス メタデータ パッケージを作成する前に、モバイル ブロード バンド アプリが開発されているし、Microsoft Store に関連付けられていることを確認します。 このアプリは、プランを購入、データの使用状況、ヘルプとサポートに加え、演算子からの付加価値サービスを強調表示などのキーのエクスペリエンスを提供する必要があります。 モバイル ブロード バンドのアプリを作成する方法の詳細については、次のリンクを参照してください。

-   [モバイル ブロード バンド WinRT API の概要](mobile-broadband-winrt-api-overview.md)

-   [通信事業者ハードウェアの概要](mobile-operator-hardware-overview.md)

-   [UWP のモバイル ブロード バンド アプリ](uwp-mobile-broadband-apps.md)

**注:**  
サービス メタデータはテストが完了し、外部で発行する準備が整うまで、Microsoft Store に発行するモバイル ブロード バンド アプリはありません。 サービス メタデータ パッケージは、プレビュー モードのテストを経過した後にのみ、アプリが Microsoft Store に公開されていることをお勧めします。



## <a name="span-idcreatingservicemetadatapackagesspanspan-idcreatingservicemetadatapackagesspanspan-idcreatingservicemetadatapackagesspancreating-service-metadata-packages"></a><span id="Creating_service_metadata_packages"></span><span id="creating_service_metadata_packages"></span><span id="CREATING_SERVICE_METADATA_PACKAGES"></span>サービス メタデータ パッケージの作成


サービス メタデータ パッケージの作成は、Windows デベロッパー センター ハードウェア ダッシュ ボードで利用可能なサービスのメタデータのウィザードを開始します。 サービス メタデータのウィザードの詳細については、次を参照してください。[手順 2 - サービス メタデータ パッケージを作成する](#2-create-the-service-metadata-package)します。 新規作成または既存のサービス メタデータ パッケージを編集するサービス メタデータのウィザードを使用することができます。 ウィザードの値を入力すると、ウィザードが検証し、エラーまたは警告を通知します。 この検証には、フィールドが見つからないか正しくない、サービスの識別子の所有権、Microsoft Store でモバイル ブロード バンド アプリが存在することの確認が含まれています。

パッケージを送信するかのオプションがある最後の確認 ページと送信の準備完了したらで**開発者**モードまたは**プレビュー**モード。

-   **開発者モード**の目的は、単にサービス メタデータ パッケージを作成し、オフライン テスト目的で使用するときに、初期の段階で使用します。 このモードでは、パッケージが署名されていないと、手動でダウンロードし、検証のためのテスト コンピューターにインストールする必要があります。 このモードは、作成し、サービス メタデータ パッケージを確認する迅速かつ迅速な方法が、デバイスで動作するように表示できます。

-   **プレビュー モード**パッケージが正しく作成し、エンド ツー エンド テストを送信する準備が確信できる場合に使用します。 このモードで、パッケージは、Windows デベロッパー センター ハードウェア ダッシュ ボードで署名して、マシンのテストが自動的にダウンロードを取得、テスト マシンが正常にプロビジョニングが提供されています。

場合テスト、プレビューを完了し、パッケージがすべてのシナリオで動作し、ライブにパッケージを発行することを確認します。

次の図では、ワークフローについて説明します。

![サービス メタデータ パッケージを作成します。](images/mbae-sxs81-createpackageworkflow.png)

新しいサービス メタデータ パッケージを作成するを参照してください。[サービス メタデータ パッケージを作成するための手順](#steps-for-creating-a-service-metadata-package)します。

既存のサービス メタデータ パッケージを編集するを参照してください。[サービス メタデータ パッケージを編集するための手順](#steps-for-editing-a-service-metadata-package)します。

## <a name="steps-for-creating-a-service-metadata-package"></a>サービス メタデータ パッケージを作成するための手順


Windows デベロッパー センター ハードウェア ダッシュ ボードにサービス メタデータ パッケージを作成するのにには、次の手順を使用します。

-   [サービス メタデータ パッケージの必要な情報を 1/ギャザー](#1-gather-the-required-information-for-the-service-metadata-package)

-   [2-サービス メタデータ パッケージの作成](#2-create-the-service-metadata-package)

-   [Microsoft Store のデバイスのアプリへの挿入の 3 ストア マニフェスト ファイル](#3-insert-the-store-manifest-file-into-the-microsoft-store-device-app)

-   [サービス メタデータ パッケージのテスト-4](#4-test-the-service-metadata-package)

-   [5-サービス メタデータ パッケージの発行](#5-publish-the-service-metadata-package)

### <a name="1-gather-the-required-information-for-the-service-metadata-package"></a>サービス メタデータ パッケージの必要な情報を 1/ギャザー

このトピックの手順 2. でサービス メタデータのウィザードの手順を進めるときは、いくつかのデバイスに関連付けられているモバイル ブロード バンド アプリ プロジェクトの package.appxmanifest ファイルに格納されている情報が必要です。 このトピックの手順 2 の準備ができるように情報を収集するのにには、次の手順を使用します。

**注意**  
この手順で値を収集する前に、モバイル ブロード バンド アプリが Microsoft Store を関連付ける必要があります。 モバイル ブロード バンドのアプリを関連付けると、パッケージ マニフェスト ファイル内の値は、Microsoft Store の開発者アカウントから情報を使用して更新されます。 ただし、モバイル ブロード バンド アプリは Microsoft Store に発行する必要はありません。 サービス メタデータ パッケージを発行する準備ができるまで、ローカル開発環境で維持できます。



**UWP デバイス アプリの情報を収集するには**

1.  Visual Studio 2013 を使用して、モバイル ブロード バンド アプリ プロジェクトを開きます。

2.  右側のウィンドウで右クリックし、 **Package.appxmanifest**ファイルを開き、をクリックし、**コードの表示**します。

3.  Package.appxmanifest ファイルから、次の属性を収集します。

    -   **Identity**要素、**名前**属性に使用される、**パッケージ名**サービス メタデータのウィザードのフィールド。

    -   **Identity**要素、**パブリッシャー**属性に使用される、**パブリッシャー**サービス メタデータのウィザードのフィールド。

    -   **アプリケーション**要素、 **Id**属性を**アプリケーション**子要素に使用される、**アプリ ID**フィールドで、サービス メタデータのウィザード。

4.  Package.appxmanifest ファイルを閉じます。

![コード ビューで、package.appxmanifest ファイル](images/mbae-sxs-appxmanifest.png)

次の手順を実行して Visual Studio 2013 を使用することがなくこれを実行できます。

**Visual Studio 2013 を使用せずにモバイル ブロード バンド アプリ情報を収集するには**

1.  モバイル ブロード バンド アプリの package.appxmanifest ファイルに移動します。

2.  ファイルを右クリックし、をクリックし、**プログラムから開く**します。

3.  クリア、**このアプリを使用して、すべての .appxmanifest ファイル** チェック ボックスをクリックします**より多くのオプション**、順にクリックします**メモ帳**します。

4.  Package.appxmanifest ファイルから、次の属性を収集します。

    -   **Identity**要素、**名前**属性に使用される、**パッケージ名**サービス メタデータのウィザードのフィールド。

    -   **Identity**要素、**パブリッシャー**属性に使用される、**パブリッシャー**サービス メタデータのウィザードのフィールド。

    -   **アプリケーション**要素、 **Id**属性を**アプリケーション**子要素に使用される、**アプリ ID**フィールドで、サービス メタデータのウィザード。

5.  保存して、package.appxmanifest ファイルを閉じます。

### <a name="2-create-the-service-metadata-package"></a>2-サービス メタデータ パッケージの作成

サービス メタデータは、Windows デベロッパー センター ハードウェア ダッシュ ボードで、サービス メタデータのウィザードを使用して作成されます。

**サービス メタデータ パッケージを作成するには**

1.  <http://sysdev.microsoft.com> に移動します。

2.  下、**デバイス メタデータ**クリックして**モバイル ブロード バンド エクスペリエンスを作成**です。

    ![これは、ダッシュ ボードのランディング ページです。](images/mbae-sxs81-dashboard.png)

3.  **サービスの情報** ページで次のフィールドに入力してをクリックし、**次**します。

    -   **Windows ネットワークの選択 UI で使用されるネットワークの名前を入力**– ネットワークの名前をお客様には、Windows 接続マネージャーに表示されます。

    -   **サービス番号を入力する**– GUID、プロビジョニングのメタデータ内の通信事業者の ID フィールドに一致する必要があります。 Visual Studio 2013 を使用して GUID を作成することができます。 GUID を作成する方法の詳細については、次を参照してください。 [GUID の作成 (guidgen.exe)](https://go.microsoft.com/fwlink/p/?linkid=330070)します。

    -   **Windows ネットワークの選択 UI に表示されるアイコンのアップロード**– クリックして**参照**、し Windows 接続マネージャーでのお客様に表示されるアイコンを選択します。

    -   **Windows 通知のイベント ハンドラーを入力します (以下の権利チェックが必要な場合を除き、省略可能) アプリで**– これは、モバイル ブロード バンド アプリで登録された通知ハンドラー。

    -   **ユーザーのモバイル ブロード バンド接続 (個人用ホット スポット) を共有できますか。** 有効なオプションは**常に許可する**、**権利チェック (Windows notification イベント ハンドラーに必要な) でのみ許可する**、および**を決して許可**します。 既定のオプションでは、常に許可します。

    -   **システムを必要とする Sim に暗証番号 (pin) を実行するには、管理者権限がロックを解除しますか?** – SIM カードのロックを解除暗証番号 (pin) をシステム管理者特権を必要とする場合は、をクリックして、**はい**オプション。

    ![ウィザードの サービス情報手順](images/mbae-sxs81-serviceinfostep.png)

4.  **ハードウェア情報** ページで、お客様のエクスペリエンスを識別するために使用する情報を選択します。 チェック ボックスを選択すると、適切なネットワークの範囲を追加できます。 生成された ID は、適切なサブスクライバーが識別されるように、Windows APN データベースに存在する必要があります。 APN データベースの詳細については、次を参照してください。 [COSA/APN データベース送信](cosa-apn-database-submission.md)します。

    -   GSM プロバイダー、International Mobile IMSI (Subscriber Identity) を使用する場合は、選択、 **IMSI**下のチェック ボックス、 **GSM**見出し。 **プロバイダー ID**ボックスに、GSM サービス プロバイダーの ID を入力します。 下、 **IMSI/ICCID 範囲**、範囲を入力し、クリックして、見出し**追加**します。

    -   GSM プロバイダー integrated 回線カード識別子 (ICCID) を使用する場合は、選択、 **SIM ICC ID**下のチェック ボックス、 **GSM**見出し。 下、**プロバイダーの ID と ICC の ID 範囲を入力**、範囲を入力し、クリックして、見出し**追加**します。

    -   GSM プロバイダー ホーム プロバイダー名を使用する場合は、選択、**ホーム プロバイダー名**下のチェック ボックス、 **GSM**見出し。 下、**ホーム プロバイダー名を入力するか、プロバイダー ID (MCC + mnc も) を入力して**見出しで、プロバイダーの ID とプロバイダーの名前を入力し、順にクリックします**追加**します。

    -   SID を使用する CDMA プロバイダーの場合は、選択、 **SID**下のチェック ボックス、 **CDMA**見出し。 **SID を入力**ボックスに、CDMA SID を入力します。

    -   プロバイダー名を使用する CDMA プロバイダーの場合は、選択、**プロバイダー名**下のチェック ボックス、 **CDMA**見出し。 **プロバイダー名の入力**ボックス CDMA サービス プロバイダーの名前を入力します。

    -   **[次へ]** をクリックします。

    ![これは、ウィザードのハードウェア情報 手順です。](images/mbae-sxs81-hardwareinfostep.png)

5.  **App info**  ページで、このトピックの手順 1 で収集した情報を入力します。 追加の特権を持つアプリを追加する場合は、クリックして**追加**、し、最大 7 以上を入力します。 すべての特権を持つアプリを入力すると、クリックして**次**します。

    ![これは、ウィザードのアプリ情報 手順です。](images/mbae-sxs81-appinfostep.png)

6.  **確認** ページで、情報が正しいことを確認します。 選択、**開発者モード**または**プレビュー モード**オプションをクリックして**送信**します。

    -   **開発者モード**パッケージが署名されていません: しする必要があります手動でダウンロードして各コンピューターにインストールします。 このオプションは、オフライン開発用にパッケージを保存する場合に使います。

    -   **プレビュー モード**– パッケージに署名し、自動的に構成されている適切なレジストリ設定をテスト コンピューターに Microsoft からダウンロードします。 プレビュー モードは、モバイル ブロード バンド アプリが Microsoft Store に公開されていることを確認するのにはチェックされません。

    ![これは、ウィザードの確認手順です。](images/mbae-sxs81-confirm.png)

### <a name="3-insert-the-store-manifest-file-into-the-microsoft-store-device-app"></a>Microsoft Store のデバイスのアプリへの挿入の 3 ストア マニフェスト ファイル

ストア マニフェスト ファイルは、UWP デバイスのアプリに含める必要があります。 サービス メタデータ パッケージ ストア マニフェスト ファイルをダウンロードして、モバイル ブロード バンド アプリ プロジェクトに挿入するには、次の手順を使用します。

**ストア マニフェスト ファイルを挿入します。**

1.  サービス メタデータ パッケージのエクスペリエンスの管理 ページで、Windows デベロッパー センター ハードウェア ダッシュ ボードで、サービス メタデータ パッケージをクリックし、クリックして**StoreManifest.xml**ストア マニフェスト ファイルをダウンロードします。

    ![ストア マニフェスト ファイルをダウンロードします。](images/mbae-sxs81-storemanifest.png)

2.  Visual Studio 2013 を使用して、モバイル ブロード バンド アプリ プロジェクトを開きます。

3.  プロジェクトを右クリックし、をクリックして**追加**、 をクリックし、**既存項目の**します。

4.  ダウンロードしたストア マニフェスト ファイルを参照してクリックして**追加**します。

5.  モバイル ブロード バンドのアプリを再コンパイルし、もう一度 Microsoft Store に発行します。

### <a name="4-test-the-service-metadata-package"></a>サービス メタデータ パッケージのテスト-4

サービス メタデータ パッケージをテストするには、モバイル ブロード バンド デバイスとサービス メタデータ パッケージのファイルが必要です。 テスト システムを構成し、サービス メタデータ パッケージをインストールする手順は、パッケージのモードによって異なります。

### <a name="span-idtestaservicemetadatapackageindevelopermodespanspan-idtestaservicemetadatapackageindevelopermodespanspan-idtestaservicemetadatapackageindevelopermodespantest-a-service-metadata-package-in-developer-mode"></a><span id="Test_a_service_metadata_package_in_developer_mode"></span><span id="test_a_service_metadata_package_in_developer_mode"></span><span id="TEST_A_SERVICE_METADATA_PACKAGE_IN_DEVELOPER_MODE"></span>開発者モードでのサービス メタデータ パッケージをテストします。

手動でパッケージをダウンロードし、正常に動作するシナリオの正しい場所にインストールする必要があります。 開発者モード パッケージは、新しいパッケージまたは既存のパッケージを作成するかどうかに応じて 2 つの異なるエントリ ポイントからアクセスする必要があります。

Windows デベロッパー センター ハードウェア ダッシュ ボードで、新しいパッケージを作成した場合はクリックして**管理エクスペリエンス**、順にクリックします**Dev パッケージが関連付けられていない**(の最初のエントリ、**管理エクスペリエンス**テーブル)。 次の図は、例を示します。

![サービス メタデータ パッケージをダウンロードします。](images/mbae-sxs81-managedevpackages.png)

エクスペリエンスに関連付けられている既存のサービス メタデータ パッケージを編集した場合のエクスペリエンスを選択、**管理エクスペリエンス**して、テーブルで開発者モード パッケージが表示されます、**メタデータパッケージ**テーブル。 クリックして**ダウンロード MBAE Zip パッケージを編集**をダウンロードします。

![サービス メタデータ パッケージをダウンロードします。](images/mbae-sxs81-manageassociatedpackages.png)

サービス メタデータ パッケージをダウンロードした後は、サービス メタデータ パッケージは署名されていないため、テスト署名を有効する必要があります。 テスト署名を有効にする**bcdedit を実行 – testsigning を設定**管理者特権でコマンド プロンプトから、コンピューターを再起動します。

テスト署名を有効にすると、コピー、 \*.devicemetadata ms が次の場所にサービス メタデータ パッケージからファイル: **%programdata%\\Microsoft\\Windows\\DeviceMetadataStore\\** <em>カルチャ</em>ここで、*カルチャ*は、コンピューターの現在のカルチャ コード。

### <a name="span-idtestaservicemetadatapackageinpreviewmodespanspan-idtestaservicemetadatapackageinpreviewmodespanspan-idtestaservicemetadatapackageinpreviewmodespantest-a-service-metadata-package-in-preview-mode"></a><span id="Test_a_service_metadata_package_in_preview_mode"></span><span id="test_a_service_metadata_package_in_preview_mode"></span><span id="TEST_A_SERVICE_METADATA_PACKAGE_IN_PREVIEW_MODE"></span>プレビュー モードでのサービス メタデータ パッケージをテストします。

サービス メタデータ パッケージは、プレビュー モードでは場合、は、テスト コンピューターに PreviewKey レジストリ エントリを作成する必要があります。 PreviewKey のレジストリ エントリを構成する方法の詳細については、次を参照してください。[プレビュー パッケージを作成する](https://msdn.microsoft.com/library/windows/hardware/br230780)します。

**注:**  
テスト プレビュー モードでは、サービス メタデータ パッケージをテストする署名を有効にすることはありません。



PreviewKey のレジストリ エントリが作成されると、モバイル ブロード バンド デバイスに接続し、ネットワーク一覧に表示されることを確認します。 そうでない場合は、次を参照してください。、[トラブルシューティング](#troubleshooting)詳細セクション。

### <a name="span-idcleartheexistingservicemetadataspanspan-idcleartheexistingservicemetadataspanspan-idcleartheexistingservicemetadataspanclear-the-existing-service-metadata"></a><span id="Clear_the_existing_service_metadata"></span><span id="clear_the_existing_service_metadata"></span><span id="CLEAR_THE_EXISTING_SERVICE_METADATA"></span>既存のサービス メタデータをクリアします。

サービス メタデータは、PC にインストールするときに、メタデータに含まれる値は、レジストリ、メタデータのキャッシュ、メタデータ ストア、WWAN プロファイル開発ノードなど、さまざまな場所に格納されます。 これは、ために、同じまたは異なるメタデータ パッケージを使用した複数のテストを繰り返します。 サービス メタデータが正しくインストールされていることを確認するには、既存のサービス メタデータをクリアする必要があります。 既存のサービス メタデータをクリアするには、すべてのトレースを削除する PowerShell スクリプトを実行するテスト コンピューターのセットアップします。 最初に、テスト コンピューターに、環境を設定する必要があります。

**注:**  
これは、Windows RT デバイスでは機能しません。 Windows RT を実行しているデバイス上のサービス メタデータをクリア"するには"という名前のプロシージャでの手順を使用します。



**サービス メタデータをクリアするための環境をセットアップするには**

1.  Psexec.exe をダウンロード (<https://go.microsoft.com/fwlink/p/?linkid=330071>)、し、そのフォルダーに抽出します。

2.  ダウンロードして Windows ドライバー キット Windows 8.1 のインストール (<https://go.microsoft.com/fwlink/?LinkId=330072>)。

3.  WDK ファイルのインストール場所に移動します。 既定の場所は**c:\\Program Files (x86)\\Windows キット\\8.1\\ツール**します。 テスト用コンピューターで x86 が実行されている場合は、x86 から devcon.exe をコピー psexec.exe と同じフォルダーにフォルダー。 テスト用コンピューターで x64 が実行されている場合は、x64 から devcon.exe をコピー フォルダー。

4.  Devcon.exe と PsExec.exe と同じフォルダーに MetadataRemovalScript.ps1 としては、次のスクリプトを保存します。

    **注:**  
    **型として保存**ボックスに、選択することを確認**すべてのファイル (\*.\*)** ファイルを保存する前にします。




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


環境を設定した後は、既存のサービス メタデータをオフにするたびに、次の手順を実行します。

**サービス メタデータをクリアするには**

1.  モバイル ブロード バンド デバイスが、テスト コンピューターに接続されていることを確認します。

2.  管理者特権でコマンド プロンプトで、psexec.exe、抽出したフォルダーに移動および実行し、 **psexec/s/i powershell**

3.  PowerShell コマンド プロンプトで、psexec.exe を抽出したフォルダーに移動します。

4.  型**set-executionpolicy unrestricted**し、Enter キーを押します。

5.  型**Y**しを入力します。

6.  型 **.\\MetadataRemovalScript.ps1**し、Enter キーを押します。

7.  メッセージが表示されたら、モバイル ブロード バンド デバイスを削除し、Enter キーを押します。

8.  テスト用コンピューターから、サービス メタデータをクリアするたびに次の手順を繰り返します。

**Windows RT を実行しているデバイス上のサービス メタデータをクリア**

1. ソフトウェア デバイス ノードを削除します。

   1.  デバイス マネージャーで、**ビュー**、 をクリックし、**非表示のデバイスを表示する**します。

   2.  デバイスのソフトウェアを展開します。

   3.  以下のデバイス ノードを右クリックし、をクリックし、**アンインストール**:**Windows.Devices.Sms.SmsDevice**と**Windows.Networking/NetworkOperators.MobileBroadbandAccount**

2. すべてのインターフェイスからすべてのモバイル ブロード バンド プロファイルを削除します。

   1. 管理者特権でコマンド プロンプトで、次のように入力します**netsh mbn 表示 pro i =。\\***

   2. プロファイルのそれぞれについて、次のように入力します。 **netsh mbn 削除プロファイル名 ="、ここにプロファイル名"は =\\*** し、Enter キーを押します。

3. すべてのモバイル ブロード バンド アダプターを無効にします。

   1.  デバイス マネージャーで、展開**ネットワーク アダプター**します。

   2.  各モバイル ブロード バンド デバイスを右クリックし、をクリックし、**を無効にする**します。

4. 管理者特権でコマンド プロンプトで、」と入力して、DSM のサービスを停止**sc stop dsmsvc**し、Enter キーを押します。

5. サービス メタデータ パッケージを含む任意のフォルダーを削除することによって、デバイスのメタデータ ストアから、サービス メタデータ パッケージを削除 **%programdata%\\Microsoft\\Windows\\DeviceMetadataStore**. MobileBroadbandInfo.xml ファイルを探すことによって、サービス メタデータ パッケージを識別できます。

6. WWAN SVC MBAE のすべてのレジストリ エントリを削除します。

   1.  レジストリ エディターでは、次のレジストリ エントリとすべての子エントリを削除します。HKEY\_ローカル\_マシン\\ソフトウェア\\Microsoft\\WwanSvc\\MobileBroadbandAccounts します。

   2.  レジストリ エントリを削除へのアクセスを持っていない場合はフル コントロール アクセス許可を付与自分でする必要があります。

7. すべてのモバイル ブロード バンド アダプターを有効にします。

   1.  デバイス マネージャーで、展開**ネットワーク アダプター**します。

   2.  各モバイル ブロード バンド デバイスを右クリックし、をクリックし、**を有効にする**します。

### <a name="5-publish-the-service-metadata-package"></a>5-サービス メタデータ パッケージの発行

サービス メタデータ パッケージが正しく動作することを確認できたら後の最後の手順は、パッケージをリリースするがします。 クリックして、特定のエクスペリエンスにアタッチされているパッケージを選択して、パッケージをリリースすることができます、**リリース** ボタン、次のようです。

![サービス メタデータ パッケージをリリースします。](images/mbae-sxs81-releasetolive.jpg)

## <a name="steps-for-editing-a-service-metadata-package"></a>サービス メタデータ パッケージを編集するための手順


サービス メタデータ パッケージを編集するには、Windows デベロッパー センター ハードウェア ダッシュ ボードのエクスペリエンスの管理ページを使用します。

![エクスペリエンスの管理 ページ](images/mbae-sxs81-manageexperience.png)

## <a name="troubleshooting"></a>トラブルシューティング


ネットワークの一覧を開き、モバイル ブロード バンド ネットワークを確認します。 サービス メタデータ パッケージで使用したアイコンと名前を使用して、ネットワークが表示されている場合**ServiceInfo.xml**ファイル、パッケージが正しく解析します。 同じ名前とアイコンを持っている、サービス メタデータ パッケージを更新する場合、または名前またはアイコンが約 1 分の詳細については、後のリストに表示されていない場合は、ここで説明したように、追加の手順を実行する必要があります。

-   メタデータ更新を強制します。

-   メタデータ キャッシュを確認してください。

-   レジストリを確認してください。

-   WWAN ログを確認してください。

### <a name="span-idforcemdrefspanspan-idforcemdrefspanforce-a-metadata-refresh"></a><span id="forcemdref"></span><span id="FORCEMDREF"></span>メタデータ更新を強制します。

メタデータとシステムのモバイル ブロード バンドのアプリの一部は失敗し、一貫性のない状態でコンピューターを残すことができるネットワーク アクセスに依存します。 この場合、サービス メタデータがインストールされていない、またはモバイル ブロード バンド アプリがインストールされていないが発生することができます。 システムは、定期的に電源を節約するためには、問題を解決するには、再試行はかなり頻繁に (数回だけ 1 日)。 次の再試行を待機しているのではなく、更新をすぐに実行を手動で適用できます。 これを行うには、次の手順を実行します。

1.  デスクトップを開く**コントロール パネルの **します。

2.  開いている**デバイスとプリンター**します。

3.  **ビュー**  メニューのをクリックして**更新**、キーを押すか、 **F5**キー。 この操作によって、メタデータを再解析され、バック グラウンド イベントを再登録します。

**重要**  
サービス メタデータ パッケージは既に正常に解析、システムは、メタデータの更新プログラムとしてこの更新を扱います。 この場合、メタデータ パッケージとがありますのファイル名に異なる GUID の更新のタイムスタンプ、 [LastModifiedDate](lastmodifieddate.md)要素の**PackageInfo.xml**します。



### <a name="span-idcheckmdcachespanspan-idcheckmdcachespancheck-the-metadata-cache"></a><span id="checkmdcache"></span><span id="CHECKMDCACHE"></span>メタデータ キャッシュを確認してください。

メタデータの更新では、問題が解決しないが、サービス メタデータ パッケージが有効であると、正しいハードウェア Id があることを確認します。 これを行うには、次の手順を実行します。

1. 移動します **%programdata%\\Microsoft\\Windows\\DeviceMetadataCache\\dmrccache\\**<em>カルチャ</em>ここで、 *カルチャ*はテスト用コンピューターの現在のカルチャのカルチャ コード (たとえば、 **en-ご**または **、es-es**)。

2. メタデータ パッケージと同じ名前を持つフォルダーを探します (なし、 **.devicemetadata ms**拡張機能)。 このディレクトリが存在しない場合、次の 4 つのいずれかに意味があります。

   -   サービス メタデータ パッケージが壊れています。

   -   サービス メタデータ パッケージには、正しいハードウェア Id がありません。

   -   モバイル ブロード バンド デバイスは、メタデータをダウンロードできる、またはサービス メタデータ パッケージをコピーする前に、デバイスに接続した状態でないです。

   -   メタデータ パッケージのデジタル署名を確認するときに問題が発生しました。 これは通常、テスト署名をテスト コンピューターに有効でないことにより発生します。

パッケージが壊れていないことと、最初に接続したモバイル ブロード バンド デバイス サービス メタデータ パッケージをコピーした後を確認する場合は、IMSI 範囲を確認します。 入力が多すぎるか少なすぎます 0 または 9 で非常に簡単になります。 確認するか、これらの項目を修正した後、問題が解決しない場合は、レジストリを確認する必要があります。

### <a name="span-idcheckregspanspan-idcheckregspancheck-the-registry"></a><span id="checkreg"></span><span id="CHECKREG"></span>レジストリを確認してください。

**警告**  
絶対に必要である場合を除き、アプリケーションに属していないレジストリ データは編集しないでください。 レジストリにエラーがある場合、システムが正しく機能しない可能性があります。 削除しないでください、どのような状況下で、 **MobileBroadbandAccounts**レジストリ キー。 Windows は再作成しないと、機能が中断されます。



レジストリを確認するには、次の手順に従います。

1.  レジストリ エディターを開きます。

2.  移動して**HKLM\\ソフトウェア\\Microsoft\\WwanSvc\\MobileBroadbandAccounts**します。

3.  このレジストリ キー内の他の 3 つのキーを探します。**アカウント**、 **NetworkInterfaceBindings**、および**データ**します。 既定では、これらのキーが存在しません。初めてモバイル ブロード バンド デバイスが挿入されたか、有効で、または、接続されていることに自動的に作成されます。

4.  場合、**アカウント**または**NetworkInterfaceBindings**キーが存在しないと、電源に接続されて既にまたは WWAN ログを確認して、モバイル ブロード バンドのアダプターでは、有効にします。

5.  これらのキーの一部またはすべてが存在する場合は、展開、**アカウント**キー、**ツリー**ビュー。 Guid のような名前を持つ 1 つまたは複数のレジストリ キーは、その内に存在する必要があります。 レジストリ ツリー エントリはレジストリ ツリーの下に表示されるようになります。

    ![解析されたアカウントのレジストリ エントリ](images/fig2-registryentries-for-parsedmobilebroadbandaccount.png)

    (値の名前は若干によって異なるかどうか、アカウントが GSM または CDMA ネットワーク) 上の図のような場合は、レジストリ キー、およびネットワークの一覧のアイコンが表示されない場合、イベント ログを見てください。

    モバイル ブロード バンド アダプターが、デバイスのメタデータ ストアにサービス メタデータ パッケージのコピー、サービス メタデータ パッケージが破損している場合、またはハードウェア Id が正しくない前に挿入されたことになります、レジストリ エントリが次の図のような場合は、. 電源接続時またはデバイス メタデータ パッケージのメタデータ ストアにコピーする前に有効にした位置の状況を解決するには、メタデータの更新で、手順を実行します。 それ以外の場合、チェック WWAN ログ」の手順に従ってください。

    ![未解析のアカウントのレジストリ エントリ](images/fig1-registryentries-for-unparsedmobilebroadbandaccount.png)

### <a name="span-idcheckwwanlogsspanspan-idcheckwwanlogsspancheck-the-wwan-logs"></a><span id="checkwwanlogs"></span><span id="CHECKWWANLOGS"></span>WWAN ログを確認してください。

ある場合ありません**アカウント**または**NetworkInterfaceBindings**下のレジストリ キー **HKLM\\ソフトウェア\\Microsoft\\WwanSvc\\MobileBroadbandAccounts**、または完全に作成されていないエントリがある場合は、WWAN ログを参照する必要があります。 次の手順では、コンピューターを既知の状態にリセットします。

1.  取り外す、または、モバイル ブロード バンド デバイスを無効に (デバイスが埋め込まれている場合は無効で、**デバイス マネージャー**)。

2.  次のレジストリ キーを削除します。

    -   **HKLM\\SOFTWARE\\Microsoft\\WwanSvc\\MobileBroadbandAccounts\\Accounts**

    -   **HKLM\\SOFTWARE\\Microsoft\\WwanSvc\\MobileBroadbandAccounts\\NetworkInterfaceBindings**

    **警告**  
    削除しないでください、どのような状況下で、 **HKLM\\ソフトウェア\\Microsoft\\WwanSvc\\MobileBroadbandAccounts\\** レジストリ キー。 Windows は再作成しないと、機能が中断されます。



ログに関心のあるエントリの 2 種類があります。 アカウント管理 WWAN サービス エントリのログ エントリ、および作業項目のパーサー。 最初の型は、ネットワークのハードウェアの問題によって引き起こされる問題をデバッグでき、2 番目の型は、メタデータの解析に関する問題をデバッグできます。

管理 WWAN サービス エントリのログ エントリが正常に処理されるネットワーク アカウントは、次に似ています。

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

ログでこれらのエントリを検索できます**アカウント管理**します。 最も重要なエントリは、この場合、**データ ストアの作成/更新開始**と**データ ストアの作成/更新が完了**します。 これらのエントリは、存在され、エラー メッセージがない、ハードウェアが正しく動作します。 (ここで説明されているレジストリ キーを格納する参照されるデータ ストアは、レジストリをチェックします)。

これに対し、SIM の削除、デバイス、エントリ通常になります次のように。

```syntax
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Account updater started for network interface {7a0a0dce-0a51-471a-8c16-6e767cd0b861}. 
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Detected removal of SIM from device bound to network interface {7A0A0DCE-0A51-471A-8C16-6E767CD0B861}. 
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Devnode create/update started. 
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Devnode create/update finished. 
[0]02CC.03E4::‎2012‎-‎01‎-‎04 09:29:50.309 [Microsoft-Windows-WWAN-SVC-EVENTS]Account Management: Account updater finished for network interface {7a0a0dce-0a51-471a-8c16-6e767cd0b861}. 
```

**注:**  
後者の例でのエントリがない**データ ストアの作成/更新開始**または**データ ストアの作成/更新が完了**します。 SIM に格納された情報は、アカウント管理プロセスに不可欠であるため、SIM がないデバイスには、必要な関連付けられているメタデータはありません。



ハードウェアが正常に処理されたネットワーク一覧で、ロゴまたは名前が表示されない場合は、メタデータ パッケージの問題である可能性があります。 これは、ログ パーサーの作業項目を使用して、調査することができます。 これらのエントリを検索する検索**パーサー タスク**します。 正常に解析のログ エントリは、通常、次のようになります。

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

これらのログを表示する、 **MobileBroadbandInfo.xml**ファイルが正しく解析された、(と共に、WWAN サービスのログ プロファイルが正常に更新する)、WWAN プロファイルとするパーサーのタスクを適用するパーサーのタスク説明されている、信頼できるプロビジョニング証明書を設定**MobileBroadbandInfo.xml**します。

プロセスの一部が失敗した場合は、そのエラーが記録されます。 たとえば、サービス プロバイダーのアイコン ファイルのデジタル署名のチェックが失敗すると、ログ エントリは通常、次のようになります。

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

1 つ以上のセットを参照してくださいが通常パーサーのタスクを 1 つ以上の時間を実行するため、`[Microsoft-Windows-Mobile-Broadband-Experience-Parser-Task]`ログ エントリ。 この場合、エントリのセットは、通常と同じ - 一時的な問題を示している可能性が同じでない場合。

## <a name="span-idadditionalresourcesspanspan-idadditionalresourcesspanspan-idadditionalresourcesspanadditional-resources"></a><span id="Additional_resources"></span><span id="additional_resources"></span><span id="ADDITIONAL_RESOURCES"></span>その他のリソース


Windows 8.1 および Windows 10 におけるモバイル ブロード バンドの詳細については、次のリンクを使用します。

-   [モバイル ブロード バンドの概要](overview-of-mobile-broadband.md)

-   [APN データベースの概要](apn-database-overview.md)

-   [サービス メタデータ](service-metadata.md)









