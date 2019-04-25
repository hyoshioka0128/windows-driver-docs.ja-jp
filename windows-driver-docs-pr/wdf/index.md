---
title: Windows 10 の WDF ドライバーの新機能
description: Windows 10 の WDF ドライバーの新機能と機能強化についてまとめています。
ms.assetid: 61fd9916-38e7-47d0-aec7-d5a489eb21eb
keywords:
- カーネルモード ドライバー WDK KMDF、KMDF について
- KMDF WDK、KMDF について
- カーネルモード ドライバー フレームワーク WDK、KMDF について
- フレームワークベース ドライバー WDK KMDF
- フレームワークベース ドライバー WDK KMDF、フレームワークベース ドライバーについて
- オブジェクト WDK KMDF
- フレームワーク オブジェクト WDK KMDF
ms.date: 10/02/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.custom: 19H1
ms.openlocfilehash: 2d3dc6a72993a7df74bae3de857cefd7709b52b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386460"
---
# <a name="whats-new-for-wdf-drivers-in-windows10"></a>Windows 10 の WDF ドライバーの新機能

このトピックでは、Windows 10 の Windows Driver Frameworks (WDF) の新機能と機能強化についてまとめています。

Windows 10、バージョン 1903 (2019 年 3 月更新、19H1) には、カーネル モード ドライバー フレームワーク (KMDF) バージョン 1.29 とユーザー モード ドライバー フレームワーク (UMDF) バージョン 2.29 が含まれます。

これらのフレームワーク バージョンを使用し、次のドライバーを構築できます。

-   Windows 10 (すべての SKU)
-   Windows Server、バージョン 1809

バージョン履歴については、「[KMDF バージョン履歴](kmdf-version-history.md)」と「[UMDF バージョン履歴](umdf-version-history.md)」を参照してください。 注記のあるものを除き、このページの UMDF 参照は、UMDF バージョン 1 では利用できないバージョン 2 の機能を表します。

## <a name="new-in-wdf-for-windows-10-version-1903"></a>Windows 10、バージョン 1903 の WDF の新機能

追加または変更された機能はありません。

## <a name="new-in-wdf-for-windows-10-version-1809"></a>Windows 10、バージョン 1809 の WDF の新機能

* 新しい API [**WdfDriverRetrieveDriverDataDirectoryString**](/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdriverretrievedriverdatadirectorystring) が追加されました

## <a name="new-in-wdf-for-windows-10-version-1803"></a>Windows 10、バージョン 1803 の WDF の新機能

* [複数のバージョンの Windows の WDF ドライバーをビルドする](building-a-wdf-driver-for-multiple-versions-of-windows.md)。
* [**WdfDeviceRetrieveDeviceDirectoryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceretrievedevicedirectorystring)

## <a name="new-in-wdf-for-windows-10-version-1709"></a>Windows 10、バージョン 1709 の WDF の新機能

「[KMDF バージョン履歴](kmdf-version-history.md)」と「[UMDF バージョン履歴](umdf-version-history.md)」を参照してください。

## <a name="new-in-wdf-for-windows-10-version-1703"></a>Windows 10、バージョン 1703 の WDF の新機能

Windows 10、バージョン 1703 では、WDF に以下の機能強化が含まれています。

* 過度のオブジェクト作成を検出する新しい WDF 検証ツール設定
 
    フレームワーク オブジェクトの親が正しく設定されず、使用後に削除されない場合があります。  この機能を利用すると、オブジェクトの最大数やこのしきい値を超過したときの動作を指定できます。
    
    監視を始めるには、次の場所に以下のレジストリ値を追加します。`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\<driver service>\Parameters\wdf`
    
  1. しきい値と共に **ObjectLeakDetectionLimit** という名前の DWORD 値を追加します。 これは **ObjectsForLeakDetection** キーで説明されている種類のオブジェクトの最大数です。
    
  2. **ObjectsForLeakDetection** という名前の新しい REG_MULTI_SZ 値を追加します。これは検証する各種類の名前を一覧表示します。 たとえば、`WDFDMATRANSACTION WDFDEVICE` を指定できます。 ハンドルの型をすべて指定するには、文字列として `*` を使用します。

  3. このしきい値を超えた場合にデバッグ解除かバグチェックを実行するかどうかを制御するには、[DbgBreakOnError](using-kmdf-verifier.md) キーを設定します。

     既定では、ObjectsForLeakDetection キーが指定されない場合、フレームワークによって WDFREQUEST、WDFWORKITEM、WDFKEY、WDFSTRING、WDFOBJECT、WDFDEVICE が監視されます。
    
     上限はインストールされているデバイスの数によって変化します。そのため、ドライバーによって 3 つの WDFDEVICE オブジェクトが作成される場合、WDF 検証ツールの上限は **ObjectLeakDetectionLimit** に指定されている値の 3 倍になります。
    
     WDFREQUEST を指定した場合、検索ツールでは、ドライバーによって作成される WDFREQUEST オブジェクトの数だけが数えられます。
    
     この機能は現在のところ、WDFMEMORY オブジェクトを追跡できます。 

