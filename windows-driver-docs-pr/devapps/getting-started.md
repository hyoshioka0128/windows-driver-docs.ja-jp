---
title: UWP デバイス アプリの概要
description: UWP デバイス アプリのビルドを開始するには、ここから始めます。
ms.assetid: 6280E9CC-422B-4100-8B38-07BADD6A578A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4189c4b4978a106f21e8197889cb4107a7b3e75
ms.sourcegitcommit: 56599ec634b3a731f2d13dff686be3b7b95390e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2019
ms.locfileid: "58419564"
---
# <a name="getting-started-with-uwp-device-apps"></a>UWP デバイス アプリの概要


UWP デバイス アプリのビルドを開始するには、ここから始めます。

![windows ストア デバイス アプリを概要します。](images/devices-diagram-350x350.png)

デバイス製造元は、デバイスのコンパニオンとして機能する UWP デバイス アプリを作成できます。 UWP デバイス アプリには、通常の UWP アプリより多くの機能を備え、ファームウェアの更新などの特権操作を実行できます。 また、UWP デバイス アプリことができます (他のアプリよりも多くのデバイス) で自動再生の開始、自動的にインストール、デバイスが接続されている場合、最初にして Windows に組み込まれているプリンター、カメラ エクスペリエンスを拡張します。

