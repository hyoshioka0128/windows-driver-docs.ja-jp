---
Description: This topic describes the USB hardware verifier tool (USB3HWVerifierAnalyzer.exe) that is used for testing and debugging specific hardware events.
title: USB ハードウェア検証ツール (USB3HWVerifierAnalyzer.exe)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8b410e79dc93cdd79d55a89e97169ae127acd78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582129"
---
# <a name="usb-hardware-verifier-usb3hwverifieranalyzerexe"></a>USB ハードウェア検証ツール (USB3HWVerifierAnalyzer.exe)


このトピックでは、テストと特定のハードウェアのイベントのデバッグに使用する USB ハードウェア検証ツール (USB3HWVerifierAnalyzer.exe) について説明します。

不適切なエンド ユーザー エクスペリエンスにつながる方法でマニフェストのほとんどのハードウェアの問題と、正確なエラーの特定が困難にすることがよくあります。 USB ハードウェア検証ツールの目的のデバイスをポート、ハブ、コント ローラー、またはこれらの組み合わせで発生するハードウェアの障害をキャプチャします。

USB ハードウェア検証ツールは、これらのタスクを実行できます。

-   ハードウェアのイベントをキャプチャし、リアルタイムで情報を表示します。
-   すべてのイベントに関する情報を含むトレース ファイルを生成します。
-   イベントは、既存のトレース ファイルを解析します。

このトピックには、次のセクションが含まれています。

