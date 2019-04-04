---
title: 手順 1 UWP デバイスのアプリを作成します。
description: このトピックでは、Microsoft Visual Studio を使用して、UWP デバイス アプリを作成するための基本的なプロセスについて説明します。 すべての UWP デバイス アプリに共通するタスクについて説明します。
ms.assetid: 4D8240AD-F589-4623-BC6E-47E304831250
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19bb9f718ff864ff2987950f9e4808bf7eda3416
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539677"
---
# <a name="step-1-create-a-uwp-device-app"></a>手順 1:UWP デバイス アプリを作成します。


![デバイス アプリのワークフロー、手順 1](images/1-device-app-workflow.png)

このトピックでは、Microsoft Visual Studio を使用して、UWP デバイス アプリを作成するための基本的なプロセスについて説明します。 すべての UWP デバイス アプリに共通するタスクについて説明します。

UWP デバイスのアプリは、内部や周辺機器デバイスに対応するとして機能するデバイスの製造元が作成した UWP アプリの特別な種類です。 デバイス メタデータを使用すると、デバイス アプリは、特権操作を実行して、デバイスが接続されているときに自動的にインストールします。 UWP デバイスのアプリに関する詳細については、[満たす UWP デバイス アプリ](meet-uwp-device-apps.md)を参照してください。

**注**  このトピックはステップ バイ ステップの一連の一部です。 参照してください[ステップ バイ ステップの UWP デバイスのアプリをビルド](build-a-uwp-device-app-step-by-step.md)導入します。

 

## <a name="span-idbeforeyoubeginspanspan-idbeforeyoubeginspanspan-idbeforeyoubeginspanbefore-you-begin"></a><span id="Before_you_begin"></span><span id="before_you_begin"></span><span id="BEFORE_YOU_BEGIN"></span>開始する前に


このステップ バイ ステップ ガイドでは、UWP アプリ プロジェクトを作成したことと、必要なデバイス ドライバーが既に存在している前提としています。

### <a name="span-idcreatingthewindowsstoreappprojectspanspan-idcreatingthewindowsstoreappprojectspanspan-idcreatingthewindowsstoreappprojectspancreating-the-microsoft-store-app-project"></a><span id="Creating_the_Windows_Store_app_project"></span><span id="creating_the_windows_store_app_project"></span><span id="CREATING_THE_WINDOWS_STORE_APP_PROJECT"></span>Microsoft Store アプリ プロジェクトを作成します。

