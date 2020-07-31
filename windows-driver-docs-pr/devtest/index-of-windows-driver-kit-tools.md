---
title: Windows Driver Kit のツールの索引
description: Windows Driver Kit のツールの索引
ms.assetid: 26db88c4-8fb8-4308-ab8a-1a1eef5e19d8
keywords:
- Disabler ツール
- DbgCon ツール
- Sniffir ツール
- Sledge ツール
- 使用状況検証ツールの呼び出し
- CUV ツール
- ツール WDK、一覧
- ドライバー開発ツール WDK、一覧
- スリープ状態の選択
- sleeper
- Acpislp
- 手動による電源状態の変更テスト
- Guidgen.exe WDK
- GUID ジェネレーター WDK
- WDK GUIDGen.exe
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: e16624f1566ea430b3d0712bd9258a644aa9c047
ms.sourcegitcommit: 7a7ce6070ed16673108cc64c33b3ddb894453cfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87412545"
---
# <a name="index-of-windows-driver-kit-tools"></a>Windows Driver Kit のツールの索引

このトピックでは、Windows Driver Kit (WDK) に含まれるツールに関する基本的な情報を提供します。 このトピックには、ドライバーの開発に役立つその他のツールへの参照も含まれています。 これらの他のツールは、オペレーティングシステムの一部として使用することも、個別のダウンロードとして入手することもできます。 各ツールの詳細については、このトピックのツールに関するドキュメントを参照してください。

最新の WDK を入手する方法については、「 [Windows Driver Kit (wdk) のダウンロード](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)」を参照してください。

## <a name="index-of-wdk-tools"></a>WDK ツールのインデックス

