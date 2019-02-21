---
title: 新しいハードウェアに付属の Bluetooth ドライバーをインストールします。
description: この付録の内容は、Windows Vista の新しいハードウェアに付属の Bluetooth ドライバーをインストールする手順を説明します。
ms.assetid: 399514FD-2BD8-4DC2-8446-F5EEB4120876
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1dc6e19d5f4a7a15537c109fd9d4a92592ed93b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529223"
---
# <a name="appendix-a-how-to-install-an-in-box-bluetooth-driver-on-new-hardware-in-windows-vista"></a>付録 a:Windows Vista の新しいハードウェアに付属の Bluetooth ドライバーをインストールする方法


この付録では、新しい Bluetooth 無線をインストールする Windows Vista に含まれている Bluetooth ドライバーを強制する手順について説明します。 Windows XP SP2 は異なりますが、詳細情報の一部と同様の手順を使用します。

## <a name="span-idstep1startdevicemanagerandselectthebluetoothradiospanspan-idstep1startdevicemanagerandselectthebluetoothradiospanspan-idstep1startdevicemanagerandselectthebluetoothradiospanstep-1-start-device-manager-and-select-the-bluetooth-radio"></a><span id="Step_1__Start_Device_Manager_and_Select_the_Bluetooth_Radio"></span><span id="step_1__start_device_manager_and_select_the_bluetooth_radio"></span><span id="STEP_1__START_DEVICE_MANAGER_AND_SELECT_THE_BLUETOOTH_RADIO"></span>手順 1:デバイス マネージャーを起動し、Bluetooth 無線を選択します。


デバイス マネージャーを起動します。

1.  をクリックして**開始**に移動します**すべてのプログラム&gt;アクセサリ&gt;コマンド プロンプト**を右クリックして**コマンド プロンプト**順にクリックします**管理者として実行**を昇格した特権でコマンド ウィンドウを開きます。
2.  次のとおりに入力します。**Devmgmt.msc**

**その他のデバイス**デバイスのデバイス マネージャーの一覧で、Bluetooth 無線のエントリを検索します。 次の図では、オプションの名前は"UGT です"。 一部のポータブル コンピューターで必要があります、Bluetooth 無線を初めて有効にする Fn ながら f5 キーなどのキーの組み合わせを使用しています。

![bluetooth update のドライバー ソフトウェアの vista](images/bthnewhwstep1.jpg)

選択したデバイスが Bluetooth 無線であることを確認するデバイス名を右クリックし、順にクリックします**プロパティ**を表示する、**プロパティ** ダイアログ ボックス。 **詳細** タブで、デバイスが Bluetooth 無線の互換性のある ID であることを確認します。

USB\\クラス\_e0 & サブクラス\_01 & 保護\_01
### <a name="span-idstep2starttheupdatedriversoftwarewizardspanspan-idstep2starttheupdatedriversoftwarewizardspanspan-idstep2starttheupdatedriversoftwarewizardspanstep-2-start-the-update-driver-software-wizard"></a><span id="Step_2__Start_the_Update_Driver_Software_Wizard"></span><span id="step_2__start_the_update_driver_software_wizard"></span><span id="STEP_2__START_THE_UPDATE_DRIVER_SOFTWARE_WIZARD"></span>手順 2:ドライバー ソフトウェアの更新ウィザードを開始します。

Bluetooth 無線ノードを右クリックし、**ドライバー ソフトウェアの更新**します。 次の図に、ページに移動して、次のようにクリックします。**参照コンピューターでドライバー ソフトウェア**します。 ドライバーを手動で選択するには、次のようにクリックします。**コンピューター上のデバイス ドライバーの一覧から選択できるように**します。

![bluetooth update のドライバー ソフトウェアの vista](images/bthnewhwstep2.jpg)

### <a name="span-idstep3selectthegenericbluetoothdriverspanspan-idstep3selectthegenericbluetoothdriverspanspan-idstep3selectthegenericbluetoothdriverspanstep-3-select-the-generic-bluetooth-driver"></a><span id="Step_3__Select_the_Generic_Bluetooth_Driver"></span><span id="step_3__select_the_generic_bluetooth_driver"></span><span id="STEP_3__SELECT_THE_GENERIC_BLUETOOTH_DRIVER"></span>手順 3:汎用の Bluetooth ドライバーを選択します。

次に、ドライバー ソフトウェアの更新ウィザードには、使用可能なドライバーの一覧が表示されます。 選択**Bluetooth ラジオ**に次の図に示すように、システムに一致する Bluetooth 無線を選択します。 使用するドライバーがない場合は、テストするための一般的なドライバーを使用できます。 これを行うには、次のように選択します。**汎用アダプター**製造元としてと**汎用の Bluetooth アダプター**モデルとして。

![bluetooth update のドライバー ソフトウェアの vista](images/bthnewhwstep3.jpg)

ドライバーを選択した後は、新しい Bluetooth 無線で指定されたドライバーをインストールすることを確認するよう要求されます。 Bluetooth 無線ではないデバイスで Bluetooth ドライバーをインストールしようとする場合、ドライバーは開始いない可能性があります。

ドライバーが正しく読み込まれると、次の図に示すように、デバイス マネージャーは [Bluetooth ラジオ] ノードで汎用の Bluetooth アダプターのエントリが必要です。

![bluetooth update のドライバー ソフトウェアの vista](images/bthnewhwstep4.jpg)

ドライバーが開始に失敗した場合など、Windows が起動エラー コードでは、返された場合、イベント ログを調べ、原因を特定します。

 

 





