---
title: 3D プリンターのカスタム USB インターフェイスのサポート
description: このトピックでは、v3 および v4 印刷ドライバーエコシステムで3D プリンターのカスタム USB インターフェイスを有効にする方法について説明します。
ms.date: 01/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: a2c485914f6e6ed302d14d8e92135208fdd47860
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652798"
---
# <a name="enable-a-custom-usb-interface-for-a-3d-printer"></a>3D プリンターのカスタム USB インターフェイスを有効にする

このトピックで説明するアーキテクチャでは、v3 および v4 print エコシステムでのカスタム USB インターフェイス3D プリンターのサポートが有効になります。 標準ポートモニターである**3dmon .dll**は、ローカルサービスの資格情報で実行されている Windows **3Dprintservice**に3d 印刷ジョブコマンドを転送します。 サービスは、パートナー DLL を読み込んで通信し、3D 印刷ジョブに必要なカスタムコマンドを実行します。 パートナー DLL、および**3dmon .dll**および**3dprintservice .exe**再頒布可能パッケージは、デバイスの USB ドライバーパッケージによってインストールされます。 パートナー DLL は、 **3Dprintservice**と通信するために、一連の関数を実装してエクスポートする必要があります。 印刷スプーラサービスとの対話に必要なその他の機能は、 **3dmon .dll**に実装されています。

> [!NOTE]
> このアーキテクチャでは、パートナー DLL がマルチインスタンスであり、スレッドセーフである必要があります。

## <a name="architecture-decisions"></a>アーキテクチャの決定

**3Dprintservice** windows サービスは、印刷ワークフロー中にパートナーが提供する dll 内の特定の定義済み api を読み込んで呼び出すために使用されます。 これらの Api は、プリンターとの通信を可能にします。

KMDF USB フィルタードライバーパッケージは、サポートされている3D プリンターの PnP 経由でインストールするために Windows Update に公開されています。 KMDF ドライバーは、パートナーソフトウェアをインストールし、3D プリンターデバイスノードを作成します。 3D プリンターデバイスノードは、Windows Update から、パートナーが発行した v4 印刷ドライバーを使用してインストールされます。

## <a name="packaging-decisions"></a>パッケージ化の決定

### <a name="binaries-and-binary-dependencies"></a>バイナリとバイナリの依存関係

このアーキテクチャでは、Windows Update のハードウェアの製造元によって発行されたドライバーを使用します。 このドライバーには、Microsoft が提供する次の再頒布可能なバイナリとその依存関係が含まれています。

- 3dmon .dll
- 3dprintservice .exe
- ms3dprintusb

#### <a name="kernel-mode-usb-filter-driver"></a>カーネルモード USB フィルタードライバー

KMDF ドライバーはパートナーによって発行され、次の図に示すコンポーネントで構成されています。 これは、デバイスとハードウェア ID (通常は、VID & PID) と一致します。 ドライバーは、インストール時に、印刷キューとスライサードライバーのインストールをトリガーする3D プリンターデバイスノードを作成します。 パートナーは、作成された3D プリンターデバイスノードの ds v4 プリンタードライバーをプロビジョニングします。

![kmdf usb フィルタードライバー](images/kmdf-usb-filter-driver.png)

##### <a name="ms3dprintusbsys"></a>MS3DPrintUSB

列挙\\3DPrint の下に3D プリンター開発ノードを作成するカーネルモードデバイスドライバー。 これは、Winusb .sys によって作成されたデバイスノードに基づいて、VID & PID と直接一致することによって、PnP サブシステムによって呼び出されます。 ドライバーの .inf ファイルは、 **3Dprintservice** (システムにまだインストールされていない場合) の設定に使用されるカスタム DLL を設定します。

##### <a name="3dmondll"></a>3dmon .dll

3DMon .dll は、Microsoft が公開しているポートモニターの再頒布可能なバイナリで、スプーラが3D プリンターとの通信に使用します。

##### <a name="3dprintserviceexe"></a>3dprintservice .exe

3DPrintService .exe は、ドライバーのセットアップ時に Windows サービスとしてインストールされる、Microsoft が公開するバイナリです。 3DMon は、このサービスと通信して、3D プリンターで印刷や bidi などの操作を実行します。

##### <a name="partnerimpldll"></a>Partnerimpl .dll

