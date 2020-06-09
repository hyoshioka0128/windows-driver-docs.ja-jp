---
title: Visual Studio でのシリアル ケーブル経由でのカーネルモード デバッグの設定
description: Microsoft Visual Studio を使用すると、null モデムケーブルでカーネルモードのデバッグを設定して実行できます。
ms.assetid: 9E50AA5F-92A2-4360-BB21-A9D4F3E9CA83
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4beff264eeb3e478f999109ef7eb2ebe98593b21
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533915"
---
# <a name="span-iddebuggersetting_up_a_null-modem_cable_connection_in_visual_studiospansetting-up-kernel-mode-debugging-over-a-serial-cable-in-visual-studio"></a><span id="debugger.setting_up_a_null-modem_cable_connection_in_visual_studio"></span>Visual Studio でのシリアル ケーブル経由でのカーネルモード デバッグの設定

> [!IMPORTANT]
> この機能は、Windows 10 バージョン1507以降のバージョンの WDK では使用できません。
>

Microsoft Visual Studio を使用すると、null モデムケーブルでカーネルモードのデバッグを設定して実行できます。 ヌルモデムケーブルは、2つのシリアルポート間でデータを送信するように構成されているシリアルケーブルです。 ほとんどのコンピューターストアで使用できます。 ヌルモデムケーブルと標準シリアルケーブルを混同しないでください。 標準のシリアルケーブルでは、シリアルポートが相互に接続されません。 ヌルモデムケーブルを接続する方法の詳細については、「[ヌルモデムケーブル配線](#null-modem-cable-wiring)」を参照してください。

Visual Studio を使用してカーネルモードのデバッグを行うには、Visual Studio に Windows Driver Kit (WDK) が統合されている必要があります。 統合環境をインストールする方法の詳細については、「 [Visual Studio を使用したデバッグ](debugging-using-visual-studio.md)」を参照してください。

Visual Studio を使用してシリアルデバッグを設定する代わりに、手動でセットアップを行うこともできます。 詳細については、「[シリアルケーブル経由でカーネルモードのデバッグを手動で設定する](setting-up-a-null-modem-cable-connection.md)」を参照してください。

デバッガーを実行するコンピューターは*ホストコンピューター*と呼ばれ、デバッグ中のコンピューターは*ターゲットコンピューター*と呼ばれます。

## <a name="span-idconfiguring_the_host_and_target_computersspanspan-idconfiguring_the_host_and_target_computersspanspan-idconfiguring_the_host_and_target_computersspanconfiguring-the-host-and-target-computers"></a><span id="Configuring_the_host_and_target_computers"></span><span id="configuring_the_host_and_target_computers"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTERS"></span>ホストとターゲットコンピューターの構成


1.  「[ドライバーの展開およびテスト用にコンピューターをプロビジョニングする (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」の説明に従って、ホストとターゲットコンピューターの構成を開始します。
2.  ホストコンピューターの Visual Studio で、[コンピューターの構成] ダイアログボックスが表示されたら、[コンピューターのプロビジョニング] を選択し、[**デバッガーの設定**] を選択します。
3.  [**接続の種類**] で [**シリアル**] を選択します。

    ![[接続の種類]、[ターゲット名]、[バスパラメーター] の各フィールドの値を含むデバッガー設定の例を示すスクリーンショット](images/setupserialvs.png)

    [**ボーレート**] では、既定値をそのまま使用するか、使用するボーレートを入力します。 [**ポート**] には、ホストコンピューターでのデバッグに使用する COM ポートの名前を入力します。 [**ターゲットポート**] に、ターゲットコンピューターでデバッグに使用する COM ポートの名前を入力します。

4.  構成プロセスには数分かかり、対象のコンピューターが1回または2回自動的に再起動される場合があります。 プロセスが完了したら、[**完了**] をクリックします。

## <a name="span-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>デバッグセッションを開始しています


1.  [Null モデム] ケーブルを、ホストとターゲットコンピューターでデバッグ用に選択した COM ポートに接続します。
2.  ホストコンピューターで、Visual Studio の [**ツール**] メニューの [**プロセスにアタッチ**] をクリックします。
3.  [**トランスポート**] で、[ **Windows カーネルモードデバッガー**] を選択します。
4.  [**修飾子**] で、以前に構成したターゲットコンピューターの名前を選択します。
5.  **[アタッチ]** をクリックします。

## <a name="span-idtroubleshooting_tips_for_debugging_over_a_serial_cablespanspan-idtroubleshooting_tips_for_debugging_over_a_serial_cablespanspan-idtroubleshooting_tips_for_debugging_over_a_serial_cablespantroubleshooting-tips-for-debugging-over-a-serial-cable"></a><span id="Troubleshooting_Tips_for_Debugging_over_a_Serial_Cable"></span><span id="troubleshooting_tips_for_debugging_over_a_serial_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_A_SERIAL_CABLE"></span>シリアルケーブルを使用したデバッグのトラブルシューティングのヒント


### <a name="span-idspecify_correct_com_ports_and_baud_ratespanspan-idspecify_correct_com_ports_and_baud_ratespanspan-idspecify_correct_com_ports_and_baud_ratespanspecify-correct-com-ports-and-baud-rate"></a><span id="Specify_correct_COM_ports_and_baud_rate"></span><span id="specify_correct_com_ports_and_baud_rate"></span><span id="SPECIFY_CORRECT_COM_PORTS_AND_BAUD_RATE"></span>正しい COM ポートとボーレートを指定してください

ホストとターゲットコンピュータでデバッグに使用している COM ポートの番号を確認します。 たとえば、ヌルモデムケーブルがホストコンピューター上の COM1 に接続されていて、ターゲットコンピューター上に COM2 が接続されているとします。 また、115200のボーレートを選択したとします。

1.  ホスト コンピューター上の Visual Studio の **[ドライバー]** メニューで、 **[Test (テスト)] &gt; [Configure Computers (コンピューターの構成)]** の順に選びます。
2.  テストコンピューターの名前を選択し、[**次へ**] をクリックします。
3.  [**コンピューターのプロビジョニング**] を選択し、[デバッガーの設定] を選択します。 **[次へ]** をクリックします。
4.  ホストコンピューターで COM1 を使用している場合は、[**ポート**] に「com1」と入力します。 ターゲットコンピューターで COM2 を使用している場合は、[**ターゲットポート**] に「com2」と入力します。
5.  ボーレート115200を使用することを選択した場合は **、「115200**」と入力します。

管理者としてコマンドプロンプトウィンドウを開き、 **bcdedit/dbgsettings**を入力することで、ターゲットコンピューターの COM ポートとボーレートの設定を再確認できます。 ターゲットコンピューターで COM2 を使用していて、ボーレートが115200の場合、 **bcdedit**の出力にはとが表示され `debugport 2` `baudrate 115200` ます。

## <a name="span-idnull-modem-cable-wiringspanspan-idnull-modem-cable-wiringspannull-modem-cable-wiring"></a><span id="null-modem-cable-wiring"></span><span id="NULL-MODEM-CABLE-WIRING"></span>ヌルモデムケーブル配線


次の表は、ヌルモデムケーブルがどのように結線されるかを示しています。

### <a name="span-id9-pin_connectorspanspan-id9-pin_connectorspan9-pin-connector"></a><span id="9-pin_connector"></span><span id="9-PIN_CONNECTOR"></span>9-コネクタをピン留めする

| コネクタ1 | コネクタ2 | シグナル        |
|-------------|-------------|----------------|
| 2           | 3           | Tx-Rx        |
| 3           | 2           | Rx-Tx        |
| 7           | 8           | RTS-CTS      |
| 8           | 7           | CTS-RTS      |
| 4           | 1 + 6         | DTR-(CD + DSR) |
| 1 + 6         | 4           | (CD + DSR)-DTR |
| 5           | 5           | シグナルグラウンド  |

 

### <a name="span-id25-pin_connectorspanspan-id25-pin_connectorspan25-pin-connector"></a><span id="25-pin_connector"></span><span id="25-PIN_CONNECTOR"></span>25-コネクタをピン留めする

| コネクタ1 | コネクタ2 | シグナル       |
|-------------|-------------|---------------|
| 2           | 3           | Tx-Rx       |
| 3           | 2           | Rx-Tx       |
| 4           | 5           | RTS-CTS     |
| 5           | 4           | CTS-RTS     |
| 6           | 20          | DSR-DTR     |
| 20          | 6           | DTR-DSR     |
| 7           | 7           | シグナルグラウンド |

 

### <a name="span-idsignal_abbreviationsspanspan-idsignal_abbreviationsspanspan-idsignal_abbreviationsspansignal-abbreviations"></a><span id="Signal_Abbreviations"></span><span id="signal_abbreviations"></span><span id="SIGNAL_ABBREVIATIONS"></span>シグナルの省略形

| 省略形 | Signal              |
|--------------|---------------------|
| Tx           | データの送信       |
| Rx           | データの受信        |
| ハンドシェーク          | 送信要求     |
| CTS          | 送信をクリア       |
| 信号          | データターミナルの準備完了 |
| DSR          | データセットの準備完了      |
| CD           | キャリア検出      |

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Visual Studio でのカーネル モード デバッグの設定](setting-up-kernel-mode-debugging-in-visual-studio.md)

 

 






