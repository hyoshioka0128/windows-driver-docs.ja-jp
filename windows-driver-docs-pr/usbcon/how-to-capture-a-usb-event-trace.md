---
Description: このトピックでは、イベント トレース、Logman ツールを使用して USB ETW をキャプチャする方法の情報を提供します。
title: Logman を使用して USB イベント トレースをキャプチャする方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cb23adec030ad43785acdc47776ef3d0eb6e182
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381039"
---
# <a name="how-to-capture-a-usb-event-trace-with-logman"></a>Logman を使用して USB イベント トレースをキャプチャする方法


このトピックの使用に関する情報を提供する、 [Logman](https://go.microsoft.com/fwlink/p/?linkid=617153) USB ETW イベントのトレースをキャプチャするツール。 Logman は、Windows に組み込まれているトレース ツールです。 Logman を使用して、イベント トレース ログ ファイルにイベントをキャプチャすることができます。

### <a name="prerequisites"></a>前提条件

イベント トレース ログ ファイルが非常に高速に拡大できますが、サイズの小さいログ ファイルは移動を容易に送信します。 トレースを開始する前に確認するデバイスのアクティビティに集中できるように、余分なイベントをログから除外する次の手順を検討してください。

-   関心のあるデバイスではない重要ではない USB デバイスをすべてを切断します。 少ない数のデバイスは、小さいトレースを読み取って分析を簡単に発生します。
-   システムに USB キーボードまたはマウスがある場合は、代わりに、リモート デスクトップを使用して、トレース コマンドを入力します。
-   開始と目的の操作を可能な限り、トレースの終了を絞り込みます。
-   USB のイベントの特定のカテゴリのみに関心がある場合は、記録されるイベントをフィルター処理するキーワードを使用できます。 詳細については、「解説」を参照してください。

USB 3.0 ドライバー スタックからのイベント トレースは、Windows 7 で導入された USB 2.0 ドライバー スタック トレースに似ています。 Windows 8 コンピューターに USB 2.0 ドライバー スタックからのイベント トレースをキャプチャできます。 USB 2.0、USB 3.0 ドライバー スタックからのイベント トレースをキャプチャする方法は似ています。 USB 2.0 接続または USB 3.0 ドライバー スタックからのイベントを個別に、キャプチャできます。 USB 3.0 ホスト コント ローラーに USB 2.0 デバイスを接続するときは、USB 3.0 ドライバー スタックからイベント トレースを取得します。 その場合は、USB 2.0 デバイス用の新しい USB 3.0 ドライバー スタック イベントを表示します。

<a name="instructions"></a>手順
------------

**USB のトレース イベントを収集するには**

1.  管理者特権を持つコマンド プロンプト ウィンドウを開きます。 これを行うには、開始をクリックします。 型**cmd**検索ボックスに、cmd.exe を右クリックし、**管理者として実行**します。
2.  コマンド プロンプト ウィンドウで、キャプチャ セッションを開始するこれらのコマンドを入力します。

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

    これらの各コマンドが完了すると、Logman を表示します `The command completed successfully.`

3.  紹介をキャプチャする操作を実行します。 たとえば、デバイスの列挙のイベントをキャプチャするには、プラグインできる「不明なデバイス」として表示されます、USB フラッシュ ドライブに**デバイス マネージャー**します。 コマンド プロンプト ウィンドウを開いたままにします。
4.  シナリオを完了した後、セッションを停止します。 キャプチャ セッションを終了するこれらのコマンドを入力します。

    USB ハブおよびポート イベントの収集を停止するには、次のコマンドを実行します。

    ```cpp
    logman stop -n usbtrace 
    logman delete -n usbtrace
    move /Y %SystemRoot%\Tracing\usbtrace_000001.etl %SystemRoot%\Tracing\usbtrace.etl

    ```

前のキャプチャ セッションでは、という名前の usbtrace.etl etl ファイルを生成します。 トレース ファイルが %systemroot% に格納されている\\トレース\\usbtrace.etl (c:\\Windows\\トレース\\usbtrace.etl)。 ファイルを別の場所に移動します。 または、次回のセッションをキャプチャするときに上書きすることを回避するために名前を変更します。

ファイルには、USB 3.0 と USB 2.0 ドライバー スタックからのイベント トレースが含まれています。 USB ドライバー スタックの 1 つだけにイベント トレースを削減する場合は、他のドライバー スタックを次のトレース セッションから削除します。 トレース セッションから削除するドライバー スタックに対応する"logman update"の行を削除する手順 2 に示したコマンド シーケンスを変更することによって行うことができます。

<a name="remarks"></a>コメント
-------

**USB 3.0 ドライバー スタックのイベントのフィルターをキャプチャします。**

ETW のキーワードをなどに注意してください**既定**と**PartialDataBusTrace** Logman のコマンドをキャプチャします。 これらの単語は、ETW キーワードを表示するイベントの種類を示すです。 ETW のキーワードを使用すると、USB ドライバーはトレース ログに書き込むし、USB 3.0 ドライバー スタックからキャプチャされたイベントを表示する情報の量をカスタマイズするイベントをフィルター処理します。 キーワードのいずれかに一致するイベントが保存されます。 分析中ではなく、キャプチャ時に使用するためのフィルター処理には、このメソッドは、することに注意してください。

要件に応じて含まれるキーワードに基づいてイベントをフィルター処理することができます。 USB 3.0 ドライバー スタックのイベントをフィルター処理するためのキーワードを次に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ETW のキーワード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Default</strong></p></td>
<td><p>一般的なトラブルシューティングに役立つイベントを示します。 イベントは、USB 2.0 の ETW イベントと同じですが、任意の USB 転送イベントを含めないでください。</p></td>
</tr>
<tr class="even">
<td><p><strong>StateMachine</strong></p></td>
<td><p>ドライバー内部のステート マシンの遷移を示しています。 イベントが含まれない、<strong>既定</strong>キーワード。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ランダウン</strong></p></td>
<td><p>トレースの先頭にデバイス情報のイベントが表示され、USB ツリーの開始時の状態をキャプチャします。 デバイス情報<strong>ランダウン</strong>イベントは、トレースには、USB ディスクリプターや接続されているデバイスの USB デバイスの説明などの詳細が含まれているように、保存する重要です。 これらのイベントが含まれている、<strong>既定</strong>キーワード。 使用しない場合、<strong>既定</strong>キーワードを使用する必要がある、<strong>ランダウン</strong>キーワード。 残りのランダウン イベントは、ドライバー内部のステート マシンの最新の状態遷移に関する情報を提供します。 これらのイベントが含まれている、 <strong>StateMachine</strong>キーワード。</p></td>
</tr>
<tr class="even">
<td><p><strong>電源</strong></p></td>
<td><p>サブセットを示しています<strong>既定</strong>イベント。 デバイスの電源の遷移イベントを示します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IRP</strong></p></td>
<td><p>サブセットを示しています<strong>既定</strong>イベント。 イベントは、ドライバーと Irp がユーザー モードの要求の結果、クライアントから Irp を表示します。 ただし、有効な USB 転送 (URB) 要求に表示されません、 <strong>IRP</strong>キーワードを必要と<strong>HeadersBusTrace</strong>、 <strong>PartialDataBusTrace</strong>、または<strong>FullDataBusTrace</strong>に表示するためにします。</p></td>
</tr>
<tr class="even">
<td><p><strong>HeadersBusTrace</strong></p></td>
<td><p>すべての USB 転送イベントが表示されますが、データ パケットは保存されません。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PartialDataBusTrace</strong></p></td>
<td><p>すべての USB 転送イベントを表示し、バスのデータのペイロードの制限を保存します。</p></td>
</tr>
<tr class="even">
<td><p><strong>FullDataBusTrace</strong></p></td>
<td><p>すべての USB 転送イベントを表示し、最大 4 KB の一括、割り込み、およびコントロールの転送のバスのデータを保存します。 最初のチェーンの MDL バッファーのみがログに記録されるに注意してください。 アイソクロナス bus データがログに記録されません (ただし、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540414" data-raw-source="[&lt;strong&gt;URB_ISOCH_TRANSFER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540414)"> <strong>URB_ISOCH_TRANSFER</strong> </a>要求の構造を保存) します。 詳細については、次を参照してください。<a href="how-to-send-chained-mdls.md" data-raw-source="[How to send chained MDLs](how-to-send-chained-mdls.md)">を送信する方法のチェーン MDLs</a>と<a href="transfer-data-to-isochronous-endpoints.md" data-raw-source="[How to transfer data to USB isochronous endpoints](transfer-data-to-isochronous-endpoints.md)">USB アイソクロナス エンドポイントにデータを転送する方法</a>します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HWVerifyHost</strong></p></td>
<td><p>サブセットを示しています<strong>既定</strong>イベント。 USB ホスト コント ローラーのハードウェアでエラーが発生したときに、イベントを示します。</p></td>
</tr>
<tr class="even">
<td><p><strong>HWVerifyHub</strong></p></td>
<td><p>サブセットを示しています<strong>既定</strong>イベント。 USB ハブのハードウェアでエラーが発生したときに、イベントを示します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HWVerifyDevice</strong></p></td>
<td><p>サブセットを示しています<strong>既定</strong>イベント。 USB デバイスのハードウェアにエラーが発生したときに、イベントを示します。</p></td>
</tr>
</tbody>
</table>



たとえば、USB デバイスの電源の遷移をキャプチャするセッションを開始するコマンドのシーケンスを示します。 接続されているデバイスに対してのみイベントがキャプチャによりプロバイダー (USB 3.0 ドライバー スタック) を選択すると、USB 3.0 ホスト コント ローラーのダウン ストリーム。

```cpp
logman create trace -n usbtrace -o %SystemRoot%\Tracing\usbtrace.etl -nb 128 640 -bs 128
logman update trace -n usbtrace -p Microsoft-Windows-USB-USBXHCI (Rundown,Power)
logman update trace -n usbtrace -p Microsoft-Windows-USB-UCX (Rundown,Power)
logman update trace -n usbtrace -p Microsoft-Windows-USB-USBHUB3 (Rundown,Power)
logman update trace -n usbtrace -p Microsoft-Windows-Kernel-IoTrace 0 2
logman start -n usbtrace
```

**電源イベントのフィルターをキャプチャします。**

USB デバイスの便利な ETW キーワードは、USB ポート ドライバーの PowerDiagnostics フラグです。 このキーワードを使用して、ポート ドライバーはホスト コント ローラーおよびエンドポイント情報をログ記録は、転送を記述するすべてのイベントが省略されます。 転送イベントを確認する必要がない場合は、85% トレース ログのサイズを小さく PowerDiagnostics キーワードを使用することができます。 次の例に示すように、トレースを開始するときに、PowerDiagnostics キーワードを指定します。

```cpp
Logman start Usbtrace -p Microsoft-Windows-USB-USBPORT PowerDiagnostics -o usbtrace.etl -ets -nb 128 640 -bs 128

Logman update Usbtrace -p Microsoft-Windows-USB-USBHUB –ets
```

フィルター選択されたトレース ログに非同期多くのホスト コント ローラーがある場合はスケジュールが有効にして、イベントを無効にする、フィルターにより選択ときに、Netmon を使用してログを表示するフィルター処理を次の例に示すように。

```cpp
NOT (Description == "USBPort_MicrosoftWindowsUSBUSBPORT:Host Controller Async Schedule Enable" 
OR Description == "USBPort_MicrosoftWindowsUSBUSBPORT:Host Controller Async Schedule Disable")
```

Netmon フィルターの詳細については、「USB Netmon フィルター」を参照してください[ケース スタディ。ETW と Netmon を使用して不明な USB デバイスのトラブルシューティングを](case-study--troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon.md)します。

転送イベント ハブの要求と XACT エラーや、停止などのエラーが発生するデバイス要求など、トレース ログにすると便利な場合があります。 転送イベントが発生せず、ログをキャプチャし、その小さいログを分析する場合があります最初。 問題のシナリオで問題の一般的な理解をした後にフィルター処理せずに、トレースを再し実行します。

## <a name="related-topics"></a>関連トピック
[USB の ETW を使用してください。](using-usb-etw.md)  
[Windows のイベント トレースは USB](usb-event-tracing-for-windows.md)  
[イベントの種類を分類に使用されるキーワードを定義します。](https://msdn.microsoft.com/library/windows/desktop/dd996915)  



