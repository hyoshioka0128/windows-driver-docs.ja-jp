---
title: 3D プリンター用のカスタムの USB インターフェイス サポート
description: このトピックでは、3 D、v3 プリンター用のインターフェイスをカスタムの USB を有効にする方法と、v4 印刷ドライバー エコシステムについて説明します。
ms.date: 01/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1728011ce0dc209c88333bac8a4ab1de81cc781f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549922"
---
# <a name="enable-a-custom-usb-interface-for-a-3d-printer"></a>3D プリンターに対してカスタム USB インターフェイスを有効にします。

このトピックで説明するアーキテクチャを使用すると、カスタム USB インターフェイス 3D プリンター v3 と v4 印刷のエコシステムでのサポート。 標準ポート モニター、 **3dmon.dll**、転送 3D 印刷ジョブのコマンドを Windows に**3DPrintService**ローカル サービスの資格情報を実行します。 サービスでは、読み込みを DLL カスタム コマンドを実行するために必要な 3D の印刷ジョブは、パートナーと通信します。 DLL、パートナーだけでなく**3dmon.dll**と**3dprintservice.exe**デバイスの USB ドライバー パッケージで再頒布可能パッケージがインストールされます。 パートナー DLL する必要があります実装およびエクスポートして、一連の関数との通信に、 **3DPrintService**します。 印刷スプーラ サービスとの対話に必要な機能の残りの部分が実装された**3dmon.dll**します。

> [!NOTE]
> このアーキテクチャでは、スレッド セーフである、複数のインスタンスをパートナー DLL が必要です。

## <a name="architecture-decisions"></a>アーキテクチャの決定

**3DPrintService**を読み込み、印刷ワークフロー中にパートナー提供の Dll で定義された特定の Api を呼び出す windows サービスを使用します。 これらの Api には、プリンターとの通信を使用します。

KMDF の USB フィルター ドライバー パッケージを使用してインストールするため Windows Update で公開されているサポートされている 3D プリンターの PnP します。 KMDF ドライバーでは、パートナー ソフトウェアがインストールされ、3 D プリンター デバイス ノードを作成します。 3D プリンター デバイス ノードは、Windows Update からのパートナーが公開した v4 印刷ドライバーを使用してインストールされます。

## <a name="packaging-decisions"></a>パッケージの決定

### <a name="binaries-and-binary-dependencies"></a>バイナリとバイナリの依存関係

Architectue では、Windows Update でハードウェアの製造元によって発行されたドライバーを使用します。 このドライバーには、次の Microsoft 提供再頒布可能バイナリとその依存関係が含まれています。

- 3dmon.dll
- 3dprintservice.exe
- ms3dprintusb.sys

#### <a name="kernel-mode-usb-filter-driver"></a>カーネル モードの USB フィルター ドライバー

KMDF ドライバーでは、パートナーによって発行され、次の図に示すようにコンポーネントで構成されます。 これはハードウェア ID を持つデバイスに対応 (通常、VID & PID)。 ドライバーは、印刷キューとスライサーのドライバーのインストールをトリガーするインストールでの 3D プリンター デバイス ノードを作成します。 パートナー provids v4 プリンター ドライバーの 3D プリンター デバイス ノードに作成されます。

![kmdf の usb フィルター ドライバー](images/kmdf-usb-filter-driver.png)

##### <a name="ms3dprintusbsys"></a>MS3DPrintUSB.sys

列挙型 3 D プリンター開発ノードを作成、カーネル モード デバイス ドライバー\\3DPrint します。 VID & Winusb.sys によって作成された [デバイス] ノードに基づく PID の直接の一致を使用して、PnP サブシステムによって呼び出されます。 ドライバーの .inf ファイルの設定を設定するために使用するカスタム DLL を**3DPrintService** (システムにインストールされていない) 場合。

##### <a name="3dmondll"></a>3dmon.dll

3DMon.dll は、Microsoft の発行したポートが 3D プリンターとの通信にスプーラーによって呼び出される再頒布可能パッケージのバイナリを監視します。

##### <a name="3dprintserviceexe"></a>3dprintservice.exe

3DPrintService.exe とは、ドライバーのセットアップ中に、Windows サービスとしてインストールされている Microsoft の発行したバイナリです。 3DMon 3D プリンターとこれに、印刷、双方向などの操作を実行するには、このサービスと通信します。

##### <a name="partnerimpldll"></a>Partnerimpl.dll

Partnerimp.dll とは、パートナーの公開された Microsoft インターフェイス実装です。 DLL は、そのプロトコルを使用して、パートナーのデバイスと通信します。 3DPrintService.exe では、ドライブの 3D プリンター デバイスの操作を実行時にこの DLL を読み込みます。

![3dprintservice](images/3dprintservice.png)

### <a name="printer-usage-sequence"></a>プリンターの使用状況のシーケンス