**注**  デバイスの Windows ランタイム Api は、デバイスのメタデータを必要としません。 つまり、アプリは、それらを使用するデバイス アプリを UWP をする必要はありません。 UWP アプリでは、USB、ヒューマン インターフェイス デバイス (HID)、Bluetooth デバイス、およびアクセスをこれらの Api を使用できます。 詳細については、次を参照してください。[デバイス統合](https://go.microsoft.com/fwlink/p/?LinkId=533279)します。

 

UWP モバイル ブロードバンド アプリに関する情報を探している場合は、「[Mobile Broadband](https://go.microsoft.com/fwlink/p/?LinkID=301754)」 (モバイル ブロードバンド) を参照してください。

## <a name="span-id1getsetupspanspan-id1getsetupspan1-get-set-up"></a><span id="1._get_set_up"></span><span id="1._GET_SET_UP"></span>1.準備


UWP デバイスのアプリを開発する: UWP アプリとデバイス メタデータの作成ウィザード開発のデバイス メタデータを開発するため、Microsoft Visual Studio では、する必要があります。

**注**  Windows 10 UWP デバイス アプリを開発するには、Microsoft Visual Studio 2017 と Windows Driver Kit (WDK) 10 をダウンロードします。 [キットとツールを取得する Windows Insider になります。](https://go.microsoft.com/fwlink/p/?LinkId=526775)

 

### <a name="span-idifyourealsodevelopingdriversspanspan-idifyourealsodevelopingdriversspanspan-idifyourealsodevelopingdriversspanif-youre-also-developing-drivers"></a><span id="If_you_re_also_developing_drivers"></span><span id="if_you_re_also_developing_drivers"></span><span id="IF_YOU_RE_ALSO_DEVELOPING_DRIVERS"></span>ドライバーも開発する場合

UWP デバイスのアプリだけでなく Windows ドライバーを開発する場合は、Microsoft Visual Studio Professional または Microsoft Visual Studio Ultimate を使用して、UWP デバイス アプリを作成します。 これらのエディションでは、新しいデバイス メタデータの作成ウィザードが含まれてし、によって、Windows Driver Kit (WDK) 8.1 も必要があります。

1.  [Visual Studio のダウンロード Professional または Visual Studio Ultimate](https://go.microsoft.com/fwlink/p/?LinkId=302196)
2.  [WDK 8.1 をダウンロードします。](https://go.microsoft.com/fwlink/p/?LinkId=302196)

### <a name="span-idifyourenotgoingtobedevelopingdriversspanspan-idifyourenotgoingtobedevelopingdriversspanspan-idifyourenotgoingtobedevelopingdriversspanif-youre-not-going-to-be-developing-drivers"></a><span id="If_you_re_not_going_to_be_developing_drivers"></span><span id="if_you_re_not_going_to_be_developing_drivers"></span><span id="IF_YOU_RE_NOT_GOING_TO_BE_DEVELOPING_DRIVERS"></span>ドライバーの開発を続けない場合

ドライバーの開発に不要な場合は、UWP デバイス アプリを作成する Microsoft Visual Studio Express 2015 for Windows を使用できます。 このバージョンの Visual Studio がデバイス メタデータの作成ウィザードが含まれていない SDK のバージョンをインストールします。 新しいデバイス メタデータの作成ウィザードを取得するには、スタンドアロンの Windows 8.1 SDK をダウンロードすることも必要があります。

1.  [ダウンロードの Visual Studio Express 2015 for Windows 10](https://visualstudio.microsoft.com/vs/express/)
2.  [スタンドアロンの Windows 8.1 SDK をダウンロードします。](https://go.microsoft.com/fwlink/p/?LinkId=302196)

## <a name="span-id2buildsomeregularwindowsstoreappsspanspan-id2buildsomeregularwindowsstoreappsspan2-build-some-regular-uwp-apps"></a><span id="2._build_some_regular_windows_store_apps"></span><span id="2._BUILD_SOME_REGULAR_WINDOWS_STORE_APPS"></span>2.いくつかの通常の UWP アプリをビルドします。


UWP デバイスのアプリは、UWP アプリの特別な種類です。 そのため、最初の UWP デバイス アプリを開発する前に設定がいくつかの通常の UWP アプリをビルドします。

-   [サインアップ - Microsoft Store の開発者アカウントの登録](https://go.microsoft.com/fwlink/p/?LinkId=302197)
-   [Microsoft Visual Studio を概要します。](https://go.microsoft.com/fwlink/p/?LinkID=267230)
-   参照してください、 [Microsoft Store のデザインの原則](https://go.microsoft.com/fwlink/p/?LinkID=299845)

## <a name="span-id3learnwhatmakeswindowsstoredeviceappsspecialspanspan-id3learnwhatmakeswindowsstoredeviceappsspecialspan3-learn-what-makes-uwp-device-apps-special"></a><span id="3._learn_what_makes_windows_store_device_apps_special"></span><span id="3._LEARN_WHAT_MAKES_WINDOWS_STORE_DEVICE_APPS_SPECIAL"></span>3.UWP デバイス アプリを特別な点について説明します。


UWP デバイスのアプリと 1 つのビルドに使用して実行できる特別なことについて説明します。

-   [UWP デバイス アプリを満たす](meet-uwp-device-apps.md)
-   [UWP デバイスのアプリのビルド](the-workflow.md)

## <a name="span-id4downloadsamplesspanspan-id4downloadsamplesspan4-download-samples"></a><span id="4._download_samples"></span><span id="4._DOWNLOAD_SAMPLES"></span>4.サンプルをダウンロードします。


デバイス関連のサンプルを見つけることができます、[デバイスとセンサー](https://go.microsoft.com/fwlink/p/?LinkID=302213)サンプル ギャラリー内のキーワード。 完全なサンプルのコンテキストでの Api を使用する方法について説明します。 デバイスのメタデータに関連付けられる StoreManifest.xml ファイルが含まれているために、UWP デバイスのアプリを判断できます。 これらのサンプルがでタグ付け、 [UWP デバイス アプリ](https://go.microsoft.com/fwlink/p/?LinkID=299847)キーワード。

## <a name="span-id4buildyourownwindowsstoredeviceappspanspan-id4buildyourownwindowsstoredeviceappspan4-build-your-own-uwp-device-app"></a><span id="4._build_your_own_windows_store_device_app"></span><span id="4._BUILD_YOUR_OWN_WINDOWS_STORE_DEVICE_APP"></span>4.UWP デバイス アプリをビルドします。


まず、次を参照してください。[ステップ バイ ステップの UWP デバイスのアプリをビルド](build-a-uwp-device-app-step-by-step.md)します。

 

 





