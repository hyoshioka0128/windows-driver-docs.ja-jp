---
title: UWP デバイス アプリの自動インストール
description: このトピックでは、自動インストールのしくみとアプリ、メタデータ、およびドライバーの更新およびアンインストール方法について説明します。
ms.assetid: ED9C7A63-5D2A-45D3-AD62-32C6876142FC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 332a9277cad1f60cd142b226f3e302e6f17db89a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387954"
---
# <a name="automatic-installation-for-uwp-device-apps"></a>UWP デバイス アプリの自動インストール


Windows 8.1、デバイスの製造元は、ユーザーが PC に自分のデバイスを接続するときに自動的にインストールする UWP デバイス アプリを構成できます。 このトピックでは、自動インストールのしくみとアプリ、メタデータ、およびドライバーの更新およびアンインストール方法について説明します。 デバイスのアプリに関する詳細については、次を参照してください。[満たす UWP デバイス アプリ](meet-uwp-device-apps.md)します。

**注**  自動インストール機能が提供しないことを通知をユーザーにアプリがインストールされている場合を考慮することが重要です。 一部のユーザーは、混乱とフラストレーション、このエクスペリエンスを検索し、アプリに不適切な評価を可能性があります。

 

デバイス アプリのパッケージの詳細を指定すると、自動インストールが有効になっている、 **UWP デバイス アプリ**の部分、 **App Info**のページ、 **デバイスメタデータの作成ウィザード**. 詳細については、次を参照してください。[手順 2。デバイス メタデータを作成する](step-2--create-device-metadata.md)します。

## <a name="span-idacquisitionoverviewspanspan-idacquisitionoverviewspanspan-idacquisitionoverviewspanacquisition-overview"></a><span id="Acquisition_overview"></span><span id="acquisition_overview"></span><span id="ACQUISITION_OVERVIEW"></span>購入の概要


UWP デバイスのアプリは、3 つの方法のいずれかで、ユーザーから入手できます。