次の表の情報は、Windows ドライバー開発者に役立つツールについて説明しています。 ツールの一覧には、WDK に付属するツール ( **wdk ツール**フィールドによって示される) が含まれています。また、個別に利用できるツールや、Windows と共にインストールされるツールも含まれています。 すべてのドライバーで一般的に使用できるツールは、[すべて](#all-drivers)のドライバーの下に一覧表示されます。 テクノロジに固有のツールは、 [Windows ポータブルデバイス (WPD) ドライバー](#windows-portable-devices-wpd-drivers)や[センサー](#sensors)に固有のツールなど、グループ化されています。

- [オーディオ/ビデオドライバー](#audio--video-drivers)
- [Bluetooth ドライバー](#bluetooth-drivers)
- [Windows イメージ取得 (WIA) ドライバー](#windows-image-acquisition-wia-drivers)
- [Windows ポータブルデバイス (WPD) ドライバー](#windows-portable-devices-wpd-drivers)
- [プリンタードライバー](#printer-drivers)
- [センサー](#sensors)
- [All Drivers (すべてのドライバー)](#all-drivers)

>[!NOTE]
>Visual Studio 環境変数% WindowsSdkDir% は、このバージョンの WDK がインストールされている Windows kit ディレクトリへのパス (たとえば、C: \\ Program Files (x86) \\ windows kit 8.1) を表し \\ ます。

### <a name="audio--video-drivers"></a>オーディオ/ビデオドライバー

|ツール名|ツールの場所|説明とヘルプファイルの場所|
|----|----|----|
|カラー調整ツールを表示する (Dccw.exe) </br>**WDK ツール**: いいえ|% Windir% \System32\Dccw.exe</br>|調整ツール。ユーザーが表示色を調整して、Windows および World Wide Web 国際標準の赤と青 (sRGB) の色空間に近づけることができます。|
|GraphEdt (Graphedt.exe)</br>**WDK のツール:** うん|% WindowsSdkDir% \tools\x86\graphedt.exe</br>% WindowsSdkDir% \tools\x64\graphedt.exe|フィルターグラフをビルドして、ストリーミングオーディオ/ビデオキャプチャドライバーをテストします。</br>ドキュメント</br>[GraphEdit の概要](https://docs.microsoft.com/windows/win32/directshow/simulating-graph-building-with-graphedit)|
|KSStudio (KsStudio.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x86\KsStudio.exe</br> % WindowsSdkDir% \tools\x64\KsStudio.exe</br></br>**メモ**このツールは、管理者特権を持つユーザーが実行する必要があります。|このツールでは、フィルターとフィルターの内部ノードの間のピン留めピン接続を示すフィルターグラフをグラフィカルに表示できます。</br>%WindowsSdkDir%\tools\x86\KsStudio.chm</br>%WindowsSdkDir%\tools\x64\KsStudio.chm</br>詳細については[、「Avstream のテストとデバッグ](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-testing-and-debugging)」を参照してください。|
|USB デバイスビューアー (Usbview.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x86\Usbview.exe</br>% WindowsSdkDir% \tools\x64\Usbview.exe|USB ホストコントローラー、USB ハブ、および接続されている USB デバイスを列挙し、デバイスに関する情報をレジストリから、および USB 要求を介してデバイスに照会できます。</br>USB デバイスビューアーのソースコードは、コードギャラリーから入手できます。「 [Usbview サンプルアプリケーション](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/usbview-sample-application/)」を参照してください。|

### <a name="bluetooth-drivers"></a>Bluetooth ドライバー

|ツール名|ツールの場所|説明とヘルプファイルの場所|
|----|----|----|
|Bluetooth 照会レコード検証ツール (Sdpverify.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x86\Sdpverifiy.exe</br>% WindowsSdkDir% \tools\x64\Sdpverifiy.exe|Windows によって解釈される Bluetooth デバイスの問い合わせレコードを表示します。</br>WDK ドキュメント: [Bluetooth の問い合わせレコードの検証](bluetooth-inquiry-record-verifier.md)|

### <a name="windows-image-acquisition-wia-drivers"></a>Windows イメージ取得 (WIA) ドライバー

|ツール名|ツールの場所|説明とヘルプファイルの場所|
|----|----|----|
|WIADbgCfg (Wiadbgcfg.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x86\wiadbgcfg.exe</br>% WindowsSdkDir% \tools\x64\wiadbgcfg.exe|WIA ドライバーのログ記録を有効にします (Windows Server 2008 以降のバージョンの Windows)。</br>**メモ**以前のバージョンの Windows では、WIALogCfg を使用します。</br>% WindowsSdkDir% \tools\x86\wiadbgcfg.htm</br>% WindowsSdkDir% \tools\x64\wiadbgcfg.htm|
|WIAInfo2 (Wiainfo2.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x86\wiainfo2.exe</br>% WindowsSdkDir% \tools\x64\wiainfo2.exe|Wia デバイスドライバーのプロパティを表示および編集できるように、WIA 項目ツリーを表示します。</br>% WindowsSdkDir% \tools\x86\wiainfo2.htm</br>% WindowsSdkDir% \tools\x64\wiainfo2.htm|
|WIAPreview (Wiapreview.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\wiapreview.exe</br>% WindowsSdkDir% \tools\x86\wiapreview.exe|WIA Preview コンポーネントとドライバーのセグメンテーションフィルターを使用する方法について説明します。</br>% WindowsSdkDir% \tools\x64\wiapreview.htm</br>% WindowsSdkDir% \tools\x86\wiapreview.htm|
|WIATest (Wiatest.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\wiatest.exe</br>% WindowsSdkDir% \tools\x86\wiatest.exe|ドライバーによって作成された項目ツリー、ドライバーによって公開されている Windows イメージ取得 (WIA) プロパティ、および各プロパティの現在の値が表示されます。 このツールを使用すると、開発および単体テスト中にドライバーをデバッグできます。</br>% WindowsSdkDir% \tools\x64\wiatest.htm</br>% WindowsSdkDir% \tools\x64\wiatest.htm|
|Windows イメージングトレースファイルビューアー (Wiatrcvw.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\Wiatrcvw.exe</br>% WindowsSdkDir% \tools\x86\Wiatrcvw.exe|WIA トレースログ (%WINDIR%\Debug\WIA\wiatrace.log) を表示し、各モジュールの WIA トレースパラメーターを変更できます。</br>%WindowsSdkDir%\tools\x64\Wiatrcvw.mht</br>%WindowsSdkDir%\tools\x64\Wiatrcvw.mht|

### <a name="windows-portable-devices-wpd-drivers"></a>Windows ポータブルデバイス (WPD) ドライバー

|ツール名|ツールの場所|説明とヘルプファイルの場所|
|----|----|----|
|WpdDeviceInspector (WpdDeviceInspector.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\WpdDeviceInspector.exe</br>% WindowsSdkDir% \tools\x86\WpdDeviceInspector.exe|は、WPD ドライバーに対してクエリを行い、デバイスとその機能を説明する包括的な HTML レポートを生成します。 たとえば、サポートされているデバイスのコマンドとオブジェクトの一覧を取得するために使用できます。 また、このツールでは、各オブジェクトでサポートされているすべてのプロパティの一覧が生成されます。</br>WDK のドキュメント:</br>[Windows ポータブル デバイス](https://docs.microsoft.com/windows/win32/windows-portable-devices)</br>[WPD ドライバー開発ツール](https://docs.microsoft.com/windows-hardware/drivers/portable/familiarizing-yourself-with-the-sample-driver)|
|WpdInfo (WpdInfo.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\WpdInfo.exe</br>% WindowsSdkDir% \tools\x86\WpdInfo.exe|デバイスを開く、閉じる、デバイス上のオブジェクトを作成または削除する、デバイスコマンドを発行するなど、一般的な WPD 操作を実行します。</br>WDK のドキュメント:</br>[Windows ポータブル デバイス](https://docs.microsoft.com/windows/win32/windows-portable-devices)</br>[WPD ドライバー開発ツール](https://docs.microsoft.com/windows-hardware/drivers/portable/familiarizing-yourself-with-the-sample-driver)|
|Microsoft ネットワークモニター (NetMon.exe)</br>**WDK ツール:** 違います|Microsoft ネットワークモニターをダウンロードする</br>[NetMon.exe](https://www.microsoft.com/download/details.aspx?displaylang=en&id=4865)|WPD コンポーネントからのトレース情報を表示します。 このツールは、以前のバージョンの WDK に付属していた WpdMon.exe を置き換えるものです。</br>WDK のドキュメント:</br>[Windows ポータブル デバイス](https://docs.microsoft.com/windows/win32/windows-portable-devices)</br>[WPD ドライバー開発ツール](https://docs.microsoft.com/windows-hardware/drivers/portable/familiarizing-yourself-with-the-sample-driver)、「[ネットワークモニターツールの使用](https://docs.microsoft.com/windows-hardware/drivers/portable/using-the-netmon-tool)」を参照してください。|

### <a name="printer-drivers"></a>プリンタードライバー

|ツール名|ツールの場所|説明とヘルプファイルの場所|
|----|----|----|
|GPDCheck (Gpdcheck.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\gpdcheck.exe</br>% WindowsSdkDir% \tools\x86\gpdcheck.exe|一般的なプリンター記述ファイル (GPD) の構文の正確性を検証します。</br>コマンドオプションの詳細については、「」と入力してください。 </br>**gpdcheck/?**|
|INFGate (Infgate.exe)</br>**WDK ツール:** うん|WindowsSdkDir% \tools\x64\infgate.exe</br>% WindowsSdkDir% \tools\x86\infgate.exe.exe|プリンターの INF ファイルに準拠しているかどうかを検証します。</br>コマンドオプションの詳細については、「」と入力してください。</br>**infgate/?**|
|isXPS (isXPS.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\isxps\isxps.exe</br>% WindowsSdkDir% \tools\x86\isxps\isxps.exe|Xps ファイルが XPS および OPC 仕様に準拠しているかどうかを検証します。</br>コマンドオプションの詳細については、「」と入力してください。</br>**isxps/?** コマンドプロンプトウィンドウに表示されます。</br>詳細については、「 [Isxps 適合性ツール](https://docs.microsoft.com/previous-versions/aa348104(v=vs.110))」を参照してください。|
|ルック sgood (Looksgood.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\looksgood.exe</br>% WindowsSdkDir% \tools\x86\looksgood.exe|XPS レンダリングエンジンの正確性を検証します。</br>コマンドオプションの詳細については、「」と入力してください。</br>**いいですか?**|
|MakeNTF (Makentf.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\makentf.exe</br>% WindowsSdkDir% \tools\x86\makentf.exe|Adobe Font Metrics (AFM) ファイルと東アジア言語のフォント AFM ファイルを Windows フォントファイル (ntf) に変換します。</br>WDK のドキュメント:</br>[AFM ファイルを NTF ファイルに変換する](https://docs.microsoft.com/windows-hardware/drivers/print/converting-afm-files-to-ntf-files)</br>[東アジア AFM ファイルを NTF ファイルに変換する](https://docs.microsoft.com/windows-hardware/drivers/print/converting-east-asian-afm-files-to-ntf-files)|
|PPDCheck (Ppdcheck.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\ppdcheck.exe</br>% WindowsSdkDir% \tools\x86\ppdcheck.exe|PostScript プリンター記述ファイル (PPD) の構文の正確性を検証します。</br>コマンドオプションの詳細については、「」と入力してください。</br>**ppdcheck/?**|
|PTConform (PTConform.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\PTConform.exe</br>% WindowsSdkDir% \tools\x86\PTConform.exe|印刷チケットまたは印刷機能のドキュメントが印刷スキーマに準拠しているかどうかを検証します。</br>コマンドオプションの詳細については、「」と入力してください。</br>**ptconform/?**|
|XpsAnalyzer (XpsAnalyzer.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\XpsAnalyzer.exe</br>% WindowsSdkDir% \tools\x86\XpsAnalyzer.exe|XPS 1.0 仕様との互換性のために、XML Paper Specification (XPS) ファイルを分析します。</br>WDK のドキュメント:</br>[XpsAnalyzer](xpsanalyzer.md)|

### <a name="sensors"></a>Sensors

|ツール名|ツールの場所|説明とヘルプファイルの場所|
|----|----|----|
|センサー診断ツール (sensordiagnostictool.exe)</br>**WDK ツール:** うん|%WindowsSdkDir%\tools\x64</br>%WindowsSdkDir%\tools\x86|センサーと場所の機能について、ドライバー、ファームウェア、およびハードウェアをテストします。 このツールでは、センサーと場所 API を呼び出して、データの取得、イベント処理、レポート間隔、変更の感度、プロパティの取得をテストします。</br>WDK のドキュメント:</br>[センサー診断ツールを使用したセンサー機能のテスト](https://docs.microsoft.com/windows-hardware/drivers/sensors/the-sensor-diagnostic-tool)|

### <a name="all-drivers"></a>All Drivers (すべてのドライバー)

|ツール名|ツールの場所|説明とヘルプファイルの場所|
|----|----|----|
|ビンの場所 (Binplace.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \bin\x86\binplace.exe|ファイルの移動、実行可能ファイルからのシンボルの抽出、およびシンボルファイルからのプライベートシンボルの削除によって、大規模なコードプロジェクトを管理します。</br>WDK のドキュメント:</br>[BinPlace](binplace.md)|
|ドライバーのコード分析</br>**WDK ツール:** うん|コード分析ツールは Visual Studio に含まれています。 ドライバー固有のコンポーネントは、WDK をインストールするときに追加されます。|C および C++ のコードエラーを検出する静的な検証ツール。 このバージョンは、カーネルモードドライバーのエラーを検出するように特別に設計されています。</br>WDK のドキュメント:</br>[ドライバーのコード分析](code-analysis-for-drivers.md)|
|Certmgr.exe (CertMgr.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \bin\x64\CertMgr.exe</br>% WindowsSdkDir% \bin\x86\CertMgr.exe|ドライバーと[ドライバーパッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)の署名に使用される証明書、証明書信頼リスト (ctl)、および証明書失効リスト (crl) を管理します。</br>WDK のドキュメント:</br>[CertMgr](certmgr.md)|
|ChkINF</br>**WDK ツール:** れ|前のパス:</br>%WindowsSdkDir%\tools\x86\Chkinf|ChkInf は非推奨となりました。 代わりに、 [InfVerif](infverif.md)を使用してください。</br>WDK のドキュメント:</br>[InfVerif](infverif.md)|
|コンピューターハードウェア識別ツール (ComputerHardwareIds.exe)</br>**WDK ツール:** うん|**Windows Driver Kit (WDK) 8:**</br>% WindowsSdkDir% \tools\x64\ComputerHardwareIds.exe</br>% WindowsSdkDir% \tools\x86\ComputerHardwareIds.exe</br>WDKPath\tools\Other\ia64\ComputerHardwareIds.exe</br>**Windows Driver Kit (WDK) 8.1:**</br>% WindowsSdkDir% \bin\x64\ComputerHardwareIds.exe</br>% WindowsSdkDir% \bin\x86\ComputerHardwareIds.exe</br>% WindowsSdkDir% \bin\arm\ComputerHardwareIds.exe|コンピューターのハードウェア Id を SMBIOS 情報から派生します。</br>WDK のドキュメント:</br>[ComputerHardwareIds](computerhardwareids.md)|
|DC2WMIParser (DC2WMIParser.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\DC2WMIParser.exe</br>% WindowsSdkDir% \tools\x86\DC2WMIParser.exe|DC2WMIParser は、ドライバーの検証ツールによって作成された WMI IRP レコードを収集し、このログをテキストファイルに変換するツールです。</br>ドキュメント</br>[IRP ログ](https://docs.microsoft.com/windows-hardware/drivers/devtest/irp-logging)|
|依存関係のウォーカー (Depends.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\depends.exe</br>% WindowsSdkDir% \tools\x86\depends.exe|アプリケーションで必要とされるモジュールの依存パターンをツリーダイアグラムで表示します。 表示には、各モジュールによってエクスポートされた関数、他のモジュールによって実際に呼び出される関数、およびモジュールを読み込んで実行するために必要な最小ファイルセットなど、多くの詳細が含まれます。</br>ツールで、**依存関係のウォーカー**のヘルプメニューから [**ヘルプトピック**] を選択します。|
|DevCon (Devcon.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\devcon.exe</br>% WindowsSdkDir% \tools\x86\devcon.exe|デバイスマネージャーのコマンドラインバージョン。 DevCon ローカルコンピューター上のデバイスを有効、無効、インストール、構成、および削除し、ローカルコンピューターとリモートコンピューター上のデバイスに関する詳細情報を表示します。</br>WDK のドキュメント:</br>[DevCon](devcon.md)|
|ドライバー (Drivers.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\drivers.exe</br>% WindowsSdkDir% \tools\x86\drivers.exe|コンピューターにインストールされているすべてのドライバーの一覧を表示します。</br>WDK のドキュメント:</br>なし|
|ドライバーの検証ツール (Verifier.exe)</br>**WDK ツール:** 違います|% Windir% \system32\verifier.exe|カーネルモードドライバーとグラフィックスドライバーを監視して、無効な関数呼び出しまたはシステムを破損する可能性があるアクションを検出します。 ドライバーがさまざまなストレスを受け、不適切な動作を検出するテストを行うことができます。</br>WDK のドキュメント:</br>[ドライバーの検証ツール](driver-verifier.md)|
|ドライバー検証ログ (DVL)</br>**WDK ツール:** うん|Microsoft Visual Studio と WDK が必要です。 [**ドライバー** ] メニューの [**ドライバー検証ログの作成**...] をクリックします。|[静的ツールロゴテスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/6ab6df93-423c-4af6-ad48-8ea1049155ae)では、適用可能なすべてのドライバー送信にドライバー検証ログ (dvl) が必要です。 DVL には、コード分析と静的ドライバー検証ツールのログ ファイルからの結果の要約が含まれています。 「[ドライバー検証ログの作成」を](https://docs.microsoft.com/windows-hardware/drivers/develop/creating-a-driver-verification-log)参照してください。|
|拡張ストレージ証明書管理ツール (EhStorCertMgrCmd.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\ehstorcertmgrcmd.exe</br>% WindowsSdkDir% \tools\x86\ehstorcertmgrcmd.exe|IEEE 1667 標準に準拠している USB 記憶装置の証明書を管理します。</br>WDK のドキュメント:</br>[Enhanced Storage Certificate Management Tool](enhanced-storage-certificate-management-tool.md)|
|イベントおよびパフォーマンスカウンターマニフェストジェネレーターツール (ECManGen.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \bin\x64\ECManGen.exe</br>% WindowsSdkDir% \bin\x86\ECManGen.exe|XML タグを使用しなくても、イベントまたはパフォーマンスカウンターマニフェスト (* 男性) をゼロから作成するためのツール。 マニフェストファイルの作成の詳細については、「[インストルメンテーションマニフェスト (Windows) の記述](https://docs.microsoft.com/windows/desktop/WES/writing-an-instrumentation-manifest)」と「[カーネルモードドライバーへのイベントトレースの追加](adding-event-tracing-to-kernel-mode-drivers.md)」を参照してください。|
|Inf2Cat (Inf2cat.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \bin\x64\inf2cat.exe</br>% WindowsSdkDir% \bin\x86\inf2cat.exe|指定された Windows バージョンの一覧に対して[ドライバーパッケージの](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)INF ファイルにデジタル署名できるかどうかを判断し、指定した場合は、指定した windows バージョンに適用される署名されていない[カタログファイル](https://docs.microsoft.com/windows-hardware/drivers/install/catalog-files)を生成します。</br>WDK のドキュメント:</br>[Inf2Cat](inf2cat.md)|
|InfVerif (InfVerif.exe)</br>**WDK ツール:** うん|c:\Program Files (x86) \Windows Kits\10\tools\arm\infverif.exe</br>c:\Program Files (x86) \Windows Kits\10\tools\arm64\infverif.exe</br>c:\Program Files (x86) \Windows Kits\10\tools\x86\infverif.exe</br>c:\Program Files (x86) \Windows Kits\10\tools\x64\infverif.exe|ドライバーの INF ファイルをテストします。 Inf 構文の問題を報告するだけでなく、INF ファイルがユニバーサルであるかどうかが報告されます。</br>WDK のドキュメント:</br>[InfVerif](infverif.md)|
|MakeCat (MakeCat.exe)</br>**WDK ツール:** うん|WDKPath\bin\amd64\MakeCat.exe</br>WDKPath\bin\ia64\MakeCat.exe</br>WDKPath\bin\x86\MakeCat.exe|[ドライバーパッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)の[カタログファイル](https://docs.microsoft.com/windows-hardware/drivers/install/catalog-files)を作成します。</br>WDK のドキュメント:</br>[MakeCat](makecat.md)|
|MakeCert (MakeCert.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \bin\x64\MakeCert.exe</br>% WindowsSdkDir% \bin\x86\MakeCert.exe|システムテストルートキーまたは指定した別のキーによって署名された x.509 証明書を作成します。</br>WDK のドキュメント:</br>[MakeCert](makecert.md)|
|MSBuild (MSBuild.exe)/br>**WDK ツール:** いいえ|Visual Studio と共にインストールされます。|Microsoft WDK で提供されるサンプル、ドライバー、および関連するソフトウェアコンポーネントを構築します。</br>[MSBuild]( https://docs.microsoft.com/visualstudio/msbuild/msbuild?view=vs-2015)|
|PnpCpu (PnPCpu.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\PnPCpu.exe</br>% WindowsSdkDir% \tools\x86\PnPCpu.exe|Windows Server 2008 の実行中のインスタンスへのプロセッサのホットアドをシミュレートします。</br>WDK のドキュメント:</br>[PNPCPU](pnpcpu.md)|
|PnPUtil (PnPUtil.exe)</br>**WDK ツール:** 違います|% Windir% \system32\pnputil.exe|Windows ドライバーストアから[ドライバーパッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)をインストールまたは削除するコマンドラインツール。</br>WDK のドキュメント:</br>[PnPUtil](pnputil.md)|
|PoolMon (Poolmon.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\poolmon.exe</br>% WindowsSdkDir% \tools\x86\poolmon.exe|システムのページングされたカーネルプールと、ターミナルサービスセッションに使用されるメモリプールから、オペレーティングシステムがメモリの割り当てについて収集したデータを表示します。 データはプール割り当てタグによってグループ化されます。</br>WDK のドキュメント:</br>[PoolMon](poolmon.md)|
|PowerCfg (PowerCfg.exe)</br>**WDK ツール:** 違います|% Windir% \system32\powercfg.exe|システムのエネルギー効率を評価するために使用されるコマンドラインツールです。</br>デベロッパーセンターのドキュメント:</br>[PowerCfg を使用してシステムのエネルギー効率を評価する](https://download.microsoft.com/download/7/E/7/7E7662CF-CBEA-470B-A97E-CE7CE0D98DC2/PowerCfg.docx)</br>コマンドオプションの詳細については、「」と入力してください。</br>**PowerCfg/?**|
|Pvk2Pfx (Pvk2Pfx.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \bin\x64\Pvk2Pfx.exe</br>% WindowsSdkDir% \bin\x86\Pvk2Pfx.exe|.Spc、.cer、および .pvk ファイルに格納されている公開キーと秘密キーの情報を personal information exchange (.pfx) ファイルにコピーします。</br>WDK のドキュメント:</br>[Pvk2Pfx](pvk2pfx.md)|
|PwrTest (Pwrtest.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\pwrtest.exe</br>% WindowsSdkDir% \tools\x86\pwrtest.exe|コンピューターから電源管理情報を行使して記録する電源管理ツール。</br>WDK のドキュメント:</br>[PwrTest](pwrtest.md)|
|SignTool (SignTool.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \bin\x64\SignTool.exe</br>% WindowsSdkDir% \bin\x86\SignTool.exe|ファイルにデジタル署名し、ファイルの署名を検証し、ファイルにタイムスタンプを付ける。</br>WDK のドキュメント:</br>[SignTool](signtool.md)|
|Stampinf (Stampinf.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \bin\x64\stampinf.exe</br>% WindowsSdkDir% \bin\x86\stampinf.exe|**DriverVer**ディレクティブなど、一般的な INF ファイルディレクティブを更新します。</br>WDK のドキュメント:</br>[Stampinf](stampinf.md)|
|静的ドライバー検証ツール</br>**WDK ツール:** うん|%WindowsSdkDir%\tools\SDV</br></br>**メモ**  Visual Studio の [**ドライバー** ] メニューから、静的ドライバー検証ツールを起動します。|Windows ドライバーのソースコードを体系的に分析し、ドライバーが Windows オペレーティングシステムのカーネルと適切に対話するかどうかを判断するドライバー用の静的検証ツール。</br>WDK のドキュメント:</br>[静的ドライバー検証ツール](static-driver-verifier.md)|
|Tracefmt (Tracefmt.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \bin\x64\tracefmt.exe</br>% WindowsSdkDir% \bin\x86\tracefmt.exe|イベントトレースログファイル (.etl) またはリアルタイムトレースセッションからのトレースメッセージを書式設定して表示します。</br>WDK のドキュメント:</br>[Tracefmt](tracefmt.md)|
|TraceLog (Tracelog.exe)</br>**WDK ツール:** うん|**WDK 8:**</br>% WindowsSdkDir% \tools\x64\tracelog.exe</br>% WindowsSdkDir% \tools\x86\tracelog.exe</br>**WDK 8.1:**</br>% WindowsSdkDir% \bin\x64\tracelog.exe</br>% WindowsSdkDir% \bin\x86\tracelog.exe</br>% WindowsSdkDir% \bin\arm\tracelog.exe|コマンドラインからトレースセッションを構成し、制御します。 遅延プロシージャ呼び出し (Dpc) と割り込みサービスルーチン (Isr) で費やされた時間を計測します。</br>WDK のドキュメント:</br>[Tracelog](tracelog.md)|
|TracePDB (Tracepdb.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \bin\x64\tracepdb.exe</br>% WindowsSdkDir% \bin\x86\tracepdb.exe|WPP トレースプロバイダーの完全またはプライベートの PDB シンボルファイルから、トレースメッセージ形式 (tmf) ファイルを作成します。</br>WDK のドキュメント:</br>[Tracepdb](tracepdb.md)|
|TraceView (Traceview.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\TraceView.exe</br>% WindowsSdkDir% \tools\x86\TraceView.exe|トレースセッションを構成および制御し、リアルタイムのトレースセッションとトレースログからの書式付きトレースメッセージを表示します。 TraceView には、バッチ処理とスクリプト作成用のグラフィックユーザーインターフェイスとコマンドラインインターフェイスがあります。</br>WDK のドキュメント:</br>[TraceView](traceview.md)|
|TraceWPP (Tracewpp.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \bin\x64\tracewpp.exe</br>% WindowsSdkDir% \bin\x86\tracewpp.exe|Windows Software Trace プリプロセッサ (WPP) を実行します。</br>WDK のドキュメント:</br>[WPP プリプロセッサ](wpp-preprocessor.md)</br>[ソフトウェア トレース ツールの調査](survey-of-software-tracing-tools.md)|
|WDF Tester</br>**WDK ツール:** うん|%WindowsSdkDir%\tools\x64</br>%WindowsSdkDir%\tools\x86|WDF ドライバーをテスト、検証、およびデバッグするために使用できる一連のツール。 ツールセットには、スクリプトまたはコンパイル済みアプリケーションで使用できる WMI プログラミングインターフェイスが用意されています。</br>WDK のドキュメント:</br>[WdfTester: WDF ドライバーのテスト ツールセット](wdftester--wdf-driver-testing-toolset.md)|
|WDF Verifier (Wdfverifier.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\wdfverifier.exe</br>% WindowsSdkDir% \tools\x86\wdfverifier.exe|KMDF および UMDF ドライバーのフレームワークの検証機能に使いやすいインターフェイスを提供します。</br>WDK のドキュメント:</br>[WDF 検証ツール制御アプリケーション](wdf-verifier-control-application.md)|
|Web Services on devices (WSD) 基本的な相互運用性ツール (WSDBIT)</br>**WDK ツール:** うん|**WSDBIT クライアント:**</br>% WindowsSdkDir% \tools\x64\wsdbit_client.exe</br>% WindowsSdkDir% \tools\x86\wsdbit_client.exe</br>**WSDBIT サーバー:**</br>% WindowsSdkDir% \tools\x64\wsdbit_server.exe</br>% WindowsSdkDir% \tools\x86\wsdbit_server.exe|Web サービス (DPWS) のデバイスプロファイルの実装が、WSDAPI で動作することを確認します。</br>WDK のドキュメント:</br>[WSD 相互運用性ツール](wsdapi-basic-interoperability-tool.md)|
|Winerror.h (Winerror.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \tools\x64\winerror.exe</br>% WindowsSdkDir% \tools\x86\winerror.exe|指定されたエラー (Winerror.h) または成功コード (Ntstatus) のエラーメッセージ識別子およびマッピング情報を返します。</br>コマンドオプションの詳細については、「」と入力してください。</br>**winerror.h/?**|
|WMIMofCk (Wmimofck.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \bin\x86\wmimofck.exe|WDK のドキュメント:</br>[wmimofck.exeの使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-wmimofck-exe)</br>コマンドオプションの詳細については、「」と入力してください。</br>**wmimofck -?**|
|WsdCodeGen (Wsdcodegen.exe)</br>**WDK ツール:** うん|% WindowsSdkDir% \bin\x64\wsdcodegen.exe</br>% WindowsSdkDir% \bin\x86\wsdcodegen.exe|Web サービスコントラクトに基づいてプロキシとスタブを自動的に生成します。 主に、このツールを使用してクライアントアプリケーションを作成できます。 ただし、テストに使用したり、ユーザーモードドライバーを作成したりすることはできます。</br>バイナリ MOF ファイル (bmf) で指定されたクラス、プロパティ、メソッド、およびイベントが WMI での使用に対して有効であることを確認します。 MOF サポートファイルを生成します。</br>Windows SDK：</br>「[デバイスの Web サービス](https://docs.microsoft.com/windows/win32/wsdapi/wsd-portal)」セクションを参照してください。|
|WSDDebug_client と WSDDebug_host</br>**WDK ツール:** うん|**デバッグクライアント:**</br>% WindowsSdkDir% \bin\x64\WSDDebug_client.exe</br>% WindowsSdkDir% \bin\x86\WSDDebug_client.exe</br>**デバッグホスト:**</br>% WindowsSdkDir% \bin\x64\WSDDebug_host.exe</br>
% WindowsSdkDir% \bin\x86\WSDDebug_host.exe|これらのツールは、デバイスまたはアプリケーションのトラブルシューティングに使用できるソフトデバイスとクライアントです。</br>Windows SDK：</br>[デバイス上の Web サービスの](https://docs.microsoft.com/windows/win32/wsdapi/wsd-portal)セクション|

### <a name="supported-platforms"></a>サポートされているプラットフォーム

Windows 10 WDK を Windows 7 以降で実行し、それを使用してこれらのオペレーティングシステムのドライバーを開発することができます。

ランタイムの要件

|クライアントの OS|サーバーの OS|
|----|----|
|Windows 10|Windows Server 2019、Windows Server 2016|
|Windows 8.1|Windows Server 2012 R2|
|Windows 8|Windows Server 2012|
|Windows 7|Windows Server 2008 R2 SP1|
