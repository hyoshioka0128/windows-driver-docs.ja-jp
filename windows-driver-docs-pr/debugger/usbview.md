---
title: USBView
description: USBView
ms.assetid: 88d2a93f-2e7c-493c-bb9e-487f1d1f2016
keywords:
- USBView
ms.date: 02/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfffcf440c5d834cd31df985827985ef026456e6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367986"
---
# <a name="usbview"></a>USBView

USBView (ユニバーサル シリアル バス ビューアー、USBView.exe) は、Windows のグラフィカル ユーザー インターフェイス アプリケーションすべての USB コント ローラーとコンピューターに接続されている USB デバイスを参照することができます。 USBView は、Windows のすべてのバージョンで動作します。

## <a name="span-idwheretogetusbviewspanspan-idwheretogetusbviewspanspan-idwheretogetusbviewspanwhere-to-get-usbview"></a><span id="Where_to_get_USBView"></span><span id="where_to_get_usbview"></span><span id="WHERE_TO_GET_USBVIEW"></span>USBView の入手先

ダウンロードして使用するのには、USBView は、次の手順を完了します。

1. [Windows SDK ダウンロードおよびインストール](https://developer.microsoft.com/windows/downloads/windows-10-sdk)します。

2. インストール時に選択だけ**ツールを Windows のデバッグ**ボックスし、その他のすべてのボックスをオフにします。

3. 既定では、x64 PC SDK はこのディレクトリに USBView をインストールします。

   `C:\Program Files (x86)\Windows Kits\10\Debuggers\x64`

4. プロセッサの種類を実行し、クリックして、ユーティリティを起動する usbview.exe のキット デバッガー ディレクトリに移動します。


## <a name="usbview-source-code"></a>USBView ソース コード

[USBView](https://go.microsoft.com/fwlink/p/?LinkId=618004)も記載されて、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub リポジトリにあります。

## <a name="span-idusingusbviewspanspan-idusingusbviewspanusing-usbview"></a><span id="using_usbview"></span><span id="USING_USBVIEW"></span>USBView を使用します。


USBView には、USB ホスト コント ローラー、USB ハブ、および接続されている USB デバイスを列挙できます。 USB デバイスの要求と、レジストリからデバイスについて照会することもできます。

USBView のメイン ウィンドウには、2 つのペインが含まれています。 左側のウィンドウには、任意の USB デバイスを選択できるように、接続指向のツリー ビューが表示されます。

右側のウィンドウには、選択した USB デバイスに関連する USB データ構造が表示されます。 これらの構造体には、デバイス、構成、インターフェイス、およびエンドポイントの記述子だけでなく、現在のデバイス構成が含まれます。


## <a name="using-device-manager-to-display-usb-information"></a>デバイス マネージャーを使用して、USB の情報を表示するには

Windows デバイス マネージャを使用して、USB 情報を表示します。

1. Windows キー + R を入力し、enter`devmgmt.msc`ポップアップ ボックスまたは Enter キーを押します。

2. デバイス マネージャーでは、強調表示されているため、コンピューターをクリックします。

3. をクリックして**アクション**、 をクリックし、**ハードウェア変更のスキャン**します。

4. 選択**ビュー**順にクリックします**非表示のデバイス**現在アクティブになっていないものなど、他のデバイスを表示します。 

5. 展開、*ユニバーサル シリアル バス コント ローラー*デバイス マネージャーのノード。

6. たとえば、対象のデバイスを検索する*USB 大容量記憶装置*します。

7. クリックし、デバイスを右クリックして**プロパティ**概要デバイスの状態情報を表示します。

8. をクリックして、**詳細**タブには追加情報を表示します。 

9. 使用して、**プロパティ**など必要な情報を表示するボックスの一覧をプル*状態*または*問題のあるコード*。


## <a name="windows-usb-troubleshooter"></a>Windows USB のトラブルシューティング

USB デバイス ハードウェアの安全な削除 ダイアログ ボックスを使用してを取り出せないを診断しようとする場合を試す可能性がある、 [Windows USB のトラブルシューティング](https://support.microsoft.com/help/17614/automatically-diagnose-and-fix-windows-usb-problems)します。


 

 





