---
Description: このトピックでは、例にイベント トレースの方法は Netmon を使用してファイル。 について説明します。
title: Netmon での USB ETW トレースの表示方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26caa503bf8ed3601146c15c2f5e73db5ac6a888
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405045"
---
# <a name="how-to-view-a-usb-etw-trace-in-netmon"></a>Netmon での USB ETW トレースの表示方法

このトピックでは、例にイベント トレースの方法は Netmon を使用してファイル。 について説明します。

Netmon をインストールして構成した後に使用するため、USB ETW ファイルで」の説明に従って[Netmon と USB ETW のパーサーをインストールする方法](how-to-install-netmon-and-the-netmon-usb-parser.md)、それを使用して、トレース ファイルを確認することができます。

## <a name="opening-an-etw-file"></a>ETW のファイルを開く

[Start] 画面で、Netmon をトレース ファイルを表示するには、ネットワーク モニターを開く"netmon"を入力します。 次のメソッドのいずれかを使用して、トレース ファイルを開きます。

* **ファイル** メニューのをクリックして**オープン**、 をクリックして**キャプチャ**、.etl ファイルを選択します。
* をクリックして、**オープン キャプチャ**ボタンをクリックし、.etl ファイルを選択します。
* CTRL + O キーを押すし、.etl ファイルを選択します。

イベント トレースはそれぞれのドライバー スタックで発生したことを示します、個々 のイベントで構成されます。 各イベントは、ドライバー スタックによって定義されているいくつかの型のいずれかに準拠しています。

![microsoft ネットワーク モニター](images/netmon-ui-intro.png)

イベントが表示されていることを確認、**フレーム概要**ウィンドウ。 上の図は、USB 2.0 ドライバー スタックから evens を示しています。 このウィンドウで、次の列に注意してください。

* **時刻のオフセット**:ログの開始時刻からのオフセットとして指定された、イベントのタイムスタンプ。
* **プロトコル名**:このドライバーは、イベント ログに記録します。 USB イベントの場合は、ドライバーは、USB ハブまたは USB ポートが。
* **説明**:イベントのわかりやすい名前。

イベントを選択して、**フレーム概要**ウィンドウ。 Netmon でのイベントの詳細を表示する、**フレーム詳細**と**16 進数の詳細**ペインがあります。 **フレーム詳細**ウィンドウで、イベントの詳細を確認する項目を展開します。
Netmon を使用して、USB のトレース ファイルを調べるの例は、次を参照してください。[ケース スタディ。ETW と Netmon を使用して不明な USB デバイスのトラブルシューティングを](case-study--troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon.md)します。

## <a name="new-columns-the-usb-etw-parser-for-usb-30-driver-stack"></a>新しい列 USB ETW パーサーの USB 3.0 ドライバー スタックします。

USB 2.0 ドライバー スタックからのイベントの重要な型は、USB 3.0 ドライバー スタックでも定義されます。 ただし、これらの型の微妙な違いがあります。 たとえば、USB 制御転送の完了イベントの種類 (**説明**:USBPort: 完了 URB\_関数\_コントロール\_転送\_データ例)。

USB 2.0 ドライバー スタック イベントの種類、**フレーム詳細**idVendor (USB VID とも呼ばれます) と idProduct (USB PID とも呼ばれます)、ウィンドウが表示されます。 この図では、イベント トレースは、USB 2.0 ホスト コント ローラーに接続されている USB 2.0 デバイスを示しています。

![microsoft ネットワーク モニター](images/vid-pid-usb2-0.png)

USB 3.0 ドライバー スタック イベントの種類、**フレーム詳細**idVendor または idPid ペインが表示されません。 新しい列を追加することによって情報がある、**フレーム概要**ウィンドウこの図のようにします。

これらの新しい列に注目してください。

* **USB デバイスの説明**
* **USB Vid**
* **USB の Pid**
* **USB の長さ**
* **USB の要求の期間**

![microsoft ネットワーク モニター](images/usb-3-netmon.png)

すべての USB イベント トレース (USB 2.0 および USB 3.0) 各 URB が完了すると、要求に関する情報を表示するようになりました。 下の「255 の 41」などの値を確認**USB 長さ**します。 これらの値は、要求の合計長 (クライアント ドライバーで指定された元の TransferBufferLength) のコンテキストの完了時に各 URB の実際の転送長さを示します。 下を完了する要求にかかる時間 (秒) でも、ご覧、**要求の期間の USB**列。

## <a name="adding-filters-to-the-display-filter-pane"></a>表示フィルター ペインにフィルターを追加します。

特定のシナリオのイベントのトレースを絞り込むためには、キャプチャ フィルターを使用できます。 USB 2.0、USB 3.0 ドライバー スタックから新しいイベント トレース フィルターを記述できます。

```syntax
USBIsError == 1      // Any error events from the USB drivers
USBIsDisconnect == 1 // Show when any device disconnected
```

すべての列をフィルター処理できます。 フィルターを作成するには、セルを右クリックして**追加"&lt;列名&gt;"ディスプレイ フィルターを**します。 Netmon は、その値と列名に基づいてフィルターを作成し、下に追加されます、**ディスプレイ フィルター**ウィンドウ。

## <a name="related-topics"></a>関連トピック

[USB の ETW を使用してください。](using-usb-etw.md)  
[Windows のイベント トレースは USB](usb-event-tracing-for-windows.md)  
[ケース スタディ:ETW と Netmon を使用して不明な USB デバイスのトラブルシューティング](case-study--troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon.md)  
