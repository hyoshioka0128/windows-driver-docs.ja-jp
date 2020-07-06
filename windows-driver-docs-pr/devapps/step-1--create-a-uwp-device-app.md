---
title: 手順 1 UWP デバイスアプリを作成する
description: このトピックでは、Microsoft Visual Studio を使用して UWP デバイスアプリを作成するための基本的なプロセスについて説明します。 すべての UWP デバイスアプリに共通のタスクについて説明します。
ms.assetid: 4D8240AD-F589-4623-BC6E-47E304831250
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24c4f753b5f068ad378d6b410d1073749960e817
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968189"
---
# <a name="step-1-create-a-uwp-device-app"></a>手順 1: UWP デバイスアプリを作成する


![デバイスアプリのワークフロー、手順1](images/1-device-app-workflow.png)

このトピックでは、Microsoft Visual Studio を使用して UWP デバイスアプリを作成するための基本的なプロセスについて説明します。 すべての UWP デバイスアプリに共通のタスクについて説明します。

UWP デバイスアプリは、デバイスの製造元が内部または周辺デバイスのコンパニオンとして機能するために作成する特別な種類の UWP アプリです。 デバイスのメタデータを使用することにより、デバイスアプリは、デバイスが接続されているときに、特権操作を実行し、自動的にインストールすることができます。 UWP デバイスアプリの詳細については、「 [uwp デバイスアプリ](meet-uwp-device-apps.md)について」を参照してください。

**メモ**   このトピックは、ステップバイステップシリーズの一部です。 概要については、「 [UWP デバイスアプリのビルド](build-a-uwp-device-app-step-by-step.md)」を参照してください。

 

## <a name="span-idbefore_you_beginspanspan-idbefore_you_beginspanspan-idbefore_you_beginspanbefore-you-begin"></a><span id="Before_you_begin"></span><span id="before_you_begin"></span><span id="BEFORE_YOU_BEGIN"></span>開始する前に


このステップバイステップガイドでは、UWP アプリプロジェクトを作成済みであり、必要なデバイスドライバーが既に存在していることを前提としています。

### <a name="span-idcreating_the_windows_store_app_projectspanspan-idcreating_the_windows_store_app_projectspanspan-idcreating_the_windows_store_app_projectspancreating-the-microsoft-store-app-project"></a><span id="Creating_the_Windows_Store_app_project"></span><span id="creating_the_windows_store_app_project"></span><span id="CREATING_THE_WINDOWS_STORE_APP_PROJECT"></span>Microsoft Store アプリプロジェクトの作成