* SleepStudy ツールから KMDF ドライバーに関する情報が提供される

    SleepStudy ソフトウェア ツールからは、システムがスリープに入ることを防ぐ、KMDF ドライバーの電源参照の数が報告されます。  詳細については、「[モダン スタンバイの SleepStudy](https://msdn.microsoft.com/windows/hardware/commercialize/design/device-experiences/modern-standby-sleepstudy)」を参照してください。

このページの残りでは、Windows 10、バージョン 1507 で追加された機能について説明します。

## <a name="wdf-source-code-is-publicly-available"></a>WDF ソース コードが公開中


-   WDF ソース コードは GitHub でオープン ソースとして入手できます。 これは、Windows 10 に付属する WDF ランタイム ライブラリのソース コードと同じです。 ドライバーと WDF のやりとりを追跡できるとき、ドライバーをさらに効果的にデバッグできます。 <http://github.com/Microsoft/Windows-Driver-Frameworks> からダウンロードしてください。

-   Windows 10 の WDF のプライベート シンボル ファイルが Microsoft Symbol Server から入手できるようになりました。

-   Windows Driver Kit (WDK) 10 サンプルも GitHub に公開されています。 <http://github.com/Microsoft/Windows-Driver-Samples> からダウンロードしてください。

## <a name="automatic-source-level-debugging-of-framework-code"></a>フレームワーク コードの自動ソース レベル デバッグ


WinDbg を使用して Windows 10 の WDF ドライバーをデバッグするとき、WinDbg によって Microsoft のパブリック GitHub リポジトリからフレームワーク ソース コードが自動的に取得されます。 この機能を利用することで、デバッグ中に WDF ソース コードをステップ実行したり、ローカル マシンにソース コードをダウンロードせず、フレームワークの内部に関する情報を取得したりできます。 詳細については、「[New support for source-level debugging of WDF code in Windows 10](https://go.microsoft.com/fwlink/p/?LinkId=618534)」 (Windows 10 の WDF コードをソース レベルでデバッグするための新しいサポート)、「[Debugging with WDF Source](https://go.microsoft.com/fwlink/p/?LinkId=618535)」 (WDF ソースでデバッグする)、「[Video: Debugging your driver with WDF source code](video--debugging-your-driver-with-wdf-source-code.md)」 (動画: WDF ソース コードでドライバーをデバッグする) を参照してください。

## <a name="universal-driver-compliance"></a>ユニバーサル ドライバー コンプライアンス


WDF ドライバーのサンプルと Visual Studio ドライバーのテンプレートはすべて、[ユニバーサル Windows ドライバー](https://msdn.microsoft.com/windows-drivers/develop/getting_started_with_universal_drivers)に準拠しています。

KMDF と UMDF 2 の機能はすべて、ユニバーサル Windows ドライバーに準拠しています。

UMDF 1 ドライバーは、Windows 10 デスクトップ エディションとそれ以前のデスクトップ版 Windows でのみ動作します。 UMDF 2 のユニバーサル機能を活用しますか。 以前の UMDF 1 ドライバーを移植する方法については、「[UMDF 1 から UMDF 2 にドライバーを移植する](porting-a-driver-from-umdf-1-to-umdf-2.md)」を参照してください。

## <a name="debugging-and-diagnosability"></a>デバッグと診断


-   すべての KMDF ドライバーと UMDF 2 ドライバーで、常にオンで常に利用できる Inflight Trace Recorder (IFR) を使用できます。 ドライバーからカスタム トレースが与えられるとき、ドライバー IFR ログにはトレース メッセージが含まれます。 新しいドライバー IFR ログは、ドライバーごとに WDF によって作成されるフレームワーク IFR ログとは分かれていることに注目してください。

    IFR は簡単にオンにできます。 「[トレースをログに記録するための Inflight Trace Recorder (IFR)](https://msdn.microsoft.com/library/windows/hardware/dn914610)」と「[KMDF ドライバーと UMDF ドライバーで Inflight Trace Recorder を使用する](using-wpp-software-tracing-in-kmdf-and-umdf-2-drivers.md)」を参照してください。

-   IFR によって、ページングできないメモリの WPP トレースの循環バッファーが保守管理されます。 ドライバーがクラッシュする場合、クラッシュ ダンプ ファイルにログが入っていることがたびたびあります。

-   ドライバー バイナリで IFR をオンにすると、ドライバーが使われている間、IFR は存在し、動作します。 トレース収集セッションを明示的に開始する必要はありません。

    -   IFR ログは、それを担当するドライバーが不明の場合やクラッシュがホストのタイムアウトであった場合を除き、ミニダンプ ファイルに入ります。

    -   デバッガーを接続している場合、[**!wdfkd.wdflogdump**](https://msdn.microsoft.com/library/windows/hardware/ff565805) を発行することでドライバーとフレームワークの両方の IFR ログにアクセスできます。

    -   デバッガーを接続していない場合でも両方のログにアクセスできます。  方法については、「[ デバッガーなしでドライバー IFR ログにアクセスする](video--accessing-driver-ifr-logs-without-a-debugger.md)」 を参照してください。

    -   UMDF ドライバーをデバッグするとき、**!wdfkd.wdflogdump** *&lt;drivername.dll&gt;* **-m** を発行することでフレームワーク ログとドライバー ログを結合できます。

-   UMDF ログ (WudfTrace.etl) とダンプは、%ProgramData%\\Microsoft\\WDF instead of %systemDrive%\\LogFiles\\Wudf に置かれるようになりました。

-   新しいデバッガー コマンド [**!wdfkd.wdfumtriage**](https://msdn.microsoft.com/library/windows/hardware/dn961126) を実行すると、システムの全 UMDF デバイスをカーネルを中心として表示できます。

-   [**!analyze**](https://msdn.microsoft.com/library/windows/hardware/ff562112) を実行すると、UMDF 検証ツールの失敗や UMDF の未処理例外を調査できます。 これはライブ カーネル デバッグと、*%ProgramData%*\\Microsoft\\WDF からのユーザー クラッシュ ダンプ ファイルのデバッグで機能します。

-   KMDF と UMDF 2 では、デバッガーの電源参照使用を監視できます。 詳細については、「[WDF を使用した Power 参照リークのデバッグ](debugging-power-reference-leaks-in-wdf.md)」を参照してください。

-   [**!wdfkd.wdfcrashdump**](https://msdn.microsoft.com/library/windows/hardware/ff565682) を使用すると、UMDF 2 ドライバーに関するエラー情報を表示できます。 詳細については、「**!wdfkd.wdfcrashdump**」を参照してください。

## <a name="performance-tracing-tool-for-wdf-drivers"></a>WDF ドライバーのパフォーマンス トレース ツール


Windows Performance Toolkit (WPT) を使用すると、所与の KMDF または UMDF 2 ドライバーのパフォーマンス データを表示できます。 トレースを有効にすると、フレームワークによって I/O、PnP、電源コールバック パスの ETW イベントが生成されます。 その後、I/O スループット レート、CPU 利用率、コールバック パフォーマンスを示す Windows Performance Analyzer (WPA) でグラフを表示できます。 WPT は Windows アセスメント & デプロイメント キット (ADK) に含まれています。

詳細については、「[Windows 10 の WDF ドライバー向けの新しいパフォーマンス ツール]( https://go.microsoft.com/fwlink/p/?LinkId=618537)」と「[WDF で Windows Performance Toolkit (WPT) を使用する](using-the-windows-performance-toolkit--wpt--with-wdf.md)」を参照してください。

## <a name="additional-support-for-hid-drivers-in-umdf"></a>UMDF の HID ドライバー向け追加サポート


-   UMDF は、HID フィルター (HIDClass によって列挙) とミニドライバーに完全対応しています。 既存の KMDF ドライバーを移植するか、新しい UMDF 2 フィルターを記述します。機能は自動的に有効になります。

-   ACPI によって列挙される UMDF HID ミニドライバーでは、選択的に中断できます。 詳細については、「[WDF HID ミニドライバーの作成](creating-umdf-hid-minidrivers.md)」を参照してください。

-   UMDF ドライバーを HID スタックにインストールし、タッチやマウスなど、入力デバイスの遅延を少なくすることができるようになりました。 入力デバイスのドライバーでは、**UmdfHostPriority** INF ディレクティブを指定する必要があります。 詳細については、「[INF ファイルでの WDF ディレクティブの指定](specifying-wdf-directives-in-inf-files.md)」を参照してください。

## <a name="support-for-interrupts-for-gpio-backed-devices"></a>GPIO でバックアップされるデバイスの割り込みをサポート


-   UMDF 2 では、ハードウェア プッシュ ボタンなど、GPIO でバックアップされるデバイスの割り込みがサポートされています。 KMDF では、「[Active-Both 割り込みの処理](handling-active-both-interrupts.md)」を参照してください。 詳細については、「[割り込みオブジェクトの作成](creating-an-interrupt-object.md)」を参照してください。

## <a name="umdf-no-longer-requires-winusb"></a>UMDF では WinUSB が不要になる


UMDF には、USB ドライバーの新しいサポートが追加されました。 UMDF 2 USB ドライバーでは WinUSB が使われなくなりました。 新しい機能を使用するために、ドライバーによって **WinUSB** ではなく **NativeUSB** に **UmdfDispatcher** ディレクティブが設定されます。 「[Specifying WDF Directives in INF Files](specifying-wdf-directives-in-inf-files.md)」 (INF ファイルに WDF ディレクティブを指定する) を参照してください。


## <a name="improved-performance"></a>パフォーマンスの向上


-   UMDF システム コンポーネントによるディスク領域の使用量が少なくなりました。

-   KMDF ドライバーと UMDF ドライバーでは、非ページ メモリの使用量が少なくなりました。

-   フレームワーク バージョンのチェック機能が改善され、ヘッダー/ライブラリの不一致が減りました。

-   UMDF の HID 転送のバッファー マッピングが改善されました。

 

 





