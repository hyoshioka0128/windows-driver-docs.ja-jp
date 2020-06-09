---
title: サメ Cove development board を使用した Visual Studio での Serial over USB を使用したカーネルモードデバッグの設定
description: このトピックでは、サメ Cove development board を使用して Visual Studio でカーネルモードデバッグ USB を設定する方法について説明します。
ms.assetid: D909CA2C-3870-4521-8F23-FBF93738F338
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4a449bd2e40613946362fcb02c446102b976b44f
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534763"
---
# <a name="span-iddebuggersetting_up_kernel-mode_debugging_using_serial_over_usb_in_visual_studiospansetting-up-kernel-mode-debugging-using-serial-over-usb-in-visual-studio"></a><span id="debugger.setting_up_kernel-mode_debugging_using_serial_over_usb_in_visual_studio"></span>Visual Studio での USB 経由のシリアル接続を使ったカーネル モード デバッグの設定

> [!IMPORTANT]
> この機能は、Windows 10 バージョン1507以降のバージョンの WDK では使用できません。
>

[サメ Cove hardware development board](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/sharks-cove-hardware-development-board)は、USB ケーブル経由でのシリアルデバッグをサポートしています。

カーネルモードのデバッグに Microsoft Visual Studio を使用するには、Visual Studio に Windows Driver Kit (WDK) が統合されている必要があります。 統合環境をインストールする方法の詳細については、「 [Visual Studio を使用したデバッグ](debugging-using-visual-studio.md)」を参照してください。

デバッガーを実行するコンピューターは*ホストコンピューター*と呼ばれ、デバッグ中のコンピューターは*ターゲットコンピューター*と呼ばれます。 このトピックでは、サメ Cove board がターゲットコンピューターです。

## <a name="span-idsetting_up_a_host_computer_for_debugging_the_sharks_cove_boardspanspan-idsetting_up_a_host_computer_for_debugging_the_sharks_cove_boardspanspan-idsetting_up_a_host_computer_for_debugging_the_sharks_cove_boardspansetting-up-a-host-computer-for-debugging-the-sharks-cove-board"></a><span id="Setting_up_a_Host_Computer_for_debugging_the_Sharks_Cove_board"></span><span id="setting_up_a_host_computer_for_debugging_the_sharks_cove_board"></span><span id="SETTING_UP_A_HOST_COMPUTER_FOR_DEBUGGING_THE_SHARKS_COVE_BOARD"></span>サメ Cove board をデバッグするためのホストコンピューターのセットアップ


1.  ホストコンピューターでデバイスマネージャーを開きます。 [**表示**] メニューの [**種類別のデバイス**] を選択します。

2.  サメ Cove board で、デバッグコネクタを見つけます。 これは、次の図に示すマイクロ USB コネクタです。

    ![サメ cove board でのデバッグコネクタを示す画像](images/sharkscovedebugconnector.png)

3.  USB 2.0 ケーブルを使用して、ホストコンピューターをサメ cove board のデバッグコネクタに接続します。

4.  ホストコンピューターのデバイスマネージャーでは、2つの COM ポートが列挙されます。 番号が最も小さい COM ポートを選択します。 [**表示**] メニューの [**接続ごとにデバイス**] を選択します。 COM ポートが USB ホストコントローラーの1つに一覧表示されていることを確認します。

    ![デバイスマネージャーで com ポートを表示する画面表示](images/serialoverusb01.png)

    COM ポート番号をメモしておきます。 これは、USB ホストコントローラーノードの下に表示される最下位の COM ポート番号です。 たとえば、前のスクリーンショットでは、USB ホストコントローラーの下にある最低の COM ポート番号は COM3 です。 この COM ポート番号は、後でデバッグセッションを開始するときに必要になります。 ドライバーが COM ポート用にまだインストールされていない場合は、[COM ポート] ノードを右クリックし、[**ドライバーの更新**] を選択します。 次に、[**更新されたドライバーソフトウェアを自動的に検索する**] を選択します。 これにはインターネット接続が必要です。

## <a name="span-idconfiguring_the_host_and_target_computersspanspan-idconfiguring_the_host_and_target_computersspanspan-idconfiguring_the_host_and_target_computersspanconfiguring-the-host-and-target-computers"></a><span id="Configuring_the_host_and_target_computers"></span><span id="configuring_the_host_and_target_computers"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTERS"></span>ホストとターゲットコンピューターの構成


この手順では、サメ Cove board が対象のコンピューターになります。

