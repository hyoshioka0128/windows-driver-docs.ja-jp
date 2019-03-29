---
title: カーネル モード デバッグのセットアップ サメ cove 開発ボードを手動で USB 経由でのシリアルを使用して
description: このトピックでは、サメ cove 開発ボードの手動で設定すると、カーネル モードのデバッグについて説明します。
ms.assetid: E6157263-74E8-4704-9668-B845043737A7
ms.date: 05/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: 72c31d23bcd9ffa5d91eabb75a2d61a179b8db14
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582285"
---
# <a name="span-iddebuggersettingupkernel-modedebuggingusingserialoverusbmanuallyspansetting-up-kernel-mode-debugging-using-serial-over-usb-manually"></a><span id="debugger.setting_up_kernel-mode_debugging_using_serial_over_usb_manually_"></span>カーネル モード デバッグのセットアップを手動で USB シリアルを使用します。


[サメ Cove 開発ボード](https://go.microsoft.com/fwlink/p?linkid=403168)USB ケーブルを介してシリアル デバッグをサポートしています。

デバッガーを実行しているコンピューターが呼び出されます、*ホスト コンピューター*、デバッグ中のコンピューターを呼び出すと、*対象のコンピュータ*します。 このトピックでは、サメ Cove ボードは、ターゲット コンピューターです。

## <a name="span-idsettingupahostcomputerfordebuggingthesharkscoveboardspanspan-idsettingupahostcomputerfordebuggingthesharkscoveboardspanspan-idsettingupahostcomputerfordebuggingthesharkscoveboardspansetting-up-a-host-computer-for-debugging-the-sharks-cove-board"></a><span id="Setting_up_a_Host_Computer_for_debugging_the_Sharks_Cove_board"></span><span id="setting_up_a_host_computer_for_debugging_the_sharks_cove_board"></span><span id="SETTING_UP_A_HOST_COMPUTER_FOR_DEBUGGING_THE_SHARKS_COVE_BOARD"></span>サメ Cove 掲示板をデバッグするためのホスト コンピューターをセットアップします。


1.  ホスト コンピューターでは、デバイス マネージャーを開きます。 **ビュー** ] メニューの [選択**デバイスの種類によって**します。

2.  サメ Cove ボードには、デバッグのコネクタを見つけます。 これは、次の図に示すように、マイクロ USB コネクタです。

    ![表示される画像サメ cove ボードのコネクタをデバッグします。](images/sharkscovedebugconnector.png)

3.  USB 2.0 ケーブルを使用して、サメ cove ボード上のデバッグ コネクタにホスト コンピューターを接続します。

4.  デバイス マネージャーで、ホスト コンピューターで 2 つの COM ポートが列挙を取得します。 最も番号が付いた COM ポートを選択します。 **ビュー** ] メニューの [選択**接続によってデバイス**します。 COM ポートが USB ホスト コント ローラーのいずれかで表示されていることを確認します。

    ![デバイス マネージャーでの com ポートを表示する画面の表示](images/serialoverusb01.png)

    COM ポートの番号をメモしてをおきます。 これは、USB ホスト コント ローラーのノード下に表示される最小の COM ポート番号です。 たとえば、上記のスクリーン ショットでは、USB ホスト コント ローラーで最下位の COM ポート番号は COM3 です。 デバッグ セッションを開始するときに、この COM ポート番号を後で必要があります。 COM ポートのドライバーがインストールされていない場合、COM ポート ノードを右クリックし、選択**ドライバーの更新**します。 選び**更新されたドライバー ソフトウェアを自動的に検索**します。 これは、インターネット接続を必要があります。

## <a name="span-idsettingupthesharkscoveboardasthetargetcomputerspanspan-idsettingupthesharkscoveboardasthetargetcomputerspanspan-idsettingupthesharkscoveboardasthetargetcomputerspansetting-up-the-sharks-cove-board-as-the-target-computer"></a><span id="Setting_Up_the_Sharks_Cove_Board_as_the_Target_Computer"></span><span id="setting_up_the_sharks_cove_board_as_the_target_computer"></span><span id="SETTING_UP_THE_SHARKS_COVE_BOARD_AS_THE_TARGET_COMPUTER"></span>対象コンピュータとしてサメ Cove ボードの設定

> [!IMPORTANT]
> BCDEdit を使用してブート情報を変更する前に、テスト用のコンピューターの BitLocker とセキュア ブートなどの Windows セキュリティ機能を一時的に中断する必要があります。
> テストが完了すると、これらのセキュリティ機能を再度有効にし、適切なセキュリティ機能を無効にするテスト PC を管理します。

1.  ターゲット コンピューター (サメ Cove ボード) で、管理者は、コマンド プロンプト ウィンドウを開きこれらのコマンドを入力します。

    **bcdedit /debug on**

    **bcdedit/dbgsettings シリアル debugport:1 baudrate:115200**

2.  ターゲット コンピューターを再起動します。

## <a name="span-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>デバッグ セッションの開始


### <a name="span-idusingwindbgspanspan-idusingwindbgspanspan-idusingwindbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>WinDbg を使用します。

ホスト コンピューターでは、WinDbg を開きます。 **ファイル**] メニューの [選択**カーネル デバッグ**します。 カーネル デバッグ ダイアログ ボックスで、開く、 **COM**タブ。**ボー レート**ボックスに、115200 を入力します。 **ポート**ボックスに、COM の入力*n*場所*n*は前にメモした COM ポート番号です。 **[OK]** をクリックします。

コマンド プロンプト ウィンドウで、次のコマンドを入力して、WinDbg でセッションを開始することもできます。*n*はホスト コンピューターでメモした COM ポートの数です。

**windbg -k com:port=COM**<em>n</em>**,baud=115200**

### <a name="span-idusingkdspanspan-idusingkdspanspan-idusingkdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>KD を使用します。

ホスト コンピューターでは、コマンド プロンプト ウィンドウを開き、次のコマンドを入力して、 *n*前にメモした COM ポート番号します。

**kd-k com:port COM を =**<em>n</em>**ボー = 115200**

## <a name="span-idusingenvironmentvariablesspanspan-idusingenvironmentvariablesspanspan-idusingenvironmentvariablesspanusing-environment-variables"></a><span id="Using_Environment_Variables"></span><span id="using_environment_variables"></span><span id="USING_ENVIRONMENT_VARIABLES"></span>環境変数の使用


ホスト コンピューターでは、COM ポートとボー レートを指定するのに環境変数を使用することができます。 デバッグ セッションを起動するたびにポートとボー レートを指定する必要はありません。 環境変数を使用して、COM ポートとボー レートを指定、コマンド プロンプト ウィンドウを開き、次のコマンドを入力する場所*n*は先ほど確認した番号の COM ポート番号です。

-   **設定\_NT\_デバッグ\_ポート COM を = * * * n*
-   **設定\_NT\_デバッグ\_ボー\_レート 115200 を =**

デバッグ セッションを開始するには、コマンド プロンプト ウィンドウを開き、次のコマンドのいずれかを入力します。

-   **kd**
-   **windbg**

## <a name="span-idtroubleshootingtipsforserialdebuggingoverausbcablespanspan-idtroubleshootingtipsforserialdebuggingoverausbcablespanspan-idtroubleshootingtipsforserialdebuggingoverausbcablespantroubleshooting-tips-for-serial-debugging-over-a-usb-cable"></a><span id="Troubleshooting_Tips_for_Serial_Debugging_over_a_USB_Cable"></span><span id="troubleshooting_tips_for_serial_debugging_over_a_usb_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_SERIAL_DEBUGGING_OVER_A_USB_CABLE"></span>USB ケーブルを介してシリアル デバッグのトラブルシューティングのヒント


### <a name="span-idspecifycorrectcomportonbothhostandtargetspanspan-idspecifycorrectcomportonbothhostandtargetspanspan-idspecifycorrectcomportonbothhostandtargetspanspecify-correct-com-port-on-both-host-and-target"></a><span id="Specify_correct_COM_port_on_both_host_and_target"></span><span id="specify_correct_com_port_on_both_host_and_target"></span><span id="SPECIFY_CORRECT_COM_PORT_ON_BOTH_HOST_AND_TARGET"></span>ホストとターゲットの両方で適切な COM ポートを指定します。

ターゲット コンピューター (サメ Cove ボード) でのデバッグで COM1 を使用していることを確認します。 管理者は、コマンド プロンプト ウィンドウを開き、入力**bcdedit/dbgsettings**します。 出力**bcdedit**表示`debugport 1`します。

ホスト コンピューターには、デバッガーまたは環境変数を設定すると起動すると、適切な COM ポートを指定します。 これは、最も番号が COM ポート デバイス マネージャーで USB ホスト コント ローラーの下に列挙されました。 たとえば、COM3 が目的のポートの場合を使用して、次のいずれかの COM ポートを指定します。

-   カーネル デバッグ ダイアログ ボックスで、WinDbg で入力で COM3、**ポート**ボックス。
-   **windbg-k com:port COM3 = しています.**
-   **kd-k com:port COM3 = しています.**
-   **設定\_NT\_デバッグ\_ポート COM3 を =**

### <a name="span-idbaudratemustbethesameonhostandtargetspanspan-idbaudratemustbethesameonhostandtargetspanspan-idbaudratemustbethesameonhostandtargetspanbaud-rate-must-be-the-same-on-host-and-target"></a><span id="Baud_rate_must_be_the_same_on_host_and_target"></span><span id="baud_rate_must_be_the_same_on_host_and_target"></span><span id="BAUD_RATE_MUST_BE_THE_SAME_ON_HOST_AND_TARGET"></span>ボー レートには、同じホストとターゲットである必要があります。

ボー レートは、ホストとターゲットの両方のコンピューターで 115200 である必要があります。

ターゲット コンピューター (サメ Cove ボード) で、管理者としてコマンド プロンプト ウィンドウを開きし、入力**bcdedit/dbgsettings**します。 出力**bcdedit**表示`baudrate 115200`します。

ホスト コンピューターには、デバッガーまたは環境変数を設定すると起動すると、適切なボー レートを指定します。 次のメソッドのいずれかを使用して、115200 のボー レートを指定します。

-   カーネル デバッグ ダイアログ ボックスで、WinDbg で入力で 115200、**ボー レート**ボックス。
-   **windbg -k ..., baud=115200**
-   **kd -k ..., baud=115200**
-   **設定\_NT\_デバッグ\_ボー\_レート 115200 を =**

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


完全なドキュメントについて、 **bcdedit**コマンドを Windows Driver Kit (WDK) ドキュメントで、ドライバーのテストおよびデバッグのブート オプションを参照してください。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[カーネル モードのデバッグを手動での設定](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

 

 






