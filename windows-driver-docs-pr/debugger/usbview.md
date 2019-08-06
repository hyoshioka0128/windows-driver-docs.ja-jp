---
title: Windows の USBView
description: USBView
ms.assetid: 88d2a93f-2e7c-493c-bb9e-487f1d1f2016
keywords:
- USBView
ms.date: 02/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7b7886cbf127904c7763d2c768f11472a517788
ms.sourcegitcommit: 21eb29567c7b9ae2801a4f5b002cf0a6daef3cf5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2019
ms.locfileid: "68796926"
---
# <a name="usbview"></a>USBView

ユニバーサルシリアルバスビューアー (USBView) または USBView .exe は、コンピューター上のすべての USB コントローラーと接続されている USB デバイスを参照するために使用できる Windows グラフィカル UI アプリです。 USBView は、すべてのバージョンの Windows で動作します。

## <a name="span-idwhere_to_get_usbviewspanspan-idwhere_to_get_usbviewspanspan-idwhere_to_get_usbviewspanwhere-to-get-usbview"></a><span id="Where_to_get_USBView"></span><span id="where_to_get_usbview"></span><span id="WHERE_TO_GET_USBVIEW"></span>USBView を取得する場所

USBView をダウンロードして使用するには、次の手順を実行します。

1. [Windows SDK をダウンロードしてインストール](https://developer.microsoft.com/windows/downloads/windows-10-sdk)します。

2. インストール中に、 **[Windows 用デバッグツール]** ボックスのみを選択し、他のすべてのボックスをオフにします。

3. 既定では、x64 PC では、SDK は USBView を次のディレクトリにインストールします。

   `C:\Program Files (x86)\Windows Kits\10\Debuggers\x64`

4. 実行しているプロセッサの種類のキットデバッガーディレクトリを開き、[USBView .exe] を選択してユーティリティを起動します。


## <a name="usbview-source-code"></a>USBView ソースコード

[Usbview](https://go.microsoft.com/fwlink/p/?LinkId=618004)は、GitHub の[Windows ドライバーサンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)リポジトリでも使用できます。

## <a name="span-idusing_usbviewspanspan-idusing_usbviewspanuse-usbview"></a><span id="using_usbview"></span><span id="USING_USBVIEW"></span>USBView を使用する


USBView は、USB ホストコントローラー、USB ハブ、および接続されている USB デバイスを列挙できます。 また、デバイスに関する情報をレジストリから照会したり、USB 要求を使用してデバイスに照会したりすることもできます。

メインの [USBView] ウィンドウには、2つのペインがあります。 左側のウィンドウには、任意の USB デバイスを選択するために使用できる接続指向のツリービューが表示されます。

右側のウィンドウには、選択した USB デバイスに関連する USB データ構造が表示されます。 これらの構造体には、デバイス、構成、インターフェイス、エンドポイント記述子、および現在のデバイス構成が含まれます。


## <a name="use-device-manager-to-display-usb-info"></a>デバイスマネージャーを使用して USB 情報を表示する

デバイスマネージャーを使用して USB 情報を表示するには:

1. [Windows ロゴキー + R] を選択し、ポップアップボックスに「 **devmgmt.msc** 」と入力して、enter キーを押します。

2. デバイスマネージャーで、コンピューターを選択して強調表示します。

3. **[アクション]** を選択し、 **[ハードウェア変更のスキャン]** を選択します。

4. **[表示]** を選択し、 **[非表示のデバイス]** を選択して、追加のデバイスを表示します (現在アクティブになっていないデバイスなど)。 

5. デバイスマネージャーの **[ユニバーサルシリアルバスコントローラー]** ノードを展開し、問題のデバイスを選択します。

7. 右クリックして **[プロパティ]** を選択し、概要デバイスの状態情報を表示します。

8. **[詳細]** タブを選択して、追加情報を表示します。 

9. **ステータス**や**問題コード**などの詳細を表示するには、 **[プロパティ]** を選択します。


## <a name="windows-usb-troubleshooter"></a>Windows USB トラブルシューティングツール

**[ハードウェアの安全な削除]** ダイアログボックスを使用してイジェクトされない USB デバイスを診断する場合は、 [Windows USB トラブルシューティングツール](https://support.microsoft.com/help/17614/windows-10-troubleshoot-common-usb-problems)を使用してください。


 

 





