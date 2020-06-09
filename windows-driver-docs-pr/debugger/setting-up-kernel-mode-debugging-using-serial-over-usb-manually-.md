---
title: サメ cove development board 用に手動で Serial over USB を使用してカーネルモードのデバッグを設定する
description: このトピックでは、サメ cove development board 用に手動でカーネルモードのデバッグを設定する方法について説明します。
ms.assetid: E6157263-74E8-4704-9668-B845043737A7
ms.date: 05/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: 43bd8536125ee197b4373a4c53b8d72ac5cccf2e
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534759"
---
# <a name="span-iddebuggersetting_up_kernel-mode_debugging_using_serial_over_usb_manually_spansetting-up-kernel-mode-debugging-using-serial-over-usb-manually"></a><span id="debugger.setting_up_kernel-mode_debugging_using_serial_over_usb_manually_"></span>Serial over USB を使用したカーネルモードのデバッグを手動で設定する


[サメ Cove hardware development board](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/sharks-cove-hardware-development-board)は、USB ケーブル経由でのシリアルデバッグをサポートしています。

デバッガーを実行するコンピューターは*ホストコンピューター*と呼ばれ、デバッグ中のコンピューターは*ターゲットコンピューター*と呼ばれます。 このトピックでは、サメ Cove board がターゲットコンピューターです。

## <a name="span-idsetting_up_a_host_computer_for_debugging_the_sharks_cove_boardspanspan-idsetting_up_a_host_computer_for_debugging_the_sharks_cove_boardspanspan-idsetting_up_a_host_computer_for_debugging_the_sharks_cove_boardspansetting-up-a-host-computer-for-debugging-the-sharks-cove-board"></a><span id="Setting_up_a_Host_Computer_for_debugging_the_Sharks_Cove_board"></span><span id="setting_up_a_host_computer_for_debugging_the_sharks_cove_board"></span><span id="SETTING_UP_A_HOST_COMPUTER_FOR_DEBUGGING_THE_SHARKS_COVE_BOARD"></span>サメ Cove board をデバッグするためのホストコンピューターのセットアップ


1.  ホストコンピューターでデバイスマネージャーを開きます。 [**表示**] メニューの [**種類別のデバイス**] を選択します。

2.  サメ Cove board で、デバッグコネクタを見つけます。 これは、次の図に示すマイクロ USB コネクタです。

    ![サメ cove board でのデバッグコネクタを示す画像](images/sharkscovedebugconnector.png)

3.  USB 2.0 ケーブルを使用して、ホストコンピューターをサメ cove board のデバッグコネクタに接続します。

4.  ホストコンピューターのデバイスマネージャーでは、2つの COM ポートが列挙されます。 番号が最も小さい COM ポートを選択します。 [**表示**] メニューの [**接続ごとにデバイス**] を選択します。 COM ポートが USB ホストコントローラーの1つに一覧表示されていることを確認します。

    ![デバイスマネージャーで com ポートを表示する画面表示](images/serialoverusb01.png)

    COM ポート番号をメモしておきます。 これは、USB ホストコントローラーノードの下に表示される最下位の COM ポート番号です。 たとえば、前のスクリーンショットでは、USB ホストコントローラーの下にある最低の COM ポート番号は COM3 です。 この COM ポート番号は、後でデバッグセッションを開始するときに必要になります。 ドライバーが COM ポート用にまだインストールされていない場合は、[COM ポート] ノードを右クリックし、[**ドライバーの更新**] を選択します。 次に、[**更新されたドライバーソフトウェアを自動的に検索する**] を選択します。 これにはインターネット接続が必要です。

## <a name="span-idsetting_up_the_sharks_cove_board_as_the_target_computerspanspan-idsetting_up_the_sharks_cove_board_as_the_target_computerspanspan-idsetting_up_the_sharks_cove_board_as_the_target_computerspansetting-up-the-sharks-cove-board-as-the-target-computer"></a><span id="Setting_Up_the_Sharks_Cove_Board_as_the_Target_Computer"></span><span id="setting_up_the_sharks_cove_board_as_the_target_computer"></span><span id="SETTING_UP_THE_SHARKS_COVE_BOARD_AS_THE_TARGET_COMPUTER"></span>ターゲットコンピューターとしてのサメ Cove Board の設定

> [!IMPORTANT]
> BCDEdit を使用してブート情報を変更する前に、テスト PC で BitLocker やセキュアブートなどの Windows のセキュリティ機能を一時的に停止することが必要になる場合があります。
> セキュリティ機能が無効になっている場合は、テストが完了し、テスト PC を適切に管理するときに、これらのセキュリティ機能を再び有効にします。

1.  ターゲットコンピューター (サメ Cove board) で、管理者としてコマンドプロンプトウィンドウを開き、次のコマンドを入力します。

    **bcdedit/debug on**

    **bcdedit/dbgsettings serial debugport: 1 ボーレート: 115200**

2.  ターゲット コンピューターを再起動します。

## <a name="span-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>デバッグセッションを開始しています


### <a name="span-idusing_windbgspanspan-idusing_windbgspanspan-idusing_windbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>WinDbg の使用

ホストコンピューターで、[WinDbg] を開きます。 [**ファイル**] メニューの [**カーネルデバッグ**] をクリックします。 [カーネルデバッグ] ダイアログボックスで、[ **COM** ] タブを開きます。[**ボーレート**] ボックスに「115200」と入力します。 [**ポート**] ボックスに「com*n* 」と入力します。ここで、 *n*は前にメモした com ポート番号です。 **[OK]** をクリックします。

