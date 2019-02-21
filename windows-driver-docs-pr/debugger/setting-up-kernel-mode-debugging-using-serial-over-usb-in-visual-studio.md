---
title: カーネル モード デバッグのセットアップ サメ Cove 開発ボードでの Visual Studio での USB 経由でシリアルの使用
description: このトピックでは、サメ Cove の開発ボードがカーネル モード Visual Studio での USB のデバッグのセットアップについて説明します。
ms.assetid: D909CA2C-3870-4521-8F23-FBF93738F338
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5449f89d31cffeb2f7e55275d9ec3e6c84a5c01f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528869"
---
# <a name="span-iddebuggersettingupkernel-modedebuggingusingserialoverusbinvisualstudiospansetting-up-kernel-mode-debugging-using-serial-over-usb-in-visual-studio"></a><span id="debugger.setting_up_kernel-mode_debugging_using_serial_over_usb_in_visual_studio"></span>カーネル モード デバッグのセットアップ シリアルを使用して、Visual Studio での USB 経由で

> [!IMPORTANT]
> この機能は、Windows 10 バージョン 1507、以降のバージョンの WDK でご利用いただけません。
>

[サメ Cove 開発ボード](https://go.microsoft.com/fwlink/p?linkid=403168)USB ケーブルを介してシリアル デバッグをサポートしています。

カーネル モード デバッグの Microsoft Visual Studio を使用するには、Windows Driver Kit (WDK) の Visual Studio と統合が必要です。 統合環境をインストールする方法については、次を参照してください。 [Windows Driver Kit (WDK)](https://go.microsoft.com/fwlink/p?linkid=301383)します。

Visual Studio を使用して、USB ケーブルを介してシリアル デバッグを設定する代わりに、セットアップを手動で行うことができます。 詳細については、次を参照してください。[カーネル モード デバッグのセットアップを手動で USB シリアルを使用して](setting-up-kernel-mode-debugging-using-serial-over-usb-manually-.md)します。

デバッガーを実行しているコンピューターが呼び出されます、*ホスト コンピューター*、デバッグ中のコンピューターを呼び出すと、*対象のコンピュータ*します。 このトピックでは、サメ Cove ボードは、ターゲット コンピューターです。

## <a name="span-idsettingupahostcomputerfordebuggingthesharkscoveboardspanspan-idsettingupahostcomputerfordebuggingthesharkscoveboardspanspan-idsettingupahostcomputerfordebuggingthesharkscoveboardspansetting-up-a-host-computer-for-debugging-the-sharks-cove-board"></a><span id="Setting_up_a_Host_Computer_for_debugging_the_Sharks_Cove_board"></span><span id="setting_up_a_host_computer_for_debugging_the_sharks_cove_board"></span><span id="SETTING_UP_A_HOST_COMPUTER_FOR_DEBUGGING_THE_SHARKS_COVE_BOARD"></span>サメ Cove 掲示板をデバッグするためのホスト コンピューターをセットアップします。


1.  ホスト コンピューターでは、デバイス マネージャーを開きます。 **ビュー** ] メニューの [選択**デバイスの種類によって**します。

2.  サメ Cove ボードには、デバッグのコネクタを見つけます。 これは、次の図に示すように、マイクロ USB コネクタです。

    ![表示される画像サメ cove ボードのコネクタをデバッグします。](images/sharkscovedebugconnector.png)

3.  USB 2.0 ケーブルを使用して、サメ cove ボード上のデバッグ コネクタにホスト コンピューターを接続します。

4.  デバイス マネージャーで、ホスト コンピューターで 2 つの COM ポートが列挙を取得します。 最も番号が付いた COM ポートを選択します。 **ビュー** ] メニューの [選択**接続によってデバイス**します。 COM ポートが USB ホスト コント ローラーのいずれかで表示されていることを確認します。

    ![デバイス マネージャーでの com ポートを表示する画面の表示](images/serialoverusb01.png)

    COM ポートの番号をメモしてをおきます。 これは、USB ホスト コント ローラーのノード下に表示される最小の COM ポート番号です。 たとえば、上記のスクリーン ショットでは、USB ホスト コント ローラーで最下位の COM ポート番号は COM3 です。 デバッグ セッションを開始するときに、この COM ポート番号を後で必要があります。 COM ポートのドライバーがインストールされていない場合、COM ポート ノードを右クリックし、選択**ドライバーの更新**します。 選び**更新されたドライバー ソフトウェアを自動的に検索**します。 これは、インターネット接続を必要があります。

## <a name="span-idconfiguringthehostandtargetcomputersspanspan-idconfiguringthehostandtargetcomputersspanspan-idconfiguringthehostandtargetcomputersspanconfiguring-the-host-and-target-computers"></a><span id="Configuring_the_host_and_target_computers"></span><span id="configuring_the_host_and_target_computers"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTERS"></span>ホストおよびターゲット コンピュータの構成


次の手順では、サメ Cove ボードは、ターゲット コンピューターです。

1.  」の説明に従って、ホストとターゲット コンピューターの構成を開始[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8.1)](https://msdn.microsoft.com/library/windows/hardware/dn745909)します。
2.  Visual Studio で、ホスト コンピューターで、コンピューターの構成 ダイアログ ボックスのような場合が選択**コンピューターをプロビジョニングし、デバッガーの設定を選択**します。
3.  **接続の種類**、選択**シリアル**します。

    ![スクリーン ショットのデバッガーの例を次のフィールドの値の設定を示す: 接続の種類、ターゲットの名前、およびバス パラメーター](images/setupserialoverusbvs.png)

    **ボー レート**115200 を入力します。 **ポート**、以前デバイス マネージャー (com3 など) でメモした COM ポートの名前を入力します。 **ターゲット ポート**com1 を入力します。

4.  構成プロセスには数分かかりますが自動的に、コンピューターを再起動ターゲットまたは 2 回。 プロセスが完了したら、クリックして**完了**します。

## <a name="span-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>デバッグ セッションの開始


1.  Visual Studio で、ホスト コンピューター上で、**ツール**] メニューの [選択**プロセスにアタッチ**します。
2.  **トランスポート**、選択**Windows カーネル モードのデバッガー**します。
3.  **修飾子**、以前に構成されているターゲット コンピューターの名前を選択します。
4.  クリックして**アタッチ**します。

## <a name="span-idtroubleshootingtipsforserialdebuggingoverausbcablespanspan-idtroubleshootingtipsforserialdebuggingoverausbcablespanspan-idtroubleshootingtipsforserialdebuggingoverausbcablespantroubleshooting-tips-for-serial-debugging-over-a-usb-cable"></a><span id="Troubleshooting_Tips_for_Serial_Debugging_over_a_USB_Cable"></span><span id="troubleshooting_tips_for_serial_debugging_over_a_usb_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_SERIAL_DEBUGGING_OVER_A_USB_CABLE"></span>USB ケーブルを介してシリアル デバッグのトラブルシューティングのヒント


### <a name="span-idspecifycorrectcomportonbothhostandtargetspanspan-idspecifycorrectcomportonbothhostandtargetspanspan-idspecifycorrectcomportonbothhostandtargetspanspecify-correct-com-port-on-both-host-and-target"></a><span id="Specify_correct_COM_port_on_both_host_and_target"></span><span id="specify_correct_com_port_on_both_host_and_target"></span><span id="SPECIFY_CORRECT_COM_PORT_ON_BOTH_HOST_AND_TARGET"></span>ホストとターゲットの両方で適切な COM ポートを指定します。

ターゲット コンピューター (サメ Cove ボード) でのデバッグで COM1 を使用していることを確認します。 管理者は、コマンド プロンプト ウィンドウを開き、入力**bcdedit/dbgsettings**します。 出力**bcdedit**表示`debugport 1`します。

ホスト コンピューターでは、デバイス マネージャーで前にメモした COM ポートを使用していることを確認します。

1.  ホスト コンピューター上の Visual Studio の **[ドライバー]** メニューで、**[Test (テスト)] &gt; [Configure Computers (コンピューターの構成)]** の順に選びます。
2.  テスト用コンピューターの名前を選択し、クリックして**次**します。
3.  選択**コンピューターをプロビジョニングし、デバッガーの設定を選択**します。 **[次へ]** をクリックします。
4.  適切な COM ポートの番号が表示されている**ポート**します。

### <a name="span-idbaudratemustbethesameonhostandtargetspanspan-idbaudratemustbethesameonhostandtargetspanspan-idbaudratemustbethesameonhostandtargetspanbaud-rate-must-be-the-same-on-host-and-target"></a><span id="Baud_rate_must_be_the_same_on_host_and_target"></span><span id="baud_rate_must_be_the_same_on_host_and_target"></span><span id="BAUD_RATE_MUST_BE_THE_SAME_ON_HOST_AND_TARGET"></span>ボー レートには、同じホストとターゲットである必要があります。

ボー レートは、ホストとターゲットの両方のコンピューターで 115200 である必要があります。

ターゲット コンピューター (サメ Cove ボード) で、管理者としてコマンド プロンプト ウィンドウを開きし、入力**bcdedit/dbgsettings**します。 出力**bcdedit**表示`baudrate 115200`します。

ホスト コンピューターでは、115200 のボー レートを使用していることを確認します。

1.  ホスト コンピューター上の Visual Studio の **[ドライバー]** メニューで、**[Test (テスト)] &gt; [Configure Computers (コンピューターの構成)]** の順に選びます。
2.  テスト用コンピューターの名前を選択し、クリックして**次**します。
3.  選択**コンピューターをプロビジョニングし、デバッガーの設定を選択**します。 **[次へ]** をクリックします。
4.  いることを確認、**ボー レート**115200 です。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Visual Studio でのカーネル モード デバッグのセットアップ](setting-up-kernel-mode-debugging-in-visual-studio.md)

 

 






