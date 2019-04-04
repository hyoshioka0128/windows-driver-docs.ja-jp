---
title: V4 ドライバー マニフェスト
description: V4 印刷ドライバー マニフェストは、特定のプリンター セットアップのディレクティブが含まれています、INF ファイルを組み合わせて使用されます。
ms.assetid: 187A10B7-2AAC-46D9-998C-C8724D8E3862
ms.date: 07/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: fc09503d34bea29e78406eb34c5884e853f0ab25
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464028"
---
# <a name="v4-driver-manifest"></a>V4 ドライバー マニフェスト


V4 印刷ドライバー マニフェストは、すべてのプリンター固有のセットアップ ディレクティブを含むテキスト ファイルです。 V4 印刷ドライバー マニフェストは組み合わせて使用 v4 印刷ドライバーの INF ファイルをセットの一部としてプリンターに固有の v4 プリンター ドライバーの。

セクションには、マニフェスト内のディレクティブが構成されています。

-   [DriverConfig セクション](#driverconfig-section)
-   [BidiFiles セクション](#bidifiles-section)
-   [DriverRender セクション](#driverrender-section)
-   [FileSave セクション](#filesave-section)
-   [PrinterExtensions セクション](#printerextensions-section)
-   [関連トピック](#related-topics)

## <a name="driverconfig-section"></a>DriverConfig セクション


次の表では、DriverConfig セクションで使用されるディレクティブを示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>ディレクティブ</th>
<th>制限</th>
<th>使用方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>RequiredFiles</strong></p>
<p>Ntprint.inf または ntprint4.inf からファイルが含まれています。</p>
<p>RequiredFiles ディレクティブは、Windows 10 では、次の値をサポートします。</p>
<p>PWGRRenderFilter.dll:ドライバーの依存ファイルの一覧には、Microsoft PWG ラスター レンダリングのフィルターを追加します。</p>
<p>PWG ラスター レンダリング フィルター レンダー フィルターでは、ドライバーの構成 PrintDeviceCapabilities ファイルで使用する必要があります。</p></td>
<td><p>問い合わせて、pscript5.dll、および mxdwdrv.dll は、このリストから省略する必要があります。 これらは自動的に解決されます。</p></td>
<td><p>例:</p>
<p>RequiredFiles =</p>
<p>UNIRES します。DLL、STDNAMES です。GPD、</p>
<p>V3HOSTINGFILTER します。DLL</p></td>
</tr>
<tr class="even">
<td><p><strong>RequiredClass</strong></p>
<p>キーとして、デバイスとその GUID のドライバー/フレンドリ名を使用して、定義済みのクラス ドライバーからのすべてのファイルを含めるには、このドライバーをによりします。 これは、printclass ドライバーを特定のドライバーをモデルにリンクするためのメカニズムです。</p></td>
<td><p>RequiredClass ディレクティブは、クラス ドライバーでは使用できません。 RequiredClass を使用する場合は、プリンター ドライバーとリンクしている印刷クラス ドライバーのファイル名の競合を避ける必要があります。</p>
<p>類似した名前のファイルは、相互に上書きされません、クラスのドライバー パッケージ ファイルと、v4 プリンター ドライバーからファイルを区別する、トラブルシューティングの際に難しいあります。</p></td>
<td><p>例:</p>
<p>RequiredClass =</p>
<p>「Fabrikam PCL5e クラス ドライバー」, {9343720D-B67E-4451-B93F-6F721C439771}</p></td>
</tr>
<tr class="odd">
<td><p><strong>DriverFile</strong></p>
<p>これは、バイナリのレンダリングを指します。 Mxdwdrv は、既定値がクラス ドライバーには、問い合わせてまたは pscript5.dll またはを指定できます。 これは、機能的 v3 INF で同じディレクティブと同じです。</p></td>
<td><p>クラスのドライバーでのみ設定できます。 有効な選択肢は、問い合わせてまたは pscript5.dll です。 V4 印刷ドライバーがか mxdwdrv.dll に RequiredClass または既定値から継承します。</p></td>
<td><p>DriverFile =</p>
<p>unidrv.dll</p></td>
</tr>
<tr class="even">
<td><p><strong>DataFile</strong></p>
<p>このドライバーをプライマリ GPD または PPD が定義します。 これは、機能的 v3 INF で同じディレクティブと同じです。</p>
<p>Windows 10 で v4 印刷ドライバーが継続されます GPD または PPD データ ファイルを指定する、PrintDeviceCapabilities 形式ではデータ ファイルも記述する可能性があります。</p></td>
<td><p>必須。</p></td>
<td><p>例:</p>
<p>DataFile=FAPDL.gpd</p>
<p>DataFile=FAPDL.xml</p></td>
</tr>
<tr class="odd">
<td><p><strong>DataFileType</strong></p>
<p>DataFileType は GPD または PPD ベース DataFile も使用もデータ ファイル、および月として PrintDeviceCapabilities ファイルを記述するときに使用する必要があります。</p></td>
<td><p>PrintDeviceCapabilities ファイルが必要です。</p></td>
<td><p>例:</p>
<p>DataFileType =</p>
<p>"application/vnd.ms-PrintDeviceCapabilities+xml"</p></td>
</tr>
<tr class="even">
<td><p><strong>フラグ</strong></p>
<p>これは、ドライバーに関連付けられている省略可能な追加の属性を指定に使用されます。</p>
<p></p>
NotShareable:このフラグは、ドライバーが共有可能ではないことを指定します。 これは、Microsoft XPS Document Writer などの仮想ドライバーに適しています。
SoftResetOnJobCancellation:このフラグは、デバイスが印刷ジョブの取り消しで USB ソフト リセット (IOCTL_USBPRINT_SOFT_RESET) が必要であるを指定します。
ArchiveEnabled v4 ドライバーでは、このフラグを使用して、操作のスプール ファイルとしてのアーカイブ用に最適化された XPS を要求します。</td>
<td><p>なし。</p></td>
<td><p>例:</p>
<p>フラグ =</p>
<p>NotShareable、</p>
<p>SoftResetOnJobCancellation</p>
<p>フラグ =</p>
<p>ArchiveEnabled、NotShareable</p></td>
</tr>
<tr class="odd">
<td><p><strong>PrinterDriverID</strong></p>
<p>これは、印刷ドライバーを説明する一意の ID です。 2 つのドライバーでは、同じ PrinterDriverID を指定する場合する必要がありますを共有するために互換性があるし、同じプリンター拡張機能をサポートします。</p></td>
<td><p>必須。</p></td>
<td><p>PrinterDriverID =</p>
<p>{guid}</p></td>
</tr>
<tr class="even">
<td><p><strong>PropertyBag</strong></p>
<p>このドライバーのドライバーのプロパティ バッグを指定します。 これは、DriverPropertyBagTool.exe または Visual Studio によって生成されたコンパイル済みのファイルです。</p></td>
<td><p>なし。</p></td>
<td><p>PropertyBag =</p>
<p>FAProperty.dpb</p></td>
</tr>
<tr class="odd">
<td><p><strong>ResourceFile</strong></p>
<p>ドライバーの文字列リソース DLL の名前を定義します。</p>
<p>Windows 10 では、ドライバーが .resx の形式を使用して ResourceFile を指定できます。</p></td>
<td><p>なし。</p></td>
<td><p>例:</p>
<p>ResourceFile =</p>
<p>FARC.dll</p></td>
</tr>
<tr class="even">
<td><p><strong>ConstraintScript</strong></p>
<p>ドライバーの JavaScript の制約のファイルの名前を定義します。</p></td>
<td><p>なし。</p></td>
<td><p>ConstraintScript =</p>
<p>FAConst.js</p></td>
</tr>
<tr class="odd">
<td><p><strong>DriverCategory</strong></p>
<p>いくつかのオプションのいずれかのデバイスのカテゴリを定義します。 有効なオプションは次のとおりです。</p>
PrintFax.Fax PrintFax.Printer PrintFax.Printer.3D PrintFax.Printer.File PrintFax.Printer.Service PrintFax.Printer.Virtual</td>
<td><p>必須。</p></td>
<td><p>DriverCategory =</p>
<p>PrintFax.Printer</p>
<p>その他のドライバー カテゴリの詳細については、<a href="printer-inf-file-entries.md" data-raw-source="[Printer INF File Entries](printer-inf-file-entries.md)">プリンター INF ファイルのエントリ</a>を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>PrinterExtensionUrl</strong></p>
<p>プリンター拡張アプリのコピーを取得するには、ユーザーの URL を指定します。 プリンターの共有で使用されます。</p></td>
<td><p>なし。</p></td>
<td><p>PrinterExtensionUrl =</p>
<p>"<a href="http://www.fabrikam.com/files/setup.exe&amp;quot" data-raw-source="http://www.fabrikam.com/files/setup.exe&amp;quot">http://www.fabrikam.com/files/setup.exe&quot</a>;</p></td>
</tr>
<tr class="odd">
<td><p><strong>DevModeMap</strong></p>
<p>Devmode のマッピング ファイルを指定します。 PrintTicket と JavaScript コードでの DEVMODE 変換に使用される XML ファイルです。</p></td>
<td><p>なし。</p></td>
<td><p>DevModeMap =</p>
<p>fadmmap.xml</p></td>
</tr>
<tr class="even">
<td><p><strong>EventFile</strong></p>
<p>ドライバーのイベントの XML ファイルを指定します。</p></td>
<td><p>なし。</p></td>
<td><p>EventFile =</p>
<p>faevents.xml</p></td>
</tr>
<tr class="odd">
<td><p><strong>QueueProperties</strong></p>
<p>キューのプロパティ バッグの形式を指定します。 これは、XML ファイルであり、コンパイルされない必要があります。</p></td>
<td><p>なし。</p></td>
<td><p>QueueProperties =</p>
<p>faQueueProps.xml</p></td>
</tr>
<tr class="even">
<td><p><strong>BidiUSBStatusInterface</strong></p>
<p>USB の双方向通信に使用する 1 つまたは複数のデバイスのインターフェイスと一致するハードウェア Id の一覧を指定します。</p></td>
<td><p>None、状態が、印刷のインターフェイスではない USB インターフェイス経由で行われた場合にのみサポートする必要がありますが、します。</p></td>
<td><p>BidiUSBStatusInterface =</p>
<p>”USB\vid_1234&amp;pid_1234”,</p>
<p>”USB\vid_1234&amp;pid_4567”</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserPropertyBagScope</strong></p>
<p>このディレクティブは、キューまたは製造元のいずれかとして、ユーザーのプロパティ バッグのスコープを指定します。</p>
<p>このディレクティブを省略すると、キューは、既定値です。 このディレクティブの有効なオプションは次のとおりです。</p>
キュー:これは、既定の構成と、Windows 8 の動作と一致します。
製造元:INF で同じ製造元の文字列を使用するすべてのキューでは、同じユーザーのプロパティ バッグを使用します。</td>
<td><p>なし。</p></td>
<td><p>UserPropertyBagScope =</p>
<p>製造元</p></td>
</tr>
<tr class="even">
<td><p><strong>RetrievePrintDeviceCapabilitiesFromDevice</strong></p>
<p>v4 ドライバーには、PrintDeviceCapabilities ファイル Ws-print v2.0 プリンターから取得する必要があります、PrintDeviceCapabilities ファイル、ドライバーのデータ ファイルとして設定して、DataFileType もことを示します限り、データ ファイルがの MIME の種類はのことを指定可能性があります"アプリケーション/vnd.ms-PrintDeviceCapabilities + xml"。 有効なオプション:</p>
<p>有効なオプション:</p>
<p>True:ドライバーのデバイスから PrintDeviceCapabilities ファイルに置き換えられますのローカル データ ファイルを使用できます。</p>
<p>False:ドライバーのローカル データ ファイルは、デバイスからの PrintDeviceCapabilities ファイルに置き換えられません。</p>
<p>指定しない場合、このディレクティブの既定値は false です。</p></td>
<td><p>なし。</p></td>
<td><p>例:</p>
<p>RetrievePrintDeviceCapabilitiesFromDevice =</p>
<p>true</p></td>
</tr>
</tbody>
</table>

 

## <a name="bidifiles-section"></a>BidiFiles セクション


BidiFiles セクションを使用して、双方向の拡張機能のファイルを定義します。 これは、TCP と WSD の Windows 7 の形式と同じです。 USB キーワードは、します。

次の表では、BidiFiles セクションで使用されるディレクティブを示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>ディレクティブ</th>
<th>制限</th>
<th>使用方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>BidiSPMFile</strong></p>
<p>これには、TCP ベースのプリンターの双方向の拡張機能ファイルを定義します。</p></td>
<td><p>なし。</p></td>
<td><p>BidiSPMFile=FaBidiSPM.xml</p></td>
</tr>
<tr class="even">
<td><p><strong>BidiWSDFile</strong></p>
<p>これには、WSD ベースのプリンターの双方向の拡張機能ファイルを定義します。</p></td>
<td><p>なし。</p></td>
<td><p>BidiWSDFile=FABidiWSD.xml</p></td>
</tr>
<tr class="odd">
<td><p><strong>BidiUSBFile</strong></p>
<p>これは、USB の双方向の拡張機能を定義します。</p></td>
<td><p>なし。</p></td>
<td><p>BidiUSBFile=FABidiUSB.xml</p></td>
</tr>
<tr class="even">
<td><p><strong>BidiUSBJSFile</strong></p>
<p>これは、USB の JavaScript の拡張機能を定義します。</p></td>
<td><p>なし。</p></td>
<td><p>BidiUSBJSFile=FABidiUSBJS.js</p></td>
</tr>
</tbody>
</table>

 

## <a name="driverrender-section"></a>DriverRender セクション


次の表では、DriverRender セクションで使用されるディレクティブを示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>ディレクティブ</th>
<th>制限</th>
<th>使用方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>PageOutputQuality.[OptionName]</strong></p>
<p>PageOutputQuality のジョブ PrintTicket の値に基づくイメージの圧縮を変更します。</p></td>
<td><p>OptionName は標準の PrintSchema 名前空間で指定された名前である必要があります。</p></td>
<td><p>PageOutputQuality.Draft=</p>
<p>MxdcImageType.JPEGHigh</p>
<p>PageOutputQuality.Normal=</p>
<p>MxdcImageType.JPEGMedium</p>
<p>PageOutputQuality.High=</p>
<p>MxdcImageType.PNG</p></td>
</tr>
<tr class="even">
<td><p><strong>XpsFormat</strong></p>
<p>このドライバーの印刷システムで生成された XPS 形式を変更します。 複数の値を指定することがあります、および順序が、ドライバーの基本設定を表します。</p></td>
<td><p>Unidrv/PScript レンダリングを使用するクラスのドライバーでは使用できません。</p></td>
<td><p>XpsFormat XPS を =</p>
<p>XpsFormat OpenXPS を =</p>
<p>XPSFormat OpenXPS、XPS を =</p>
<p>XPSFormat XPS、OpenXPS を =</p></td>
</tr>
<tr class="odd">
<td><p><strong>OutputFormat</strong></p>
<p>OutputFormat ディレクティブでは、MIME の種類を使用してこのドライバーによって生成される 1 つの PDL について説明します。</p>
<p>この情報は、WSD プリンター CreateJob または CreateJob2 操作中に使用されます。</p></td>
<td><p>なし。</p></td>
<td><p>有効な使用法の種類は次のとおりです。</p>
<p>OutputFormat =</p>
<p>"application/oxps"</p>
<p>OutputFormat =</p>
<p>"application/vnd.ms-xpsdocument"</p>
<p>OutputFormat =</p>
<p>"image/pwg-raster"</p>
<p>OutputFormat =</p>
<p>"application/vnd.ms-3mfdocument"</p>
<p>その他の有効な定義された MIME 型はここでも指定できます。</p></td>
</tr>
</tbody>
</table>

 

PageOutputQuality ディレクティブの MxdcImageType キーワードには、次の許可されている値があります。

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
<p>高い圧縮 JPEG (より小さいファイル)</p></td>
</tr>
<tr class="even">
<td><p><strong>MxdcImageType.JPEGMedium</strong></p>
<p>中規模の圧縮 JPEG</p></td>
</tr>
<tr class="odd">
<td><p><strong>MxdcImageType.JPEGLow</strong></p>
<p>低レベルの圧縮 JPEG</p></td>
</tr>
<tr class="even">
<td><p><strong>MxdcImageType.PNG</strong></p>
<p>PNG ファイルの種類 (最大ファイル)</p></td>
</tr>
</tbody>
</table>

 

## <a name="filesave-section"></a>FileSave セクション


このセクションでは、ファイルの保存するシナリオをサポートします。 このセクションで指定に表示されるファイル拡張子で新しい PORTPROMPT ポートの種類に対して v4 印刷ドライバーのインストール時、**共通ファイル**ウィンドウもサポートするローカライズ可能なリソース文字列を指定します、拡張機能と、ダイアログ ボックス自体。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>ディレクティブ</th>
<th>制限</th>
<th>使用方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>&lt;FileExtensionName&gt;</strong></p>
<p>このディレクティブは、PORTPROMPT ポートを使用してこのドライバーからファイルを保存するときに使用される FileExtension について説明します。 値は、ドライバーの ResourceFile からの resourceID です。 XPS と OXPS のみの場合は、0 のリソース Id を指定することがあり、印刷スプーラーはこれらの内部のリソースを使用します。</p></td>
<td><p>なし。</p></td>
<td><p>&lt;FileExtensionName&gt;=</p>
<p>&lt;resourceID&gt;</p>
<p>Xps 1234 を =</p></td>
</tr>
<tr class="even">
<td><p><strong>SaveAsTitle</strong></p>
<p>このディレクティブは、ファイルの保存 ダイアログで使用するタイトルをについて説明します。 値は、ドライバーの ResourceFile からの resourceID です。</p></td>
<td><p>なし。</p></td>
<td><p>SaveAsTitle =</p>
<p>&lt;resourceID&gt;</p>
<p>SaveAsTitle =</p>
<p>4321</p></td>
</tr>
</tbody>
</table>

 

## <a name="printerextensions-section"></a>PrinterExtensions セクション


PrinterExtensions セクションでは、プリンターの拡張機能とサポート呼び出しモードを指定します。 これらのエントリの両方は、アプリは印刷システムで自動的に登録されます。 さらに、アプリは、2 つの異なるパラメーターを PrinterDriverID とその順序で、ReasonID で構成されます。 その結果、各エントリは、異なる PrinterExtensionID GUID を使用する必要があります。

次の表では、PrinterExtensions セクションで使用されるディレクティブを示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>ディレクティブ</th>
<th>制限</th>
<th>使用方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DriverEvent</strong></p>
<p>アプリ サービス DriverEvent モード。</p></td>
<td><p>なし。</p></td>
<td><p>DriverEvent =</p>
<p>app.exe,{extensionID GUID}</p></td>
</tr>
<tr class="even">
<td><p><strong>PrintPreferences</strong></p>
<p>アプリ サービス PrintPreferences モード。</p></td>
<td><p>なし。</p></td>
<td><p>PrintPreferences =</p>
<p>app.exe, {extensionID GUID}</p></td>
</tr>
</tbody>
</table>

 

V4 印刷ドライバー マニフェストの例を次に示します。

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
PrinterExtensionUrl="http://www.fabrikam.com/download.asp?uiapp=120"
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