-   **自動インストール**:アプリは自動的に取得し、周辺機器が、PC に接続されている最初にインストールされています。 これは、UWP デバイスのアプリがインストールされている最も一般的な方法です。
-   **手動インストール**:ユーザーは、Microsoft Store でアプリを検索し、そこからインストールされます。 通常はアプリの更新プログラムおよびその他の UWP アプリをインストールする方法です。
-   **OEM プレインストール**:PC 内部デバイスまたはシステム コンポーネント用のアプリは、新しい PC の一部として OEM からプレインストールできます。 詳細については、次を参照してください。[プレインストール アプリを使用して DISM](https://go.microsoft.com/fwlink/p/?LinkId=325524)します。

**注**  PC 内部デバイス用の UWP デバイス アプリは自動インストールの資格がありません。 手動でインストールして OEM のみ取得をプレインストールします。

 

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


自動インストールが機能するためには、ユーザーにする必要があります。

-   オプトイン、**推奨設定**Windows のインストール時にします。

-   Microsoft Store にサインインします。

-   オンラインであります。

これにより、Windows メタデータ、アプリ、および (必要な) 場合、ドライバーを自動的に取得できます。 インターネット接続が使用できない場合、自動インストールは、インターネットにアクセスできる場合、後で実行されます。

## <a name="span-idhowautomaticinstallationworksspanspan-idhowautomaticinstallationworksspanspan-idhowautomaticinstallationworksspanhow-automatic-installation-works"></a><span id="How_automatic_installation_works"></span><span id="how_automatic_installation_works"></span><span id="HOW_AUTOMATIC_INSTALLATION_WORKS"></span>自動インストールの動作


![自動インストールの 4 つの手順: デバイスの接続、デバイス メタデータのダウンロード、該当するデバイス ドライバーのダウンロード、アプリのダウンロード](images/autoinstallbehindscenes.png)

自動インストールに 4 つの段階があります。

1.  **デバイスが接続されている**:Windows が Windows メタデータとインターネット サービス (WMIS) からデバイス メタデータを要求するときに、デバイスが接続されているか、PC とペアリングと必要に応じて、Windows Update からのデバイス ドライバー。

2.  **デバイス メタデータをダウンロードする**:Windows では、WMIS からデバイス メタデータをダウンロードし、デバイスに関連付けられているアプリを識別するために解析します。 これにより、アプリのダウンロードがトリガーされます。

3.  **デバイス ドライバーがダウンロードされる**:ドライバーが必要な場合、Windows は Windows Update からダウンロードし、それらを自動的にインストールします。

4.  **デバイス アプリがインストールされている**:Windows をアプリをダウンロードしてインストールして、**すべてのアプリ**現在ログイン ユーザーの画面。

次の手順のいずれかの中にエラーがある場合、ユーザーにエラー メッセージが表示されます、**デバイス**のページ、**設定**アプリ。

### <a name="span-idifthereisnointernetconnectionspanspan-idifthereisnointernetconnectionspanspan-idifthereisnointernetconnectionspanif-there-is-no-internet-connection"></a><span id="If_there_is_no_Internet_connection"></span><span id="if_there_is_no_internet_connection"></span><span id="IF_THERE_IS_NO_INTERNET_CONNECTION"></span>インターネット接続がない場合

PC がインターネットに接続されていないまたは従量制課金接続では、Windows は自動インストールを実行する待機します。 次回、PC が無制限のインターネット接続では、Windows は自動的に再試行します。 インストールは、ユーザーを妨げることがなく、バック グラウンドでサイレント モードで実行されます。

### <a name="span-idiftheuserisnotloggedintothewindowsstorespanspan-idiftheuserisnotloggedintothewindowsstorespanspan-idiftheuserisnotloggedintothewindowsstorespanif-the-user-is-not-logged-into-the-microsoft-store"></a><span id="If_the_user_is_not_logged_into_the_Windows_Store"></span><span id="if_the_user_is_not_logged_into_the_windows_store"></span><span id="IF_THE_USER_IS_NOT_LOGGED_INTO_THE_WINDOWS_STORE"></span>ユーザーが Microsoft Store にログインしていない場合

ユーザーの Microsoft アカウントで Microsoft Store にログインしていない、Windows 自動インストールを実行する待機します。 次回ユーザーがログイン Microsoft アカウントでは、Microsoft Store Windows は自動的に再試行します。 インストールは、ユーザーを妨げることがなく、バック グラウンドでサイレント モードで実行されます。

## <a name="span-idupdatingdevicedriversspanspan-idupdatingdevicedriversspanspan-idupdatingdevicedriversspanupdating-device-drivers"></a><span id="Updating_device_drivers"></span><span id="updating_device_drivers"></span><span id="UPDATING_DEVICE_DRIVERS"></span>デバイス ドライバーの更新


ドライバーの更新プログラムは、ユーザーが Windows Update から更新プログラムの受信をオプトインする限り、オプションの更新プログラムとして Windows Update を通じて配布されます。 ドライバーの更新プログラムはない場合は、ユーザーがデバイスのセットアップが完了し、既にメタデータとドライバーがインストールされて、デバイスに自動的に配布します。

ドライバーの更新プログラムの設計と既存のアプリケーションの互換性を確保するためにアプリの更新プログラム、ドライバーの更新プログラムは結合されます。 ドライバーの更新が、Windows の更新を配布する場合、または、ユーザーが手動で再インストールまたはドライバーを更新する場合、アプリする必要がありますこれを適切に処理します。 アプリは、カスタム ドライバーを使用している場合は、互換性と機能のコントラクトを維持することを確認してあります。 詳細については、次を参照してください。[内部デバイス用の UWP デバイス アプリ](uwp-device-apps-for-specialized-devices.md)します。

## <a name="span-idupdatingdevicemetadataspanspan-idupdatingdevicemetadataspanspan-idupdatingdevicemetadataspanupdating-device-metadata"></a><span id="Updating_device_metadata"></span><span id="updating_device_metadata"></span><span id="UPDATING_DEVICE_METADATA"></span>デバイス メタデータを更新します。


新規または別の UWP デバイス アプリを指す WMIS によって配布されているメタデータを更新できます。 更新されたメタデータは、新しいアプリの送信後に約 8 から 15 日接続および最初に設定する新しいデバイスに新しいアプリが表示されます。 ただし、更新されたメタデータに示されている新しいアプリは Pc をデバイスのセットアップが既に完了すると、ユーザーがデバイスのデバイス メタデータを以前に受信するために自動的に配布されていません。

デバイスの最初にセットアップのときに 1 回だけ、UWP デバイス アプリは自動的にダウンロードされます。 別のアプリをポイントするデバイスのメタデータが更新されると、できるように、ユーザーが取得できる、Microsoft Store から手動で、古いアプリは、ユーザーに新しいものをアドバタイズする必要があります。 最終的には、Microsoft Store から古いアプリを削除する必要があります。 移動して、ユーザーは、新しいアプリにアクセスもできます、**デバイス**ページで、**設定**アプリとクリックすると、 **Get アプリ**デバイスにリンクします。

**特別な注意を追加するための特権アクセス**:UWP デバイス アプリの権限 (アクセスする前に存在しない) 場合、デバイスへのアクセスを付与すると、新しいメタデータがある場合は、アプリを送信する前に、少なくとも 20 日をメタデータに送信します。 新しいメタデータ提供されます新規ユーザーに送信された後に、8 ~ 15 日。 次に、Microsoft Store にアプリの更新プログラムを発行します。 ユーザーは、アプリの更新プログラムを取得し、ユーザーに必要なドライバーが更新されると仮定すると、ときに、アプリには、デバイスへのアクセスが特権があります。

## <a name="span-idupdatingdeviceappsspanspan-idupdatingdeviceappsspanspan-idupdatingdeviceappsspanupdating-device-apps"></a><span id="Updating_device_apps"></span><span id="updating_device_apps"></span><span id="UPDATING_DEVICE_APPS"></span>デバイス アプリを更新します。


UWP デバイス アプリの更新プログラムは、その他の UWP アプリの更新と同様、ユーザーが手動でトリガーされます。 Microsoft Store では、ユーザーにすべての利用可能なアプリの更新が表示されます。 アプリを更新して、ユーザーを手動で選択します。 古いメタデータとドライバーと互換性があるアプリを設計する必要があります。 デバイスのメタデータまたはドライバーがあります、アプリの最新の状態 Microsoft Store から UWP デバイス アプリを手動でインストールがメタデータまたはドライバーの配布を自動的にトリガーがあるため。

## <a name="span-iduninstallingdevicesoftwarespanspan-iduninstallingdevicesoftwarespanspan-iduninstallingdevicesoftwarespanuninstalling-device-software"></a><span id="Uninstalling_device_software"></span><span id="uninstalling_device_software"></span><span id="UNINSTALLING_DEVICE_SOFTWARE"></span>デバイス ソフトウェアをアンインストールします。


デバイス ドライバーとデバイスのメタデータは、Microsoft Store のデバイス アプリとは無関係にアンインストールされます。 ユーザーがデバイスをアンインストールするとき、ドライバーとメタデータはデバイスのアンインストールの一部として自動的にアンインストールします。

UWP デバイスのアプリは、ユーザーによって手動でアンインストールする必要があります。 インストールが完了したら、デバイス ドライバーとデバイスのメタデータは自動的にアンインストールされません。

 

 