1.  「[ドライバーの展開およびテスト用にコンピューターをプロビジョニングする (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」の説明に従って、ホストとターゲットコンピューターの構成を開始します。
2.  ホストコンピューターの Visual Studio で、[コンピューターの構成] ダイアログボックスが表示されたら、[コンピューターのプロビジョニング] を選択し、[**デバッガーの設定**] を選択します。
3.  [**接続の種類**] で [**シリアル**] を選択します。

    ![[接続の種類]、[ターゲット名]、[バスパラメーター] の各フィールドの値を含むデバッガー設定の例を示すスクリーンショット](images/setupserialoverusbvs.png)

    [**ボーレート**] に「115200」と入力します。 [**ポート**] には、前にデバイスマネージャーでメモした COM ポートの名前 (たとえば、「com3」) を入力します。 [**ターゲットポート**] に「com1」と入力します。

4.  構成プロセスには数分かかり、対象のコンピューターが1回または2回自動的に再起動される場合があります。 プロセスが完了したら、[**完了**] をクリックします。

## <a name="span-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>デバッグセッションを開始しています


1.  ホストコンピューターで、Visual Studio の [**ツール**] メニューの [**プロセスにアタッチ**] をクリックします。
2.  [**トランスポート**] で、[ **Windows カーネルモードデバッガー**] を選択します。
3.  [**修飾子**] で、以前に構成したターゲットコンピューターの名前を選択します。
4.  **[アタッチ]** をクリックします。

## <a name="span-idtroubleshooting_tips_for_serial_debugging_over_a_usb_cablespanspan-idtroubleshooting_tips_for_serial_debugging_over_a_usb_cablespanspan-idtroubleshooting_tips_for_serial_debugging_over_a_usb_cablespantroubleshooting-tips-for-serial-debugging-over-a-usb-cable"></a><span id="Troubleshooting_Tips_for_Serial_Debugging_over_a_USB_Cable"></span><span id="troubleshooting_tips_for_serial_debugging_over_a_usb_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_SERIAL_DEBUGGING_OVER_A_USB_CABLE"></span>USB ケーブルを使用したシリアルデバッグのトラブルシューティングのヒント


### <a name="span-idspecify_correct_com_port_on_both_host_and_targetspanspan-idspecify_correct_com_port_on_both_host_and_targetspanspan-idspecify_correct_com_port_on_both_host_and_targetspanspecify-correct-com-port-on-both-host-and-target"></a><span id="Specify_correct_COM_port_on_both_host_and_target"></span><span id="specify_correct_com_port_on_both_host_and_target"></span><span id="SPECIFY_CORRECT_COM_PORT_ON_BOTH_HOST_AND_TARGET"></span>ホストとターゲットの両方で正しい COM ポートを指定してください

ターゲットコンピューター (サメ Cove board) で、デバッグに COM1 を使用していることを確認します。 管理者としてコマンドプロンプトウィンドウを開き、「 **bcdedit/dbgsettings**」と入力します。 **Bcdedit**の出力が表示され `debugport 1` ます。

ホストコンピューターで、デバイスマネージャーでメモしておいた COM ポートを使用していることを確認します。

1.  ホスト コンピューター上の Visual Studio の **[ドライバー]** メニューで、 **[Test (テスト)] &gt; [Configure Computers (コンピューターの構成)]** の順に選びます。
2.  テストコンピューターの名前を選択し、[**次へ**] をクリックします。
3.  [**コンピューターのプロビジョニング**] を選択し、[デバッガーの設定] を選択します。 **[次へ]** をクリックします。
4.  正しい COM ポート番号が**ポート**に対して一覧表示されていることを確認します。

### <a name="span-idbaud_rate_must_be_the_same_on_host_and_targetspanspan-idbaud_rate_must_be_the_same_on_host_and_targetspanspan-idbaud_rate_must_be_the_same_on_host_and_targetspanbaud-rate-must-be-the-same-on-host-and-target"></a><span id="Baud_rate_must_be_the_same_on_host_and_target"></span><span id="baud_rate_must_be_the_same_on_host_and_target"></span><span id="BAUD_RATE_MUST_BE_THE_SAME_ON_HOST_AND_TARGET"></span>ホストとターゲットのボーレートは同じである必要があります

ホストコンピューターとターゲットコンピューターの両方で、ボーレートが115200である必要があります。

ターゲットコンピューター (サメ Cove board) で、管理者としてコマンドプロンプトウィンドウを開き、「 **bcdedit/dbgsettings**」と入力します。 **Bcdedit**の出力が表示され `baudrate 115200` ます。

ホストコンピューターで、115200のボーレートを使用していることを確認します。

1.  ホスト コンピューター上の Visual Studio の **[ドライバー]** メニューで、 **[Test (テスト)] &gt; [Configure Computers (コンピューターの構成)]** の順に選びます。
2.  テストコンピューターの名前を選択し、[**次へ**] をクリックします。
3.  [**コンピューターのプロビジョニング**] を選択し、[デバッガーの設定] を選択します。 **[次へ]** をクリックします。
4.  **ボーレート**が115200であることを確認します。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック



