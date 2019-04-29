---
Description: 新機能とのユニバーサル シリアル バス (USB) Windows 8.1 での機能強化を次に示します。
title: Windows 8.1 の新機能については、usb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e7c846902fe660db70227bde70c3a06577e803d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389189"
---
# <a name="windows-81-whats-new-for-usb"></a>Windows 8.1:USB の新機能


新機能とのユニバーサル シリアル バス (USB) Windows 8.1 での機能強化を次に示します。

-   [UWP アプリを開発するための Windows ランタイム USB API](#usb-sdk)
-   [強化されたデバイスの列挙の Microsoft OS 2.0 記述子](#microsoft-os-2-0-descriptors-for-improved-device-enumeration)
-   [WinUSB アイソクロナスのサポート](#usb-wdk)
-   [USB ドライバー スタックの機能強化](#usb-driver-stack-improvements)
-   [USB ハードウェア認定キット (HCK) でのテスト](#usb-tests-in-the-hardware-certification-kit-hck)
-   [USB の強化された診断ツールとデバッガー拡張機能](#improved-usb-diagnostic-tools-and-debugger-extensions-)
-   [関連トピック](#related-topics)

## <a name="windows-runtime-usb-api-for-developing-uwp-apps"></a>UWP アプリを開発するための Windows ランタイム USB API


Windows ランタイムには、新しい名前空間が用意されています。[**Windows.Devices.Usb** ](https://msdn.microsoft.com/library/windows/apps/dn278466) (を参照してください[USB デバイスのアプリの作成 (を使用して UWP アプリC##/vb/c)](https://msdn.microsoft.com/library/windows/apps/xaml/dn263144)簡単な概要について)。 名前空間を使用して、カスタムの USB デバイスと通信する UWP アプリを記述できます。

詳しくは、次のトピックをご覧ください。

-   [USB デバイスとの対話を開始する (UWP アプリ) の完了](talking-to-usb-devices-start-to-finish.md)
-   [アプリケーション マニフェストに USB デバイスの機能を追加する方法](updating-the-app-manifest-with-usb-device-capabilities.md)
-   [USB デバイス (UWP アプリ) に接続する方法](how-to-connect-to-a-usb-device--uwp-app-.md)
-   [USB 制御転送 (UWP アプリ) を送信する方法](how-to-send-a-usb-control-transfer--uwp-app-.md)
-   [USB 割り込み転送要求 (UWP アプリ) を送信する方法](how-to-send-a-usb-interrupt-transfer--uwp-app-.md)
-   [USB 一括転送要求 (UWP アプリ) を送信する方法](how-to-send-a-usb-bulk-transfer--uwp-app-.md)
-   [USB ディスクリプター (UWP アプリ) を取得する方法](how-to-get-usb-descriptors--uwp-app-.md)
-   [USB インターフェイスの設定 (UWP アプリ) を選択する方法](how-to-select-a-usb-interface-setting--uwp-app-.md)

これらのサンプルの使用法を示す、 [ **Windows.Devices.Usb** ](https://msdn.microsoft.com/library/windows/apps/dn278466)名前空間。

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
<td><p><a href="" id="custom-usb-device-access-sample"></a><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[Custom USB device access sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">カスタム USB デバイスへのアクセスのサンプル</a></p></td>
<td><p>このサンプルでは、USB デバイスと通信する方法を示します。 このサンプルは、OSR USB FX2 ラーニング キットと SuperMUTT デバイスと通信できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="usb-cdc-control-sample"></a><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[USB CDC Control sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">USB CDC コントロールのサンプル</a></p></td>
<td><p>このサンプルは、CDC (通信デバイス クラス) の USB デバイスと通信する方法を示していて、送信し、USB シリアル コンバーター ケーブルなどのシリアル ポートを使用してデータを受け取ります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="firmware-update-usb-device-sample"></a><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[Firmware Update USB Device sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">ファームウェアの更新プログラムの USB デバイスのサンプル</a></p></td>
<td><p>このサンプルでは、UWP アプリが、USB デバイスのファームウェアを更新する方法を示します。 更新操作は、バック グラウンド タスクとして実行されます。</p></td>
</tr>
</tbody>
</table>

## <a name="microsoft-os-20-descriptors-for-improved-device-enumerations"></a>強化されたデバイスの列挙型の Microsoft OS 2.0 記述子 
 
Microsoft OS 2.0 記述子は、デバイスの識別とドライバーのインストールを向上させるエクスペリエンスします。

MS OS 2.0 記述子の仕様では、これらの機能強化を提供します。

-   デバイス プラットフォームに固有のプロパティを返すことを許可するには、新しい BOS デバイス機能記述子を定義します。 BOS 記述子は、検索は、通常、意図しないデバイスの動作につながる必要がありますいない列挙型が必要な手順は、USB バージョン 2.1 以降の標準の USB 仕様で定義された標準的な記述子です。
-   記述子を対象とすると、デバイス全体、特定の構成、または関数を使用できます。
-   により、デバイスを複数の記述子のセットを返す各セットが特定の範囲の Windows バージョンに適用されます。 これにより、デバイスが接続されているシステム上の Windows のバージョンに応じて異なる方法で列挙できます。
-   再開時間を短縮:デバイスは、時間が短縮される再開時間を識別できますから状態を中断します。

仕様の詳細については、次を参照してください。 [USB デバイスの Microsoft OS ディスクリプター](microsoft-defined-usb-descriptors.md)します。

## <a name="isochronous-support-for-winusb"></a>WinUSB アイソクロナスのサポート


Microsoft 提供の WinUSB (カーネル モード ドライバー) と、USB デバイスのアイソクロナス エンドポイントの転送をようになりました

ユーザー モード DLL、Winusb.dll、公開これら[WinUSB Functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb) Windows デスクトップ アプリを使用してこのような転送を開始します。

-   [**WinUsb\_RegisterIsochBuffer**](https://msdn.microsoft.com/library/windows/hardware/dn265566)
-   [**WinUsb\_UnregisterIsochBuffer**](https://msdn.microsoft.com/library/windows/hardware/dn265567)
-   [**WinUsb\_WriteIsochPipeAsap**](https://msdn.microsoft.com/library/windows/hardware/dn265569)
-   [**WinUsb\_ReadIsochPipeAsap**](https://msdn.microsoft.com/library/windows/hardware/dn265565)
-   [**WinUsb\_WriteIsochPipe**](https://msdn.microsoft.com/library/windows/hardware/dn265568)
-   [**WinUsb\_ReadIsochPipe**](https://msdn.microsoft.com/library/windows/hardware/dn265564)
-   [**WinUsb\_GetCurrentFrameNumber**](https://msdn.microsoft.com/library/windows/hardware/dn265549)
-   [**WinUsb\_GetAdjustedFrameNumber**](https://msdn.microsoft.com/library/windows/hardware/dn265548)

## <a name="usb-driver-stack-improvements"></a>USB ドライバー スタックの機能強化


Windows 8.1 のでは、USB 3.0 と 2.0 ドライバー スタックの両方の信頼性とパフォーマンスが改善されました。

-   InstantGo をサポートする新しいプラットフォーム、S0 の全体的なシステム電源消費量が非常に短いことがあります。 このようなシステムの場合でも、USB デバイスが中に選択的に使用するいくつかのミリ ワットの中断、重要で開始します。 新しいシステムの最適化の電源の目標が、USB 2.0 スタックとで、Usbccgp.sys と USB 3.0 ドライバー スタックの強化された Windows 8 の実装、D3cold を実装します。
-   ドライバーがインストールされていないときに電源管理が向上します。 USB ドライバー スタックは、今すぐ、ハブ、コント ローラーに接続されている唯一のデバイスである場合に中断する原因となる USB ポートを中断します。
-   ウォッチドッグのタイムアウトのクラッシュを回避するためには、DPC のパフォーマンスが改善されました。
-   デバイスが USB 2.0 仕様で指定された既定値は 10 ミリ秒よりも高速回復できるようになりました。 また、ホスト コント ローラーのドライバーは、再開の USB 2.0 仕様に必要な 20 ミリ秒未満の信号をアサートします。
-   USB 3.0 ドライバー スタックは、コントロールや一括 isochronous データ転送を実行するときより信頼性の高いようになりました。

## <a name="usb-tests-in-the-hardware-certification-kit-hck"></a>USB ハードウェア認定キット (HCK) でのテスト

-   これらの USB テスト ハードウェア認定キット (HCK) でが改善されました。 デバイスの列挙型のテストは、簡略化されたトポロジを使用してテスト中に手動介入を削減する新しいパラメーターを指定するようになりました。 中断のテストは、改善されたロギング機能しました。

    -   [USB ポートが公開されているコント ローラーのテスト](https://msdn.microsoft.com/library/windows/hardware/hh998021.aspx)
    -   [USB ハブに USB ポートのテストが公開されています。](https://msdn.microsoft.com/library/windows/hardware/jj123960.aspx)
    -   [ハブの選択的テストを中断します。](https://msdn.microsoft.com/library/windows/hardware/jj124844.aspx)
    -   [USB 公開ポート システム テスト](https://msdn.microsoft.com/library/windows/hardware/jj123655.aspx)
    -   [USB セレクティブ サスペンド テスト (xHCI)](https://msdn.microsoft.com/library/windows/hardware/jj124491.aspx)
    -   [USB 3.0 テストを中断します。](https://msdn.microsoft.com/library/windows/hardware/jj125210.aspx)
-   MUTT および SuperMUTT デバイスが USB-準拠デバイスの場合。 デバイスと付属のソフトウェア パッケージに USB テストの HCK スイートに統合します。 USB のコントローラー、デバイス、システムの開発周期において、特にストレス テストにおいて使用できる自動化されたテストを提供します。

    MUTT ハードウェアを購入できる[JJG テクノロジ](http://jjgtechnologies.com/mutt.md)します。 デバイスのファームウェアがインストールされているインストールではありません。 ファームウェアをインストールするから MUTT ソフトウェア パッケージをダウンロード[この Web サイト](https://msdn.microsoft.com/windows/hardware/jj590752)MUTTUtil.exe を実行します。 詳細については、パッケージに付属のマニュアルを参照してください。

## <a name="improved-usb-diagnostic-tools-and-debugger-extensions"></a>USB の強化された診断ツールとデバッガー拡張機能


-   コマンド、同様のパターンには、USB 2.0 および 3.0 (USBKD.dll および USB3KD.dll) 用のカーネル デバッグ拡張機能が強化されました。 Usbccgp.sys のデバッガーの拡張機能は、ご利用いただけます。
-   Message Analyzer (Netmon) に示すように USB イベントとはわかりやすいようになりました。 イベントをグループ化もしてコント ローラー、ハブ、およびなどで並べ替えられます。

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://msdn.microsoft.com/library/windows/hardware/ff538930)  



