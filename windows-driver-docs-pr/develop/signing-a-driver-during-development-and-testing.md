---
ms.assetid: 1EBE8D0C-5F27-4FBE-8B0C-8AAD40F6FBC6
title: 開発中とテスト中のドライバーへの署名
description: 64 ビット版 Windows にインストールできるのは、署名されたドライバー パッケージだけです。  テスト目的の場合は、ドライバー パッケージにテスト署名できます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aac999925a9775473b10b7358646e28b27dcb1c9
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "67364232"
---
# <a name="signing-a-driver-during-development-and-testing"></a>開発中とテスト中のドライバーへの署名

64 ビット バージョンの Windows を実行しているコンピューターにドライバーをインストールする前に、ドライバー パッケージに署名する必要があります。 テスト用に、一般リリース用の署名よりも緩やかな形式でドライバー パッケージにテスト署名することができます。

Microsoft Visual Studio では、テスト署名は既定で有効になっています。 「[テンプレートを使った KMDF ドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/writing-a-kmdf-driver-based-on-a-template)」の説明に従って、KMDF ドライバー ソリューションを作成したとします。 ソリューションをビルドすると、ドライバー パッケージにテスト署名されたことが **[出力]** ウィンドウに表示されます。

![[出力] ウィンドウのスクリーン ショット](images/SigningADriver01.png)

## <a name="span-idenabling_test_signing_manuallyspanspan-idenabling_test_signing_manuallyspanenabling-test-signing-manually"></a><span id="enabling_test_signing_manually"></span><span id="ENABLING_TEST_SIGNING_MANUALLY"></span>手動でのテスト署名の有効化


テスト署名を手動で有効にするには、次の手順を実行します。

1.  Visual Studio で、ドライバー パッケージ プロジェクトのあるソリューションを開きます。 ドライバー パッケージ プロジェクトを右クリックし、 **[プロパティ]** をクリックします。

2.  パッケージのプロパティ ページで、 **[Configuation Properties (構成プロパティ)] &gt; [Driver Signing (ドライバーの署名)] &gt; [全般]** の順に移動します。 **[Sign Mode (署名モード)]** ドロップダウン リストで、 **[Test Sign (テスト署名)]** をクリックします。

3.  パッケージのプロパティ ページで、 **[Configuation Properties (構成プロパティ)] &gt; [Inf2Cat] &gt; [全般]** の順に移動します。 **[Run Inf2Cat (Inf2Cat の実行)]** ドロップダウン リストで、 **[はい]** を選びます。

## <a name="span-idviewing_the_signed_driver_packagespanspan-idviewing_the_signed_driver_packagespanspan-idviewing_the_signed_driver_packagespanviewing-the-signed-driver-package"></a><span id="Viewing_the_signed_driver_package"></span><span id="viewing_the_signed_driver_package"></span><span id="VIEWING_THE_SIGNED_DRIVER_PACKAGE"></span>署名されたドライバー パッケージの表示


ソリューションをビルドした後、エクスプローラーで、ドライバー パッケージを含むフォルダーに移動します。 パッケージ内のファイルの 1 つはカタログ ファイルです。 カタログ ファイルには、パッケージのデジタル署名が含まれています。 署名されたパッケージ内のファイルを表示する例については、「[テンプレートを使った KMDF ドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/writing-a-kmdf-driver-based-on-a-template)」をご覧ください。

## <a name="span-idsharing_a_signing_certificatespanspan-idsharing_a_signing_certificatespanspan-idsharing_a_signing_certificatespansharing-a-signing-certificate"></a><span id="Sharing_a_signing_certificate"></span><span id="sharing_a_signing_certificate"></span><span id="SHARING_A_SIGNING_CERTIFICATE"></span>署名証明書の共有


ドライバー パッケージにテスト署名すると、Visual Studio は署名証明書 (PFX ファイル) を作成し、ホスト コンピューター上の署名ストアにインポートします。 テスト署名されたドライバー パッケージをテスト コンピューターに展開すると、Visual Studio は検証証明書 (CER ファイル) をテスト コンピューターにコピーします。 他のホスト コンピューター上でドライバーをビルドしている開発者と証明書を共有する場合は、検証証明書ではなく、署名証明書を共有する必要があります。

署名証明書を共有するには、次の手順を実行します。

-   Visual Studio の [ソリューション エクスプローラー] ウィンドウで、ドライバー パッケージ プロジェクトを右クリックして、 **[プロパティ]** をクリックします。
-   パッケージのプロパティ ページで、 **[Configuation Properties (構成プロパティ)] &gt; [Driver Signing (ドライバーの署名)] &gt; [全般]** の順に移動します。 **[Test Certificate (テスト証明書)]** フィールドで、 **[ストアから選択]** を選びます。

-   [証明書の選択] ダイアログ ボックスで、テスト署名証明書を探します。 証明書の名前は "WDKTestCert <*ユーザー名*>" のようになります。 テスト署名証明書を選択して、 **[プロパティ]** をクリックします。 **[詳細]** タブで、 **[ファイルへコピー]** をクリックします。
-   証明書のエクスポート ウィザードの指示に従って、PFX ファイルをエクスポートします。 秘密キーをエクスポートするかどうかを確認するメッセージが表示されたら、 **[はい、秘密キーをエクスポートします]** をクリックします。
-   エクスポートされた PFX ファイルを他の開発者と共有します。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [初めてのドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/writing-your-first-driver)
* [ドライバーのビルド](building-a-driver.md)
* [ドライバーの開発、テスト、および展開](index.md)
 

 