また、コマンドプロンプトウィンドウで次のコマンドを入力して、WinDbg を使用してセッションを開始することもできます。*n*は、ホストコンピューターでメモした COM ポートの番号です。

**windbg-k com: port = com**<em>n</em>**, baud = 115200**

### <a name="span-idusing_kdspanspan-idusing_kdspanspan-idusing_kdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>KD の使用

ホストコンピューターで、コマンドプロンプトウィンドウを開き、次のコマンドを入力します。ここで、 *n*は前にメモした COM ポート番号です。

**kd-k com: port = com**<em>n</em>**, baud = 115200**

## <a name="span-idusing_environment_variablesspanspan-idusing_environment_variablesspanspan-idusing_environment_variablesspanusing-environment-variables"></a><span id="Using_Environment_Variables"></span><span id="using_environment_variables"></span><span id="USING_ENVIRONMENT_VARIABLES"></span>環境変数の使用


ホストコンピューターでは、環境変数を使用して COM ポートとボーレートを指定できます。 その後、デバッグセッションを開始するたびに、ポートとボーレートを指定する必要はありません。 環境変数を使用して COM ポートとボーレートを指定するには、コマンドプロンプトウィンドウを開き、次のコマンドを入力します。ここで、 *n*は前にメモした com ポート番号の番号です。

-   **set \_ NT \_ DEBUG \_ PORT = COM * * * n*
-   **\_NT デバッグのボーレートを設定する \_ \_ \_ : 115200**

デバッグセッションを開始するには、コマンドプロンプトウィンドウを開き、次のいずれかのコマンドを入力します。

-   **kd**
-   **windbg**

## <a name="span-idtroubleshooting_tips_for_serial_debugging_over_a_usb_cablespanspan-idtroubleshooting_tips_for_serial_debugging_over_a_usb_cablespanspan-idtroubleshooting_tips_for_serial_debugging_over_a_usb_cablespantroubleshooting-tips-for-serial-debugging-over-a-usb-cable"></a><span id="Troubleshooting_Tips_for_Serial_Debugging_over_a_USB_Cable"></span><span id="troubleshooting_tips_for_serial_debugging_over_a_usb_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_SERIAL_DEBUGGING_OVER_A_USB_CABLE"></span>USB ケーブルを使用したシリアルデバッグのトラブルシューティングのヒント


### <a name="span-idspecify_correct_com_port_on_both_host_and_targetspanspan-idspecify_correct_com_port_on_both_host_and_targetspanspan-idspecify_correct_com_port_on_both_host_and_targetspanspecify-correct-com-port-on-both-host-and-target"></a><span id="Specify_correct_COM_port_on_both_host_and_target"></span><span id="specify_correct_com_port_on_both_host_and_target"></span><span id="SPECIFY_CORRECT_COM_PORT_ON_BOTH_HOST_AND_TARGET"></span>ホストとターゲットの両方で正しい COM ポートを指定してください

ターゲットコンピューター (サメ Cove board) で、デバッグに COM1 を使用していることを確認します。 管理者としてコマンドプロンプトウィンドウを開き、「 **bcdedit/dbgsettings**」と入力します。 **Bcdedit**の出力が表示され `debugport 1` ます。

ホストコンピューターで、デバッガーを起動するとき、または環境変数を設定するときに、正しい COM ポートを指定します。 これは、デバイスマネージャーの USB ホストコントローラーで列挙された、番号が最も小さい COM ポートです。 たとえば、必要なポートが "COM3" の場合は、次のいずれかの方法を使用して COM ポートを指定します。

-   [WinDbg] の [カーネルデバッグ] ダイアログボックスで、[**ポート**] ボックスに「COM3」と入力します。
-   **windbg-k com: port = COM3,...**
-   **kd-k com: port = COM3,...**
-   **\_NT \_ デバッグポートの設定 \_ = COM3**

### <a name="span-idbaud_rate_must_be_the_same_on_host_and_targetspanspan-idbaud_rate_must_be_the_same_on_host_and_targetspanspan-idbaud_rate_must_be_the_same_on_host_and_targetspanbaud-rate-must-be-the-same-on-host-and-target"></a><span id="Baud_rate_must_be_the_same_on_host_and_target"></span><span id="baud_rate_must_be_the_same_on_host_and_target"></span><span id="BAUD_RATE_MUST_BE_THE_SAME_ON_HOST_AND_TARGET"></span>ホストとターゲットのボーレートは同じである必要があります

ホストコンピューターとターゲットコンピューターの両方で、ボーレートが115200である必要があります。

ターゲットコンピューター (サメ Cove board) で、管理者としてコマンドプロンプトウィンドウを開き、「 **bcdedit/dbgsettings**」と入力します。 **Bcdedit**の出力が表示され `baudrate 115200` ます。

ホストコンピューターで、デバッガーを起動するとき、または環境変数を設定するときに、適切なボーレートを指定します。 次のいずれかの方法を使用して、115200のボーレートを指定します。

-   [WinDbg] の [カーネルデバッグ] ダイアログボックスで、[**ボーレート**] ボックスに「115200」と入力します。
-   **windbg-k...、baud = 115200**
-   **kd-k...、baud = 115200**
-   **\_NT デバッグのボーレートを設定する \_ \_ \_ : 115200**

## <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


**Bcdedit**コマンドの完全なドキュメントについては、Windows driver KIT (WDK) ドキュメントの「ドライバーテストおよびデバッグ用のブートオプション」を参照してください。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[カーネル モードのデバッグを手動でセットアップする](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

 

 






