---
title: Bluetooth のユーザー インターフェイス
description: ソフトウェア開発者および仕入先の Windows で Bluetooth のユーザー インターフェイスの使い方について説明します
ms.assetid: 7E342615-217A-4252-AAC4-7F7EE013840D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc4ad313beb432d5d92688f034b6c9a97ddb3160
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354035"
---
# <a name="bluetooth-user-interface"></a>Bluetooth のユーザー インターフェイス


## <a name="span-idwhatisthebluetoothfiletransferwizardspanspan-idwhatisthebluetoothfiletransferwizardspanspan-idwhatisthebluetoothfiletransferwizardspanwhat-is-the-bluetooth-file-transfer-wizard"></a><span id="What_is_the_Bluetooth_File_Transfer_Wizard_"></span><span id="what_is_the_bluetooth_file_transfer_wizard_"></span><span id="WHAT_IS_THE_BLUETOOTH_FILE_TRANSFER_WIZARD_"></span>Bluetooth ファイルの転送ウィザードとは何ですか。


Bluetooth ファイルの転送ウィザードでは、コンピューターと Bluetooth デバイスの間でファイルを転送することができます。 たとえば、ユーザーは、コンピューターと携帯電話または (pda) とのファイルを転送することができます。 Bluetooth ファイルの転送ウィザードでは、Bluetooth をサポートする 2 台のコンピューターの間もファイルを転送できます。

**注**  Bluetooth ファイルの転送ウィザードを使用して GUI が Fsquirt.exe ファイルで実装されている既定値。 このファイルは、Bluetooth ファイルの転送ウィザードの GUI の既定の置換を有効に基になる転送ウィザードのメカニズムからアンフックすることができます。 詳細については、次の質問を参照してください。

 

## <a name="span-idhowdoiunhookfsquirtexespanspan-idhowdoiunhookfsquirtexespanhow-do-i-unhook-fsquirtexe"></a><span id="how_do_i_unhook_fsquirt.exe_"></span><span id="HOW_DO_I_UNHOOK_FSQUIRT.EXE_"></span>Fsquirt.exe をアンフックする方法は?


付属の Bluetooth ファイルの転送ウィザードを置き換える独自のアプリケーションを必要に応じて、ソフトウェア開発者は、基になる転送ウィザード機構から Fsquirt.exe をアンフック、次の手順を実行することで。

1.  という名前の DWORD 値を作成する**DisableFsquirt** 、hklm\\システム\\CurrentControlSet\\サービス\\Bthport\\パラメーターのレジストリ キー。
2.  値を設定**DisableFsquirt** 0x1
3.  コマンド プロンプト ウィンドウで、次のコマンドを実行または再起動: **fsquirt.exe-登録を解除**

Fsquirt.exe を再度有効にするには、次の手順を実行します。

1.  削除、 **DisableFsquirt**レジストリからの値。
2.  再起動するか、コマンド プロンプト ウィンドウで、次のコマンドを実行します**fsquirt.exe-登録。**

## <a name="span-idinwindowsvistawhydoesthebluetoothnotificationareaiconsometimesdisappearspanspan-idinwindowsvistawhydoesthebluetoothnotificationareaiconsometimesdisappearspanspan-idinwindowsvistawhydoesthebluetoothnotificationareaiconsometimesdisappearspanin-windows-vista-why-does-the-bluetooth-notification-area-icon-sometimes-disappear"></a><span id="In_Windows_Vista__why_does_the_Bluetooth_notification_area_icon_sometimes_disappear_"></span><span id="in_windows_vista__why_does_the_bluetooth_notification_area_icon_sometimes_disappear_"></span><span id="IN_WINDOWS_VISTA__WHY_DOES_THE_BLUETOOTH_NOTIFICATION_AREA_ICON_SOMETIMES_DISAPPEAR_"></span>Windows vista では、理由は、Bluetooth 通知エリア アイコン場合がありますが表示されなくなります。


Windows Vista RTM および Windows Vista SP1 では、Bluetooth の通知領域アイコンは、Bluetooth 無線がコンピューターに接続されているときに表示されます。 アイコンは、最大で 10 分間のアクティブなままに構成されますが、通知領域からその期間の後にアイコンが表示されなくなります。

ユーザーが永続的な Bluetooth 通知エリア アイコン場合、選択できます、 **Bluetooth アイコン、通知領域に表示する**チェック ボックスをオン、**オプション**のコントロール パネルの Bluetooth の設定 タブアプリケーション。

![bluetooth の通知の設定](images/bluetoothnotificationsettings.jpg)

**注**  引き続きコンピューターを探索可能なこれを行う新しい Bluetooth デバイスの追加などの関連のタスクを実行する、コントロール パネルの Bluetooth 設定アプリケーションを使用することができる場合でも、Bluetooth アイコンが通知領域ではありません。

 

