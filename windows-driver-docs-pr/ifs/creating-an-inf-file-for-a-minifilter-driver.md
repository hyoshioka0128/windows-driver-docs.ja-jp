---
title: ミニフィルター ドライバー用の INF ファイルの作成
description: ミニフィルター ドライバー用の INF ファイルの作成
ms.assetid: 2ae41287-e3c5-4df5-8dec-8575343d5319
keywords:
- INF ファイル WDK ファイル システム ミニフィルター ドライバー
- DestinationDirs セクション WDK ファイル システム
- WDK のファイル システムのバージョン
- 文字列は、WDK のファイル システムをセクションします。
- DefaultUninstall セクション WDK ファイル システム
- ServiceInstall セクション WDK ファイル システム
- DefaultInstall セクション WDK ファイル システム
- AddRegistry セクション WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90713fedfef6f76bb2c6eeaa2910bf9447fb9756
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464310"
---
# <a name="creating-an-inf-file-for-a-minifilter-driver"></a>ミニフィルター ドライバー用の INF ファイルの作成


## <span id="ddk_creating_an_inf_file_for_a_minifilter_driver_if"></span><span id="DDK_CREATING_AN_INF_FILE_FOR_A_MINIFILTER_DRIVER_IF"></span>


ファイル システム ミニフィルター ドライバーの INF ファイルには、次のセクションでは、一般に含まれています。

バージョン (必須)

DestinationDirs (推奨されるが、省略可能)

DefaultInstall (必須)

DefaultInstall.Services (必須)

ServiceInstall (必須)

AddRegistry (必須)

DefaultUninstall (省略可能)

DefaultUninstall.Services (省略可能)

文字列 (必須)

**注**  以降では、Windows Vista x64 ベース システム、すべてのカーネル モード コンポーネントでは、ファイル システム ドライバー (ファイル システム、従来のフィルターおよびミニフィルター ドライバー) などの非 PnP (プラグ アンド プレイ) ドライバーを含む必要があります署名します。読み込みと実行します。 このシナリオでは、次の一覧には、ファイル システム ドライバーに関連する情報が含まれています。
-   ファイル システム ドライバーなど、非 PnP ドライバーの INF ファイルを格納する必要はありません\[製造元\]または\[モデル\]セクション。

-   [ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)にある、コマンド ライン ツール、 \\bin\\WDK のインストール ディレクトリの SelfSign ディレクトリを直接「記号を埋め込む」を使用するドライバー SYS実行可能ファイルです。 パフォーマンス上の理由から、ブート開始ドライバーが埋め込みの署名を含める必要があります。

