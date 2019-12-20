---
Description: Windows 8.1 での Universal Serial Bus (USB) の新機能と強化された機能を次に示します。
title: Windows 8.1-USB の新機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce6171bcef7118b24ba3a43fea7b520b4b369c6c
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210144"
---
# <a name="windows-81-whats-new-for-usb"></a>Windows 8.1: USB の新機能


Windows 8.1 での Universal Serial Bus (USB) の新機能と強化された機能を次に示します。

-   [UWP アプリを開発するための Windows ランタイムの USB API](#windows-runtime-usb-api-for-developing-uwp-apps)
-   [デバイスの列挙を改善するための Microsoft OS 2.0 記述子](#microsoft-os-20-descriptors-for-improved-device-enumerations)
-   [WinUSB のアイソクロナスサポート](#isochronous-support-for-winusb)
-   [USB ドライバースタックの機能強化](#usb-driver-stack-improvements)
-   [ハードウェア認定キット (HCK) の USB テスト](#usb-tests-in-the-hardware-certification-kit-hck)
-   [強化された USB 診断ツールとデバッガー拡張機能](#improved-usb-diagnostic-tools-and-debugger-extensions)
-   [関連トピック](#related-topics)

## <a name="windows-runtime-usb-api-for-developing-uwp-apps"></a>UWP アプリを開発するための Windows ランタイムの USB API


Windows ランタイムには、新しい名前空間が用意され[**ています (「** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb) [usb デバイスC#C++用アプリの作成](https://docs.microsoft.com/previous-versions/windows/apps/dn263144(v=win.10))」を参照)。簡単な概要については、「」を参照してください。 名前空間を使用すると、カスタム USB デバイスと通信する UWP アプリを作成できます。

詳しくは、次のトピックをご覧ください。

-   [USB デバイスとの対話、終了の開始 (UWP アプリ)](talking-to-usb-devices-start-to-finish.md)
-   [アプリマニフェストに USB デバイス機能を追加する方法](updating-the-app-manifest-with-usb-device-capabilities.md)
-   [USB デバイスに接続する方法 (UWP アプリ)](how-to-connect-to-a-usb-device--uwp-app-.md)
-   [USB 制御転送を送信する方法 (UWP アプリ)](how-to-send-a-usb-control-transfer--uwp-app-.md)
-   [USB 割り込み転送要求を送信する方法 (UWP アプリ)](how-to-send-a-usb-interrupt-transfer--uwp-app-.md)
-   [USB 一括転送要求を送信する方法 (UWP アプリ)](how-to-send-a-usb-bulk-transfer--uwp-app-.md)
-   [USB 記述子を取得する方法 (UWP アプリ)](how-to-get-usb-descriptors--uwp-app-.md)
-   [USB インターフェイス設定を選択する方法 (UWP アプリ)](how-to-select-a-usb-interface-setting--uwp-app-.md)

これらのサンプルでは、 [**Windows のデバイス**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)の名前空間の使用方法を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>UWP アプリのサンプル</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="" id="custom-usb-device-access-sample"></a><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[Custom USB device access sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">カスタム USB デバイスアクセスのサンプル</a></p></td>
<td><p>このサンプルでは、USB デバイスと通信する方法を示します。 このサンプルは、OSR USB FX2 learning kit および SuperMUTT デバイスと通信できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="usb-cdc-control-sample"></a><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[USB CDC Control sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">USB CDC 制御のサンプル</a></p></td>
<td><p>このサンプルでは、usb CDC (通信デバイスクラス) デバイスと通信し、USB シリアルコンバーターケーブルなどのシリアルポートを介してデータを送受信する方法を示します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="firmware-update-usb-device-sample"></a><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[Firmware Update USB Device sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">ファームウェア更新の USB デバイスのサンプル</a></p></td>
<td><p>このサンプルでは、UWP アプリで USB デバイスのファームウェアを更新する方法を示します。 更新操作はバックグラウンドタスクとして実行されます。</p></td>
</tr>
</tbody>
</table>

## <a name="microsoft-os-20-descriptors-for-improved-device-enumerations"></a>デバイスの列挙を改善するための Microsoft OS 2.0 記述子 
 
Microsoft OS 2.0 記述子により、デバイスの識別とドライバーのインストールエクスペリエンスが向上します。

MS OS 2.0 記述子の仕様では、次の機能強化が行われています。

-   デバイスがプラットフォーム固有のプロパティを返すことができるように、新しい BOS デバイス機能記述子を定義します。 BOS 記述子は、USB バージョン2.1 以上の標準の USB 仕様で定義されている標準記述子です。そのため、予期しないデバイスの動作を発生させないようにするために、通常の列挙の手順が必要になります。
-   デバイス全体、特定の構成、または関数に対して、記述子のスコープを設定できます。
-   各セットが Windows の特定の範囲に適用される複数の記述子セットをデバイスが返すことができるようにします。 これにより、デバイスが接続されているシステム上の Windows のバージョンによって、デバイスの列挙が異なることがあります。
-   再開時間の短縮: デバイスは再開時間を識別できるため、中断状態からの時間が短縮されます。

仕様の詳細については、「 [USB デバイス用の MICROSOFT OS 記述子](microsoft-defined-usb-descriptors.md)」を参照してください。

## <a name="isochronous-support-for-winusb"></a>WinUSB のアイソクロナスサポート


Microsoft 提供の WinUSB (カーネルモードドライバー) は、USB デバイスのアイソクロナスエンドポイントとの間の転送をサポートするようになりました。

ユーザーモードの DLL である Winusb .dll は、Windows デスクトップアプリがこのような転送を開始するために使用できる[Winusb 関数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)を公開します。

-   [**WinUsb\_RegisterIsochBuffer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_registerisochbuffer)
-   [**WinUsb\_UnregisterIsochBuffer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_unregisterisochbuffer)
-   [**WinUsb\_WriteIsochPipeAsap**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap)
-   [**WinUsb\_ReadIsochPipeAsap**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap)
-   [**WinUsb\_WriteIsochPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe)
-   [**WinUsb\_ReadIsochPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipe)
-   [**WinUsb\_GetCurrentFrameNumber**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getcurrentframenumber)
-   [**WinUsb\_GetAdjustedFrameNumber**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getadjustedframenumber)

## <a name="usb-driver-stack-improvements"></a>USB ドライバースタックの機能強化


Windows 8.1 では、USB 3.0 と2.0 の両方のドライバースタックのパフォーマンスと信頼性が向上しています。

-   InstantGo をサポートする新しいプラットフォームでは、S0 の全体的なシステム電力消費量が非常に低くなる可能性があります。 このようなシステムでは、USB デバイスがセレクティブサスペンド中に使用する数ミリワットもありますが、これは重要です。 新しいシステムの電力を最適化することを目標として、usb 2.0 stack と Usbccgp の D3cold と、USB 3.0 ドライバースタックの強化された Windows 8 実装を実装しました。
-   ドライバーがインストールされていない場合の電源管理の向上。 USB ドライバースタックは、コントローラーに接続されている唯一のデバイスである場合、ハブが中断する原因となる USB ポートを中断するようになりました。
-   ウォッチドッグのタイムアウトがクラッシュしないように、DPC のパフォーマンスが向上しました。
-   USB 2.0 仕様で指定されている既定の10ミリ秒より早くデバイスを回復できるようになりました。 また、ホストコントローラードライバーは、USB 2.0 仕様で必要とされる20ミリ秒未満の信号の再開をアサートします。
-   コントロール、一括、およびアイソクロナスデータ転送を実行すると、USB 3.0 ドライバースタックの信頼性が向上しました。

## <a name="usb-tests-in-the-hardware-certification-kit-hck"></a>ハードウェア認定キット (HCK) の USB テスト

-   ハードウェア認定キット (HCK) のこれらの USB テストが改善されました。 デバイスの列挙テストに新しいパラメーターが追加されました。これにより、簡略化されたトポロジを使用したテスト中の手動介入が減少します。 中断テストのログ記録機能が改善されました。

    -   [USB で公開されているポートコントローラーのテスト](https://docs.microsoft.com/previous-versions/windows/hardware/hck/hh998021(v=vs.85))
    -   [USB ハブの公開ポートテスト USB](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj123960(v=vs.85))
    -   [ハブの選択的中断テスト](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124844(v=vs.85))
    -   [USB 公開ポート システム テスト](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj123655(v=vs.85))
    -   [USB 選択的中断テスト (xHCI)](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124491(v=vs.85))
    -   [USB 3.0 テストの中断](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj125210(v=vs.85))
-   MUTT と SuperMUTT デバイスは、現在は USB に準拠しているデバイスです。 デバイスと付随するソフトウェアパッケージは、HCK suite の USB テストに統合されています。 USB のコントローラー、デバイス、システムの開発周期において、特にストレス テストにおいて使用できる自動化されたテストを提供します。

    MUTT ハードウェアは、 [Jjg テクノロジ](https://jjgtechnologies.com/mutt.md)から購入できます。 デバイスにインストールされているファームウェアがインストールされていません。 ファームウェアをインストールするには、[この Web サイト](https://msdn.microsoft.com/windows/hardware/jj590752)から MUTT ソフトウェアパッケージをダウンロードし、MUTTUtil を実行します。 詳細については、パッケージに含まれているドキュメントを参照してください。

## <a name="improved-usb-diagnostic-tools-and-debugger-extensions"></a>強化された USB 診断ツールとデバッガー拡張機能


-   USB 2.0 と3.0 のカーネルデバッグ拡張機能 (USBKD .dll および USB3KD) が、類似したコマンドパターンになるように改善されました。 Usbccgp のデバッガー拡張機能を使用できるようになりました。
-   Message Analyzer (Netmon) に表示される USB イベントは、よりわかりやすいものになりました。 イベントは、コントローラーやハブなどによってグループ化および並べ替えを行うこともできます。

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  



