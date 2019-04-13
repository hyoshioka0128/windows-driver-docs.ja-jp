---
Description: Microsoft メッセージ アナライザー (MMA) を使用して、キャプチャし、ライブの USB トレースを表示または既存のトレースを表示することができます。
Search.SourceType: Video
title: Microsoft Message Analyzer を使用して USB トレースをキャプチャして表示する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 417d26c54f265fd541272b7eb170f29d6abc4b33
ms.sourcegitcommit: 4c67665bf7cd4fd3599ff0751a3b0427d119937c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2019
ms.locfileid: "59554052"
---
# <a name="capture-and-view-usb-traces-with-microsoft-message-analyzer"></a>Microsoft Message Analyzer を使用して USB トレースをキャプチャして表示する


**要約**

-   Microsoft Message Analyzer のインストールとセットアップ
-   キャプチャし、ライブの USB トレースを表示

Microsoft メッセージ アナライザー (MMA) を使用して、キャプチャし、ライブの USB トレースを表示または既存のトレースを表示することができます。

Logman、コマンド ライン ツールを使用し、それらを Netmon 3.4 で解析してトレースをキャプチャするのではなく、1 つの GUI からそれらのすべてのタスクを実行できます。

## <a name="install-and-launch-microsoft-message-analyzer"></a>インストールし、Microsoft Message Analyzer の起動


1.  [Microsoft Message Analyzer をダウンロード](https://www.microsoft.com/download/details.aspx?id=44226)に従ってツールのインストールと**インストール手順**ダウンロード ページにします。 をダウンロードしたら、クリックし、インストールの指示に従ってください**項目を更新**します。

2.  インストールの完了後、ツールを起動し、開始ページが表示されます。

## <a name="set-up-a-trace-session-and-capture-usb-events"></a>トレース セッションを設定し、USB イベントのキャプチャ


このビデオでは、特定の列を追加することで、USB トレースの Microsoft Message Analyzer を設定する方法を示します。 起動して、セッションを停止するライブ トレースをキャプチャする方法も示します。

**注**  **デバイス**USB 2 または USB 3 のトレースのシナリオを選択します。 USB 3 トレースは、Windows 8 およびそれ以降のバージョンで使用可能なだけに注意してください。 デバイスの速度ではなく、デバイスが接続されているホスト コント ローラー ベースの選択を行います。 たとえば、高速度 xHCI コント ローラーに接続されたデバイス、USB 3 のトレースのシナリオを選択する必要がある場合です。

>[!VIDEO https://www.microsoft.com/videoplayer/embed/e5300401-351e-4dcc-bcc2-edd07079d7fa]

## <a name="analyze-a-usb-trace"></a>USB のトレースを分析します。


Microsoft Message Analyzer がキャプチャされ、人間が判読できる形式で表示されますが、情報を動的に解析します。 ほとんどの情報を示した、**概要**列。 その列には、USB ドライバー スタックは、デバイスに送信要求など、イベントに関する詳細が表示されます。 必要なフィルターを追加して、それらの要求の結果を表示できます。

このビデオでは、デバイスの列挙エラーの根本原因を特定する方法について説明します。

>[!VIDEO https://www.microsoft.com/videoplayer/embed/29cb1d44-a38a-4105-9513-256e69e9f6a0]

## <a name="related-topics"></a>関連トピック
[ブログ:Microsoft メッセージ アナライザー (MMA) の USB の ETW トレースのキャプチャ](https://techcommunity.microsoft.com/t5/Microsoft-USB-Blog/bg-p/MicrosoftUSBBlog/archive/2013/11/09/capturing-usb-etw-traces-with-microsoft-message-analyzer-mma.aspx)  
[Windows のイベント トレースは USB](usb-event-tracing-for-windows.md)  



