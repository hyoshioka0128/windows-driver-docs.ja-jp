---
title: シリアル ケーブル経由のカーネルモード デバッグの手動設定
description: デバッグ ツールの Windows カーネルのヌル モデム ケーブルを介してデバッグをサポートします。
ms.assetid: f7311928-bab1-4692-8dd6-5e464dd7127a
keywords:
- デバッグのケーブル接続のセットアップ
- ヌル モデム ケーブル
- デバッグ ケーブル
- ケーブルの接続
- ケーブル接続のデバッグ (null モデム) ケーブル)
ms.date: 07/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3d46ae155ae7a2b8ec69b8f79ee0f0232776b074
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570779"
---
# <a name="setting-up-kernel-mode-debugging-over-a-serial-cable-manually"></a>シリアル ケーブル経由のカーネルモード デバッグの手動設定


デバッグ ツールの Windows カーネルのヌル モデム ケーブルを介してデバッグをサポートします。 ヌル モデム ケーブルは、2 つのシリアル ポートの間でデータを送信するように構成されているシリアル ケーブルです。 これらは、ほとんどのコンピューター ストアで使用できます。 標準のシリアル ケーブルでヌル モデム ケーブルを混同しないでください。 標準のシリアル ケーブルは、互いにシリアル ポートを接続できません。 方法については、ヌル モデム ケーブルはワイヤード (有線) を参照してください[ヌル モデム ケーブル配線](#null-modem-cable-wiring)します。

デバッガーを実行しているコンピューターが呼び出されます、*ホスト コンピューター*、デバッグ中のコンピューターを呼び出すと、*対象のコンピュータ*します。

## <a name="span-idsettingupthetargetcomputerspanspan-idsettingupthetargetcomputerspanspan-idsettingupthetargetcomputerspansetting-up-the-target-computer"></a><span id="Setting_Up_the_Target_Computer"></span><span id="setting_up_the_target_computer"></span><span id="SETTING_UP_THE_TARGET_COMPUTER"></span>ターゲット コンピューターをセットアップします。


> [!IMPORTANT]
> Bcdedit を使用してブート情報を変更する前に、テスト用のコンピューターの BitLocker とセキュア ブートなどの Windows セキュリティ機能を一時的に中断する必要があります。 セキュア ブートは、再度有効に完了したらとデバッグは無効になりましたカーネル デバッグします。  


1. 対象のコンピューターに管理者としてコマンド プロンプト ウィンドウを開くし、次のコマンドを入力場所*n* 、対象のコンピューターでデバッグするために使用する COM ポートの番号と*レート*は、ボー レートがデバッグに使用します。

   **bcdedit /debug on**

   **bcdedit/dbgsettings シリアル debugport:**<em>n</em> **baudrate:**<em>レート</em>

   **注**ボー レートには、ホスト コンピューターと対象のコンピュータで同じである必要があります。 推奨されるレートは、115200 です。

     

2. ターゲット コンピューターを再起動します。

## <a name="span-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>デバッグ セッションの開始


ホストおよびターゲット コンピューターでのデバッグ用に選択した COM ポートには、ヌル モデム ケーブルを接続します。

### <a name="span-idusingwindbgspanspan-idusingwindbgspanspan-idusingwindbgspanusing-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>WinDbg を使用します。

ホスト コンピューターでは、WinDbg を開きます。 **ファイル**] メニューの [選択**カーネル デバッグ**します。 カーネル デバッグ ダイアログ ボックスで、開く、 **COM**タブ。**ボー レート**ボックスに、デバッグ用に選択した割合を入力します。 **ポート**ボックスに、COM の入力*n*場所*n*はホスト コンピューターでのデバッグ用に選択した COM ポート番号です。 **[OK]** をクリックします。

コマンド プロンプト ウィンドウで、次のコマンドを入力して、WinDbg でセッションを開始することもできます。*n* 、ホスト コンピューターでデバッグするために使用する COM ポートの番号と*レート*ボー レートをデバッグするためには。

**windbg -k com:port=COM**<em>n</em>**,baud=**<em>rate</em>

### <a name="span-idusingkdspanspan-idusingkdspanspan-idusingkdspanusing-kd"></a><span id="Using_KD"></span><span id="using_kd"></span><span id="USING_KD"></span>KD を使用します。

ホスト コンピューターでは、コマンド プロンプト ウィンドウを開き、次のコマンドを入力して場所*n* 、ホスト コンピューターでデバッグするために使用する COM ポートの数と*レート*ボー レートを使用デバッグ。

**kd-k com:port COM を =**<em>n</em>**、ボー =**<em>レート</em>

## <a name="span-idusingenvironmentvariablesspanspan-idusingenvironmentvariablesspanspan-idusingenvironmentvariablesspanusing-environment-variables"></a><span id="Using_Environment_Variables"></span><span id="using_environment_variables"></span><span id="USING_ENVIRONMENT_VARIABLES"></span>環境変数の使用


ホスト コンピューターでは、COM ポートとボー レートを指定するのに環境変数を使用することができます。 デバッグ セッションを起動するたびにポートとボー レートを指定する必要はありません。 環境変数を使用して、COM ポートとボー レートを指定、コマンド プロンプト ウィンドウを開き、次のコマンドを入力する場所*n* 、ホスト コンピューターでデバッグするために使用する COM ポートの番号と*レート*ボー レートをデバッグするためには。

- **設定\_NT\_デバッグ\_ポート COM を = * * * n*
- **設定\_NT\_デバッグ\_ボー\_率 =**<em>レート</em>

デバッグ セッションを開始するには、コマンド プロンプト ウィンドウを開き、次のコマンドのいずれかを入力します。

-   **kd**
-   **windbg**

## <a name="span-idtroubleshootingtipsfordebuggingoveraserialcablespanspan-idtroubleshootingtipsfordebuggingoveraserialcablespanspan-idtroubleshootingtipsfordebuggingoveraserialcablespantroubleshooting-tips-for-debugging-over-a-serial-cable"></a><span id="Troubleshooting_Tips_for_Debugging_over_a_Serial_Cable"></span><span id="troubleshooting_tips_for_debugging_over_a_serial_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_A_SERIAL_CABLE"></span>シリアル ケーブル経由でのデバッグのトラブルシューティングのヒント


### <a name="span-idspecifycorrectcomportonbothhostandtargetspanspan-idspecifycorrectcomportonbothhostandtargetspanspan-idspecifycorrectcomportonbothhostandtargetspanspecify-correct-com-port-on-both-host-and-target"></a><span id="Specify_correct_COM_port_on_both_host_and_target"></span><span id="specify_correct_com_port_on_both_host_and_target"></span><span id="SPECIFY_CORRECT_COM_PORT_ON_BOTH_HOST_AND_TARGET"></span>ホストとターゲットの両方で適切な COM ポートを指定します。

ホストとターゲットのコンピューターでデバッグを使用する COM ポートの数を決定します。 たとえば、ターゲット コンピューター上にホスト コンピューターと COM2 で COM1 に接続されて、ヌル モデム ケーブルがあるとします。

対象のコンピューターに管理者としてコマンド プロンプト ウィンドウを開き、入力**bcdedit/dbgsettings**します。 対象のコンピューターの出力に COM2 を使用しているかどうかは**bcdedit**表示する必要があります`debugport 2`します。

ホスト コンピューターには、デバッガーまたは環境変数を設定すると起動すると、適切な COM ポートを指定します。 ホスト コンピューターで COM1 を使用する場合は、COM ポートを指定する、次のメソッドのいずれかを使用します。

-   カーネル デバッグ ダイアログ ボックスで、WinDbg で入力の COM1、**ポート**ボックス。
-   **windbg -k com:port=COM1, ...**
-   **kd-k com:port = COM1、.**
-   **設定\_NT\_デバッグ\_ポート COM1 を =**

### <a name="span-idbaudratemustbethesameonhostandtargetspanspan-idbaudratemustbethesameonhostandtargetspanspan-idbaudratemustbethesameonhostandtargetspanbaud-rate-must-be-the-same-on-host-and-target"></a><span id="Baud_rate_must_be_the_same_on_host_and_target"></span><span id="baud_rate_must_be_the_same_on_host_and_target"></span><span id="BAUD_RATE_MUST_BE_THE_SAME_ON_HOST_AND_TARGET"></span>ボー レートには、同じホストとターゲットである必要があります。

シリアル ケーブル経由でのデバッグに使用するボー レートは、ホストとターゲットのコンピューターで同じ値に設定する必要があります。 たとえば、115200 のボー レートを選択したとします。

対象のコンピューターに管理者としてコマンド プロンプト ウィンドウを開き、入力**bcdedit/dbgsettings**します。 出力**bcdedit**表示`baudrate 115200`します。

ホスト コンピューターには、デバッガーまたは環境変数を設定すると起動すると、適切なボー レートを指定します。 次のメソッドのいずれかを使用して、115200 のボー レートを指定します。

-   カーネル デバッグ ダイアログ ボックスで、WinDbg で入力で 115200、**ボー レート**ボックス。
-   **windbg -k ..., baud=115200**
-   **kd -k ..., baud=115200**
-   **設定\_NT\_デバッグ\_ボー\_レート 115200 を =**

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

 

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


完全なドキュメントについて、 **bcdedit**コマンドを Windows Driver Kit (WDK) ドキュメントで、ドライバーのテストおよびデバッグのブート オプションを参照してください。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[カーネル モードのデバッグを手動での設定](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

 

 






