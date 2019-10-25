---
Description: このトピックでは、Logman ツールを使用した USB ETW イベントトレースのキャプチャについて説明します。
title: Logman を使用して USB イベント トレースをキャプチャする方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da15c2a3b419fc860bd4081db82dae8348c45988
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844991"
---
# <a name="how-to-capture-a-usb-event-trace-with-logman"></a>Logman を使用して USB イベント トレースをキャプチャする方法


このトピックでは、 [Logman](https://go.microsoft.com/fwlink/p/?linkid=617153)ツールを使用した USB ETW イベントトレースのキャプチャについて説明します。 Logman は、Windows に組み込まれているトレースツールです。 Logman を使用して、イベントをイベントトレースログファイルに取り込むことができます。

### <a name="prerequisites"></a>前提条件

イベントトレースログファイルは非常に高速に拡張できますが、より小さなログファイルの移動と送信が容易になります。 トレースを開始する前に、次の手順を実行して、調査するデバイスアクティビティに集中できるように、余分なイベントをログから除外することを検討してください。

-   対象のデバイスではない、重要ではない USB デバイスを切断します。 デバイスが少なくなるほど、トレースが小さくなり、読み取りと分析が容易になります。
-   システムに USB キーボードまたはマウスが搭載されている場合は、代わりにリモートデスクトップを使用してトレースコマンドを入力します。
-   トレースの開始位置と終了位置を、関心のある操作の中でできるだけ狭くします。
-   特定のカテゴリの USB イベントのみに関心がある場合は、キーワードを使用して、記録されたイベントをフィルター処理できます。 詳細については、「解説」を参照してください。

USB 3.0 ドライバースタックからのイベントトレースは、Windows 7 で導入された USB 2.0 ドライバースタックトレースに似ています。 USB 2.0 ドライバースタックからのイベントトレースは、Windows 8 コンピューターでキャプチャできます。 USB 2.0 と USB 3.0 ドライバースタックからイベントトレースをキャプチャする方法は似ています。 USB 2.0 または USB 3.0 ドライバースタックから個別にイベントをキャプチャできます。 Usb 2.0 デバイスを USB 3.0 ホストコントローラーに接続すると、USB 3.0 ドライバースタックからイベントトレースが取得されます。 その場合は、USB 2.0 デバイスの新しい USB 3.0 ドライバースタックイベントを表示します。

<a name="instructions"></a>手順
------------

**USB トレースイベントを収集するには**

1.  管理者特権を持つコマンドプロンプトウィンドウを開きます。 これを行うには、[スタート] ボタンをクリックし、検索ボックスに「 **cmd** 」と入力します。 cmd.exe を右クリックし、 **[管理者として実行]** を選択します。
2.  コマンドプロンプトウィンドウで、次のコマンドを入力してキャプチャセッションを開始します。

    ```cpp
    logman create trace -n usbtrace -o %SystemRoot%\Tracing\usbtrace.etl -nb 128 640 -bs 128
    logman update trace -n usbtrace -p Microsoft-Windows-USB-USBXHCI (Default,PartialDataBusTrace)
    logman update trace -n usbtrace -p Microsoft-Windows-USB-UCX (Default,PartialDataBusTrace)
    logman update trace -n usbtrace -p Microsoft-Windows-USB-USBHUB3 (Default,PartialDataBusTrace)
    logman update trace -n usbtrace -p Microsoft-Windows-USB-USBPORT
    logman update trace -n usbtrace -p Microsoft-Windows-USB-USBHUB
    logman update trace -n usbtrace -p Microsoft-Windows-Kernel-IoTrace 0 2
    logman start -n usbtrace

    ```

    これらの各コマンドが完了すると、Logman が表示され `The command completed successfully.`

3.  キャプチャする操作を実行します。 たとえば、デバイスの列挙イベントをキャプチャするには、**デバイスマネージャー**に "不明なデバイス" と表示される USB フラッシュドライブを接続します。 [コマンドプロンプト] ウィンドウを開いたままにします。
4.  シナリオを完了した後、セッションを停止します。 キャプチャセッションを終了するには、次のコマンドを入力します。

    次のコマンドを実行して、USB ハブとポートイベントの収集を停止することができます。

    ```cpp
    logman stop -n usbtrace 
    logman delete -n usbtrace
    move /Y %SystemRoot%\Tracing\usbtrace_000001.etl %SystemRoot%\Tracing\usbtrace.etl

    ```

前のキャプチャセッションでは、usbtrace という名前の etl ファイルが生成されます。 トレースファイルは% SystemRoot%\\Tracing\\トレースに格納されます (C:\\Windows\\トレース\\usbtrace。 ファイルを別の場所に移動するか、次のセッションをキャプチャするときに上書きされないように名前を変更します。

このファイルには、USB 3.0 および USB 2.0 ドライバースタックからのイベントトレースが含まれています。 イベントトレースを1つの USB ドライバースタックだけに縮小する場合は、次のトレースセッションから他のドライバースタックを削除します。 これを行うには、手順2で示されているコマンドシーケンスを変更して、トレースセッションから削除するドライバースタックに対応する "logman 更新" 行を削除します。

<a name="remarks"></a>注釈
-------

**USB 3.0 ドライバースタックイベントのキャプチャフィルター**

Logman キャプチャコマンドでは、 **Default**や**PARTIALDATABUSTRACE**などの ETW キーワードに注意してください。 これらの単語は、表示するイベントの種類を示す ETW キーワードです。 ETW キーワードを使用して、USB ドライバーがトレースログに書き込むイベントをフィルター処理し、USB 3.0 ドライバースタックからキャプチャされたイベントについて表示する情報の量をカスタマイズできます。 いずれかのキーワードに一致するイベントが保存されます。 このフィルター処理方法は、分析時ではなくキャプチャ時に使用することに注意してください。

要件に応じて、キーワードに基づいてイベントをフィルター処理できます。 USB 3.0 ドライバースタックイベントをフィルター処理するためのキーワードを次に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ETW キーワード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>標準</strong></p></td>
<td><p>一般的なトラブルシューティングに役立つイベントを示します。 イベントは、USB 2.0 ETW イベントに似ていますが、USB 転送イベントは含まれていません。</p></td>
</tr>
<tr class="even">
<td><p><strong>StateMachine</strong></p></td>
<td><p>ドライバー内部のステートマシンの遷移を表示します。 これらのイベントは、 <strong>Default</strong>キーワードには含まれていません。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ランダウン</strong></p></td>
<td><p>トレースの開始時にデバイス情報イベントを表示し、USB ツリーの開始状態をキャプチャします。 デバイス情報<strong>ランダウン</strong>イベントは、接続されているデバイスの usb 記述子や usb デバイスの説明などの詳細がトレースに含まれるように保存することが重要です。 これらのイベントは、 <strong>Default</strong>キーワードに含まれています。 <strong>Default</strong>キーワードを使用しない場合は、<strong>ランダウン</strong>キーワードを使用する必要があります。 残りのランダウンイベントは、ドライバー内部のステートマシンの最新の状態遷移に関する情報を提供します。 これらのイベントは、 <strong>StateMachine</strong>キーワードに含まれています。</p></td>
</tr>
<tr class="even">
<td><p><strong>電源</strong></p></td>
<td><p><strong>既定</strong>のイベントのサブセットを表示します。 デバイスの電源遷移イベントを表示します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IRP</strong></p></td>
<td><p><strong>既定</strong>のイベントのサブセットを表示します。 イベントは、クライアントドライバーからの Irp と、ユーザーモード要求に起因する Irp を示します。 ただし、有効な USB 転送 (URB) 要求は、 <strong>IRP</strong>キーワードと共に表示されず、表示されるためには<strong>HeadersBusTrace</strong>、 <strong>PartialDataBusTrace</strong>、または<strong>FullDataBusTrace</strong>が必要です。</p></td>
</tr>
<tr class="even">
<td><p><strong>HeadersBusTrace</strong></p></td>
<td><p>すべての USB 転送イベントを表示しますが、データパケットは保存しません。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PartialDataBusTrace</strong></p></td>
<td><p>すべての USB 転送イベントを表示し、バスデータの制限されたペイロードを保存します。</p></td>
</tr>
<tr class="even">
<td><p><strong>FullDataBusTrace</strong></p></td>
<td><p>すべての USB 転送イベントを表示し、一括、割り込み、制御転送のために最大 4 KB のバスデータを保存します。 チェーンされた MDL の最初のバッファーだけがログに記録されることに注意してください。 アイソクロナスバスデータはログに記録されません (ただし、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_isoch_transfer" data-raw-source="[&lt;strong&gt;URB_ISOCH_TRANSFER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_isoch_transfer)"><strong>URB_ISOCH_TRANSFER</strong></a>要求構造は保存されます)。 詳細については、「<a href="how-to-send-chained-mdls.md" data-raw-source="[How to send chained MDLs](how-to-send-chained-mdls.md)">チェーン MDLs を送信する方法</a>」および「<a href="transfer-data-to-isochronous-endpoints.md" data-raw-source="[How to transfer data to USB isochronous endpoints](transfer-data-to-isochronous-endpoints.md)">データを USB アイソクロナスエンドポイントに転送する方法</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HWVerifyHost</strong></p></td>
<td><p><strong>既定</strong>のイベントのサブセットを表示します。 イベントは、USB ホストコントローラーのハードウェアでエラーが発生したことを示します。</p></td>
</tr>
<tr class="even">
<td><p><strong>HWVerifyHub</strong></p></td>
<td><p><strong>既定</strong>のイベントのサブセットを表示します。 イベントは、USB ハブハードウェアでエラーが発生したことを示します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HWVerifyDevice</strong></p></td>
<td><p><strong>既定</strong>のイベントのサブセットを表示します。 イベントは、USB デバイスハードウェアでエラーが発生したことを示します。</p></td>
</tr>
</tbody>
</table>



例として、USB デバイスの電源遷移をキャプチャするセッションを開始する一連のコマンドを次に示します。 プロバイダー (USB 3.0 ドライバースタック) の選択により、イベントは、USB 3.0 ホストコントローラーの下流に接続されているデバイスに対してのみキャプチャされます。

```cpp
logman create trace -n usbtrace -o %SystemRoot%\Tracing\usbtrace.etl -nb 128 640 -bs 128
logman update trace -n usbtrace -p Microsoft-Windows-USB-USBXHCI (Rundown,Power)
logman update trace -n usbtrace -p Microsoft-Windows-USB-UCX (Rundown,Power)
logman update trace -n usbtrace -p Microsoft-Windows-USB-USBHUB3 (Rundown,Power)
logman update trace -n usbtrace -p Microsoft-Windows-Kernel-IoTrace 0 2
logman start -n usbtrace
```

**Power イベントのキャプチャフィルター**

Usb デバイス用の便利な ETW キーワードは、USB ポートドライバーの PowerDiagnostics フラグです。 このキーワードを使用すると、ポートドライバーはホストコントローラーとエンドポイント情報をログに記録しますが、転送を記述するすべてのイベントを除外します。 転送イベントを確認する必要がない場合は、PowerDiagnostics キーワードを使用して、トレースログのサイズを85% 程度減らすことができます。 トレースを開始するときに PowerDiagnostics キーワードを指定します。次に例を示します。

```cpp
Logman start Usbtrace -p Microsoft-Windows-USB-USBPORT PowerDiagnostics -o usbtrace.etl -ets -nb 128 640 -bs 128

Logman update Usbtrace -p Microsoft-Windows-USB-USBHUB –ets
```

フィルター選択されたトレースログに多数のホストコントローラーの非同期スケジュールがある場合は、次の例に示すように、Netmon フィルターを使用してログを表示するときにフィルター処理できます。

```cpp
NOT (Description == "USBPort_MicrosoftWindowsUSBUSBPORT:Host Controller Async Schedule Enable" 
OR Description == "USBPort_MicrosoftWindowsUSBUSBPORT:Host Controller Async Schedule Disable")
```

Netmon フィルターの詳細については、「[ケーススタディ: ETW および Netmon を使用した不明な usb デバイスのトラブルシューティング](case-study--troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon.md)」の「Usb Netmon フィルター」を参照してください。

場合によっては、ハブ要求や、XACT エラーやストールなどのエラーが発生するデバイス要求などの転送イベントをトレースログに記録すると便利です。 最初に、転送イベントのないログをキャプチャし、その小さいログを分析することができます。 次に、問題のシナリオの問題についてよく理解してから、フィルターを適用せずにトレースを再度実行します。

## <a name="related-topics"></a>関連トピック
[USB ETW の使用](using-usb-etw.md)  
[USB Windows イベントトレーシング](usb-event-tracing-for-windows.md)  
[イベントの種類を分類するために使用するキーワードの定義](https://docs.microsoft.com/windows/desktop/WES/defining-keywords-used-to-classify-types-of-events)  



