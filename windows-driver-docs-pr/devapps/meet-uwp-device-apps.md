---
title: UWP デバイス アプリを満たす
description: このトピックでは、通常の UWP アプリから一意にさまざまな UWP デバイスのアプリを構成する機能、機能の概要を示します。
ms.assetid: 395745E6-7A97-4B26-A82C-0729E7B999C6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3227bcab091c9ba6c7584e12546f661abb47eb42
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536319"
---
# <a name="meet-uwp-device-apps"></a>UWP デバイス アプリを満たす


デバイスの製造元は、自分のデバイスに付属として機能する UWP デバイス アプリを作成できます。 デバイス アプリでは、さまざまな周辺機器または内部のデバイスの機能を使用できるし、ファームウェアの更新など、特権操作を実行できます。 このトピックでは、通常の UWP アプリから一意にさまざまな UWP デバイスのアプリを構成する機能、機能の概要を示します。

**注**  これらの各機能は省略可能です。 1 つのデバイス アプリをそれらのすべてを使用する必要はありません。 これらすべての機能には、デバイスのメタデータが必要です。

 

どのような UWP デバイス アプリは、1 つを作成する方法の詳細については、[構築 UWP デバイス アプリ](the-workflow.md)を参照してください。

## <a name="span-iddeviceupdatespanspan-iddeviceupdatespanspan-iddeviceupdatespan-device-update"></a><span id="_Device_update"></span><span id="_device_update"></span><span id="_DEVICE_UPDATE"></span> デバイスの更新


デバイスのメタデータでの特権を持つアプリとして指定すると、UWP デバイス アプリはデバイスのバック グラウンド タスクでマルチ ステップのデバイスの操作を実行できます。 この特殊なバック グラウンド タスクは、アプリがバック グラウンドに移動し、中断された場合でも、完了するまで実行できます。 これは、サービスに、永続的な設定またはファームウェア、変更のように座って、進行状況バーを視聴するユーザーを必要とせず、信頼性の高いデバイスを許可する必要があります。

![windows ストア デバイス アプリはバック グラウンドでファームウェアの更新プログラムなどのデバイスの更新プログラムを実行することができます。](images/deviceupdateuserconsent.png)

デバイス (デバイスの更新プログラム) をサービスのバック グラウンド タスクを作成するには、使用、 [DeviceServicingTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308965)トリガーします。 ようなトリガーでは、 [DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)、すべての UWP アプリで利用できますが、信頼性の高いコンテンツの同期のことができます。 詳細については、[デバイスとの同期と UWP デバイス アプリ用の更新プログラム](device-sync-and-update-for-uwp-device-apps.md)を参照してください。

**注**  デバイスのバック グラウンド タスクは、アプリがバック グラウンドで実行できるし、不定の操作または無限の同期を許可するものではありません時間を制限します。

 

## <a name="span-idautoplayspanspan-idautoplayspanspan-idautoplayspanautoplay"></a><span id="AutoPlay"></span><span id="autoplay"></span><span id="AUTOPLAY"></span>自動再生


を、自動再生でサポートされているデバイスが、PC に接続しているときに自動的に起動する、UWP デバイス アプリを含め、UWP アプリを構成することができます。 ただし、そのアプリは自動再生ハンドラーをサポートし、アプリ マニフェストでエクスペリエンスの ID を指定する必要があります。 その他の UWP アプリがデバイスの自動再生ハンドラーとして機能できるようにすることもできます。

![デバイスの自動再生ダイアログ ボックスの例](images/autoplayfordeviceapps.png)

自動再生と Windows 8.1 ではサポートされてデバイス クラスに関する詳細については、[UWP デバイス アプリの自動再生](autoplay-for-uwp-device-apps.md)を参照してください。

## <a name="span-iddeviceappsforprintersspanspan-iddeviceappsforprintersspanspan-iddeviceappsforprintersspandevice-apps-for-printers"></a><span id="Device_apps_for_printers"></span><span id="device_apps_for_printers"></span><span id="DEVICE_APPS_FOR_PRINTERS"></span>プリンター デバイス アプリ


