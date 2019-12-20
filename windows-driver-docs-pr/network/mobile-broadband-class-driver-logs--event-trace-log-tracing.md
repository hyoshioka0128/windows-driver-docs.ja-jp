---
title: モバイルブロードバンドクラスドライバーログのイベントトレースログのトレース
description: このトピックでは、エンジニアがモバイルブロードバンドクラスドライバーのイベントトレースログを操作して、問題の確認とトラブルシューティングを行うのに役立つ情報を提供します。
ms.assetid: 9742BFCA-CC22-497A-B11F-D3E89F0B4FE6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33c3bf3f56f75ed2d3834c3fd139130bf92d446d
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210858"
---
# <a name="mobile-broadband-class-driver-logs-event-trace-log-tracing"></a>モバイルブロードバンドクラスドライバーログ: イベントトレースログトレース


このトピックでは、エンジニアがモバイルブロードバンドクラスドライバーのイベントトレースログを操作して、問題の確認とトラブルシューティングを行うのに役立つ情報を提供します。

このトピックの情報は、以下に適用されます。

-   Windows 8

## <a name="etl-tracing"></a>ETL トレース


次の手順では、イベントトレースログ (ETL) を確認する方法について説明します。

1.  [**開始**] をクリックして eventviewer を開き &gt; &gt; **EventVwr**を**実行**します。
2.  左側のウィンドウで、[**アプリケーションとサービスログ**] &gt; **Microsoft** &gt; **Windows**] の順に移動します。

    ![windows フォルダーに移動する手順を示すスクリーンショット](images/mbcdlogs1.png)

3.  [ **Windows** to **wmbclass] の下に移動します。**

    ![wmbclass フォルダーを開いています。 windows mobile ブロードバンドクラスドライバーチャネルが表示されています](images/mbcdlogs2.png)

4.  [ **Windows Mobile ブロードバンドクラスドライバーチャネル**] を右クリックし、[**ログの有効化**] をクリックします。 [ログの**無効化**] が表示されている場合は、ログは既に有効になっています。

    ![[ログと更新の有効化] オプションを示すショートカットメニューのスクリーンショット](images/mbcdlogs3.png)

5.  問題を再現し、[最新の状態に**更新**] をクリックします。 **更新**が完了すると、中央のウィンドウにログが表示されます。

    ![ログのスクリーンショット。イベントは上部ペインで選択されています。 下部のペインには [全般] タブが表示され、[説明] タブと [詳細] タブが選択されていません。](images/mbcdlogs4.png)

6.  右側の [**操作] ウィンドウ**を使用して、ログをフィルター処理できます。

    ![[操作] ウィンドウの [現在のログをフィルター] を使用すると、イベント id とイベントレベルでフィルター処理された現在のログが表示されます。 この場合、イベントレベルは error で、イベント id は-105 です。](images/mbcdlogs5.png)

## <a name="mobile-broadband-logs"></a>モバイルブロードバンドログ


問題とシナリオに応じて、次のような解決策を決定するためにさまざまな情報が必要になります。

**制御パス**

SMS の接続、送信、受信、USSD メッセージの送信または受信、プロファイルの使用に関する問題が発生した場合は、次の情報を収集してください。

1.  **netsh トレースの開始 wwan\_dbg**
2.  システムの予期しない動作につながるタスクを実行します
3.  **netsh トレースの停止**
4.  `%localappdata%\temp\nettraces\` の下のすべてのファイルをアップロードする

**IP 構成**

IP アドレスの構成に問題がある場合は、次の手順を実行してください。

1. **netsh トレースの開始 wwan\_dbg**
2. システムの予期しない動作につながるタスクを実行 &lt;
3. **netsh トレースの停止**
4. 次の情報をアップロードします。

    - `%localappdata%\temp\nettraces\` の下にあるすべてのファイル

    - **Ipconfig/all**の出力

**データパス**

データパケットの破棄、再試行、スループットの問題、または接続の制限に関連する問題のトラブルシューティングを行う場合は、次の手順を実行してください。

1.  **netsh trace start wwan\_dbg、InternetClient、nid\_wpp provider = {c5aa495b-8432-4de5-9d7c-8afc7d3b522a} 0xFFFFFFFF 255**
2.  モバイルブロードバンドアダプターで netmon トレースを開始します。
3.  システムの予期しない動作につながるタスクを実行します
4.  Netmon トレースを停止し、netmon キャプチャを保存します。
5.  **netsh トレースの停止**
6.  次の情報をアップロードします。
    -   `%localappdata%\temp\nettraces\` の下にあるすべてのファイル
    -   Netmon キャプチャをアップロードします。

**デバイス列挙型**

ドライバーの読み込みに関する問題など、USB レイヤーでのデバイスの列挙に関連する問題のトラブルシューティングを行う場合 (ドライバーを起動できない場合) は、次の手順を実行してください。

1.  **logman は、USBTrace-p Microsoft-Windows-USB 128 128 640---------------------------------------**
2.  **logman update USBTrace-p 128 128 640 USBHUB----------------------------------**
3.  **logman 更新トレース USBTrace-p {bc6c9364-fc67-42c5-acf7-abed3b12ecc6} 0xFFFFFFFF 255 –変更**
4.  システムの予期しない動作につながるタスクを実行します
5.  **Logman が USBTrace を停止します。**
6.  次の情報をアップロードします。
    -   logman を使用して作成された `USBTrace.etl`
    -   `c:\windows\inf\setupapi.dev.log`
    -   **Devcon hwids "USB\\VID\_DeviceVendorID\*"** の出力
        -   最新バージョンの Devcon は、WDK に含まれています。
        -   https://support.microsoft.com/kb/311272 に古いバージョンが存在します

 

 