開始する前に、Visual Studio をインストールし、UWP アプリプロジェクトを作成しておく必要があります。 まだ行っていない場合は、[こちらからツールをダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=302196)できます。 Microsoft Visual Studio の使用を開始するには、「 [Visual Studio を使用した UWP アプリの開発](https://go.microsoft.com/fwlink/p/?LinkID=267230)」を参照してください。

### <a name="span-iddevice_driver_requirementsspanspan-iddevice_driver_requirementsspanspan-iddevice_driver_requirementsspandevice-driver-requirements"></a><span id="Device_driver_requirements"></span><span id="device_driver_requirements"></span><span id="DEVICE_DRIVER_REQUIREMENTS"></span>デバイスドライバーの要件

UWP デバイスアプリと Api によっては、デバイスが Microsoft が提供するドライバーをサポートしていること、またはドライバーが特定のドライバーモデルをサポートしていることが必要です。 次の表に、一部のデバイスアプリと Api のドライバー要件を示します。

| デバイスアプリまたは API                      | ドライバー情報                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| カメラ用 UWP デバイスアプリ   | カメラのドライバーは AvStream ドライバーモデルを使用する必要があります。 AvStream ドライバーモデルの詳細については、Windows Driver Kit の[Avstream の概要](https://go.microsoft.com/fwlink/p/?LinkId=273032)に関するトピックを参照してください。 ドライバーのインストールパッケージには、カメラにカスタム効果を提供するために、ドライバーの MFT (メディアファンデーション変換) と呼ばれる追加のコンポーネントが用意されています。 詳細については、「 [Windows ストアデバイスアプリ (カメラ用](uwp-device-apps-for-webcams.md))」を参照してください。 |
| プリンター用の UWP デバイス アプリ | プリンターでは、v4 プリンタードライバーを使用する必要があります。 詳細については[、「v4 印刷ドライバーの開発](https://go.microsoft.com/fwlink/p/?LinkId=314231)」を参照してください。                                                                                                                                                                                                                                                                                                                                                         |
| USB Api                               | Windows ランタイムの[Windows. Devices. Usb](https://go.microsoft.com/fwlink/p/?LinkId=306694)api を使用するには、デバイスが Winusb.sys ドライバーと互換性がある必要があります。                                                                                                                                                                                                                                                                                                                                      |
| ヒューマンインターフェイスデバイス (HID) Api      | HID Api は、USB、Bluetooth、Bluetooth スマート、および I2C トランスポートを使用するように設計されています。 [HumanInterfaceDevice](https://go.microsoft.com/fwlink/p/?LinkId=306697) api を Windows ランタイム使用するには、デバイスが HIDClass.sys ドライバーおよびトランスポートで必要なドライバーと互換性がある必要があります。 詳細については、「 [HID Architecture](https://docs.microsoft.com/previous-versions/jj126193(v=vs.85))」を参照してください。                                                                                                            |
| Bluetooth GATT Api                    | Bluetooth GATT Api の Windows ランタイムを使用するに[は、デバイス](https://go.microsoft.com/fwlink/p/?LinkId=306698)が BthLEEnum.sys ドライバーと互換性がある必要があります。                                                                                                                                                                                                                                                                                   |
| Bluetooth RFCOMM Api                  | Bluetooth RFCOMM Api Windows ランタイムを使用するに[は、デバイス](https://go.microsoft.com/fwlink/p/?LinkId=306699)に Rfcomm.sys および BthEnum.sys ドライバーとの互換性がある必要があります。                                                                                                                                                                                                                                                                                    |

 

**重要**   カスタムドライバーを使用してデバイスにアクセスするには、Microsoft からの承認が必要です。 カスタムドライバーを使用して特殊なデバイスへのデバイスアクセスを実装する Oem および Ihv は、まず Microsoft の担当者に連絡して、Windows エコシステムチームとのシナリオについて話し合う必要があります。 詳細については、「 [UWP デバイスアプリの設計ガイド](https://go.microsoft.com/fwlink/p/?LinkId=306693)」の「カスタムドライバーアクセスモデル」セクションを参照してください。

 

## <a name="span-idcreate_a_windows_store_accountspanspan-idcreate_a_windows_store_accountspanspan-idcreate_a_windows_store_accountspancreate-a-microsoft-store-account"></a><span id="Create_a_Windows_Store_account"></span><span id="create_a_windows_store_account"></span><span id="CREATE_A_WINDOWS_STORE_ACCOUNT"></span>Microsoft Store アカウントを作成する


Microsoft Store の開発者アカウントが必要です。 後の手順でアプリマニフェストとデバイスメタデータを作成するときに、発行者名が必要になります。 ストアプロファイルを作成したら、アプリの名前を予約することもできます。

Microsoft Store アカウントを作成するには、 [UWP アプリのサインアップページ](https://go.microsoft.com/fwlink/p/?LinkId=302197)にアクセスし、[**今すぐサインアップ**] をクリックします。

**発行元の表示名**を入力するときに、Microsoft Store にアプリを表示する名前を入力します。 アカウントの検証が完了するまで、この名前を変更することはできません。 名前は慎重に選択してください。お客様が参照するときにこの名前が表示され、この名前でアプリを把握できるようになります。

## <a name="span-idassociate_your_app_with_the_windows_storespanspan-idassociate_your_app_with_the_windows_storespanspan-idassociate_your_app_with_the_windows_storespanassociate-your-app-with-the-microsoft-store"></a><span id="Associate_your_app_with_the_Windows_Store"></span><span id="associate_your_app_with_the_windows_store"></span><span id="ASSOCIATE_YOUR_APP_WITH_THE_WINDOWS_STORE"></span>アプリを Microsoft Store に関連付ける


Microsoft Store アカウントを作成し、発行者名を選択したら、アプリを Microsoft Store に関連付けます。 これにより、 **package.appxmanifest**という名前のローカルアプリケーションパッケージマニフェストファイルに次の値が自動的にダウンロードされます。

-   パッケージ表示名

-   パッケージ名

-   パブリッシャー ID

-   発行者の表示名

**メモ**   デバイスメタデータを既に作成してある場合は、アプリを Microsoft Store に関連付けた後、アプリマニフェストの値を使用してデバイスメタデータを更新する必要があります。

 

**アプリを Microsoft Store に関連付けるには**

1.  **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[ストア] [**アプリを &gt; ストアと関連付ける**] の順に選択します。

2.  [**アプリケーションと Microsoft Store の関連付け**] ダイアログボックスで、[**次へ**] をクリックします。 Microsoft Store にサインインするように求められます。

3.  **サインイン**ページで、Microsoft Store にサインインし、[**次へ**] をクリックします。

4.  [**このパッケージのアプリ名を選択**してください] ページで、予約済みの**アプリ名**を選択します。 また、[**名前の予約**] をクリックして、予約する Microsoft Store にアクセスすることもできます。

5.  アプリ名を選択したら、[**次へ**] をクリックします。

6.  [概要] ページで、選択した値を確認します。 問題がなければ、[**関連付け**] をクリックします。 それ以外の場合は、[**前**へ] をクリックして戻り、エラーを修正します。 [**関連付け**] をクリックすると、発行元の表示名とその他の値がアプリパッケージマニフェストに自動的にダウンロードされます。

## <a name="span-idreview_the_app_package_manifestspanspan-idreview_the_app_package_manifestspanspan-idreview_the_app_package_manifestspanreview-the-app-package-manifest"></a><span id="Review_the_app_package_manifest"></span><span id="review_the_app_package_manifest"></span><span id="REVIEW_THE_APP_PACKAGE_MANIFEST"></span>アプリケーションパッケージマニフェストを確認する


アプリを Microsoft Store に関連付けた後、アプリのパッケージマニフェストをレビューして、発行元の表示名とその他の値が正常に挿入されたことを確認します。 アプリのタイトルと名前が、デバイスへの強力な接続を示していることを確認します。 アプリパッケージで許可されるアプリは1つだけであることにも注意してください。

**アプリケーションパッケージマニフェストを確認するには**

1.  **ソリューションエクスプローラー**で、 **package.appxmanifest**ファイルをダブルクリックします。 マニフェストデザイナーが開きます。 マニフェストデザイナーは、基になる XML ファイル用のグラフィカルな UI です。

2.  マニフェストデザイナーでファイルを開いた後、[パッケージ**化**] タブをクリックして、パッケージとパブリッシャーの情報を表示します。

    **メモ**   XML で同じ情報を表示するには、 **package.appxmanifest**を右クリックし、[ **Open With &gt; XML (テキスト) エディター**] を選択します。

     

3.  パッケージ名、発行者名、アプリ ID をメモしておきます。 これらは、次の手順「[手順 2: デバイスメタデータを作成](step-2--create-device-metadata.md)する」で必要になります。

## <a name="span-idchoose_a_publisher_certificatespanspan-idchoose_a_publisher_certificatespanspan-idchoose_a_publisher_certificatespanchoose-a-publisher-certificate"></a><span id="Choose_a_publisher_certificate"></span><span id="choose_a_publisher_certificate"></span><span id="CHOOSE_A_PUBLISHER_CERTIFICATE"></span>発行元証明書の選択


マニフェストデザイナーでアプリケーションパッケージマニフェストを確認している間に、マニフェスト内の**発行者**名と一致する発行元証明書を選択します。 マニフェストデザイナーが開いている状態で、[**パッケージ化**] タブの [**証明書の選択**] をクリックして、適切な証明書を選択します。

## <a name="span-iddevelop_your_windows_store_device_appspanspan-iddevelop_your_windows_store_device_appspanspan-iddevelop_your_windows_store_device_appspandevelop-your-uwp-device-app"></a><span id="Develop_your_Windows_Store_device_app"></span><span id="develop_your_windows_store_device_app"></span><span id="DEVELOP_YOUR_WINDOWS_STORE_DEVICE_APP"></span>UWP デバイスアプリの開発


UWP デバイスアプリの開発を開始するときは、次の点を考慮してください。

### <a name="span-iddevice_capabilitiesspanspan-iddevice_capabilitiesspanspan-iddevice_capabilitiesspandevice-capabilities"></a><span id="Device_capabilities"></span><span id="device_capabilities"></span><span id="DEVICE_CAPABILITIES"></span>デバイスの機能

デバイスにアクセスするには、アプリケーションパッケージマニフェストでデバイス機能を指定する必要がある場合があります。 これらは、アプリのプロジェクトの package.appxmanifest ファイルの[DeviceCapability](https://go.microsoft.com/fwlink/p/?LinkId=306696)要素で指定されます。 デバイスの機能によっては、手動で指定する必要があることに注意してください。 詳細については、「[パッケージマニフェストにデバイス機能を指定する方法](https://go.microsoft.com/fwlink/p/?LinkID=306695)」を参照してください。

### <a name="span-idautoplay_for_windows_store_device_appsspanspan-idautoplay_for_windows_store_device_appsspanspan-idautoplay_for_windows_store_device_appsspanautoplay-for-uwp-device-apps"></a><span id="AutoPlay_for_Windows_Store_device_apps"></span><span id="autoplay_for_windows_store_device_apps"></span><span id="AUTOPLAY_FOR_WINDOWS_STORE_DEVICE_APPS"></span>UWP デバイスアプリの自動再生

自動再生は、デバイスが接続されている場合、既定でアプリを起動します。 この機能を使用するには、アプリケーションパッケージマニフェストとデバイスメタデータを編集する必要があります。 詳細については、「 [UWP デバイスアプリの自動再生](autoplay-for-uwp-device-apps.md)」を参照してください。

### <a name="span-idsync_or_update_your_device_in_the_backgroundspanspan-idsync_or_update_your_device_in_the_backgroundspanspan-idsync_or_update_your_device_in_the_backgroundspansync-or-update-your-device-in-the-background"></a><span id="Sync_or_update_your_device_in_the_background"></span><span id="sync_or_update_your_device_in_the_background"></span><span id="SYNC_OR_UPDATE_YOUR_DEVICE_IN_THE_BACKGROUND"></span>デバイスをバックグラウンドで同期または更新する

デバイスのバックグラウンドタスクを使用して、UWP デバイスアプリからデバイスを同期または更新することができます。 この機能を使用するには、デバイスメタデータでアプリを特権アプリとして指定する必要があります。 詳細については、「[デバイスの同期と UWP デバイスアプリの更新](device-sync-and-update-for-uwp-device-apps.md)」を参照してください。

### <a name="span-idlearn_morespanspan-idlearn_morespanspan-idlearn_morespanlearn-more"></a><span id="Learn_more"></span><span id="learn_more"></span><span id="LEARN_MORE"></span>詳細情報

**[プリンターの UWP デバイスアプリ](uwp-device-apps-for-printers.md)**: プリンターの状態を表示し、印刷設定のエクスペリエンスを拡張します。 Windows 8.1 以降では、アプリで印刷ジョブを管理したり、プリンターのメンテナンスを実行したりすることもできます。

カメラ**[用 UWP デバイスアプリ](uwp-device-apps-for-webcams.md)**: カメラのオプションエクスペリエンスを拡張します。 アプリでは、ドライバー MFT でカスタム効果を提供することもできます。

**[デバイスの統合](https://go.microsoft.com/fwlink/p/?LinkId=533279)**: USB、HID、Bluetooth、スキャンなどの Windows ランタイム api について説明します。

**[内部デバイス用の UWP デバイスアプリ](uwp-device-apps-for-specialized-devices.md)**: OEM が PC 内部のデバイス用にデバイスアプリを作成する方法を説明します。


 

## <a name="span-iduse_the_windows_app_certification_kitspanspan-iduse_the_windows_app_certification_kitspanspan-iduse_the_windows_app_certification_kitspanuse-the-windows-app-certification-kit"></a><span id="Use_the_Windows_App_Certification_Kit"></span><span id="use_the_windows_app_certification_kit"></span><span id="USE_THE_WINDOWS_APP_CERTIFICATION_KIT"></span>Windows アプリ認定キットを使用する


アプリが認定を受ける可能性を最大限に高めるために、お客様のコンピューターで証明書を検証してテストしてから、Microsoft Store の認定と登録を申請してください。 詳細については、「 [Windows アプリ認定キット](https://go.microsoft.com/fwlink/p/?LinkId=273040)」を参照してください。

## <a name="span-idnext_stepspanspan-idnext_stepspanspan-idnext_stepspannext-step"></a><span id="Next_step"></span><span id="next_step"></span><span id="NEXT_STEP"></span>次のステップ


[手順 2: デバイスメタデータを作成する](step-2--create-device-metadata.md)

 

 





