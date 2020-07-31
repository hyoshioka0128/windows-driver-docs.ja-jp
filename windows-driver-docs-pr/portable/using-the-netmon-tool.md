---
Description: ネットワークモニターツール (NetMon.exe) は、WPD コンポーネントからのトレースを表示するために使用できる Windows ベースのアプリケーションです。
title: Network Monitor Tool の使用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3270b86853196087d49b90ab1d5fad869c35337
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402305"
---
# <a name="using-the-network-monitor-tool"></a>Network Monitor Tool の使用

ネットワークモニターツール (*NetMon.exe*) は、WPD コンポーネントからのトレースを表示するために使用できる Windows ベースのアプリケーションです。 このツールを使用すると*WpdMon.exe*が置き換えられ、Windows 8 の WPD トレースを収集して表示する新しい手段が提供されます。

## <a name="installing-and-configuring-netmonexe"></a>NetMon.exe のインストールと構成

ネットワークモニターツールをインストールして構成するには、次の手順を実行します。

1. [*NetMon.exe*](https://go.microsoft.com/fwlink/p/?linkid=248501)をダウンロードしてインストールします。
2. [Windows Driver Kit を](https://go.microsoft.com/fwlink/p/?linkid=178709)ダウンロードしてインストールします。
3. *管理者*権限を持つ*Powershell.exe*のインスタンスを起動し、次の一連のコマンドを実行して、開発用コンピューターに WPD パーサーをインストールします。
   1. PowerShell-Set-executionpolicy RemoteSigned
   2. cd " \\ Program Files (x86) \\ Windows kit \\ 8.0 \\ Tools \\ x86 \\ ネットワークモニターパーサー \\ usb"
   3. ..\\NplAutoProfile.ps1
   4. cd.. \\wpd
   5. ..\\NplAutoProfile.ps1 **Note**    、WPD パーサーは Windows Driver Kit に含まれています。

4. [ツール]/[オプション] ダイアログボックスを使用して*NetMon.exe*オプションを構成します。
   1. **[全般**] タブで、[**フレームの概要で固定幅のフォントを使用する**] チェックボックスをオンにします。
   2. [**色のルール**] タブで、[**開く**] を選択し、[ \\ Program Files (x86) \\ Windows kit \\ 8.0 \\ Tools \\ x86 \\ ネットワークモニターパーサー \\ wpd \\ wpd. nmcr] を選択します。 [**開く**] をクリックし、[OK] をクリックし**ます。**

これらの手順を完了すると、 *NetMon.exe*は、WPD トレースファイルを調べる準備が整います。 トレースの収集を開始するには、次のセクション「トレースの収集」に記載されている手順に従います。

## <a name="collecting-traces"></a>トレースの収集

トレースを生成するには、コマンドスクリプトを作成する必要があります。 次の内容をテキストファイルにコピーし、.cmd ファイル名拡張子を付けて保存します。

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

コマンドファイルを作成したら、管理者特権のコマンドセッションから Windows 8 コンピューターで実行します。

サンプルコマンドファイルの内容を使用した場合、トレースは、ファイル wpd トレースに格納され \_ ます。

## <a name="viewing-traces"></a>トレースの表示

トレースを表示するには、 *NetMon.exe*を起動し、[ファイル]、[開く]、[キャプチャ] メニューの順に選択して、上で収集した wpd \_ トレースの .etl ファイルを開きます。 トレースファイルを開くと、NetMon.exe がさまざまなレイヤーにトレースを表示することがわかります。

- WPDAPI – wpd API レベルの情報を WPD コマンドと応答と共に表示します
- WPDMTP – mtp のコマンドと応答を使用して、MTP レベルの情報を表示します。
- Transport (WPDMTPUS または WPDMTPIP または WPDMTPBT) –トランスポートレベルのパケットを表示します。

次の図は、API レベルでの WPDAPI 要求を示しています。 要求は、トランスポートに到着してからバブルアップする MTP 要求の形式で WPDMTP を経由します。

![トレースの表示](images/framesummary1.png)

- トランスポートレベルのログ記録では、データフェーズ中に実際のデータはログに記録されません。 **GetDeviceInfo**や**SendObjectPropList**などのコマンドで送受信されたデータセットの wpdmtp 応答メッセージを確認します。
- [**フレームの概要**] ウィンドウで WPDMTP 応答行をクリックすると、対応する項目が [**フレームの詳細**] ウィンドウに展開されます。
- [**フレームの詳細**] ウィンドウで [+] をクリックして、さらに展開し、探索します。 MTP 操作に dataphase がある場合、デバイスから受信したデータセットは WPDMTP 応答項目の**DataSetOfDataPhase**フィールドに表示されます。

![トレースの表示](images/framedetails1.png)

- 項目をクリックして展開すると、[**フレームの詳細**] ウィンドウには、WPD/MTP のわかりやすいメッセージが表示されます。 WPD パーサーを記述するときの規則は、ヘッダーレベルで詳細の概要を確認できることを示しています。 たとえば、GetServiceCapabilities 呼び出しでは、 **DataSetOfDataPhase**フィールドの横に、そのデータセット内の形式の数が表示されます。
- [**フレームの概要**] ウィンドウで、**変換元**と**変換先**の列を削除してわかりやすくすることができます。
- [**フレームの詳細**] ウィンドウでフィールドをクリックすると、対応する値が [ **16 進の詳細**] ウィンドウで強調表示されます。

## <a name="filtering-with-netmonexe"></a>NetMon.exe を使用したフィルター処理

ネットワークモニターツールには、いくつかのフィルター処理機能が用意されています。

- MTP トレースのみを表示するには、[**フィルターの表示**] ウィンドウに「 **! wpdmtp** 」と入力し、[**適用**] をクリックします。
- ドライバーがエラーを返したケースをフィルター処理するには、次のようにします。
  - **表示フィルター**ウィンドウに「 **wpderror! = 0** 」と入力し、[**適用**] をクリックします。
- 特定のシナリオに対して、すべてのメソッド呼び出しをフィルター処理できます。 たとえば、次のフィルターは、GetServiceProperties のすべての呼び出しを取得します。

    WPDMTP。対応する Ingcommand。 MTPOpcode = = 0x9304

- 同様に、次のフィルターは同じメソッドの呼び出しを取得します。

    WPDMTP。対応する Ingcommand。 MTPOpcode = = MTP \_ オペコード \_ getserviceproperties