Partnerimp .dll は、発行された Microsoft インターフェイスのパートナーの実装です。 DLL は、プロトコルを使用してパートナーのデバイスと通信します。 3D プリンターデバイスの操作を実行するには、実行時にこの DLL が読み込まれます。

![3dprintservice](images/3dprintservice.png)

### <a name="printer-usage-sequence"></a>プリンターの使用状況シーケンス

- スプーラは、3DPrintService windows サービスにコマンドを送信する 3dmon .dll と通信します。
- NetworkService のアカウント資格情報を使用して、3DPrintService .exe を実行します。
- 3dmon .dll 経由のスプーラは、3D プリンターが使用されている場合は常に、3DPrintService にコマンドを送信します。
- 3DPrintService は、パートナーが提供する実装 Dll で、実行時にコマンドを処理し、Api を呼び出します。
- 3DPrintService は、パートナーから提供された Dll からスプーラに応答を送ります。

## <a name="interfaces-and-interactions"></a>インターフェイスと相互作用

パートナー DLL は、次の API 関数をエクスポートする必要があります。

### <a name="hresult-installin-lpcwstr-args"></a>HRESULT Install (\] LPCWSTR args の\[)

この API はオプションであり、製造元がデバイスのカスタムソフトウェアまたは登録をインストールするために使用できます。 たとえば、デバイスのドライバーパッケージに含まれるモデリングのインストールがあります。 この API は、インストールを有効にするためにシステムの資格情報を使用して呼び出されます。

### <a name="dword-printapisupported"></a>DWORD PrintApiSupported ()

この API は、サポートされている3D 印刷サービス API のバージョンを示すために、サードパーティの製造元によって使用されます。 以下の Api は、3DPrintService のバージョン1と互換性があります。

### <a name="hresult-initializeprintlpcwstr-pprintername-lpcwstr-pportname-dword-dwjobid-lpvoid-pppartnerdata"></a>HRESULT InitializePrint (LPCWSTR pPrinterName、LPCWSTR pPortName、DWORD dwJobId、LPVOID\* ppPartnerData)

この API は、プリンターの初期化を開始する前に、印刷イベントの前に呼び出されます。 プリンターは、ppPartnerData パラメーターにジョブ固有の状態を保存できます。 この呼び出しは、StartDocPort 呼び出しに似ています。

- **jobId** -ジョブの追跡に使用されるジョブ id
- 3D プリンターの**portName** -portName
- **printerName** -この印刷ジョブが送信されているプリンターの名前
- **Pppartnerdata** -ジョブ固有のデータを格納するために使用できるポインターへのポインター

### <a name="hresult-printfilein-dword-jobid-in-lpwstr-portname-in-lpwstr-printername-in-lpwstr-pathtorenderedfileinlpvoid-pppartnerdata"></a>HRESULT PrintFile (\] DWORD jobId 内の\[、\] LPWSTR portName の \[、\[LPWSTR printerName の\]、\[LPWSTR pathToRenderedFile、\] LPVOID\[ppPartnerData)

この API は、プリンターでドキュメントを印刷するために、サードパーティの製造元によって使用されます。

- **jobId** -ジョブの追跡に使用されるジョブ id
- 3D プリンターの**portName** -portName
- **printerName** -印刷ジョブが送信されているプリンターの名前
- **Pathtorenderedfile** -レンダリング後にスプールされたファイルの場所への UNC パス。 サードパーティの製造元は、この場所からファイルを処理し、デバイスでドキュメントを印刷します。
- **Pppartnerdata** -INITIALIZEPRINT API 呼び出し中にパートナー固有のデータ設定を格納する isused を指すポインターへのポインター。
- **printerName**は、ポート名を使用してレジストリから取得できます。 サードパーティの製造元は、ポート名を使用してデバイスと通信することができます maynot。 プリンター名は Windows コンピューター上で一意であり、そのソフトウェアはジョブを印刷するプリンターを識別できます。 コンピューター上でアクティブになっているすべてのプリンターは、次のレジストリキーにあります。

    **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\印刷\\プリンター**

![3d プリンターレジストリ](images/3d-printer-registry.png)

