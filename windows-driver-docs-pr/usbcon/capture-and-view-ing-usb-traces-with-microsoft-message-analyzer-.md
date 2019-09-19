---
Description: Microsoft Message Analyzer (MMA) を使用して、ライブ USB トレースをキャプチャして表示したり、既存のトレースを表示したりすることができます。
Search.SourceType: Video
title: Microsoft Message Analyzer を使用して USB トレースをキャプチャして表示する
ms.date: 08/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: ddb1c47d35a5c7b3e58427d8e9e77e0514110b18
ms.sourcegitcommit: 4943143e8395db70beda5a98ad734fe1bb7068dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/18/2019
ms.locfileid: "71080184"
---
# <a name="capture-and-view-usb-traces-with-microsoft-message-analyzer"></a>Microsoft Message Analyzer を使用して USB トレースをキャプチャして表示する

**概要**

-   Microsoft Message Analyzer のインストールとセットアップ
-   ライブ USB トレースをキャプチャして表示する

Microsoft Message Analyzer (MMA) を使用して、ライブ USB トレースをキャプチャして表示したり、既存のトレースを表示したりすることができます。

コマンドラインツールの logman を使用してトレースをキャプチャし、それを Netmon 3.4 で解析するのではなく、1つの GUI からすべてのタスクを実行することができます。

## <a name="install-and-launch-microsoft-message-analyzer"></a>Microsoft Message Analyzer のインストールと起動

1.  [Microsoft Message Analyzer をダウンロード](https://www.microsoft.com/download/details.aspx?id=44226)し、ダウンロードページの**インストール手順**に従ってツールをインストールします。 ダウンロードが完了したら、インストールのプロンプトに従って、 **[項目の更新]** を選択します。

2.  インストールが完了すると、ツールが起動し、スタートページが表示されます。

## <a name="set-up-a-trace-session-and-capture-usb-events"></a>トレースセッションを設定し、USB イベントをキャプチャする

このビデオでは、特定の列を追加して、USB トレース用に Microsoft Message Analyzer をセットアップする方法について説明します。 また、セッションを開始および停止することでライブトレースをキャプチャする方法についても説明します。

> [!NOTE]
> **[デバイス]** で、usb 2 または usb 3 のトレースシナリオを選択します。 USB 3 トレースは、Windows 8 以降のバージョンでのみ使用可能であることに注意してください。 デバイスの速度ではなく、デバイスが接続されているホストコントローラーに基づいて選択してください。 たとえば、xHCI コントローラーに接続されている高速デバイスがある場合は、USB 3 トレースシナリオを選択します。

>[!VIDEO https://www.microsoft.com/videoplayer/embed/e5300401-351e-4dcc-bcc2-edd07079d7fa]



## <a name="analyze-a-usb-trace"></a>USB トレースの分析


Microsoft Message Analyzer は、キャプチャされた情報を動的に解析し、ユーザーが判読できる形式で表示します。 この情報の大部分は、 **[概要]** 列に表示されます。 この列には、USB ドライバースタックがデバイスに送信する要求など、イベントに関する詳細情報が表示されます。 必要なフィルターを追加することにより、それらの要求の結果を表示できます。

このビデオでは、デバイスの列挙エラーの根本原因を特定する方法について説明します。

>[!VIDEO https://www.microsoft.com/videoplayer/embed/29cb1d44-a38a-4105-9513-256e69e9f6a0]

## <a name="related-topics"></a>関連トピック
[ブログMicrosoft Message Analyzer (MMA) を使用した USB ETW トレースのキャプチャ](https://techcommunity.microsoft.com/t5/Microsoft-USB-Blog/bg-p/MicrosoftUSBBlog/archive/2013/11/09/capturing-usb-etw-traces-with-microsoft-message-analyzer-mma.aspx)  
[USB Windows イベントトレーシング](usb-event-tracing-for-windows.md)  