-   INF ファイルでは、指定された、 [Inf2cat](https://go.microsoft.com/fwlink/p/?linkid=79443)コマンド ライン ツールは、ドライバー パッケージのカタログ (.cat) ファイルを作成するために使用できます。 カタログ ファイルのみを受信できる[WHQL](https://go.microsoft.com/fwlink/p/?linkid=8705)ロゴ署名します。

-   管理者特権で未署名のドライバを Windows Vista 以降の x64 ベース システムでインストールもできます。 ドライバーを読み込む (およびため、実行する) に失敗するただし、署名されていないためです。

-   ドライバーの署名の詳細については、[ドライバーの署名](https://msdn.microsoft.com/library/windows/hardware/ff544865)を参照してください。

-   運転署名プロセスの詳細については、[カーネル モード コード署名のチュートリアル](https://go.microsoft.com/fwlink/p/?linkid=79445)を参照してください。

-   カスタム カーネル モード開発ツールを含むすべてのカーネル モード コンポーネントに署名する必要があります。 詳細については、[開発およびテスト (Windows Vista 以降) の中にドライバーの署名](https://msdn.microsoft.com/library/windows/hardware/ff552275)を参照してください。

 

### <a name="span-idversionsectionrequiredspanspan-idversionsectionrequiredspanspan-idversionsectionrequiredspanversion-section-required"></a><span id="Version_Section__required_"></span><span id="version_section__required_"></span><span id="VERSION_SECTION__REQUIRED_"></span>バージョンのセクション (必須)

[**バージョン**](https://msdn.microsoft.com/library/windows/hardware/ff547502)セクションでは指定クラスと GUID ミニフィルター ドライバーの種類によって決定される次のコード例に示すようにします。

```cpp
[Version]
Signature   = "$WINDOWS NT$"
Class       = "ActivityMonitor"
ClassGuid   = {b86dff51-a31e-4bac-b3cf-e8cfe75c9fc2}
Provider    = %Msft%
DriverVer   = 10/09/2001,1.0.0.0
CatalogFile = 
```

次の表は、値で、ファイル システム ミニフィルター ドライバーを指定する必要があります、 [**バージョン**](https://msdn.microsoft.com/library/windows/hardware/ff547502)セクション。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">入力</th>
<th align="left">[値]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>署名</strong></p></td>
<td align="left"><p>「$WINDOWS NT $」</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Class</strong></p></td>
<td align="left"><p>参照してください<a href="file-system-filter-driver-classes-and-class-guids.md" data-raw-source="[File System Filter Driver Classes and Class GUIDs](file-system-filter-driver-classes-and-class-guids.md)">ファイル システム フィルター ドライバーのクラスとクラス Guid</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ClassGuid</strong></p></td>
<td align="left"><p>参照してください<a href="file-system-filter-driver-classes-and-class-guids.md" data-raw-source="[File System Filter Driver Classes and Class GUIDs](file-system-filter-driver-classes-and-class-guids.md)">ファイル システム フィルター ドライバーのクラスとクラス Guid</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Provider</strong></p></td>
<td align="left"><p>INF ファイルでは、Microsoft 以外のプロバイダーを指定してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>DriverVer</strong></p></td>
<td align="left"><p>参照してください<a href="https://msdn.microsoft.com/library/windows/hardware/ff547394" data-raw-source="[&lt;strong&gt;INF DriverVer directive&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547394)"> <strong>INF DriverVer ディレクティブ</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>CatalogFile</strong></p></td>
<td align="left"><p>署名されているウイルス対策ミニフィルター ドライバーについては、このエントリには、WHQL が指定したカタログ ファイルの名前が含まれています。 その他のミニフィルター ドライバーこのエントリは空白にする必要があります。 詳細については、の説明を参照して、 <strong>CatalogFile</strong>エントリ<a href="https://msdn.microsoft.com/library/windows/hardware/ff547502" data-raw-source="[&lt;strong&gt;INF Version Section&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547502)"> <strong>INF バージョン セクション</strong></a>します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddestinationdirssectionoptionalbutrecommendedspanspan-iddestinationdirssectionoptionalbutrecommendedspanspan-iddestinationdirssectionoptionalbutrecommendedspandestinationdirs-section-optional-but-recommended"></a><span id="DestinationDirs_Section__optional_but_recommended_"></span><span id="destinationdirs_section__optional_but_recommended_"></span><span id="DESTINATIONDIRS_SECTION__OPTIONAL_BUT_RECOMMENDED_"></span>DestinationDirs セクション (推奨されるが、省略可能)

[ **DestinationDirs** ](https://msdn.microsoft.com/library/windows/hardware/ff547383)セクション ミニフィルター ドライバーとアプリケーション ファイルのコピー先ディレクトリを指定します。

このセクションで、 **ServiceInstall**  セクションで、システム定義の数値でよく知られているシステムのディレクトリを指定することができます。 これらの値の一覧は、[ **INF DestinationDirs セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547383)を参照してください。 次のコード例で、値 12 がドライバーのディレクトリを参照 (%windir%\\system32\\ドライバー)、値 10 が Windows ディレクトリ (%windir%) を指します。

```cpp
[DestinationDirs]
DefaultDestDir = 12
Minispy.DriverFiles = 12
Minispy.UserFiles   = 10,FltMgr
```

### <a name="span-iddefaultinstallsectionrequiredspanspan-iddefaultinstallsectionrequiredspanspan-iddefaultinstallsectionrequiredspandefaultinstall-section-required"></a><span id="DefaultInstall_Section__required_"></span><span id="defaultinstall_section__required_"></span><span id="DEFAULTINSTALL_SECTION__REQUIRED_"></span>(必須) DefaultInstall セクション

[ **DefaultInstall** ](https://msdn.microsoft.com/library/windows/hardware/ff547356) ] セクションで、 [ **CopyFiles** ](https://msdn.microsoft.com/library/windows/hardware/ff546346)ディレクティブ ミニフィルター ドライバーのドライバー ファイル、ユーザー アプリケーションのコピーファイルで指定されている変換先を[ **DestinationDirs** ](https://msdn.microsoft.com/library/windows/hardware/ff547383)セクション。

**注**   、 [ **CopyFiles** ](https://msdn.microsoft.com/library/windows/hardware/ff546346)ディレクティブが、カタログ ファイルまたは INF ファイル自体を参照する必要があります。 SetupAPI では、これらのファイルが自動的にコピーします。

 

Windows オペレーティング システムの複数のバージョンでは、ドライバーをインストールする 1 つの INF ファイルを作成することができます。 この種類の INF ファイルを作成するには追加作成して[ **DefaultInstall**](https://msdn.microsoft.com/library/windows/hardware/ff547356)、 [ **DefaultInstall.Services**](https://msdn.microsoft.com/library/windows/hardware/ff547360)、 **DefaultUninstall**、および**DefaultUninstall.Services**セクションの各オペレーティング システムのバージョン。 各セクションのラベルでは、*装飾*(.ntx86、.ntia64、または .nt など) を適用するオペレーティング システムのバージョンを指定します。 この種類の INF ファイルを作成する方法の詳細については、[INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](https://msdn.microsoft.com/library/windows/hardware/ff540206)を参照してください。

次のコード例を示しています、典型的な[ **DefaultInstall** ](https://msdn.microsoft.com/library/windows/hardware/ff547356)セクション。

```cpp
[DefaultInstall]
OptionDesc = %MinispyServiceDesc%
CopyFiles = Minispy.DriverFiles, Minispy.UserFiles
```

### <a name="span-iddefaultinstallservicessectionrequiredspanspan-iddefaultinstallservicessectionrequiredspanspan-iddefaultinstallservicessectionrequiredspandefaultinstallservices-section-required"></a><span id="DefaultInstall.Services_Section__required_"></span><span id="defaultinstall.services_section__required_"></span><span id="DEFAULTINSTALL.SERVICES_SECTION__REQUIRED_"></span>(必須) DefaultInstall.Services セクション

[ **DefaultInstall.Services** ](https://msdn.microsoft.com/library/windows/hardware/ff547360)セクションが含まれています、 [ **AddService** ](https://msdn.microsoft.com/library/windows/hardware/ff546326)方法とタイミングを制御するディレクティブのサービスを次のコード例に示すように、特定のドライバーが読み込まれます。

```cpp
[DefaultInstall.Services]
AddService = %MinispyServiceName%,,Minispy.Service
```

### <a name="span-idserviceinstallsectionrequiredspanspan-idserviceinstallsectionrequiredspanspan-idserviceinstallsectionrequiredspanserviceinstall-section-required"></a><span id="ServiceInstall_Section__required_"></span><span id="serviceinstall_section__required_"></span><span id="SERVICEINSTALL_SECTION__REQUIRED_"></span>(必須) ServiceInstall セクション

**ServiceInstall**セクションには、ドライバー サービスを読み込むために使用される情報が含まれています。 MiniSpy サンプル ドライバーのこのセクションの名前は"Minispy.Service"次のコード例に示すように。 名前、 **ServiceInstall**にセクションを表示する必要があります、 [ **AddService** ](https://msdn.microsoft.com/library/windows/hardware/ff546326)ディレクティブで、 [ **DefaultInstall.Services**](https://msdn.microsoft.com/library/windows/hardware/ff547360)セクション。

```cpp
[Minispy.Service]
DisplayName    = %MinispyServiceName%
Description    = %MinispyServiceDesc%
ServiceBinary  = %12%\minispy.sys
ServiceType    = 2 ;    SERVICE_FILE_SYSTEM_DRIVER
StartType      = 3 ;    SERVICE_DEMAND_START
ErrorControl   = 1 ;    SERVICE_ERROR_NORMAL%
LoadOrderGroup = "FSFilter Activity Monitor"
AddReg         = Minispy.AddRegistry
Dependencies   = FltMgr
```

**ServiceType**エントリは、サービスの種類を指定します。 ミニフィルター ドライバーが 2 の値を指定する必要があります (サービス\_ファイル\_システム\_ドライバー)。 詳細については、 **ServiceType**エントリを参照してください[ **INF AddService ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546326)します。

**StartType**エントリでは、サービスを開始するタイミングを指定します。 次の表に、可能な値**StartType**とそれに対応する型を開始します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">[値]</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000000</p></td>
<td align="left"><p>SERVICE_BOOT_START</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000001</p></td>
<td align="left"><p>SERVICE_SYSTEM_START</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000002</p></td>
<td align="left"><p>SERVICE_AUTO_START</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000003</p></td>
<td align="left"><p>SERVICE_DEMAND_START</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000004</p></td>
<td align="left"><p>SERVICE_DISABLED</p></td>
</tr>
</tbody>
</table>

 

開始の詳細については、「ドライバーを開始型」を参照してください[何を決定しますと、ドライバーが読み込まれる](what-determines-when-a-driver-is-loaded.md)します。

**LoadOrderGroup**エントリがフィルター マネージャーとミニフィルター ドライバーと従来のファイル システム フィルター ドライバーの間の相互運用性を確認する必要がある情報を提供します。 指定する必要があります、 **LoadOrderGroup**を開発しているミニフィルター ドライバーの種類に適した値。 ロード順序グループを選択するを参照してください。[ロード順序グループとミニフィルター ドライバーの高度](load-order-groups-and-altitudes-for-minifilter-drivers.md)します。

指定する必要がありますに注意してください、 **LoadOrderGroup**値ミニフィルター ドライバーのスタートアップの種類は、サービスではない場合でも、\_ブート\_を開始します。 ミニフィルター ドライバーは、この方法で、従来のファイル システム フィルター ドライバーと異なります。

**注**  フィルター マネージャーの**StartType**値はサービス\_ブート\_を開始してその**LoadOrderGroup**値は FSFilter インフラストラクチャ. これらの値は、フィルター マネージャーが、ミニフィルター ドライバーが読み込まれる前に常に読み込まれていることを確認します。

 

方法の詳細については**StartType**と**LoadOrderGroup**エントリが特定のドライバーが読み込まれるときを参照してください[何を決定しますと、ドライバーが読み込まれる](what-determines-when-a-driver-is-loaded.md)します。

**注**  ミニフィルター ドライバーは、従来のファイル システム フィルター ドライバーとは異なり、 **StartType**と**LoadOrderGroup**値は場所を特定できませんミニフィルター ドライバーミニフィルターのインスタンスのスタックにアタッチします。 この場所はミニフィルター インスタンスが指定されている高度によって決まります。

 

**ErrorControl**エントリは、システムの起動時に開始するサービスが失敗した場合に実行されるアクションを指定します。 ミニフィルター ドライバーが 1 の値を指定する必要があります (サービス\_エラー\_通常)。 詳細については、 **ErrorControl**エントリを参照してください[ **INF AddService ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546326)します。

[ **AddReg** ](https://msdn.microsoft.com/library/windows/hardware/ff546320)ディレクティブを指すライター定義されている 1 つまたは複数の INF **AddRegistry**セクションでは、新しくインストールされたため、レジストリに格納される情報を含むサービス。 ミニフィルター ドライバーを使用して、 **AddRegistry**セクション ミニフィルター ドライバーのインスタンスを定義して、既定のインスタンスを指定します。

**依存関係**エントリを任意のサービスまたはドライバーが依存するロード順序グループの名前を指定します。 ミニフィルター ドライバーをすべて FltMgr、これはフィルター マネージャーのサービスの名前を指定してください。

### <a name="span-idaddregistrysectionrequiredspanspan-idaddregistrysectionrequiredspanspan-idaddregistrysectionrequiredspanaddregistry-section-required"></a><span id="AddRegistry_Section__required_"></span><span id="addregistry_section__required_"></span><span id="ADDREGISTRY_SECTION__REQUIRED_"></span>(必須) AddRegistry セクション

**AddRegistry**セクション キーと値をレジストリに追加します。 ミニフィルター ドライバーを使用して、 **AddRegistry**セクション ミニフィルターのインスタンスを定義して、既定のインスタンスを指定します。 フィルター マネージャー ミニフィルター ドライバーの新しいインスタンスを作成するたびに、この情報が使用されます。

MiniSpy サンプル ドライバーで、次の**AddRegistry**で %strkey% トークン定義と共に、セクション、 [**文字列**](https://msdn.microsoft.com/library/windows/hardware/ff547485)セクションで、次の 3 つのインスタンスを定義します。MiniSpy サンプル ドライバーの既定のインスタンスとしてその 1 つと呼びます。

```cpp
[Minispy.AddRegistry]
HKR,%RegInstancesSubkeyName%,%RegDefaultInstanceValueName%,0x00000000,%DefaultInstance%
HKR,%RegInstancesSubkeyName%"\"%Instance1.Name%,%RegAltitudeValueName%,0x00000000,%Instance1.Altitude%
HKR,%RegInstancesSubkeyName%"\"%Instance1.Name%,%RegFlagsValueName%,0x00010001,%Instance1.Flags%
HKR,%RegInstancesSubkeyName%"\"%Instance2.Name%,%RegAltitudeValueName%,0x00000000,%Instance2.Altitude%
HKR,%RegInstancesSubkeyName%"\"%Instance2.Name%,%RegFlagsValueName%,0x00010001,%Instance2.Flags%
HKR,%RegInstancesSubkeyName%"\"%Instance3.Name%,%RegAltitudeValueName%,0x00000000,%Instance3.Altitude%
HKR,%RegInstancesSubkeyName%"\"%Instance3.Name%,%RegFlagsValueName%,0x00010001,%Instance3.Flags%
```

### <a name="span-iddefaultuninstallsectionoptionalspanspan-iddefaultuninstallsectionoptionalspanspan-iddefaultuninstallsectionoptionalspandefaultuninstall-section-optional"></a><span id="DefaultUninstall_Section__optional_"></span><span id="defaultuninstall_section__optional_"></span><span id="DEFAULTUNINSTALL_SECTION__OPTIONAL_"></span>DefaultUninstall セクション (省略可能)

**DefaultUninstall**セクションは省略可能ですが、ドライバーをアンインストールする場合はお勧めします。 含まれている[ **DelFiles** ](https://msdn.microsoft.com/library/windows/hardware/ff547363)と[**して**](https://msdn.microsoft.com/library/windows/hardware/ff547374)ディレクティブを次のコード例に示すように、ファイルおよびレジストリのエントリを削除します。

```cpp
[DefaultUninstall]
DelFiles   = Minispy.DriverFiles, Minispy.UserFiles
DelReg     = Minispy.DelRegistry
```

### <a name="span-iddefaultuninstallservicessectionoptionalspanspan-iddefaultuninstallservicessectionoptionalspanspan-iddefaultuninstallservicessectionoptionalspandefaultuninstallservices-section-optional"></a><span id="DefaultUninstall.Services_Section__optional_"></span><span id="defaultuninstall.services_section__optional_"></span><span id="DEFAULTUNINSTALL.SERVICES_SECTION__OPTIONAL_"></span>DefaultUninstall.Services セクション (省略可能)

**DefaultUninstall.Services**セクションは省略可能ですが、ドライバーをアンインストールする場合はお勧めします。 含まれている[ **DelService** ](https://msdn.microsoft.com/library/windows/hardware/ff547377) MiniSpy サンプル ドライバーから次のコード例に示すように、ミニフィルター ドライバーのサービスを削除するためのディレクティブ。

**注**   、 [ **DelService** ](https://msdn.microsoft.com/library/windows/hardware/ff547377)ディレクティブは、SPSVCINST を常に指定する必要があります\_STOPSERVICE フラグ (0x00000200) が削除される前に、サービスを停止します。

 

```cpp
[DefaultUninstall.Services]
DelService = Minispy,0x200
```

### <a name="span-idstringssectionrequiredspanspan-idstringssectionrequiredspanspan-idstringssectionrequiredspanstrings-section-required"></a><span id="Strings_Section__required_"></span><span id="strings_section__required_"></span><span id="STRINGS_SECTION__REQUIRED_"></span>文字列のセクション (必須)

[**文字列**](https://msdn.microsoft.com/library/windows/hardware/ff547485)セクションは、INF ファイルで使用されている各 %strkey% トークンを定義します。

1 つの国際 INF ファイルを作成するにはロケールに固有の追加を作成して**文字列**。<em>LanguageID</em> INF ファイルのセクション。 国際対応の INF ファイルの詳細については、[International INF ファイルの作成](https://msdn.microsoft.com/library/windows/hardware/ff540208)を参照してください。

次のコード例を示しています、典型的な[**文字列**](https://msdn.microsoft.com/library/windows/hardware/ff547485)セクション。

```cpp
[Strings]
Msft               = "Microsoft Corporation"
MinispyServiceDesc = "Minispy mini-filter driver"
MinispyServiceName = "Minispy"
RegInstancesSubkeyName = "Instances"
RegDefaultInstanceValueName  = "DefaultInstance"
RegAltitudeValueName    = "Altitude"
RegFlagsValueName  = "Flags"

DefaultInstance    = "Minispy - Top Instance"
Instance1.Name     = "Minispy - Middle Instance"
Instance1.Altitude = "370000"
Instance1.Flags    = 0x1 ; Suppress automatic attachments
Instance2.Name     = "Minispy - Bottom Instance"
Instance2.Altitude = "365000"
Instance2.Flags    = 0x1 ; Suppress automatic attachments
Instance3.Name     = "Minispy - Top Instance"
Instance3.Altitude = "385000"
Instance3.Flags    = 0x1 ; Suppress automatic attachments
```

 

 