### <a name="hresult-query_in_-lpcwstr-command-_in_-lpcwstr-commanddata-_out_-lpwstr-resultbuffer-_out_-resultbuffersize--_in_-lpvoid-pppartnerdata"></a>HRESULT クエリ (\_ LPCWSTR コマンドの\_、\_ LPCWSTR commandData での \_、\_LPWSTR resultBuffer、\_ Out \_Resultbuffer、、\_、LPVOID \_ppPartnerData)

- クエリとして送信された**コマンド**文字列コマンド
- **Commanddata** -command の引数 (省略可能)
- **Resultbuffer** -クエリ引数の呼び出しの結果 >
- **Resultbuffersize** -結果バッファー文字列のサイズ
- **Pppartnerdata** -現在のパートナー DLL インスタンスのポインターへのポインター

3Dprint サービスは、パートナー DLL を呼び出して、コマンドに割り当てられるバッファーのサイズを取得します。

応答文字列を保持するためにメモリを割り当てると、実際の結果を取得するために DLL が再度呼び出されます。

DLL は、 **Query ()** 関数が呼び出されるたびに新しい通信チャネルを開かずに、以前の**IntializePrint ()** 呼び出しのインスタンスデータを使用して、デバイスと通信できます。

この API は、プリンターとの通信に使用され、デバイスの構成や印刷の進行状況に関する情報を取得したり、デバイスの取り外しイベントのパートナー DLL に通知したりします。

次のコマンドは、製造元によってサポートされている必要があります。

| コマンド | CommandData | 出力 | 備考 |
|---------|-------------|--------|----------|
| \\\\Printer: JobStatus | | Job 始まっ = {"Status": "ok"} <br> 完了時に使用される状態 {"Status": "Completed"} | スプーラによって、印刷キューの UI に返された値がすべて表示されます。 これにより、印刷中に、印刷キューの UI に関連する情報がデバイスに表示されます。 デバイスは、ここに任意の文字列 ("Busy" や "33% complete" など) を返すことができます。これは、印刷キューのジョブ状態のままで表示されます。 |
| \\\\Printer. 3DPrint: JobCancel | | {"Status": "Completed"} | スプーラは、ユーザーが印刷をキャンセルしたときに、このコマンドを起動します。 キャンセルが成功し、ハンドルとスレッドが閉じられた場合、パートナー DLL はこの値を返します。 |
| \\\\プリンターの機能: データ | | Printdevicecap(PDC) スキーマに準拠した XML 文字列。 | PDC クエリは、プリンターに関する詳細情報を取得したいアプリによって呼び出されます。 データはデバイスの機能を説明するために使用され、ドライバーが Microsoft スライサーに依存している場合はスライサー設定を含めることができます。 PDC の例については、以下を参照してください。 |
| \\\\Printer. 3DPrint: 切断 | | {"Status": "OK"} | このクエリは、プリンターデバイスの PnP 切断が発生するたびにトリガーされます。 パートナーは、任意の必要なアクションを実行できます。たとえば、開いているハンドルを閉じて、適切な再接続を行うことができます。 |
| \\\\プリンタの印刷: 接続 | | {"Status": "OK"} | このクエリは、プリンターデバイスの PnP 接続があるときにトリガーされます。 パートナーは、必要なアクションを実行できます。 |

#### <a name="print-device-capabilities-xml"></a>印刷デバイスの機能の XML

次の印刷デバイス機能の XML を例として使用できます。