- 3dmon.dll 3DPrintService windows サービスにコマンドを送信すると、スプーラーの通信します。
- NetworkService アカウントの資格情報で実行される、3DPrintService.exe
- 3dmon.dll を使用して、スプーラーが 3D プリンターが使用されるたびに、3DPrintService にコマンドを送信します。
- コマンドとパートナー提供の実装の Dll 上で実行時に Api を呼び出す、3DPrintService
- パートナー提供の Dll からスプーラーへの応答から 3DPrintService 手

## <a name="interfaces-and-interactions"></a>インターフェイスとの相互作用

パートナーの DLL には、次の API 関数をエクスポートする必要があります。

### <a name="hresult-installin-lpcwstr-args"></a>HRESULT のインストール (\[で\]LPCWSTR args)

この API は、オプションを製造元によってカスタムのソフトウェアまたは自分のデバイスの登録をインストールするのに使用できます。 たとえば、インストールを使用して、デバイスのドライバー パッケージに含まれているモデリングの。 この API は、インストールを有効にするシステムの資格情報で呼び出されます。

### <a name="dword-printapisupported"></a>DWORD PrintApiSupported()

この API は、サポートされている 3D 印刷サービス API のバージョンを示す、サード パーティの製造元によって使用されます。 次の Api は、3DPrintService のバージョン 1 と互換性のあります。

### <a name="hresult-initializeprintlpcwstr-pprintername-lpcwstr-pportname-dword-dwjobid-lpvoid-pppartnerdata"></a>HRESULT InitializePrint(LPCWSTR pPrinterName, LPCWSTR pPortName, DWORD dwJobId, LPVOID\* ppPartnerData)

この API は、印刷イベント、プリンターの初期化を開始する前に呼び出されます。 プリンターは、ppPartnerData パラメーターは、特定のジョブの状態を保存できます。 この呼び出しは、StartDocPort 呼び出しに似ています。

- **jobId** -ジョブを追跡するために使用されるジョブ id
- **portName** -3D、プリンターの portname
- **printerName** - プリンターに送信される印刷ジョブの名前
- **ppPartnerData** -ポインターに使用できる任意のジョブ固有のデータを格納するには

### <a name="hresult-printfilein-dword-jobid-in-lpwstr-portname-in-lpwstr-printername-in-lpwstr-pathtorenderedfileinlpvoid-pppartnerdata"></a>HRESULT PrintFile (\[で\]DWORD の jobId\[で\]LPWSTR portName、\[で\]LPWSTR printerName、\[で\]LPWSTR pathToRenderedFile、\[で\]LPVOID\* ppPartnerData)

この API は、自社のプリンターにドキュメントを印刷するサード パーティの製造元によって使用されます。

- **jobId** -ジョブを追跡するために使用されるジョブ id
- **portName** -3D、プリンターの portname
- **printerName** - プリンターに送信される印刷ジョブの名前
- **pathToRenderedFile**のレンダリングが実行された後は、スプール ファイルの場所への UNC パス。 サード パーティ製の製造元がこの場所からファイルを処理し、自分のデバイスで、ドキュメントの印刷
- **ppPartnerData** - ポインターにポインター InitializePrint API の呼び出し中にパートナーの特定のデータ設定を格納するその使われます。
- **printerName**ポート名を使用して、レジストリから取得できます。 サード パーティの製造元は使えませんを自分のデバイスとの通信にポート名を使用できます。 プリンター名は、Windows マシン上で一意と、ソフトウェアに、ジョブを印刷するプリンターを識別するのに行えるようになります。 すべてのプリンターをコンピューターでアクティブでは、次のレジストリ キーの位置はあります。

    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Print\\Printers**

![3d プリンター レジストリ](images/3d-printer-registry.png)

### <a name="hresult-queryin-lpcwstr-command-in-lpcwstr-commanddata-out-lpwstr-resultbuffer-out-resultbuffersize--in-lpvoid-pppartnerdata"></a>HRESULT クエリ (\_で\_LPCWSTR コマンド、\_で\_LPCWSTR commandData、\_アウト\_LPWSTR resultBuffer、\_アウト\_resultBufferSize、 \_\_ LPVOID\* ppPartnerData)

- **コマンド**-文字列をクエリとして送信されたコマンド
- **commandData** -コマンド引数 (省略可能)
- **resultBuffer** -クエリの引数の呼び出しの結果 >
- **resultBufferSize** - 結果バッファーの文字列のサイズ
- **ppPartnerData** - 現在のパートナー DLL インスタンスのポインターにポインター

3Dprint サービスは、コマンド用に割り当てる、パートナー、バッファーのサイズを取得する DLL を呼び出します。

応答文字列を保持するためにメモリを割り当てた後、DLL が呼び出されますもう一度を実際の結果を取得します。

DLL は、以前のインスタンス データを使用できます**IntializePrint()** たびに新しい通信チャネルを開くことがなく、デバイスと通信する呼び出し、 **Query()** 関数が呼び出されます。

