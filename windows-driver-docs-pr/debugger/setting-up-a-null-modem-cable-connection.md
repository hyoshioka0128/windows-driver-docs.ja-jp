---
title: シリアル ケーブル経由のカーネルモード デバッグの手動設定
description: Windows 用デバッグツールは、ヌルモデムケーブルを使用したカーネルデバッグをサポートしています。
ms.assetid: f7311928-bab1-4692-8dd6-5e464dd7127a
keywords:
- セットアップ、デバッグケーブル接続を確立する
- ヌルモデムケーブル
- デバッグケーブル
- ケーブル接続
- ケーブル接続、デバッグ (ヌルモデム) ケーブル)
ms.date: 07/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: b4be0257b1750e1f04e1de2d9976181e7fd76f60
ms.sourcegitcommit: 0a31c9fa18d5bf02373e7c000abd65e3db78b280
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2020
ms.locfileid: "76910361"
---
# <a name="setting-up-kernel-mode-debugging-over-a-serial-cable-manually"></a>シリアル ケーブル経由のカーネルモード デバッグの手動設定

Windows 用デバッグツールは、ヌルモデムケーブルを使用したカーネルデバッグをサポートしています。 ヌルモデムケーブルは、2つのシリアルポート間でデータを送信するように構成されているシリアルケーブルです。 ヌルモデムケーブルと標準シリアルケーブルを混同しないでください。 標準のシリアルケーブルでは、シリアルポートが相互に接続されません。 ヌルモデムケーブルを接続する方法の詳細については、「[ヌルモデムケーブル配線](#null-modem-cable-wiring)」を参照してください。

デバッガーを実行するコンピューターは*ホストコンピューター*と呼ばれ、デバッグ中のコンピューターは*ターゲットコンピューター*と呼ばれます。

## <a name="span-idsetting_up_the_target_computerspanspan-idsetting_up_the_target_computerspanspan-idsetting_up_the_target_computerspansetting-up-the-target-computer"></a><span id="Setting_Up_the_Target_Computer"></span><span id="setting_up_the_target_computer"></span><span id="SETTING_UP_THE_TARGET_COMPUTER"></span>ターゲットコンピューターのセットアップ

> [!IMPORTANT]
> Bcdedit を使用してブート情報を変更する前に、テスト PC で BitLocker やセキュアブートなどの Windows のセキュリティ機能を一時的に停止することが必要になる場合があります。
> デバッグが完了し、カーネルデバッグを無効にした後、セキュアブートを再度有効にすることができます。  

1. ターゲットコンピューターで、管理者としてコマンドプロンプトウィンドウを開き、次のコマンドを入力します。ここで、 *n*はターゲットコンピューターでデバッグに使用される COM ポートの番号、 *rate*はデバッグに使用されるボーレートです。

   **bcdedit/debug on**

   **bcdedit/dbgsettings serial debugport:** <em>n</em> **ボーレート:** <em>レート</em>

   **メモ** ボーレートは、ホストコンピューターとターゲットコンピューターで同じである必要があります。 推奨されるレートは115200です。

2. ターゲット コンピューターを再起動します。

## <a name="span-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>デバッグセッションを開始しています

[Null モデム] ケーブルを、ホストとターゲットコンピューターでデバッグ用に選択した COM ポートに接続します。

### <a name="span-idusing_windbgspanspan-idusing_windbgspanspan-idusing_windbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>WinDbg の使用

ホストコンピューターで、[WinDbg] を開きます。 **[ファイル]** メニューの **[カーネルデバッグ]** をクリックします。 カーネルデバッグ ダイアログボックスで、 **COM** タブを開きます。**ボーレート** ボックスに、デバッグのために選択したレートを入力します。 **[ポート]** ボックスに「com*n* 」と入力します。ここで、 *n*はホストコンピューターでデバッグするために選択した com ポート番号です。 **[OK]** をクリックすると、

また、コマンドプロンプトウィンドウで次のコマンドを入力して、WinDbg を使用してセッションを開始することもできます。*n*はホストコンピューターでのデバッグに使用される COM ポートの番号で、 *rate*はデバッグに使用されるボーレートです。

**windbg-k com: port = com**<em>n</em> **、baud =** <em>rate</em>

### <a name="span-idusing_kdspanspan-idusing_kdspanspan-idusing_kdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>KD の使用

ホストコンピューターで、コマンドプロンプトウィンドウを開き、次のコマンドを入力します。ここで、 *n*はホストコンピューターでのデバッグに使用される COM ポートの番号、 *rate*はデバッグに使用されるボーレートです。

**kd-k com: port = com**<em>n</em> **、baud =** <em>rate</em>

## <a name="span-idusing_environment_variablesspanspan-idusing_environment_variablesspanspan-idusing_environment_variablesspanusing-environment-variables"></a><span id="Using_Environment_Variables"></span><span id="using_environment_variables"></span><span id="USING_ENVIRONMENT_VARIABLES"></span>環境変数の使用


ホストコンピューターでは、環境変数を使用して COM ポートとボーレートを指定できます。 その後、デバッグセッションを開始するたびに、ポートとボーレートを指定する必要はありません。 環境変数を使用して COM ポートとボーレートを指定するには、コマンドプロンプトウィンドウを開き、次のコマンドを入力します。ここで、 *n*はホストコンピューターでのデバッグに使用される COM ポートの番号、 *rate*はデバッグに使用されるボーレートです。

- **設定 \_NT\_デバッグ\_ポート = COM ** * * n
- **\_NT\_デバッグ\_ボー\_率 =** <em>レート</em>を設定します。

デバッグセッションを開始するには、コマンドプロンプトウィンドウを開き、次のいずれかのコマンドを入力します。

-   **kd**
-   **windbg**

## <a name="span-idtroubleshooting_tips_for_debugging_over_a_serial_cablespanspan-idtroubleshooting_tips_for_debugging_over_a_serial_cablespanspan-idtroubleshooting_tips_for_debugging_over_a_serial_cablespantroubleshooting-tips-for-debugging-over-a-serial-cable"></a><span id="Troubleshooting_Tips_for_Debugging_over_a_Serial_Cable"></span><span id="troubleshooting_tips_for_debugging_over_a_serial_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_A_SERIAL_CABLE"></span>シリアルケーブルを使用したデバッグのトラブルシューティングのヒント


### <a name="span-idspecify_correct_com_port_on_both_host_and_targetspanspan-idspecify_correct_com_port_on_both_host_and_targetspanspan-idspecify_correct_com_port_on_both_host_and_targetspanspecify-correct-com-port-on-both-host-and-target"></a><span id="Specify_correct_COM_port_on_both_host_and_target"></span><span id="specify_correct_com_port_on_both_host_and_target"></span><span id="SPECIFY_CORRECT_COM_PORT_ON_BOTH_HOST_AND_TARGET"></span>ホストとターゲットの両方で正しい COM ポートを指定してください

ホストとターゲットコンピュータでデバッグに使用している COM ポートの番号を確認します。 たとえば、ヌルモデムケーブルがホストコンピューター上の COM1 に接続されていて、ターゲットコンピューター上に COM2 が接続されているとします。

ターゲットコンピューターで、管理者としてコマンドプロンプトウィンドウを開き、「 **bcdedit/dbgsettings**」と入力します。 ターゲットコンピューターで COM2 を使用している場合は、 **bcdedit**の出力に `debugport 2`が表示されます。

ホストコンピューターで、デバッガーを起動するとき、または環境変数を設定するときに、正しい COM ポートを指定します。 ホストコンピューターで COM1 を使用している場合は、次のいずれかの方法を使用して COM ポートを指定します。

-   WinDbg の カーネルデバッグ ダイアログボックスで、**ポート** ボックスに「COM1」と入力します。
-   **windbg-k com: port = COM1,...**
-   **kd-k com: port = COM1,...**
-   **\_NT\_デバッグ\_ポート = COM1 に設定します。**

### <a name="span-idbaud_rate_must_be_the_same_on_host_and_targetspanspan-idbaud_rate_must_be_the_same_on_host_and_targetspanspan-idbaud_rate_must_be_the_same_on_host_and_targetspanbaud-rate-must-be-the-same-on-host-and-target"></a><span id="Baud_rate_must_be_the_same_on_host_and_target"></span><span id="baud_rate_must_be_the_same_on_host_and_target"></span><span id="BAUD_RATE_MUST_BE_THE_SAME_ON_HOST_AND_TARGET"></span>ホストとターゲットのボーレートは同じである必要があります

シリアルケーブルでのデバッグに使用するボーレートは、ホストコンピューターとターゲットコンピューターで同じ値に設定する必要があります。 たとえば、115200のボーレートを選択したとします。

ターゲットコンピューターで、管理者としてコマンドプロンプトウィンドウを開き、「 **bcdedit/dbgsettings**」と入力します。 **Bcdedit**の出力に `baudrate 115200`が表示されます。

ホストコンピューターで、デバッガーを起動するとき、または環境変数を設定するときに、適切なボーレートを指定します。 次のいずれかの方法を使用して、115200のボーレートを指定します。

-   WinDbg の カーネルデバッグ ダイアログボックスで、**ボーレート** ボックスに「115200」と入力します。
-   **windbg-k...、baud = 115200**
-   **kd-k...、baud = 115200**
-   **\_NT\_デバッグ\_ボー\_率 = 115200 に設定します。**

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

 

## <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

**Bcdedit**コマンドの完全なドキュメントについては、「 [bcdedit Options Reference](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcd-boot-options-reference)」を参照してください。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[カーネルモードデバッグの手動設定](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)
