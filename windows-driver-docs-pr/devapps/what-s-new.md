---
title: UWP アプリのデバイスは新機能
description: このセクションでは、UWP デバイス アプリの新機能の概要を提供します。
ms.assetid: AF18ACFD-EA38-4ABD-9369-3974C019E132
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c7c164aa7b7058524141cc7a77f4954a4cc177e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557589"
---
# <a name="whats-new-for-uwp-device-apps"></a>UWP アプリのデバイスは新機能


このセクションでは、UWP デバイス アプリの新機能の概要を提供します。 デバイスのアプリに関する詳細については、[満たす UWP デバイス アプリ](meet-uwp-device-apps.md)を参照してください。

**ヒント:**  デバイスの Windows ランタイム Api は、デバイスのメタデータを必要としません。 つまり、アプリは、それらを使用するデバイス アプリを UWP をする必要はありません。 UWP アプリでは、これらの Api を使用して、USB、ヒューマン インターフェイス デバイス (HID)、Bluetooth GATT、Bluetooth RFCOMM、Wi-Fi Direct デバイス、および詳細にアクセスします。 詳細については、[デバイス統合](https://go.microsoft.com/fwlink/p/?LinkId=533279)を参照してください。

 

## <a name="span-idwhatsnewforwindows10spanspan-idwhatsnewforwindows10spanspan-idwhatsnewforwindows10spanwhats-new-for-windows-10"></a><span id="What_s_new_for_Windows_10"></span><span id="what_s_new_for_windows_10"></span><span id="WHAT_S_NEW_FOR_WINDOWS_10"></span>Windows 10 の新機能については


Windows 10 では、Microsoft Store のデバイスのアプリ機能の変更点はありません。 Windows 8.1 のプロセスを構築、テスト、および Windows 10 で機能し続けます UWP デバイス アプリを送信します。 ただし、カスタム機能を備えたユニバーサル Windows プラットフォーム (UWP) アプリの開発をお勧めします。 詳細については、次を参照してください。[ハードウェア サポート アプリ (HSA)。アプリ開発者のための手順](hardware-support-app--hsa--steps-for-app-developers.md)します。

## <a name="span-iddevicemetadatawizardspanspan-iddevicemetadatawizardspanspan-iddevicemetadatawizardspandevice-metadata-wizard"></a><span id="Device_metadata_wizard"></span><span id="device_metadata_wizard"></span><span id="DEVICE_METADATA_WIZARD"></span>デバイス メタデータのウィザード


Windows 8.1 では、デバイス メタデータの新規作成ウィザードについて説明します。 簡単に作成デバイス メタデータ パッケージ UWP デバイス アプリを生の XML を編集する必要はありません。 新規作成ウィザードは、ダッシュ ボードに送信する前にローカルで、アプリに対するデバイスのメタデータを検証することもできます。 このウィザードがプロセスに収める方法に関する詳細については、[ステップ バイ ステップの UWP デバイスのアプリをビルド](build-a-uwp-device-app-step-by-step.md)を参照してください。

**注**  デバイス メタデータの作成ウィザードを取得するには、インストールする必要があります、[スタンドアロン Windows 8.1 の SDK](https://go.microsoft.com/fwlink/p/?linkid=309209)このトピックの手順を完了する前にします。 Microsoft Visual Studio Express for Windows をインストールすると、ウィザードが含まれていない SDK のバージョンがインストールされます。

 

## <a name="span-idbackgroundtasksfordevicesyncandupdatespanspan-idbackgroundtasksfordevicesyncandupdatespanspan-idbackgroundtasksfordevicesyncandupdatespan-background-tasks-for-device-sync-and-update"></a><span id="_Background_tasks_for_device_sync_and_update"></span><span id="_background_tasks_for_device_sync_and_update"></span><span id="_BACKGROUND_TASKS_FOR_DEVICE_SYNC_AND_UPDATE"></span> デバイスとの同期と更新のためのバック グラウンド タスク


Windows 8.1 では、メンバー、アプリがバック グラウンドに移動し、中断された場合でも完了まで実行することに、UWP デバイス アプリでバック グラウンド タスクで複数ステップのデバイス操作を実行できます。 これは、座って進行状況バーを視聴するユーザーを必要とせずに信頼性の高いデバイス (永続的な設定またはファームウェアの変更) のサービスとコンテンツの同期を許可する必要があります。 使用、 [DeviceServicingTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308965)デバイスが提供するため、 [DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)コンテンツ同期します。 これらのバック グラウンド タスクが、アプリがバック グラウンドで実行できるし、不定の操作または無限の同期を許可するものではありません時間数を制限に注意してください。 詳細については、[デバイスとの同期と UWP デバイス アプリ用の更新プログラム](device-sync-and-update-for-uwp-device-apps.md)を参照してください。

**注**  、 [DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)デバイスの同期、デバイスのメタデータは必要ありません。

 

## <a name="span-idautoplayforwindowsstoredeviceappsspanspan-idautoplayforwindowsstoredeviceappsspanspan-idautoplayforwindowsstoredeviceappsspanautoplay-for-uwp-device-apps"></a><span id="AutoPlay_for_Windows_Store_device_apps"></span><span id="autoplay_for_windows_store_device_apps"></span><span id="AUTOPLAY_FOR_WINDOWS_STORE_DEVICE_APPS"></span>UWP デバイス アプリの自動再生


周辺デバイスが (後、アプリがインストールされている場合)、PC に接続されているときに自動的に起動する UWP デバイス アプリを構成できます。 Windows 8.1 のでは、デバイス アプリの自動再生は、ヒューマン インターフェイス デバイス (HID)、スマート カード、およびポートの一般的なサポートを追加します。 詳細については、[UWP デバイス アプリの自動再生](autoplay-for-uwp-device-apps.md)を参照してください。

## <a name="span-idprintercapabilitiesspanspan-idprintercapabilitiesspanspan-idprintercapabilitiesspanprinter-capabilities"></a><span id="Printer_capabilities"></span><span id="printer_capabilities"></span><span id="PRINTER_CAPABILITIES"></span>プリンターの機能


Windows 8.1、UWP デバイス アプリは、印刷ジョブを管理およびプリンターの保守タスクを実行します。 詳細については、[印刷ジョブを管理する方法](how-to-manage-print-jobs.md)と[プリンターのメンテナンスを行う方法](how-to-do-printer-maintenance.md)を参照してください。

新しいサンプルでは、強調表示されているこれらの機能を確認できます[印刷ジョブの管理とプリンターの保守](https://go.microsoft.com/fwlink/p/?LinkID=299829)します。 サンプルに含まれているプリンターの拡張機能ライブラリは、COM インターフェイス PrinterExtensionLib の COM の実装をラップします。 このライブラリは、UWP デバイス アプリで再利用するが簡単に設計されました。

## <a name="span-iduserexperiencechangesspanspan-iduserexperiencechangesspanspan-iduserexperiencechangesspanuser-experience-changes"></a><span id="User_experience_changes"></span><span id="user_experience_changes"></span><span id="USER_EXPERIENCE_CHANGES"></span>ユーザー エクスペリエンスの変更


固定されず UWP デバイス アプリと Windows 8.1 にインストールされているその他の UWP アプリの整合性を提供する**開始**にインストールします。 **開始**、最近インストールされた UWP デバイス アプリを含むすべてのアプリを表示する (画面の中央) からユーザーをスワイプできます。

組み込みのカメラ アプリが含まれなく Windows 8.1、**オプション**ボタンをクリックします。 これは UWP デバイス アプリからカメラ オプションのカスタマイズされたフライアウトはそのアプリに表示されていることを意味します。 ただし、他の UWP アプリを使用する、 **Windows.Media.Capture.CameraCaptureUI**クラスのカスタマイズされたフライアウトを公開できます**より多くのオプション**、インストールされている場合。

 

 