-   [USB ハードウェア検証ツールのアナライザー ツールを取得します。](#getting-the-usb-hardware-verifier-analyzer-tool)
-   [USB ハードウェア検証ツールを使用してイベントをキャプチャする方法](#how-to-capture-events-by-using-a-usb-hardware-verifier)
-   [USB ハードウェアの検証フラグ](#usb-hardware-verifier-flags)

## <a name="getting-the-usb-hardware-verifier-analyzer-tool"></a>USB ハードウェア検証ツールのアナライザー ツールを取得します。


USB ハードウェアの検証ツールをからダウンロード可能である MUTT ソフトウェア パッケージに含まれている[MUTT ソフトウェア パッケージ ツール](mutt-software-package.md)します。

ツール パッケージには、ストレスおよび転送テスト (電源切り替え効果を含む) および SuperSpeed テストを実行するいくつかのツールが含まれています。 パッケージには、Readme ドキュメント (個別のダウンロードとして入手可能) もあります。 ドキュメントでは、MUTT ハードウェアの種類の概要を示します。 さまざまなテストを実行し、コント ローラー、ハブ、デバイス、トポロジの提案し、BIOS および UEFI テストに関するステップ バイ ステップ ガイダンスを提供します。

## <a name="how-to-capture-events-by-using-a-usb-hardware-verifier"></a>USB ハードウェア検証ツールを使用してイベントをキャプチャする方法


ハードウェア検証ツールを使用してイベントをキャプチャするには、これらの手順を実行します。

1. 管理者特権のコマンド プロンプトで次のコマンドを実行してセッションを開始します。

   ``` syntax
   USB3HWVerifierAnalyzer.exe
   ```

   このツールには、これらのオプションがサポートされています。

   <table>
   <colgroup>
   <col width="50%" />
   <col width="50%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th>オプション</th>
   <th>説明</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td><p><a href="" id="---v--vendorid-"></a> -v &lt;VendorID&gt;</p></td>
   <td><p>指定した VendorID のハードウェアの検証ツールのすべてのイベントを記録します。</p></td>
   </tr>
   <tr class="even">
   <td><p><a href="" id="----p--productid-"></a> -p &lt;ProductID&gt;</p></td>
   <td><p>指定された ProductID に対してハードウェアの検証ツールのすべてのイベントを記録します。</p></td>
   </tr>
   <tr class="odd">
   <td><p><a href="" id="-f--etl-file-"></a>-f &lt;ETL ファイル&gt;</p></td>
   <td><p>指定した ETL ファイルを解析します。 リアルタイムの解析はサポートされていません。 このオプションでは、ツールは、オフライン ファイルを解析します。</p></td>
   </tr>
   <tr class="even">
   <td><p>/v 出力</p></td>
   <td><p>コンソールには、すべてのイベントを表示します。</p></td>
   </tr>
   </tbody>
   </table>

     

2. ハードウェアのイベントをキャプチャするテスト シナリオを実行します。

   、セッション中に発生すると、USB ハードウェア検証ツールはハードウェアについての情報をキャプチャします。 特定のハードウェア用のイベントをフィルター処理する場合は、VendorId とハードウェアの ProductId を指定します。 ツールは、完全にデバイスが列挙を取得する前に発生したイベントに関する/PID VID) などのいくつかの情報をキャプチャしません可能性があります。 不足している情報は、(次に説明します)、セッションの最後に生成される詳細なレポートで使用できます。

   ハードウェアの検証ツールからの出力例を次に示します。

   ``` syntax
   Session Name : TraceSessionWedJun062021182012

   Attempting to start session TraceSessionWedJun062021182012...
   Trace Session created...Status : 0

   Provider Enable Success, Status : 0

   Provider Enable Success, Status : 0

   Provider Enable Success, Status : 0

   Provider Enable Success, Status : 0

   Provider Enable Success, Status : 0
   12983512883.067484s: (UsbHub3/176):
           Event Message:DescriptorValidationError20HubPortPwrCtrlMaskZero
           VendorID/ProductID: 0x451/0x2077
           DeviceInterfacePath: \??\USB#VID_0451&PID_2077#6&c4be011&0&2#{f18a0e88-c30c-11d0-8815-00a0c906bed8}
           DeviceDescription: Generic USB Hub
           PortPath:  0x2, 0x0, 0x0, 0x0, 0x0, 0x0
   12983512888.452400s: (UsbHub3/173)
           Event Message: SuperSpeed Device is Connected on the 2.0 Bus:
           PortPath:  0x2, 0x4, 0x0, 0x0, 0x0, 0x0
   12983512900.098652s: (UsbHub3/176):
           Event Message:DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
           PortPath:  0x3, 0x0, 0x0, 0x0, 0x0, 0x0
   12983512900.098654s: (UsbHub3/176):
           Event Message:DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
           PortPath:  0x3, 0x0, 0x0, 0x0, 0x0, 0x0
   12983512900.098656s: (UsbHub3/176):
           Event Message:DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
           PortPath:  0x3, 0x0, 0x0, 0x0, 0x0, 0x0
   12983512900.098658s: (UsbHub3/176):
           Event Message:DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
           PortPath:  0x3, 0x0, 0x0, 0x0, 0x0, 0x0
   12983512900.098658s: (UsbHub3/176):
           Event Message:DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
           PortPath:  0x3, 0x0, 0x0, 0x0, 0x0, 0x0
   12983512900.098660s: (UsbHub3/176):
           Event Message:DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
           PortPath:  0x3, 0x0, 0x0, 0x0, 0x0, 0x0
   12983512900.099415s: (UsbHub3/176):
           Event Message:DescriptorValidationErrorStringMismatchBetweenBlengthAndBufferLength
           PortPath:  0x3, 0x0, 0x0, 0x0, 0x0, 0x0
   12983512900.100168s: (UsbHub3/176):
           Event Message:DescriptorValidationErrorStringMismatchBetweenBlengthAndBufferLength
           PortPath:  0x3, 0x0, 0x0, 0x0, 0x0, 0x0

   Provider disable Success, Status : 0

   Provider disable Success, Status : 0

   Provider disable Success, Status : 0

   Provider disable Success, Status : 0

   Provider disable Success, Status : 0

   Session Stopped...Status : 0
   ```

3. CTRL + C キーを押してセッションを停止します。

   セッションの最後に、AllEvents.etl という名前のファイルは、現在のディレクトリに追加されます。 このファイルには、セッション中にキャプチャされたすべてのイベントに関するトレース情報が含まれています。

   AllEvents.etl、だけでなくは、コマンド ウィンドウには、レポートが表示されます。 レポートには、リアルタイムの出力でが実行されなかった特定の情報が含まれます。 次の出力は、前のセッションのテスト レポートの例を示します。 USB ハードウェアの検証が発生したすべてのイベントを表示します。

   ``` syntax
   Record #1 (Key = 0x57ff0de4858)
     VendorID/ProductID: 0x451/0x2077
     DeviceInterfacePath: \??\USB#VID_0451&PID_2077#6&c4be011&0&2#{f18a0e88-c30c-11d0-8815-00a0c906bed8}
     DeviceDescription: Generic USB Hub
     PortPath:  0x2, 0x0, 0x0, 0x0, 0x0, 0x0
     All errors encountered:
   #1: (UsbHub3/176): DescriptorValidationError20HubPortPwrCtrlMaskZero
   #2: (UsbHub3/179): Client Initiated Recovery Action
   #3: (UsbHub3/179): Client Initiated Recovery Action
   #4: (UsbHub3/179): Client Initiated Recovery Action
   #5: (UsbHub3/179): Client Initiated Recovery Action
   #6: (UsbHub3/179): Client Initiated Recovery Action
   #7: (UsbHub3/179): Client Initiated Recovery Action
   #8: (UsbHub3/179): Client Initiated Recovery Action
   #9: (UsbHub3/179): Client Initiated Recovery Action
   #10: (UsbHub3/179): Client Initiated Recovery Action
   #11: (UsbHub3/179): Client Initiated Recovery Action
   #12: (UsbHub3/179): Client Initiated Recovery Action
   #13: (UsbHub3/179): Client Initiated Recovery Action
   #14: (UsbHub3/179): Client Initiated Recovery Action

   Record #2 (Key = 0x57ff62a36a8)
     VendorID/ProductID: 0x1058/0x740
     DeviceInterfacePath: \??\USB#VID_1058&PID_0740#57583931453631414E5A3331#{a5dcbf10-6530-11d2-901f-00c04fb951ed}
     DeviceDescription: USB Mass Storage Device
     PortPath:  0x2, 0x4, 0x0, 0x0, 0x0, 0x0
     All errors encountered:
   #1: (UsbHub3/173): SuperSpeed Device is Connected on the 2.0 Bus

   Record #3 (Key = 0x57ff79fd4e8)
     VendorID/ProductID: 0x1edb/0xbd3b
     PortPath:  0x3, 0x0, 0x0, 0x0, 0x0, 0x0
     All errors encountered:
   #1: (UsbHub3/176): DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
   #2: (UsbHub3/176): DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
   #3: (UsbHub3/176): DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
   #4: (UsbHub3/176): DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
   #5: (UsbHub3/176): DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
   #6: (UsbHub3/176): DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
   #7: (UsbHub3/176): DescriptorValidationErrorStringMismatchBetweenBlengthAndBufferLength
   #8: (UsbHub3/176): DescriptorValidationErrorStringMismatchBetweenBlengthAndBufferLength

   ```

   前の例のレポートで、次に注意してください。、**キー**フィールドの各レコードの値。 レポートによって、情報を分類する**キー**を読みやすくするための値。 同じ**キー**値 AllEvents.etl でキャプチャされたイベントで使用されます。

4. 次のコマンドを実行して AllEvents.etl をテキスト形式に変換します。

   ``` syntax
   USB3HWVerifierAnalyzer.exe -f AllEvents.etl /v > Output.txt 
   ```

   出力ファイルで既に説明したように検索**キー**値。 値は、これらのフィールドのいずれかに関連付けられた: **fid\_UcxController**、 **fid\_HubDevice**、および**fid\_UsbDevice**.

5. Netmon し、AllEvents.etl を開く**追加&lt;フィールド\_名前&gt;フィルターを表示する**コント ローラー、ハブ、およびデバイスでイベントをフィルター処理します。

## <a name="usb-hardware-verifier-flags"></a>USB ハードウェアの検証フラグ


| Flag                                                | 示します.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|-----------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| DeviceHwVerifierClientInitiatedResetPipe            | クライアント ドライバーでは、特定のパイプ I/O エラーに応答をリセットすることで復旧アクションが開始されます。 特定のクライアント ドライバーは、他のシナリオでエラーからの回復を実行する場合があります。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| DeviceHwVerifierClientInitiatedResetPort            | クライアント ドライバーでは、I/O の障害に対する応答として、デバイスをリセットすることで復旧アクションが開始されます。 特定のクライアント ドライバーは、他のシナリオでエラーからの回復を実行する場合があります。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| DeviceHwVerifierClientInitiatedCyclePort            | クライアント ドライバーでは、ポートを循環させることで復旧アクションを開始します。 このフラグが原因で、デバイスを再列挙プラグ アンド プレイのマネージャー。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| DeviceHwVerifierSetIsochDelayFailure                | USB 3.0 デバイス セットに失敗しました\_アイソクロナス\_遅延要求。 デバイスでは、ドライバーには、要求の情報は不要か、または一時的なエラーが発生したため、要求を失敗ことができます。 ただし、それらの理由と、ドライバーを区別できません。 このエラーは、レポートにはキャプチャされません。                                                                                                                                                                                                                                                                                                                                                                                                                         |
| DeviceHwVerifierSetSelFailure                       | USB 3.0 デバイス セットに失敗しました\_セルフ_サービス要求。 デバイスは、リンク電源管理 (LPM) の要求情報を使用します。 デバイスでは、ドライバーには、要求の情報は不要か、または一時的なエラーが発生したため、要求を失敗ことができます。 ただし、それらの理由と、ドライバーを区別できません。 このエラーは、レポートにはキャプチャされません。                                                                                                                                                                                                                                                                                                                                                         |
| DeviceHwVerifierSerialNumberMismatchOnRenumeration  | デバイスを最初に列挙中にレポートされたものではなく再列挙中に別のシリアル番号を報告します。 再列挙体は、リセット ポートまたはシステム再開操作の結果として発生します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| DeviceHwVerifierSuperSpeedDeviceWorkingAtLowerSpeed | USB 3.0 デバイスが SuperSpeed より低いバス速度を動作しています。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| DeviceHwVerifierControlTransferFailure              | デバイスの既定のエンドポイントが失敗するコントロール転送が失敗しました。 デバイスまたはコント ローラーのエラーの結果として、転送は失敗します。 ハブのログは、転送エラーの USBD ステータス コードを示します。 このフラグがセットを除外\_SEL とセット\_アイソクロナス\_遅延コントロールがエラーを転送します。 これらの種類の要求は、DeviceHwVerifierSetIsochDelayFailure と DeviceHwVerifierSetSelFailure フラグが適用されます。                                                                                                                                                                                                                                                                                                                |
| DeviceHwVerifierDescriptorValidationFailure         | デバイスによって返される記述子は、USB 仕様に準拠していません。 ハブのログでは、正確なエラーを示します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| DeviceHwVerifierInterfaceWakeCapabilityMismatch     | RemoteWake ビットが正しく設定されていないデバイス。 リモート ウェイク アップをサポートする USB 3.0 デバイスでは、関数のスリープ解除もサポートする必要があります。 デバイスに、関数のウェイク アップのサポートを示す 2 つの方法はあります。 最初の方法は、使用、 **bmAttributes**構成記述子と、2 番目のフィールドは、GET への応答が\_状態要求の対象とするインターフェイス。 RemoteWake ビット値非複合デバイスの場合、GET によって返される値に一致する必要があります\_0 インターフェイスを対象と進捗します。 複合デバイスは、RemoteWake ビットは少なくとも 1 つの関数の 1 である必要があります。 それ以外の場合、このフラグは、デバイスに、ここに矛盾する値が報告されたことを示します。 |
| DeviceHwVerifierBusRenumeration                     | デバイスでは、バスに再列挙です。 再列挙体は、リセット ポートまたはシステム再開操作の結果として発生します。 再列挙場合も、デバイスが無効/有効にまたは停止して開始します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| HubHwVerifierTooManyResets                          | ハブを行われたすぎるを短期間で多くのリセット操作。 これらのリセットが成功した場合でも、ハブでは、要求は処理されていないとエラーが繰り返し発生します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| HubHwVerifierControlTransferFailure                 | コントロールの転送を対象とするハブの既定のエンドポイントが失敗しました。 デバイスまたはコント ローラーのエラーの結果として、転送は失敗します。 ハブのログは、障害の USBD ステータス コードを示します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| HubHwVerifierInterruptTransferFailure               | データ転送を対象とするハブの割り込みのエンドポイントが失敗しました。 デバイスまたはコント ローラーのエラーの結果として、転送は失敗します。 ハブのログは、障害の USBD ステータス コードを示します。 要求のため失敗しました、転送が取り消された場合、エラーはキャプチャされません。                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| HubHwVerifierNoSelectiveSuspendSupport              | RemoteWake ビットは、ハブの構成記述子では 1 に設定されていません。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| HubHwVerifierPortResetTimeout                       | 中にデバイスを再列挙の列挙または、ポートのリセット操作はタイムアウトになっています。ポートのリセットが完了したことを示すポートの変更通知が受信されません。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| HubHwVerifierInvalidPortStatus                      | USB 仕様に従って、ターゲット ポートのポートの状態が正しくありません。 特定のデバイスには、無効な状態を報告するハブを可能性があります。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| HubHwVerifierPortLinkStateSSInactive                | ターゲット ポートとダウン ストリーム デバイス間のリンクは、エラー状態です。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| HubHwVerifierPortLinkStateCompliance                | 準拠モードでのターゲット ポートとダウン ストリーム デバイスの間のリンクです。 システムのスリープ-再開に関連するシナリオによっては、コンプライアンスのモード エラーが発生し、そのような場合、エラーはキャプチャされません。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| HubHwVerifierPortDeviceDisconnected                 | ターゲット ポートでダウン ストリーム デバイスは、バスに接続していません。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| HubHwVerifierPortOverCurrent                        | ダウン ストリームのポートは、過電流の状態を報告します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| HubHwVerifierControllerOperationFailure             | ターゲット ポートに接続されているデバイスのエンドポイントを構成するデバイスを有効にする) などのコント ローラー操作が失敗しました。 セットからエラー\_エンドポイントのアドレスとリセットの要求はキャプチャされません。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |

 

## <a name="related-topics"></a>関連トピック
[USB の診断結果とテスト ガイド](usb-driver-testing-guide.md)  