UWP デバイス アプリでの印刷にカスタマイズした設定のフライアウトを使用したプリンター特別な機能を強調表示でき、通知をサポートします。 UWP デバイス アプリことができますもプリンターのステータスを表示、印刷ジョブの管理およびプリンターのメンテナンスを実施します。

については、これらのトピックを参照してください。

-   [プリンターのステータスを表示する方法](how-to-display-printer-status.md)
-   [印刷設定をカスタマイズする方法](how-to-customize-print-settings.md)
-   [印刷通知の操作](working-with-print-notifications.md)
-   [印刷ジョブを管理する方法](how-to-manage-print-jobs.md)
-   [プリンターのメンテナンスを実行する方法](how-to-do-printer-maintenance.md)
-   [プリンター拡張機能ライブラリの概要](printer-extension-library-overview.md)

## <a name="span-iddeviceappsforcamerasspanspan-iddeviceappsforcamerasspanspan-iddeviceappsforcamerasspandevice-apps-for-cameras"></a><span id="Device_apps_for_cameras"></span><span id="device_apps_for_cameras"></span><span id="DEVICE_APPS_FOR_CAMERAS"></span>カメラ用のデバイス アプリ


UWP デバイス アプリは、カスタマイズされたカメラの設定および特殊なカメラの効果をカメラの特殊な機能を強調表示もできます。

詳細については、これらのトピックを参照してください。

-   [カメラのオプションをカスタマイズする方法](how-to-customize-camera-options.md)
-   [カメラ driver MFT の作成](creating-a-camera-driver-mft.md)
-   [複数ピン カメラ ドライバー仕様に関する考慮事項](driver-mfts-on-multi-pin-cameras.md)
-   [内蔵カメラの位置を特定します。](identifying-the-location-of-internal-cameras.md)

## <a name="span-iddeviceappsforinternaldevicesspanspan-iddeviceappsforinternaldevicesspanspan-iddeviceappsforinternaldevicesspandevice-apps-for-internal-devices"></a><span id="Device_apps_for_internal_devices"></span><span id="device_apps_for_internal_devices"></span><span id="DEVICE_APPS_FOR_INTERNAL_DEVICES"></span>内部デバイス用のデバイス アプリ


Oem およびコンポーネント サプライヤーは、PC の内部的なデバイス用の UWP デバイス アプリを開発できます。 システム コンテナーに関連付けられているデバイスにアクセスするには、デバイスのメタデータでの特権を持つアプリとしてアプリを指定してください。 内部デバイス用のアプリは通常、PC にプレインストールされているし、Microsoft Store からダウンロードできます。 詳細については、[内部デバイス用の UWP デバイス アプリ](uwp-device-apps-for-specialized-devices.md)を参照してください。

## <a name="span-idautomaticinstallationspanspan-idautomaticinstallationspanspan-idautomaticinstallationspanautomatic-installation"></a><span id="Automatic_installation"></span><span id="automatic_installation"></span><span id="AUTOMATIC_INSTALLATION"></span>自動インストール


UWP デバイス アプリは、ユーザーが各自の PC にデバイスを接続するときに自動的にインストールできます。 インターネットへの接続を使用できない場合は、Windows が後でもう一度試行されます。 デバイスのアプリがインストールされている**すべてのアプリ**します。

![windows ストア デバイス アプリが自動的にインストールできます。](images/autoinstalluserexperience.png)

**警告**  自動インストール機能が提供しないことを通知をユーザーにアプリがインストールされている場合を考慮することが重要です。 一部のユーザーは、混乱とフラストレーション、このエクスペリエンスを検索し、アプリに不適切な評価を可能性があります。

 

自動インストールの詳細については、[プリンターとカメラの自動インストール](auto-install-for-uwp-device-apps.md)を参照してください。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[UWP デバイス アプリをビルドします。](the-workflow.md)

[UWP デバイス アプリの自動インストール](auto-install-for-uwp-device-apps.md)

[UWP デバイス アプリの自動再生](autoplay-for-uwp-device-apps.md)

[デバイスとの同期と UWP デバイス アプリの更新](device-sync-and-update-for-uwp-device-apps.md)

 

 






