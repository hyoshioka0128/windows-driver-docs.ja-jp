---
Description: The Network Monitor tool (NetMon.exe) is a Windows-based application that you can use to view traces from WPD components.
title: ネットワーク監視ツールを使用します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0de82fbc512572af5f18e1524fe032adbed34a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560601"
---
# <a name="using-the-network-monitor-tool"></a>ネットワーク監視ツールを使用します。


ネットワーク モニター ツール (*NetMon.exe*) WPD コンポーネントからトレースを表示するために使用できる Windows ベースのアプリケーションです。 代わりに、ツール*WpdMon.exe*の収集し、Windows 8 で WPD トレースを表示する新しい手段を提供します。

## <a name="span-idinstallingandconfiguringnetmonexespanspan-idinstallingandconfiguringnetmonexespaninstalling-and-configuring-netmonexe"></a><span id="installing_and_configuring_netmon.exe"></span><span id="INSTALLING_AND_CONFIGURING_NETMON.EXE"></span>インストールと構成 NetMon.exe


をインストールして、ネットワーク監視ツールを構成するには、次の手順を完了します。

1.  ダウンロードしてインストール*NetMon.exe*から[ここ](https://go.microsoft.com/fwlink/p/?linkid=248501)します。
2.  ダウンロードしてインストールから Windows Driver Kit[ここ](https://go.microsoft.com/fwlink/p/?linkid=178709)します。
3.  インスタンスを起動し、WPD パーサーを開発用コンピューターにインストール*Powershell.exe*で*管理者*アクセス許可と、次の一連のコマンドを実行します。
    1.  PowerShell - ExecutionPolicy RemoteSigned
    2.  cd"\\Program Files (x86)\\Windows キット\\8.0\\ツール\\x86\\ネットワーク モニター パーサー\\usb"
    3.  ..\\NplAutoProfile.ps1
    4.  cd.\\wpd
    5.  ..\\NplAutoProfile.ps1**注**  WPD パーサーは、Windows Driver Kit に含まれます。

         

4.  構成、 *NetMon.exe*ツール/オプション ダイアログを使用してオプション。
    1.  **全般** タブで、チェック、**フレーム概要で固定幅フォントを使用して**ボックス。
    2.  **色ルール** タブで、選択**オープン**選び\\Program Files (x86)\\Windows キット\\8.0\\ツール\\x86\\ネットワーク モニター パーサー\\wpd\\wpd.nmcr します。 をクリックして**オープン**、その後に**ok をクリックします。**

これらの手順が完了したら*NetMon.exe* WPD トレース ファイルを調査する準備ができました。 トレースの収集を開始するには、次のセクションでは、トレースの収集の設定を指示します。

## <a name="span-idcollectingtracesspanspan-idcollectingtracesspanspan-idcollectingtracesspancollecting-traces"></a><span id="Collecting_Traces"></span><span id="collecting_traces"></span><span id="COLLECTING_TRACES"></span>トレースの収集


トレースを生成するには、コマンドのスクリプトを作成する必要があります。 テキスト ファイルに以下をコピーし、.cmd のファイル名拡張子で保存します。

```cmd
echo off
@REM ---------------------------------------------------------------------------------------
@REM UNCOMMENT THE LOGMAN COMMANDS FOR THE FOLLOWING PROVIDERS AS REQUIRED
@REM Microsoft-Windows-WPD-API                 To log API traffic
@REM Microsoft-Windows-WPD-MTPClassDriver      To log MTP command, response and datasets
@REM Microsoft-Windows-WPD-MTPUS               To log USB traffic at WpdMtpUS layer
@REM Microsoft-Windows-WPD-MTPIP               To log IP traffic at WpdMtpIP layer
@REM Microsoft-Windows-WPD-MTPBT               To log BT traffic at WpdMtpBt layer
@REM Microsoft-Windows-USB-USBPORT             To log USB core layer traffic
@REM Microsoft-Windows-USB-USBHUB              To log USB core layer traffic
@REM ---------------------------------------------------------------------------------------

@REM Start Logging

logman start  -ets WPD -p Microsoft-Windows-WPD-API            -bs 100 -nb 128 640 -o wpd_trace.etl
logman update -ets WPD -p Microsoft-Windows-WPD-MTPClassDriver -bs 100 -nb 128 640
logman update -ets WPD -p Microsoft-Windows-WPD-MTPUS          -bs 100 -nb 128 640
logman update -ets WPD -p Microsoft-Windows-WPD-MTPIP          -bs 100 -nb 128 640
logman update -ets WPD -p Microsoft-Windows-WPD-MTPBT          -bs 100 -nb 128 640
logman update -ets WPD -p Microsoft-Windows-USB-USBPORT        -bs 100 -nb 128 640
logman update -ets WPD -p Microsoft-Windows-USB-USBHUB         -bs 100 -nb 128 640
logman update -ets WPD -p Microsoft-Windows-Kernel-IoTrace 0 2
echo. 
echo Please run your scenario now and
pause

@REM Stop logging
logman stop -ets WPD
```

コマンド ファイルを作成した後は、管理者特権のコマンド セッションから Windows 8 コンピューターに実行します。

サンプルのコマンド ファイルの内容を使用した場合、トレースは、ファイル wpd に格納されます\_trace.etl します。

## <a name="span-idviewingtracesspanspan-idviewingtracesspanspan-idviewingtracesspanviewing-traces"></a><span id="Viewing_Traces"></span><span id="viewing_traces"></span><span id="VIEWING_TRACES"></span>トレースの表示


トレースを表示する起動*NetMon.exe*では、ファイル/オープン/キャプチャ メニューを選択し、wpd を開く\_まで trace.etl ファイルに収集します。 トレース ファイルを開くと、NetMon.exe がさまざまなレイヤーで、トレースを表示することが表示されます。

-   WPDAPI – WPD コマンドと応答を使用して WPD API レベルから情報を表示します
-   WPDMTP – MTP コマンドと応答を使用して MTP レベルから情報を表示します
-   トランスポート (WPDMTPUS または WPDMTPIP または WPDMTPBT) – はトランスポートのレベルのパケットを示しています

次の図は、API レベルで WPDAPI 要求を示します。 トランスポートの到達をバブルアップし MTP 要求の形式で WPDMTP を通じて、要求が送信されます。

![トレースの表示](images/framesummary1.png)

-   トランスポート レベルのログ記録では、データ フェーズ中に、実際のデータは記録されません。 データセットのようなコマンドの中に送受信された WPDMTP 応答メッセージを調べ**GetDeviceInfo**または**SendObjectPropList**します。
-   WPDMTP 応答内の行をクリックすると、**フレーム概要** ウィンドウで、対応する項目が展開され、**フレーム詳細**ウィンドウ。
-   「+」の s をクリックして、**フレーム詳細**をさらに展開し、詳細ウィンドウ。 デバイスから受信するデータセットは MTP 操作、dataphase にされている場合、 **DataSetOfDataPhase** WPDMTP 応答項目のフィールド。

![トレースの表示](images/framedetails1.png)

-   項目を展開しを参照してください をクリックすることができます、**フレーム詳細**ウィンドウ WPD/MTP のわかりやすいメッセージが表示されます。 ヘッダーのレベルの詳細の概要を表示できるが WPD パーサーを作成する場合、規則の後にします。 GetServiceCapabilities 呼び出しなどで、 **DataSetOfDataPhase**フィールドの横に、そのデータセットの形式の数を示しています。
-   削除することができます、**ソース**と**先**内の列、**フレーム概要**明確さを向上させるためにウィンドウ
-   内のフィールドをクリックすると**フレーム詳細** ウィンドウで、対応する値が強調表示されて、 **16 進数の詳細**ウィンドウ。

## <a name="span-idfilteringwithnetmonexespanspan-idfilteringwithnetmonexespanfiltering-with-netmonexe"></a><span id="filtering_with_netmon.exe"></span><span id="FILTERING_WITH_NETMON.EXE"></span>NetMon.exe によるフィルター処理


ネットワーク監視ツールでは、いくつかのフィルター処理機能を提供します。

-   MTP トレースのみを表示するには、次のように入力します。 **! wpdmtp**で、**ディスプレイ フィルター**ウィンドウとクリック**適用**。
-   フィルター ドライバーにエラーが返される位置の場合。
    -   型**wpderror! = 0**で、**ディスプレイ フィルター**ウィンドウとクリック**適用**。
-   メソッドの呼び出し、特定のシナリオのすべてのフィルター処理することができます。 たとえば、次のフィルターでは、すべて GetServiceProperties への呼び出しの取得は。

    WPDMTP.CorrespondingCommand.MTPOpcode == 0x9304

-   同様に、次のフィルターは、同じメソッドの呼び出しを取得しました。

    WPDMTP.CorrespondingCommand.MTPOpcode == MTP\_OPCODE\_GETSERVICEPROPERTIES

 

 