```xml
<?xml version="1.0"?>
<PrintDeviceCapabilities
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="https://www.w3.org/2001/XMLSchema"
    xmlns:xml="https://www.w3.org/XML/1998/namespace"
    xmlns:psk="https://schemas.microsoft.com/windows/2003/08/printing/printschemakeywords"
    xmlns:psk3d="https://schemas.microsoft.com/3dmanufacturing/2013/01/pskeywords3d"
    xmlns:psk3dx="https://schemas.microsoft.com/3dmanufacturing/2014/11/pskeywords3dextended"
    xmlns:pskv="https://schemas.microsoft.com/3dmanufacturing/2014/11/pskeywordsvendor"
    xmlns:psf="https://schemas.microsoft.com/windows/2003/08/printing/printschemaframework"
    xmlns:psf2="https://schemas.microsoft.com/windows/2013/12/printing/printschemaframework2"
    xmlns="https://schemas.microsoft.com/windows/2013/12/printing/printschemaframework2"
    version="2">
    <CapabilitiesChangeID xsi:type="xsd:string">{9F58AF07-DCB6-4865-8CA3-A52EA5DCB05F}</CapabilitiesChangeID>

  <psk3d:Job3DOutputArea psf2:psftype="Property">
    <psk3d:Job3DOutputAreaWidth>150001</psk3d:Job3DOutputAreaWidth>
    <psk3d:Job3DOutputAreaDepth>150001</psk3d:Job3DOutputAreaDepth>
    <psk3d:Job3DOutputAreaHeight>150001</psk3d:Job3DOutputAreaHeight>
  </psk3d:Job3DOutputArea>

  <psk3d:Job3DMaterials psf2:psftype="Property">

      <psk3dx:MaterialPLA>
         <psk:DisplayName>PLA</psk:DisplayName>
         <psk3d:Job3DMaterialType>psk3d:PLA</psk3d:Job3DMaterialType>
         <psk3d:MaterialColor>#FFFFFFFF</psk3d:MaterialColor>

         <psk3dx:platformtemperature>0</psk3dx:platformtemperature>
         <psk3dx:filamentdiameter>1750</psk3dx:filamentdiameter>
         <psk3dx:filamentcalibrationoverride>1.0</psk3dx:filamentcalibrationoverride>
         <psk3dx:extrudertemperature>207</psk3dx:extrudertemperature>

         <psk3dx:SpeedFactor>1.0</psk3dx:SpeedFactor>

         <psk3dx:SetupCommands>
            <!-- Executed during pre-commands: nozzle pre-heating, priming, etc -->
            <psk3dx:command>M104 S207 T1</psk3dx:command>
            <psk3dx:command>M140 S50</psk3dx:command>
         </psk3dx:SetupCommands>

         <psk3dx:SelectCommands>
            <!-- Executed during printing: T0/T1 selection, nozzle wiping sequence,turn fan on/off/gradual, retract the material, temperature, etc-->
            <psk3dx:command>; PLA on</psk3dx:command>
            <psk3dx:command>M108 T1</psk3dx:command>
         </psk3dx:SelectCommands>

         <psk3dx:DeselectCommands>
            <!-- Executed during printing: retract the material, park the nozzle, reduce temperature, etc -->
            <psk3dx:command>; PLA off</psk3dx:command>
         </psk3dx:DeselectCommands>


      </psk3dx:MaterialPLA>
  </psk3d:Job3DMaterials>

  <psk3dx:customStatus>Slicing</psk3dx:customStatus>
  <psk3dx:userprompt>Confirm the 3D printer is calibrated and ready for the next print</psk3dx:userprompt>

   <!— Additional Slicer settings follow (optional) -->

</PrintDeviceCapabilities>
```

印刷の開始時にユーザーがデバイスと対話できるようにボードの表示とボタンがない3D プリンターの場合は、 **psdk3dx: userPrompt**に示されているように、適切なユーザープロンプトメッセージを含む PDC xml を返すことをお勧めします。 これは、既存の印刷を開始しないようにするためのものです。 *Psk3dx: customstatus&gt;&lt;* カスタムステータスメッセージは、スライス中にメッセージを表示するために使用されます。

### <a name="hresult-cleanuplpcwstr-pprintername-lpcwstr-pportname-dword-dwjobid-lpvoid-pppartnerdata"></a>HRESULT クリーンアップ (LPCWSTR pPrinterName、LPCWSTR pPortName、DWORD dwJobId、LPVOID\* ppPartnerData)

- **Dwjobid** -スプーラのジョブを追跡するために使用されるジョブ id
- 3D プリンターの**pPortName** -portname
- **pPrinterName** -この印刷ジョブが送信されているプリンターの名前
- **Pppartnerdata** -INITIALIZEPRINT API 呼び出し中にジョブ固有のデータ設定を保持するポインターへのポインター

クリーンアップは、印刷ジョブが正常に完了したとき、または印刷ジョブに対するキャンセルクエリの完了時に呼び出されます。 パートナー DLL が、この印刷用に初期化されたリソースをクリーンアップする機会を提供します。

### <a name="hresult-uninstallinlpcwstr-args"></a>HRESULT UnInstall (\]LPCWSTR args の\[)

この API は、3D プリンターデバイスを uninstaling するときに呼び出され、製造元がインストールしたソフトウェアをアンインストールするためのメカニズムを提供します。
