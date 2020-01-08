---
title: V4 ドライバー マニフェスト
description: V4 印刷ドライバーマニフェストには、プリンター固有のセットアップディレクティブが含まれており、INF ファイルと共に使用されます。
ms.assetid: 187A10B7-2AAC-46D9-998C-C8724D8E3862
ms.date: 07/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7e770542d4d91c8c0f7ccf45326e6e508fb7beb7
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652954"
---
# <a name="v4-driver-manifest"></a>V4 ドライバー マニフェスト


V4 印刷ドライバーマニフェストは、すべてのプリンター固有のセットアップディレクティブが含まれているテキストファイルです。 V4 印刷ドライバーのマニフェストは、プリンター固有の v4 印刷ドライバーのセットアップの一部として、v4 印刷ドライバーの INF ファイルと組み合わせて使用されます。

マニフェスト内のディレクティブは、次のセクションで構成されます。

-   [DriverConfig セクション](#driverconfig-section)
-   [BidiFiles セクション](#bidifiles-section)
-   [DriverRender セクション](#driverrender-section)
-   [FileSave セクション](#filesave-section)
-   [プリンター拡張セクション](#printerextensions-section)
-   [関連トピック](#related-topics)

## <a name="driverconfig-section"></a>DriverConfig セクション


次の表は、DriverConfig セクションで使用されるディレクティブを示しています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Directive</th>
<th>制限</th>
<th>使用方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>RequiredFiles</strong></p>
<p>Ntprint.inf または ntprint4 のファイルが含まれています。</p>
<p>RequiredFiles ディレクティブは、Windows 10 で次の値をサポートします。</p>
<p>PWGRRenderFilter: ドライバーの依存ファイルの一覧に Microsoft PWG ラスターレンダリングフィルターを追加します。</p>
<p>PWG ラスターレンダリングフィルター表示フィルターでは、ドライバーが構成に PrintDeviceCapabilities ファイルを使用する必要があります。</p></td>
<td><p>この一覧から、Unidrv、pscript5、および mxdwdrv .dll を省略する必要があります。 これらは自動的に解決されます。</p></td>
<td><p>例:</p>
<p>RequiredFiles =</p>
<p>UNIRES。DLL、STDNAMES。GPD,</p>
<p>V3HOSTINGFILTER.DLL</p></td>
</tr>
<tr class="even">
<td><p><strong>RequiredClass</strong></p>
<p>このドライバーは、デバイスのドライバー/フレンドリ名とその GUID をキーとして使用して、定義されたクラスドライバーのすべてのファイルをインクルードします。 これは、printclass ドライバーをモデル固有のドライバーにリンクするためのメカニズムです。</p></td>
<td><p>RequiredClass ディレクティブは、クラスドライバーでは使用できません。 RequiredClass を使用する場合は、リンク先のプリンタードライバーと印刷クラスドライバーの間でファイル名の競合を回避する必要があります。</p>
<p>類似した名前のファイルは相互に上書きされませんが、トラブルシューティング中に、クラスドライバーパッケージファイルと v4 プリンタードライバーのファイルを区別することが困難な場合があります。</p></td>
<td><p>次に例を示します。</p>
<p>RequiredClass =</p>
<p>"Fabrikam PCL5e Class Driver", {9343720D-B67E-4451-B93F-6F721C439771}</p></td>
</tr>
<tr class="odd">
<td><p><strong>DriverFile</strong></p>
<p>これはレンダリングバイナリを指します。 Mxdwdrv は既定値ですが、クラスドライバーでは、unidrv または pscript5 を指定することもできます。 これは、v3 INF の同じディレクティブと機能的に同じです。</p></td>
<td><p>はクラスドライバーでのみ設定できます。 有効な選択肢は、unidrv または pscript5 です。 V4 印刷ドライバーは、RequiredClass から継承するか、既定で mxdwdrv .dll に継承します。</p></td>
<td><p>DriverFile =</p>
<p>unidrv</p></td>
</tr>
<tr class="even">
<td><p><strong>データ</strong></p>
<p>これにより、このドライバーのプライマリ GPD または PPD が定義されます。 これは、v3 INF の同じディレクティブと機能的に同じです。</p>
<p>Windows 10 では、v4 印刷ドライバーは GPD または PPD データファイルを引き続き指定できますが、PrintDeviceCapabilities 形式のデータファイルを記述する場合もあります。</p></td>
<td><p>必須。</p></td>
<td><p>例:</p>
<p>データファイル = FAPDL. gpd</p>
<p>データファイル = FAPDL .xml</p></td>
</tr>
<tr class="odd">
<td><p><strong>[DataFileType]</strong></p>
<p>DataFileType は、PrintDeviceCapabilities ファイルをデータファイルとして記述するときに使用する必要があります。また、GPD または PPD ベースのデータファイルと共に使用することもできます。</p></td>
<td><p>PrintDeviceCapabilities ファイルの場合は必須です。</p></td>
<td><p>次に例を示します。</p>
<p>DataFileType =</p>
<p>"application/vnd.ms-PrintDeviceCapabilities+xml"</p></td>
</tr>
<tr class="even">
<td><p><strong>フラグ</strong></p>
<p>これは、ドライバーに関連付けられている追加のオプションの属性を指定するために使用されます。</p>
<p></p>
NotShareable 可能: このフラグは、ドライバーが共有可能でないことを指定します。 これは、Microsoft XPS ドキュメントライターなどの仮想ドライバーに適しています。
SoftResetOnJobCancellation: このフラグは、デバイスが印刷ジョブのキャンセル時に USB ソフトリセット (IOCTL_USBPRINT_SOFT_RESET) を必要とすることを指定します。
アーカイブが有効になっている v4 ドライバーは、このフラグを使用して、アーカイブ最適化 XPS をスプールファイルとして要求します。</td>
<td><p>なし。</p></td>
<td><p>例:</p>
<p>Flags =</p>
<p>NotShareable 可能、</p>
<p>SoftResetOnJobCancellation</p>
<p>Flags =</p>
<p>アーカイブが有効、NotShareable 可能</p></td>
</tr>
<tr class="odd">
<td><p><strong>プリンター Driverid</strong></p>
<p>これは、印刷ドライバーを説明する一意の ID です。 2つのドライバーで同じプリンター Driverid が指定されている場合、共有と同じプリンターの拡張機能をサポートするためには互換性がある必要があります。</p></td>
<td><p>必須。</p></td>
<td><p>プリンター Driverid =</p>
<p>guid</p></td>
</tr>
<tr class="even">
<td><p><strong>PropertyBag</strong></p>
<p>このドライバーのドライバープロパティバッグを指定します。 これは、DriverPropertyBagTool または Visual Studio によって生成されるコンパイル済みのファイルです。</p></td>
<td><p>なし。</p></td>
<td><p>PropertyBag =</p>
<p>FAProperty. dpb</p></td>
</tr>
<tr class="odd">
<td><p><strong>ResourceFile</strong></p>
<p>ドライバーの文字列リソース DLL の名前を定義します。</p>
<p>Windows 10 では、ドライバーは .resx 形式を使用して ResourceFile を指定できます。</p></td>
<td><p>なし。</p></td>
<td><p>例:</p>
<p>ResourceFile =</p>
<p>FARC .dll</p></td>
</tr>
<tr class="even">
<td><p><strong>ConstraintScript</strong></p>
<p>ドライバーの JavaScript 制約ファイルの名前を定義します。</p></td>
<td><p>なし。</p></td>
<td><p>ConstraintScript =</p>
<p>FAConst js</p></td>
</tr>
<tr class="odd">
<td><p><strong>DriverCategory</strong></p>
<p>デバイスのカテゴリをいくつかのオプションのいずれかに定義します。 有効なオプションは次のとおりです。</p>
PrintFax. Fax PrintFax. printer. 3-D printfax. printer. printer. Virtual. printer. Virtual. printer. Virtual.</td>
<td><p>必須。</p></td>
<td><p>DriverCategory =</p>
<p>PrintFax.Printer</p>
<p>その他のドライバーカテゴリの詳細については、「<a href="printer-inf-file-entries.md" data-raw-source="[Printer INF File Entries](printer-inf-file-entries.md)">プリンター INF ファイルのエントリ</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>プリンター Extensionurl</strong></p>
<p>プリンター拡張アプリのコピーを取得するためのユーザーの URL を指定します。 プリンター共有で使用されます。</p></td>
<td><p>なし。</p></td>
<td><p>プリンター Extensionurl =</p>
<p>"<a href="https://www.fabrikam.com/files/setup.exe&quot" data-raw-source="https://www.fabrikam.com/files/setup.exe&quot">https://www.fabrikam.com/files/setup.exe&quot</a>;</p></td>
</tr>
<tr class="odd">
<td><p><strong>DevModeMap</strong></p>
<p>Devmode マッピングファイルを指定します。 これは、JavaScript コードでの変換を DEVMODE に置き換えるために、PrintTicket と共に使用される XML ファイルです。</p></td>
<td><p>なし。</p></td>
<td><p>DevModeMap =</p>
<p>fてマップします。</p></td>
</tr>
<tr class="even">
<td><p><strong>EventFile</strong></p>
<p>ドライバーイベント XML ファイルを指定します。</p></td>
<td><p>なし。</p></td>
<td><p>EventFile =</p>
<p>faevents .xml</p></td>
</tr>
<tr class="odd">
<td><p><strong>QueueProperties</strong></p>
<p>キュープロパティバッグの形式を指定します。 これは XML ファイルであるため、コンパイルすることはできません。</p></td>
<td><p>なし。</p></td>
<td><p>QueueProperties =</p>
<p>faQueueProps .xml</p></td>
</tr>
<tr class="even">
<td><p><strong>BidiUSBStatusInterface</strong></p>
<p>USB Bidi 通信に使用する1つ以上のデバイスインターフェイスに一致するハードウェア Id の一覧を指定します。</p></td>
<td><p>なし。ただし、印刷インターフェイスではない USB インターフェイスを介して状態が行われた場合にのみサポートされます。</p></td>
<td><p>BidiUSBStatusInterface =</p>
<p>"USB \ vid_1234 & pid_1234"、</p>
<p>"USB \ vid_1234 & pid_4567"</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserPropertyBagScope</strong></p>
<p>このディレクティブでは、ユーザープロパティバッグのスコープをキューまたは製造元として指定します。</p>
<p>このディレクティブを省略した場合は、Queue が既定値になります。 このディレクティブの有効なオプションは次のとおりです。</p>
Queue: これは既定の構成であり、Windows 8 の動作と一致します。
製造元: 同じ製造元の文字列を INF で使用するすべてのキューで、同じユーザープロパティバッグが使用されます。</td>
<td><p>なし。</p></td>
<td><p>UserPropertyBagScope =</p>
<p>製造元</p></td>
</tr>
<tr class="even">
<td><p><strong>RetrievePrintDeviceCapabilitiesFromDevice</strong></p>
<p>v4 ドライバーでは、PrintDeviceCapabilities ファイルをドライバーのデータファイルとして設定し、DataFileType によってデータファイルの種類が "application/PrintDeviceCapabilities + xml" であることが示されている場合に、WS-I 2.0 プリンターからファイルを取得する必要があることを指定できます。 有効なオプション:</p>
<p>有効なオプション:</p>
<p>True: ドライバーのローカルデータファイルを、デバイスの PrintDeviceCapabilities ファイルに置き換えることができます。</p>
<p>False: ドライバーのローカルデータファイルは、デバイスの PrintDeviceCapabilities ファイルに置き換えられません。</p>
<p>指定しない場合、このディレクティブの既定値は false になります。</p></td>
<td><p>なし。</p></td>
<td><p>次に例を示します。</p>
<p>RetrievePrintDeviceCapabilitiesFromDevice =</p>
<p>true</p></td>
</tr>
</tbody>
</table>

 

## <a name="bidifiles-section"></a>BidiFiles セクション


BidiFiles セクションは、Bidi 拡張ファイルを定義するために使用されます。 これは、TCP および WSD の Windows 7 形式と同じです。 USB キーワードは新しいものです。

次の表は、BidiFiles セクションで使用されるディレクティブを示しています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Directive</th>
<th>制限</th>
<th>使用方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>BidiSPMFile</strong></p>
<p>これにより、TCP/IP ベースのプリンター用の Bidi 拡張ファイルが定義されます。</p></td>
<td><p>なし。</p></td>
<td><p>BidiSPMFile = FaBidiSPM</p></td>
</tr>
<tr class="even">
<td><p><strong>BidiWSDFile</strong></p>
<p>これにより、WSD ベースのプリンター用の Bidi 拡張ファイルが定義されます。</p></td>
<td><p>なし。</p></td>
<td><p>BidiWSDFile = FABidiWSD</p></td>
</tr>
<tr class="odd">
<td><p><strong>BidiUSBFile</strong></p>
<p>これにより、USB 用の Bidi 拡張機能が定義されます。</p></td>
<td><p>なし。</p></td>
<td><p>BidiUSBFile = FABidiUSB</p></td>
</tr>
<tr class="even">
<td><p><strong>BidiUSBJSFile</strong></p>
<p>これにより、USB 用の JavaScript 拡張機能が定義されます。</p></td>
<td><p>なし。</p></td>
<td><p>BidiUSBJSFile = FABidiUSBJS</p></td>
</tr>
</tbody>
</table>

 

## <a name="driverrender-section"></a>DriverRender セクション


次の表は、DriverRender セクションで使用されるディレクティブを示しています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Directive</th>
<th>制限</th>
<th>使用方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>PageOutputQuality。OptionName</strong></p>
<p>PageOutputQuality のジョブの PrintTicket の値に基づいて、イメージの圧縮を変更します。</p></td>
<td><p>OptionName は、標準の PrintSchema 名前空間で指定された名前である必要があります。</p></td>
<td><p>PageOutputQuality. Draft =</p>
<p>MxdcImageType。 JPEGHigh</p>
<p>PageOutputQuality. Normal =</p>
<p>MxdcImageType. JPEGMedium</p>
<p>PageOutputQuality. High =</p>
<p>MxdcImageType .PNG</p></td>
</tr>
<tr class="even">
<td><p><strong>XpsFormat</strong></p>
<p>このドライバーの印刷システムによって生成される XPS 形式を変更します。 複数の値を指定できます。順序はドライバーの設定を表します。</p></td>
<td><p>Unidrv/PScript レンダリングを使用するクラスドライバーでは使用できません。</p></td>
<td><p>XpsFormat = XPS</p>
<p>XpsFormat = OpenXPS</p>
<p>XPSFormat = OpenXPS、XPS</p>
<p>XPSFormat = XPS、OpenXPS</p></td>
</tr>
<tr class="odd">
<td><p><strong>OutputFormat</strong></p>
<p>OutputFormat ディレクティブは、MIME の種類を使用してこのドライバーによって生成される単一の PDL を記述します。</p>
<p>この情報は、WSD プリンターの CreateJob または CreateJob2 操作中に使用されます。</p></td>
<td><p>なし。</p></td>
<td><p>有効な使用法の種類は次のとおりです。</p>
<p>OutputFormat =</p>
<p>"application/oxps"</p>
<p>OutputFormat =</p>
<p>"application/vnd. ms-xpsdocument"</p>
<p>OutputFormat =</p>
<p>"image/pwg"</p>
<p>OutputFormat =</p>
<p>"application/vnd. ms-3mfdocument"</p>
<p>その他の有効な定義済み MIME の種類は、ここで指定することもできます。</p></td>
</tr>
</tbody>
</table>

 

PageOutputQuality ディレクティブの MxdcImageType キーワードには、次の許可された値があります。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>MxdcImageType 値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>MxdcImageType.JPEGHigh</strong></p>
<p>高圧縮 JPEG (小さいファイル)</p></td>
</tr>
<tr class="even">
<td><p><strong>MxdcImageType.JPEGMedium</strong></p>
<p>中程度の圧縮 JPEG</p></td>
</tr>
<tr class="odd">
<td><p><strong>MxdcImageType.JPEGLow</strong></p>
<p>低圧縮 JPEG</p></td>
</tr>
<tr class="even">
<td><p><strong>MxdcImageType.PNG</strong></p>
<p>PNG ファイルの種類 (最大ファイル)</p></td>
</tr>
</tbody>
</table>

 

## <a name="filesave-section"></a>FileSave セクション


このセクションでは、ファイル保存のシナリオをサポートしています。 新しい PORTPROMPT ポートの種類に対して v4 印刷ドライバーがインストールされている場合、このセクションでは、 **[共通ファイル]** ウィンドウに表示するファイル拡張子を指定します。また、拡張機能とダイアログボックス自体をサポートするローカライズ可能なリソース文字列も指定します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Directive</th>
<th>制限</th>
<th>使用方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>&lt;FileExtensionName&gt;</strong></p>
<p>このディレクティブは、PORTPROMPT ポートを使用して、このドライバーからファイルを保存するときに使用される FileExtension を記述します。 値は、ドライバーの ResourceFile の resourceID です。 XPS および OXPS のみの場合は、resourceID を指定することができます。また、印刷スプーラではその内部リソースが使用されます。</p></td>
<td><p>なし。</p></td>
<td><p>&lt;FileExtensionName&gt;=</p>
<p>&lt;resourceID&gt;</p>
<p>Xps = 1234</p></td>
</tr>
<tr class="even">
<td><p><strong>SaveAsTitle</strong></p>
<p>このディレクティブは、[ファイルの保存] ダイアログで使用するタイトルを記述します。 値は、ドライバーの ResourceFile の resourceID です。</p></td>
<td><p>なし。</p></td>
<td><p>SaveAsTitle =</p>
<p>&lt;resourceID&gt;</p>
<p>SaveAsTitle =</p>
<p>4321</p></td>
</tr>
</tbody>
</table>

 

## <a name="printerextensions-section"></a>プリンター拡張セクション


[プリンター拡張] セクションでは、プリンターの拡張機能と、それがサポートする呼び出しモードを指定します。 これらの両方のエントリについて、アプリは自動的に印刷システムに登録されます。 さらに、アプリは、プリンター Driverid と理由 Id の2つの異なるパラメーターを使用して構成されます。 その結果、各エントリは別のプリンター Extensionid GUID を使用する必要があります。

次の表は、[プリンター拡張] セクションで使用されるディレクティブを示しています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Directive</th>
<th>制限</th>
<th>使用方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DriverEvent</strong></p>
<p>DriverEvent モードを提供しているアプリ。</p></td>
<td><p>なし。</p></td>
<td><p>DriverEvent =</p>
<p>app-v、{extensionID GUID}</p></td>
</tr>
<tr class="even">
<td><p><strong>PrintPreferences</strong></p>
<p>PrintPreferences モードを提供しているアプリ。</p></td>
<td><p>なし。</p></td>
<td><p>PrintPreferences =</p>
<p>app-v、{extensionID GUID}</p></td>
</tr>
</tbody>
</table>

 

次に、v4 印刷ドライバーマニフェストのサンプルを示します。

```INF
[DriverConfig]
DataFile=FAPDL.xml
RequiredFiles=UNIRES.DLL,STDNAMES.GPD,STDDTYPE.GDL,STDSCHEM.GDL,STDSCHMX.GDL,XPSSVCS.DLL,MSXPSINC.GPD,PWGRRenderFilter.DLL
ResourceFile=FARC.dll
PropertyBag=FAProperty.dpb
PrinterDriverID={GUID}
DriverCategory=PrintFax.Printer
ConstraintScript=faconst.js
EventFile=faevents.xml
PrinterExtensionUrl="https://www.fabrikam.com/download.asp?uiapp=120"
UserPropertyBagScope=Manufacturer
DataFileType="application/vnd.ms-PrintDeviceCapabilities+xml"
RetrievePrintDeviceCapabilitiesFromDevice=true

[BidiFiles]
BidiSPMFile=FABidiSPM.xml
BidiWSDFile=FABidiWSD.xml
BidiUSBFile=FaBidiUSB.xml
BidiUSBJSFile=FABidiUSBJS.js

[DriverRender]
PageOutputQuality.Draft=MxdcImageType.JPEGHigh
PageOutputQuality.Normal=MxdcImageType.JPEGMedium
PageOutputQuality.High=MxdcImageType.PNG
OutputFormat="image/pwg-raster"

[PrinterExtensions]
DriverEvent=FAapp.exe,{GUID}
PrintPreferences=FAapp.exe,{GUID2}
```

## <a name="related-topics"></a>関連トピック
[プリンターの INF ファイルのエントリ](printer-inf-file-entries.md)  