この API は、デバイスの構成に関する情報を取得、進行状況を印刷するか、デバイスの DLL は、イベントを取り外し、パートナーに通知するプリンターとの通信に使用されます。

次のコマンドは、製造元でサポートする必要があります。

| コマンド | CommandData | 出力 | コメント |
|---------|-------------|--------|----------|
| \\\\Printer.3DPrint:JobStatus | | Job Commenced = {"Status": "ok"} <br> 完了時に使用する状態 {"Status"。"Completed"} | スプーラー印刷キューの UI ですべての戻り値が表示されます。 これにより、デバイスに印刷キューの UI で、印刷時に関連する情報を表示できます。 デバイスは、任意の文字列は、ここ (「取り込み中」または「33% 完了」など) を返すことができ、印刷キューのジョブの状態でそのまま表示されます。 |
| \\\\Printer.3DPrint:JobCancel | | {"Status":"Completed"} | ユーザーは、印刷をキャンセルすると、スプーラーはこのコマンドを呼び出します。 パートナーの DLL は、キャンセルが成功し、ハンドルおよびスレッドを終了しているときにこの値を返します。 |
| \\\\Printer.Capabilities:Data | | PrintDeviceCapabilites (PDC) スキーマに準拠した XML 文字列。 | PDC のクエリは、プリンターに関する詳細情報を取得するアプリによって呼び出されます。 データは、デバイスの機能の記述に使用され、ドライバーは、Microsoft のスライサーに依存する場合、スライサーの設定を含めることができます。 PDC サンプルについては以下をご覧ください。 |
| \\\\Printer.3DPrint:Disconnect | | {"Status":"OK"} | このクエリは、プリンター デバイスの PnP 切断が発生するたびにトリガーされます。 パートナーは、必要なアクションを引き受けることができます、適切な許可に開いているハンドルが再接続に近い例です。 |
| \\\\Printer.3DPrint:Connect | | {"Status":"OK"} | このクエリは、プリンター デバイスの PnP 接続があるたびにトリガーされます。 パートナーは、必要なアクションを引き受けることができます。 |

#### <a name="print-device-capabilities-xml"></a>印刷デバイス機能 XML

XML は、例として使用できるデバイスの機能は、次の印刷します。

```xml
<?xml version="1.0"?>
<PrintDeviceCapabilities
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns:xml="http://www.w3.org/XML/1998/namespace"
    xmlns:psk="http://schemas.microsoft.com/windows/2003/08/printing/printschemakeywords"
    xmlns:psk3d="http://schemas.microsoft.com/3dmanufacturing/2013/01/pskeywords3d"
    xmlns:psk3dx="http://schemas.microsoft.com/3dmanufacturing/2014/11/pskeywords3dextended"
    xmlns:pskv="http://schemas.microsoft.com/3dmanufacturing/2014/11/pskeywordsvendor"
    xmlns:psf="http://schemas.microsoft.com/windows/2003/08/printing/printschemaframework"
    xmlns:psf2="http://schemas.microsoft.com/windows/2013/12/printing/printschemaframework2"
    xmlns="http://schemas.microsoft.com/windows/2013/12/printing/printschemaframework2"
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

上記のように適切なユーザー入力メッセージのセットで PDC xml を返すアドボケイトを内蔵型の表示と印刷の先頭に、デバイスと対話するユーザーを許可するボタンがない 3 D プリンター、 **psdk3dx:userPrompt**. これは、既存の上に新しい印刷を起動できないようにします。 カスタム ステータス メッセージ*&lt;psk3dx:customStatus&gt;* スライス処理中にすべてのメッセージを表示するために使用します。

### <a name="hresult-cleanuplpcwstr-pprintername-lpcwstr-pportname-dword-dwjobid-lpvoid-pppartnerdata"></a>HRESULT Cleanup(LPCWSTR pPrinterName, LPCWSTR pPortName, DWORD dwJobId, LPVOID\* ppPartnerData)

- **dwJobId** -スプーラーにジョブを追跡するために使用されるジョブ id
- **pPortName** -3D、プリンターの portname
- **pPrinterName** - プリンターに送信される印刷ジョブの名前
- **ppPartnerData** -ポインターにポインターを InitializePrint API の呼び出し中にジョブの特定のデータ設定を保持します。

クリーンアップは、印刷ジョブが正常に完了またはキャンセル クエリ印刷ジョブの完了時に呼び出されます。 この印刷用に初期化されたリソースをクリーンアップするパートナー DLL の機会を提供します。

### <a name="hresult-uninstallinlpcwstr-args"></a>HRESULT をアンインストール (\[で\]LPCWSTR args)

この API は、3D プリンター デバイスの uninstaling ときに呼び出され、製造元がインストールされているソフトウェアをアンインストールするメカニズムを提供します。
