---
title: Visual Studio でのシリアル ケーブル経由でのカーネル モードのデバッグのセットアップ
description: Microsoft Visual Studio を使用して、設定し、ヌル モデム ケーブル経由でのカーネル モードのデバッグを実行することができます。
ms.assetid: 9E50AA5F-92A2-4360-BB21-A9D4F3E9CA83
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 368ebc2681fce48dc5ef26a11538515be7fda63f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529706"
---
# <a name="span-iddebuggersettingupanull-modemcableconnectioninvisualstudiospansetting-up-kernel-mode-debugging-over-a-serial-cable-in-visual-studio"></a><span id="debugger.setting_up_a_null-modem_cable_connection_in_visual_studio"></span>Visual Studio でのシリアル ケーブル経由でのカーネル モードのデバッグのセットアップ

> [!IMPORTANT]
> この機能は、Windows 10 バージョン 1507、以降のバージョンの WDK でご利用いただけません。
>

Microsoft Visual Studio を使用して、設定し、ヌル モデム ケーブル経由でのカーネル モードのデバッグを実行することができます。 ヌル モデム ケーブルは、2 つのシリアル ポートの間でデータを送信するように構成されているシリアル ケーブルです。 これらは、ほとんどのコンピューター ストアで使用できます。 標準のシリアル ケーブルでヌル モデム ケーブルを混同しないでください。 標準のシリアル ケーブルは、互いにシリアル ポートを接続できません。 方法については、ヌル モデム ケーブルはワイヤード (有線) を参照してください[ヌル モデム ケーブル配線](#null-modem-cable-wiring)します。

カーネル モードのデバッグを Visual Studio を使用するには、Windows Driver Kit (WDK) の Visual Studio と統合が必要です。 統合環境をインストールする方法については、次を参照してください。 [Windows ドライバー開発](https://go.microsoft.com/fwlink/p?linkid=301383)します。

Visual Studio を使用してシリアル デバッグを設定する代わりに、セットアップを手動で行うことができます。 詳細については、次を参照してください。[カーネル モード デバッグのセットアップをシリアル ケーブルを手動で](setting-up-a-null-modem-cable-connection.md)します。

デバッガーを実行しているコンピューターが呼び出されます、*ホスト コンピューター*、デバッグ中のコンピューターを呼び出すと、*対象のコンピュータ*します。

## <a name="span-idconfiguringthehostandtargetcomputersspanspan-idconfiguringthehostandtargetcomputersspanspan-idconfiguringthehostandtargetcomputersspanconfiguring-the-host-and-target-computers"></a><span id="Configuring_the_host_and_target_computers"></span><span id="configuring_the_host_and_target_computers"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTERS"></span>ホストおよびターゲット コンピュータの構成


1.  」の説明に従って、ホストとターゲット コンピューターの構成を開始[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8.1)](https://msdn.microsoft.com/library/windows/hardware/dn745909)します。
2.  Visual Studio で、ホスト コンピューターで、コンピューターの構成 ダイアログ ボックスのような場合が選択**コンピューターをプロビジョニングし、デバッガーの設定を選択**します。
3.  **接続の種類**、選択**シリアル**します。

    ![スクリーン ショットのデバッガーの例を次のフィールドの値の設定を示す: 接続の種類、ターゲットの名前、およびバス パラメーター](images/setupserialvs.png)

    **ボー レート**既定値を受け入れるか、使用するボー レートを入力します。 **ポート**、ホスト コンピューターでデバッグするために使用する COM ポートの名前を入力します。 **ターゲット ポート**、ターゲット コンピューターでデバッグするために使用する COM ポートの名前を入力します。

4.  構成プロセスには数分かかりますが自動的に、コンピューターを再起動ターゲットまたは 2 回。 プロセスが完了したら、クリックして**完了**します。

## <a name="span-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>デバッグ セッションの開始


1.  ホストおよびターゲット コンピューターでのデバッグ用に選択した COM ポートには、ヌル モデム ケーブルを接続します。
2.  Visual Studio で、ホスト コンピューター上で、**ツール**] メニューの [選択**プロセスにアタッチ**します。
3.  **トランスポート**、選択**Windows カーネル モードのデバッガー**します。
4.  **修飾子**、以前に構成されているターゲット コンピューターの名前を選択します。
5.  クリックして**アタッチ**します。

## <a name="span-idtroubleshootingtipsfordebuggingoveraserialcablespanspan-idtroubleshootingtipsfordebuggingoveraserialcablespanspan-idtroubleshootingtipsfordebuggingoveraserialcablespantroubleshooting-tips-for-debugging-over-a-serial-cable"></a><span id="Troubleshooting_Tips_for_Debugging_over_a_Serial_Cable"></span><span id="troubleshooting_tips_for_debugging_over_a_serial_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_A_SERIAL_CABLE"></span>シリアル ケーブル経由でのデバッグのトラブルシューティングのヒント


### <a name="span-idspecifycorrectcomportsandbaudratespanspan-idspecifycorrectcomportsandbaudratespanspan-idspecifycorrectcomportsandbaudratespanspecify-correct-com-ports-and-baud-rate"></a><span id="Specify_correct_COM_ports_and_baud_rate"></span><span id="specify_correct_com_ports_and_baud_rate"></span><span id="SPECIFY_CORRECT_COM_PORTS_AND_BAUD_RATE"></span>適切な COM ポートとボー レートを指定します。

ホストとターゲットのコンピューターでデバッグを使用する COM ポートの数を決定します。 たとえば、ターゲット コンピューター上にホスト コンピューターと COM2 で COM1 に接続されて、ヌル モデム ケーブルがあるとします。 また、115200 のボー レートを選択したとします。

1.  ホスト コンピューター上の Visual Studio の **[ドライバー]** メニューで、**[Test (テスト)] &gt; [Configure Computers (コンピューターの構成)]** の順に選びます。
2.  テスト用コンピューターの名前を選択し、クリックして**次**します。
3.  選択**コンピューターをプロビジョニングし、デバッガーの設定を選択**します。 **[次へ]** をクリックします。
4.  使用するかどうか COM1、ホスト コンピューター上の**ポート**com1 を入力します。 使用するかどうか COM2 対象のコンピューターの**ターゲット ポート**com2 を入力します。
5.  かどうかは、115200 のボー レートを使用した**ボー レート**115200 を入力します。

管理者としてコマンド プロンプト ウィンドウを開き、入力して、ターゲット コンピューター上に再確認 COM ポートとボー レートの設定をできます**bcdedit/dbgsettings**します。 対象のコンピュータと 115200 の出力のボー レートを COM2 を使用している場合**bcdedit**表示する必要があります`debugport 2`と`baudrate 115200`します。

## <a name="span-idnull-modem-cable-wiringspanspan-idnull-modem-cable-wiringspannull-modem-cable-wiring"></a><span id="null-modem-cable-wiring"></span><span id="NULL-MODEM-CABLE-WIRING"></span>ヌル モデム ケーブルを配線


次の表にどのようにヌル モデム ケーブルを接続します。

### <a name="span-id9-pinconnectorspanspan-id9-pinconnectorspan9-pin-connector"></a><span id="9-pin_connector"></span><span id="9-PIN_CONNECTOR"></span>9 ピンのコネクタ

| コネクタ 1 | コネクタ 2 | 信号        |
|-------------|-------------|----------------|
| 2           | 3           | Tx - Rx        |
| 3           | 2           | Rx - Tx        |
| 7           | 8           | RTS - CTS      |
| 8           | 7           | CTS - RTS      |
| 4           | 1+6         | DTR - (CD + DSR) |
| 1+6         | 4           | (CD + DSR) - DTR |
| 5           | 5           | シグナル地上  |

 

### <a name="span-id25-pinconnectorspanspan-id25-pinconnectorspan25-pin-connector"></a><span id="25-pin_connector"></span><span id="25-PIN_CONNECTOR"></span>25 ピンのコネクタ

| コネクタ 1 | コネクタ 2 | 信号       |
|-------------|-------------|---------------|
| 2           | 3           | Tx - Rx       |
| 3           | 2           | Rx - Tx       |
| 4           | 5           | RTS - CTS     |
| 5           | 4           | CTS - RTS     |
| 6           | 20          | DSR - DTR     |
| 20          | 6           | DTR - DSR     |
| 7           | 7           | シグナル地上 |

 

### <a name="span-idsignalabbreviationsspanspan-idsignalabbreviationsspanspan-idsignalabbreviationsspansignal-abbreviations"></a><span id="Signal_Abbreviations"></span><span id="signal_abbreviations"></span><span id="SIGNAL_ABBREVIATIONS"></span>シグナルの省略形

| 省略形 | シグナル              |
|--------------|---------------------|
| テキサス州           | データを送信します。       |
| Rx           | データの受信        |
| RTS          | 要求の送信     |
| テクニカル サポート          | オフにすると、送信       |
| DTR          | ターミナルのデータを準備します。 |
| DSR          | データ セットが準備完了      |
| CD           | 通信事業者を検出します。      |

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Visual Studio でのカーネル モード デバッグのセットアップ](setting-up-kernel-mode-debugging-in-visual-studio.md)

 

 