## <a name="span-idcanvendorsaddtabstothecontrolpanelbluetoothsettingsapplicationspanspan-idcanvendorsaddtabstothecontrolpanelbluetoothsettingsapplicationspanspan-idcanvendorsaddtabstothecontrolpanelbluetoothsettingsapplicationspancan-vendors-add-tabs-to-the-control-panel-bluetooth-settings-application"></a><span id="Can_vendors_add_tabs_to_the_Control_Panel_Bluetooth_Settings_application_"></span><span id="can_vendors_add_tabs_to_the_control_panel_bluetooth_settings_application_"></span><span id="CAN_VENDORS_ADD_TABS_TO_THE_CONTROL_PANEL_BLUETOOTH_SETTINGS_APPLICATION_"></span>ベンダーは、コントロール パネルの Bluetooth 設定アプリケーションにタブを追加できますか。


はい、ベンダーは、アプリケーションのシェルのプロパティ シート ハンドラーを実装することでタブを追加できます。 たとえば、Ihv インボックス Bluetooth スタック実装の拡張機能がファイル転送などのプロファイル バージョン 2.1 の Bluetooth の仕様に追加された機能拡張のタブを追加するプロパティ シート ハンドラーを実装できます。 プロパティ シート ハンドラーを実装する方法の詳細については、次を参照してください。[プロパティ シート ハンドラー](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/cc144106(v=vs.85))します。

## <a name="span-idwhydoeswindows7andwindowsvistadisplayadialogboxwhenabluetoothaudiodeviceisinitiallyconnectedspanspan-idwhydoeswindows7andwindowsvistadisplayadialogboxwhenabluetoothaudiodeviceisinitiallyconnectedspanspan-idwhydoeswindows7andwindowsvistadisplayadialogboxwhenabluetoothaudiodeviceisinitiallyconnectedspanwhy-does-windows-7-and-windows-vista-display-a-dialog-box-when-a-bluetooth-audio-device-is-initially-connected"></a><span id="Why_does_Windows_7_and_Windows_Vista_display_a_dialog_box_when_a_Bluetooth_audio_device_is_initially_connected_"></span><span id="why_does_windows_7_and_windows_vista_display_a_dialog_box_when_a_bluetooth_audio_device_is_initially_connected_"></span><span id="WHY_DOES_WINDOWS_7_AND_WINDOWS_VISTA_DISPLAY_A_DIALOG_BOX_WHEN_A_BLUETOOTH_AUDIO_DEVICE_IS_INITIALLY_CONNECTED_"></span>理由は Windows 7 および Windows Vista ダイアログ ボックスを表示、Bluetooth のオーディオ デバイスが最初に接続されている場合ですか。


Windows では、ヘッドセット (HSP)、ハンドフリー (HFP) の既定のサポートを提供しない可能性があります。 またはオーディオの配布 (A2DP) オーディオ プロファイルの詳細。 Windows を通常表示場合は、Bluetooth のオーディオ デバイスは、必要なドライバーがないシステムと組み合わせて使用、**新しいハードウェアが見つかりました** ダイアログ ボックス。 ただし、次のいずれかが当てはまる場合に、このダイアログ ボックスは表示されません。

-   コンピューターの OEM には、Bluetooth のオーディオをサポートしているプロファイル パックが用意されています。
-   以前、エンドユーザーは、Bluetooth ヘッドセットをインストールして、IHV または Windows Update で提供されるメディアから、オーディオ ドライバーをダウンロードします。

## <a name="span-idhowdoienhancethefunctionalityandbetterrepresentmybluetoothdeviceindevicesandprintersspanspan-idhowdoienhancethefunctionalityandbetterrepresentmybluetoothdeviceindevicesandprintersspanspan-idhowdoienhancethefunctionalityandbetterrepresentmybluetoothdeviceindevicesandprintersspanhow-do-i-enhance-the-functionality-and-better-represent-my-bluetooth-device-in-devices-and-printers"></a><span id="How_do_I_enhance_the_functionality_and_better_represent_my_Bluetooth_device_in_Devices_and_Printers_"></span><span id="how_do_i_enhance_the_functionality_and_better_represent_my_bluetooth_device_in_devices_and_printers_"></span><span id="HOW_DO_I_ENHANCE_THE_FUNCTIONALITY_AND_BETTER_REPRESENT_MY_BLUETOOTH_DEVICE_IN_DEVICES_AND_PRINTERS_"></span>機能を強化してはどうすればデバイスとプリンターの Bluetooth デバイスをわかりやすく表すでしょうか。


Bluetooth デバイスのデバイス メタデータ パッケージを作成するには、デバイスとプリンターにリアルなアイコンやユーザー設定の説明など、デバイスのデバイスに固有の情報が表示されるようにします。 Bluetooth デバイスに、ユーザーのエクスペリエンスを大幅に向上させるこのことができます。 たとえばより効果的にデバイスをサポートするすべての機能を公開する可能性があります。 特定のデバイス クラスでは、Ihv をさらにカスタマイズとブランド化されたデバイスの特定のユーザー インターフェイスを提供することで、デバイス エクスペリエンスを強化できる Device stage も利用できます。

デバイスのデバイス メタデータ パッケージを作成する方法の詳細については、次を参照してください。[デバイスとプリンターのデバイス メタデータ パッケージを作成する方法](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/)します。

Device Stage の詳細については、次を参照してください。 **"デバイス ステージ一般的な開発キット"MSDN Web サイト**します。

**注**  Device Stage を利用するデバイス ID のプロファイル実装する必要が、ハードウェア ID、仕入先 ID、および PID が含まれます。

 

 

 





