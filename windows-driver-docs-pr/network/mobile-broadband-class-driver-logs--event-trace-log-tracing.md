---
title: モバイル ブロード バンド クラス ドライバー ログ イベントのトレース ログのトレース
description: このトピックでは、エンジニアをレビューして、問題のトラブルシューティングを行うモバイル ブロード バンド クラス ドライバー イベント トレース ログと操作に役立つ情報を提供します。
ms.assetid: 9742BFCA-CC22-497A-B11F-D3E89F0B4FE6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c54fd625e34cba642b3bd6f2288e36f33c13c510
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375763"
---
# <a name="mobile-broadband-class-driver-logs-event-trace-log-tracing"></a>モバイル ブロード バンド クラス ドライバー ログ:イベント トレース ログのトレース


このトピックでは、エンジニアをレビューして、問題のトラブルシューティングを行うモバイル ブロード バンド クラス ドライバー イベント トレース ログと操作に役立つ情報を提供します。

このトピックの情報に適用されます。

-   Windows 8

## <a name="etl-tracing"></a>ETL トレース


次の手順では、イベント トレース ログ (ETL) を確認する方法について説明します。

1.  イベント ビューアー を開く**開始** &gt; **実行** &gt; **EventVwr**します。
2.  左側のウィンドウに移動します**Applications and Services Logs** &gt; **Microsoft** &gt; **Windows**します。

    ![windows フォルダーに移動する手順を示すスクリーン ショット](images/mbcdlogs1.png)

3.  移動 さらに**Windows**に**wmbclass します。**

    ![windows モバイル ブロード バンド クラス ドライバーのチャネルを示す、wmbclass フォルダーを開く](images/mbcdlogs2.png)

4.  右クリック**Windows モバイル ブロード バンド クラス ドライバー チャンネル**クリック**ログの有効化**。 表示された場合**ログの無効化**ログが既に有効になっています。

    ![コンテキスト メニューが表示されたスクリーン ショットは、ログを有効にし、オプションの更新](images/mbcdlogs3.png)

5.  キーを押して、問題を再現**更新**します。 後**更新**、中央のペインに、ログが表示されます。

    ![上のウィンドウのイベントが選択されているログのスクリーン ショット。 下のウィンドウの説明の 全般 タブおよび選択されていない詳細 タブを示しています。](images/mbcdlogs4.png)

6.  使用してログをフィルター処理することができます、**操作ウィンドウ**右側にします。

    ![現在のログをフィルターを使用して、[操作] ウィンドウで、現在のログをイベント id とイベントのレベルでフィルター処理を例に示します。 この場合、イベントのレベルは、エラーとイベント id は-105 します。](images/mbcdlogs5.png)

## <a name="mobile-broadband-logs"></a>モバイル ブロード バンド ログ


によって、問題とシナリオでは、さまざまな情報は、次を含むソリューションを決定するために必要があります。

**コントロールのパス**

接続の問題が発生した場合の送信または受信 SMS、USSD のメッセージを受信または、プロファイルを使用して送信を収集してください、次の情報。

1.  **netsh トレース開始 wwan\_dbg**
2.  システムの予期しない動作につながるタスクを実行します。
3.  **netsh トレースの停止**
4.  すべてのファイルをアップロードします。 `%localappdata%\temp\nettraces\`

**IP 構成**

IP アドレスの構成に関する問題がある場合は場合、は、次を実行してください。

1.  1. **netsh トレース開始 wwan\_dbg**
2.  2. &lt;システムの予期しない動作につながるタスクを実行します。
3.  3**netsh トレースの停止。**
4.  4. 次の情報をアップロードします。

    • 下のすべてのファイル `%localappdata%\temp\nettraces\`

    • 出力の**ipconfig/all**

**データ パス**

データ パケットの削除に関連する問題のトラブルシューティングを行う場合の再試行、スループットの問題、または接続が制限を実行してください以下。

1.  **netsh trace start wwan\_dbg,InternetClient,nid\_wpp provider={c5aa495b-8432-4de5-9d7c-8afc7d3b522a} 0xFFFFFFFF 255**
2.  モバイル ブロード バンド アダプターでは、netmon のトレースを開始します。
3.  システムの予期しない動作につながるタスクを実行します。
4.  Netmon のトレースを停止し、ネットワーク モニターのキャプチャを保存します。
5.  **netsh トレースの停止**
6.  次の情報をアップロードします。
    -   すべてのファイル `%localappdata%\temp\nettraces\`
    -   Netmon のキャプチャをアップロードします。

**デバイスの列挙**

USB 層でデバイスの列挙に関連する問題のトラブルシューティングを行う場合 (ドライバーではなく起動に失敗する)、ドライバーの読み込みの問題などを実行してください以下。

1.  **logman start USBTrace -p Microsoft-Windows-USB-USBPORT -ets -nb 128 640 -bs 128 -o USBTrace.etl**
2.  **logman 更新 USBTrace-p Microsoft Windows USB USBHUB-ets-nb 128 640 bs 128**
3.  **logman update trace USBTrace -p {bc6c9364-fc67-42c5-acf7-abed3b12ecc6} 0xFFFFFFFF 255 –ets**
4.  システムの予期しない動作につながるタスクを実行します。
5.  **Logman stop USBTrace ets**
6.  次の情報をアップロードします。
    -   `USBTrace.etl` logman を使用して作成
    -   `c:\windows\inf\setupapi.dev.log`
    -   出力の**devcon hwids"USB\\VID\_DeviceVendorID\*"**
        -   Devcon.exe の最新バージョンとは、WDK の一部です。
        -   以前のバージョンが存在します http://support.microsoft.com/kb/311272

 

 





