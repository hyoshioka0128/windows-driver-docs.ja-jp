---
title: Windows での USBView
description: USBView
ms.assetid: 88d2a93f-2e7c-493c-bb9e-487f1d1f2016
keywords:
- USBView
ms.date: 02/22/2017
ms.localizationpriority: high
ms.openlocfilehash: 3a7f5270d5b4231129571f391989581754fc14df
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533825"
---
# <a name="usbview"></a>USBView

ユニバーサル シリアル バス ビューアー (USBView) または USBView.exe は、ご使用のコンピューター上のすべての USB コントローラーと接続されている USB デバイスを参照するために使用できる Windows グラフィカル UI アプリです。 USBView は、すべてのバージョンの Windows で動作します。

## <a name="span-idwhere_to_get_usbviewspanspan-idwhere_to_get_usbviewspanspan-idwhere_to_get_usbviewspanwhere-to-get-usbview"></a><span id="Where_to_get_USBView"></span><span id="where_to_get_usbview"></span><span id="WHERE_TO_GET_USBVIEW"></span>USBView の入手先

USBView をダウンロードして使用するには、次の手順を行います。

1. [Windows SDK をダウンロードしてインストールします](https://developer.microsoft.com/windows/downloads/windows-10-sdk)。

2. インストール時に、 **[Debugging Tools for Windows]** ボックスのみを選択して、それ以外のすべてのボックスの選択を解除します。

3. SDK により、USBView は、x64 PC では既定で次のディレクトリにインストールされます。

   `C:\Program Files (x86)\Windows Kits\10\Debuggers\x64`

4. 実行しているプロセッサの種類のキット デバッガー ディレクトリを開き、USBView.exe を選択してユーティリティを起動します。


## <a name="usbview-source-code"></a>USBView ソース コード

[USBView](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/usbview) は、GitHub の [Windows ドライバー サンプル](https://github.com/Microsoft/Windows-driver-samples) リポジトリでも入手できます。

## <a name="span-idusing_usbviewspanspan-idusing_usbviewspanuse-usbview"></a><span id="using_usbview"></span><span id="USING_USBVIEW"></span>USBView を使用する


USBView を使用すると、USB ホストコントローラー、USB ハブ、接続されている USB デバイスを列挙できます。 また、デバイスに関する情報をレジストリから照会したり、USB 要求を通じてデバイスに照会したりすることもできます。

メインの USBView ウィンドウには、2 つのペインがあります。 左側のペインには、任意の USB デバイスを選択するために使用できる接続指向のツリー ビューが表示されます。

右側のペインには、選択した USB デバイスに関連する USB データ構造が表示されます。 これらの構造には、デバイス、構成、インターフェイス、エンドポイント記述子の他に、現在のデバイス構成も含まれます。


## <a name="use-device-manager-to-display-usb-info"></a>デバイス マネージャーを使用して USB 情報を表示する

デバイス マネージャーを使用して USB 情報を表示するには、次の手順を行います。

1. Windows ロゴ キーを押しながら R キーを押して、ポップアップ ボックスに「**devmgmt.msc**」と入力して、Enter キーを押します。

2. デバイス マネージャーで、ご使用のコンピューターを選択して強調表示します。

3. **[アクション]** 、 **[ハードウェア変更のスキャン]** の順に選択します。

4. **[表示]** 、 **[非表示のデバイス]** の順に選択し、追加のデバイス (現在アクティブになっていないデバイスなど) を表示します。 

5. デバイス マネージャーで **[ユニバーサル シリアル バス コントローラー]** ノードを展開し、対象のデバイスを選択します。

7. 右クリックして **[プロパティ]** を選択し、デバイス ステータス情報の概要を表示します。

8. 追加情報を表示するには、 **[詳細]** タブをクリックします。 

9. **[状態]** や **[問題コード]** などの詳細を表示するには、 **[プロパティ]** を選択します。


## <a name="windows-usb-troubleshooter"></a>Windows USB トラブルシューティング ツール

**[ハードウェアを安全に取り外してメディアを取り出す]** ダイアログ ボックスを使用してイジェクトされない USB デバイスを診断する場合は、[Windows USB トラブルシューティング ツール](https://support.microsoft.com/help/17614/windows-10-troubleshoot-common-usb-problems)を使用してみてください。


 

 