を開始する前に、Visual Studio をインストールしても、UWP アプリ プロジェクトを作成する必要があります。 場合は、まだを完了していない、[ここでツールをダウンロードする](https://go.microsoft.com/fwlink/p/?LinkId=302196)します。 Microsoft Visual Studio で開始するを参照してください。[開発の UWP アプリの Visual Studio を使用して](https://go.microsoft.com/fwlink/p/?LinkID=267230)します。

### <a name="span-iddevicedriverrequirementsspanspan-iddevicedriverrequirementsspanspan-iddevicedriverrequirementsspandevice-driver-requirements"></a><span id="Device_driver_requirements"></span><span id="device_driver_requirements"></span><span id="DEVICE_DRIVER_REQUIREMENTS"></span>デバイス ドライバーの要件

一部の UWP デバイス アプリと Api は、デバイスが Microsoft 提供のドライバーをサポートしているか、ドライバーが特定のドライバー モデルをサポートしている必要があります。 このテーブルは、一部のデバイス アプリと Api のドライバーの要件を一覧表示します。

| デバイスのアプリまたは API                      | ドライバー情報                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| カメラ用の UWP デバイス アプリ   | カメラのドライバーは AvStream ドライバー モデルを使用する必要があります。 AvStream ドライバー モデルの詳細については、、 [AVStream の概要](https://go.microsoft.com/fwlink/p/?LinkId=273032)、Windows Driver Kit でを参照してください。 A カメラのカスタム効果を提供するドライバーのインストール パッケージで、Driver MFT (media foundation 変換) と呼ばれる追加のコンポーネントを指定することができます。 詳細については、[Windows ストアのカメラ用のデバイス アプリ](uwp-device-apps-for-webcams.md)を参照してください。 |
| プリンター用の UWP デバイス アプリ | プリンター、v4 プリンター ドライバーを使用する必要があります。 参照してください[v4 印刷ドライバーの開発](https://go.microsoft.com/fwlink/p/?LinkId=314231)の詳細。                                                                                                                                                                                                                                                                                                                                                         |
| USB Api                               | Windows ランタイムを使用する[Windows.Devices.Usb](https://go.microsoft.com/fwlink/p/?LinkId=306694)Api では、デバイスは Winusb.sys ドライバーとの互換性である必要があります。                                                                                                                                                                                                                                                                                                                                      |
| ヒューマン インターフェイス デバイス (HID) Api      | HID Api は USB、Bluetooth、Bluetooth Smart、および I2C トランスポート経由で使用するために設計されています。 Windows ランタイムを使用する[Windows.Devices.HumanInterfaceDevice](https://go.microsoft.com/fwlink/p/?LinkId=306697) Api では、デバイスは HIDClass.sys ドライバーとトランスポートによって必要なドライバーと互換性のあるである必要があります。 詳細については、[HID アーキテクチャ](https://msdn.microsoft.com/library/windows/hardware/jj126193)を参照してください。                                                                                                            |
| Bluetooth GATT Api                    | Windows ランタイムの Bluetooth GATT Api を使用する[Windows.Devices.Bluetooth.GenericAttributeProfile](https://go.microsoft.com/fwlink/p/?LinkId=306698)デバイスを BthLEEnum.sys ドライバーとの互換性にする必要があります。                                                                                                                                                                                                                                                                                   |
| Bluetooth RFCOMM Api                  | Windows ランタイムの Bluetooth RFCOMM Api を使用する[Windows.Devices.Bluetooth.Rfcomm](https://go.microsoft.com/fwlink/p/?LinkId=306699)デバイスは、Rfcomm.sys と BthEnum.sys ドライバーと互換性のあるである必要があります。                                                                                                                                                                                                                                                                                    |

 

**重要な**  カスタム ドライバーを使用してデバイスのアクセスには、Microsoft からの承認が必要です。 Oem および Ihv がカスタム ドライバーを使用して特殊化されたデバイスのデバイスへのアクセスを実装する必要があります最初にお問い合わせください Microsoft の担当者には、Windows エコシステム チームとそのシナリオについて説明します。 詳細については、カスタム ドライバー アクセス モデル」セクションを参照してください、[特殊なデバイス、PC の内部の UWP デバイス アプリ設計ガイド](https://go.microsoft.com/fwlink/p/?LinkId=306693)します。

 

## <a name="span-idcreateawindowsstoreaccountspanspan-idcreateawindowsstoreaccountspanspan-idcreateawindowsstoreaccountspancreate-a-microsoft-store-account"></a><span id="Create_a_Windows_Store_account"></span><span id="create_a_windows_store_account"></span><span id="CREATE_A_WINDOWS_STORE_ACCOUNT"></span>Microsoft Store アカウントを作成します。


Microsoft Store での開発者アカウントが必要です。 アプリケーション マニフェストと後の手順でデバイスのメタデータを作成するときに、発行元名が必要があります。 ストアのプロファイルを作成したら、アプリの名前を予約することもできます。

Microsoft Store アカウントを作成するには、 [UWP アプリのサインアップ ページ](https://go.microsoft.com/fwlink/p/?LinkId=302197)クリック**今すぐサインアップ**します。

入力したときに、**発行者表示名**、するは、Microsoft Store でアプリが表示されるはずの名前を入力します。 アカウントの確認が完了するまで、この名前を変更することはできません。 参照と、この名前で、アプリを把握する場合は、この名前が表示されます、名前を慎重に選択します。

## <a name="span-idassociateyourappwiththewindowsstorespanspan-idassociateyourappwiththewindowsstorespanspan-idassociateyourappwiththewindowsstorespanassociate-your-app-with-the-microsoft-store"></a><span id="Associate_your_app_with_the_Windows_Store"></span><span id="associate_your_app_with_the_windows_store"></span><span id="ASSOCIATE_YOUR_APP_WITH_THE_WINDOWS_STORE"></span>Microsoft Store アプリを関連付ける


Microsoft Store アカウントを作成し、発行元の名前を選択したら、後にアプリを Microsoft Store に関連付けます。 これは自動的にダウンロード、次の値、ローカル アプリ パッケージ マニフェスト ファイルを名前付き**Package.appxmanifest**します。

-   パッケージ表示名

-   パッケージ名

-   発行者 ID

-   発行者表示名

**注**  場合は、アプリを Microsoft Store に関連付けた後は、デバイス メタデータ、既に開発して、アプリ マニフェストから値を持つデバイスのメタデータを更新する必要があります。

 

**Microsoft Store にアプリを関連付ける**

1.  **ソリューション エクスプ ローラー**プロジェクトを右クリックし、**ストア&gt;アプリケーションをストアと関連付ける**します。

2.  **アプリケーションを Microsoft Store と関連付ける**ダイアログ ボックスで、をクリックして**次**します。 Microsoft Store にサインインするメッセージが表示されます。

3.  **サインイン** ページで、Microsoft Store にサインインしてクリックして**次へ**します。

4.  **アプリ名をこのパッケージを選択します。** ページで、選択、**アプリ名**予約済み。 クリックすることもできます**予約名**を予約する 1 つの Microsoft Store に移動します。

5.  アプリ名を選択すると、クリックして**次**します。

6.  [概要] ページで、選択した値を確認します。 問題がなければ、クリックして**関連付ける**します。 それ以外の場合、をクリックして**前**をクリックして戻り、エラーを修正します。 クリックすると**関連付ける**発行者表示名、およびその他の値をアプリ パッケージのマニフェストに自動的にダウンロードします。

## <a name="span-idreviewtheapppackagemanifestspanspan-idreviewtheapppackagemanifestspanspan-idreviewtheapppackagemanifestspanreview-the-app-package-manifest"></a><span id="Review_the_app_package_manifest"></span><span id="review_the_app_package_manifest"></span><span id="REVIEW_THE_APP_PACKAGE_MANIFEST"></span>アプリ パッケージのマニフェストを確認してください。


Microsoft Store からアプリを関連付ける後は、アプリのパッケージ マニフェストを発行者表示名、およびその他の値には、期待どおりが挿入されていたことを確認します。 アプリのタイトルと名前で、デバイスへの接続を強力な示されていることを確認します。 アプリ パッケージにその 1 つだけのアプリが許可されているにも注意してください。

**アプリ パッケージのマニフェストを確認するには**

1.  **ソリューション エクスプ ローラー**、ダブルクリックして、 **package.appxmanifest**ファイル。 マニフェスト デザイナーが開きます。 マニフェスト デザイナーは、基になる XML ファイルのグラフィカル UI です。

2.  マニフェスト デザイナーで、ファイルが開いたら、 をクリックして、**パッケージ** タブに、パッケージとパブリッシャーの情報を参照してください。

    **注**   XML で同じ情報を表示する右クリック**package.appxmanifest**選択**プログラムから開く&gt;XML (テキスト) エディター**。

     

3.  メモのパッケージ名、発行者名、アプリの id。 次の手順では、必要があります[手順 2。デバイス メタデータを作成する](step-2--create-device-metadata.md)します。

## <a name="span-idchooseapublishercertificatespanspan-idchooseapublishercertificatespanspan-idchooseapublishercertificatespanchoose-a-publisher-certificate"></a><span id="Choose_a_publisher_certificate"></span><span id="choose_a_publisher_certificate"></span><span id="CHOOSE_A_PUBLISHER_CERTIFICATE"></span>発行者の証明書を選択します。


マニフェスト デザイナーを使用したアプリのパッケージ マニフェストをレビューすることは、選択に一致する発行者の証明書、**パブリッシャー**マニフェスト内の名前。 マニフェスト デザイナーがで開いている間、**パッケージ**] タブで [**証明書の選択**を適切な証明書を選択します。

## <a name="span-iddevelopyourwindowsstoredeviceappspanspan-iddevelopyourwindowsstoredeviceappspanspan-iddevelopyourwindowsstoredeviceappspandevelop-your-uwp-device-app"></a><span id="Develop_your_Windows_Store_device_app"></span><span id="develop_your_windows_store_device_app"></span><span id="DEVELOP_YOUR_WINDOWS_STORE_DEVICE_APP"></span>UWP デバイス アプリを開発します。


UWP デバイス アプリの開発を開始すると、次の点を検討してください。

### <a name="span-iddevicecapabilitiesspanspan-iddevicecapabilitiesspanspan-iddevicecapabilitiesspandevice-capabilities"></a><span id="Device_capabilities"></span><span id="device_capabilities"></span><span id="DEVICE_CAPABILITIES"></span>デバイスの機能

デバイスにアクセスするには、アプリのパッケージ マニフェストでデバイスの機能を指定する必要があります。 指定されて、 [DeviceCapability](https://go.microsoft.com/fwlink/p/?LinkId=306696)アプリのプロジェクトの Package.appxmanifest ファイルの要素。 いくつかのデバイス機能を手動で指定する必要がありますに注意してください。 詳細については、[パッケージ マニフェストでデバイスの機能を指定する方法](https://go.microsoft.com/fwlink/p/?LinkID=306695)を参照してください。

### <a name="span-idautoplayforwindowsstoredeviceappsspanspan-idautoplayforwindowsstoredeviceappsspanspan-idautoplayforwindowsstoredeviceappsspanautoplay-for-uwp-device-apps"></a><span id="AutoPlay_for_Windows_Store_device_apps"></span><span id="autoplay_for_windows_store_device_apps"></span><span id="AUTOPLAY_FOR_WINDOWS_STORE_DEVICE_APPS"></span>UWP デバイス アプリの自動再生

自動再生デバイスが接続されているときに、既定では、アプリを開始します。 この機能を使用するには、アプリのパッケージ マニフェストとデバイスのメタデータを編集する必要があります。 詳細については、[UWP デバイス アプリの自動再生](autoplay-for-uwp-device-apps.md)を参照してください。

### <a name="span-idsyncorupdateyourdeviceinthebackgroundspanspan-idsyncorupdateyourdeviceinthebackgroundspanspan-idsyncorupdateyourdeviceinthebackgroundspansync-or-update-your-device-in-the-background"></a><span id="Sync_or_update_your_device_in_the_background"></span><span id="sync_or_update_your_device_in_the_background"></span><span id="SYNC_OR_UPDATE_YOUR_DEVICE_IN_THE_BACKGROUND"></span>同期またはバック グラウンドでデバイスを更新します。

同期または、デバイスのバック グラウンド タスクを使用して UWP デバイス アプリからデバイスを更新することができます。 この機能を使用するには、デバイスのメタデータでの特権を持つアプリとしてアプリを指定する必要があります。 詳細については、[デバイスとの同期と UWP デバイス アプリ用の更新プログラム](device-sync-and-update-for-uwp-device-apps.md)を参照してください。

### <a name="span-idlearnmorespanspan-idlearnmorespanspan-idlearnmorespanlearn-more"></a><span id="Learn_more"></span><span id="learn_more"></span><span id="LEARN_MORE"></span>詳細情報

|                                                                                                         |                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [プリンター用の UWP デバイス アプリ](uwp-device-apps-for-printers.md)                    | プリンターのステータスを表示し、印刷設定のエクスペリエンスを拡張します。 Windows 8.1 以降、アプリも印刷ジョブを管理できプリンターのメンテナンスを実施できます。 |
| [カメラ用の UWP デバイス アプリ](uwp-device-apps-for-webcams.md)                      | オプションのカメラ エクスペリエンスを拡張します。 アプリでは、Driver MFT を使用したカスタムの効果も提供できます。                                                              |
| [デバイスの統合](https://go.microsoft.com/fwlink/p/?LinkId=533279)                                  | USB、HID、Bluetooth、スキャン、および複数の Windows ランタイム Api について説明します。                                                                                  |
| [内部デバイス用の UWP デバイス アプリ](uwp-device-apps-for-specialized-devices.md) | リーン Oem が PC に内部デバイスのデバイスのアプリを作成する方法。                                                                                            |

 

## <a name="span-idusethewindowsappcertificationkitspanspan-idusethewindowsappcertificationkitspanspan-idusethewindowsappcertificationkitspanuse-the-windows-app-certification-kit"></a><span id="Use_the_Windows_App_Certification_Kit"></span><span id="use_the_windows_app_certification_kit"></span><span id="USE_THE_WINDOWS_APP_CERTIFICATION_KIT"></span>Windows アプリ認定キットを使用します。


アプリの認定資格を取得やすければを得られるように、検証し、認定および Microsoft Store への掲載のために送信する前に、コンピューターにテストします。 詳細については、[Windows アプリ認定キット](https://go.microsoft.com/fwlink/p/?LinkId=273040)を参照してください。

## <a name="span-idnextstepspanspan-idnextstepspanspan-idnextstepspannext-step"></a><span id="Next_step"></span><span id="next_step"></span><span id="NEXT_STEP"></span>次の手順


[手順 2:デバイス メタデータを作成します。](step-2--create-device-metadata.md)

 

 





