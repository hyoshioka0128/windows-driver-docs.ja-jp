---
Description: This topic provides information about how to view the timeline of events captured in a USB ETW log.
title: Xperf と Netmon を使用して USB のパフォーマンスの問題の分析
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12f14a2fc092b8055d6062247aad1e4f3836cd88
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548831"
---
# <a name="analyzing-usb-performance-issues-by-using-xperf-and-netmon"></a>Xperf と Netmon を使用して USB のパフォーマンスの問題の分析


このトピックでは、USB ETW ログでキャプチャされたイベントのタイムラインを表示する方法についての情報を提供します。

Xperf は、パフォーマンスの問題を分析するためのカーネル イベントのセットを提供します。 これらのイベントを記録し、グラフに表示します。

Xperf と USB の ETW イベントの両方に精通している場合は、ログと問題のシナリオの Xperf ログ USB ETW の作成に 2 つのログ ファイルをマージおよびまとめて分析します。 Xperf と Netmon を組み合わせて使用するには、システム イベント (Xperf) と、特定のシナリオには、USB イベント (Netmon) の両方を表示することができます。

管理者特権でコマンド プロンプトから次のコマンドを発行して、並列で 2 つのトレースを開始します。

```cpp
Xperf –on Diag

Logman start Usbtrace -p Microsoft-Windows-USB-USBPORT -o usbtrace.etl -ets -nb 128 640 -bs 128

Logman update Usbtrace -p Microsoft-Windows-USB-USBHUB –ets
```

問題のシナリオで操作を実行し、管理者特権でコマンド プロンプトから次のコマンドを発行して、トレースを停止します。

```cpp
Logman stop Usbtrace -ets

Xperf –stop
```

1 つのファイル (特権は必要ありません)、次のコマンドを使用して、2 つのトレース ログ ファイルをマージします。

```cpp
Xperf –merge usbtrace.etl C:\kernel.etl merged.etl
```

この例では、merged.etl というマージされたファイルを作成します。 Xperf Performance Analyzer または Netmon は、このファイルを開くことができます。 Xperf で、ファイルを開くには、次のコマンドを実行します。

```cpp
Xperf merged.etl
```

Xperf では、この図のように、カーネル イベントのさまざまな種類の特殊化されたグラフが表示されます。 Xperf の記録のオプションと、Xperf GUI の詳細については[Xperf コマンド ライン ツールの詳細は、](https://msdn.microsoft.com/library/cc305221.aspx)と[Windows パフォーマンス アナライザー (WPA)](https://msdn.microsoft.com/library/cc305187.aspx)します。

![windows パフォーマンス アナライザー](images/xperf3.png)

Netmon、Netmon を実行で、マージされたトレース ログを開く**ファイル -&gt;開く -&gt;キャプチャ**、ファイルを選択します。 Xperf、ネットワーク モニターには、マージされたファイルを同時に開いていることができます。 特定の期間のシステムと USB スタックが発生したかを分析するには、Xperf GUI と Netmon を切り替えることができます。 システムのイベントだけでなく、Xperf で USB イベントを表示できますが、USB イベントは Netmon で読みやすくすることができます。

既定では、Netmon は、マージされたトレース ファイルにすべてのイベントを表示します。 USB イベントのみを表示するには、次のフィルターが適用されます。

```cpp
ProtocolName == "USBHub_MicrosoftWindowsUSBUSBHUB" OR ProtocolName == "USBPort_MicrosoftWindowsUSBUSBPORT"
```

Netmon フィルター表示ウィンドウで、このフィルターのテキストを入力できます。 Netmon でフィルターを使用する方法については、この「USB Netmon フィルター」を参照してください。[ケース スタディ。ETW と Netmon を使用して不明な USB デバイスのトラブルシューティングを](case-study--troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon.md)します。

USB イベントのタイミングを分析するには、Netmon で表示されるイベント間の時間差を見ることができます。

**表示されるイベントの時刻の差を表示するには**

1.  **フレーム概要**ウィンドウで、列のタイトルを右クリックし、選択**列の選択**します。
2.  **無効になっている列**一覧で、[**時間の変動**、] をクリックして**追加**、順にクリックします**OK**します。
3.  イベントのタイミングを表示したいだけを表示するフィルターを記述します。 たとえば、一括転送ディスパッチの重複しないと完了イベントの間の遅延を表示するには、次のフィルターを追加します。
    ```cpp
    Description == "USBPort_MicrosoftWindowsUSBUSBPORT:Dispatch URB_FUNCTION_BULK_OR_INTERRUPT_TRANSFER" 
    OR Description == "USBPort_MicrosoftWindowsUSBUSBPORT:Complete URB_FUNCTION_BULK_OR_INTERRUPT_TRANSFER" 
    OR Description == "USBPort_MicrosoftWindowsUSBUSBPORT:Complete URB_FUNCTION_BULK_OR_INTERRUPT_TRANSFER with Data"

    ```

    1.  トレースに記録されるイベントからイベント Id (説明) を選択できます。
    2.  イベント ID でフィルターを使用するイベントの説明を右クリックし、**フレーム概要**ペイン**フィルター表示する説明の追加**します。

## <a name="related-topics"></a>関連トピック
[Windows のイベント トレースは USB](usb-event-tracing-for-windows.md)  
[Xperf を使用して USB ETW を使用しました。](using-xperf-with-usb-etw.md)  



