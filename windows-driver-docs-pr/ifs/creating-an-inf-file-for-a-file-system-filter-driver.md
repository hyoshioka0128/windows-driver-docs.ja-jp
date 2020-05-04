---
title: ファイル システム フィルター ドライバー用の INF ファイルの作成
description: ファイル システム フィルター ドライバー用の INF ファイルの作成
ms.assetid: 1e8d0e59-eabd-4bdb-9675-e693a0b364ca
keywords:
- INF ファイル WDK ファイルシステム、作成
- Setupapi.log WDK ファイルシステム
- 文字列セクション WDK ファイルシステム
- DefaultUninstall セクション WDK ファイルシステム
- ServiceInstall セクション WDK ファイルシステム
- DefaultInstall セクション WDK ファイルシステム
- SourceDisksNames セクション WDK ファイルシステム
- DestinationDirs セクション WDK ファイルシステム
- バージョンセクション WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e059b72e9e6185ab2278ca662fa42d28afddbf28
ms.sourcegitcommit: b3bcd94c24b19b4c76c3b49672e237af03b3a7f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2020
ms.locfileid: "82173544"
---
# <a name="creating-an-inf-file-for-a-file-system-filter-driver"></a>ファイル システム フィルター ドライバー用の INF ファイルの作成


## <span id="ddk_creating_an_inf_file_for_a_file_system_filter_driver_if"></span><span id="DDK_CREATING_AN_INF_FILE_FOR_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


Windows セットアップおよびデバイスインストーラーサービス (総称して「 [setupapi.log](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)」といいます) は、Windows セットアップとドライバーのインストールを制御する機能を提供します。 インストールプロセスは INF ファイルによって制御されます。

ファイルシステムフィルタードライバーの INF ファイルは、Setupapi.log がドライバーのインストールに使用する指示を提供します。 INF ファイルは、ドライバーを実行するために必要なファイル、およびドライバーファイルのソースディレクトリと宛先ディレクトリを指定するテキストファイルです。 INF ファイルには、Setupapi.log によってレジストリに格納されるドライバー構成情報 (ドライバーの開始の種類や読み込み順序グループなど) も含まれています。

INF ファイルとその作成方法の詳細については、「 [Inf ファイル](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)および inf ファイルの作成」[セクションと「ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)」を参照してください。 ドライバーの署名に関する一般的な情報については、「[ドライバーの署名](https://docs.microsoft.com/windows-hardware/drivers/install/driver-signing)」を参照してください。

1つの INF ファイルを作成して、複数のバージョンの Windows オペレーティングシステムにドライバーをインストールすることができます。 このような INF ファイルの作成の詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の Inf ファイルの作成](https://docs.microsoft.com/windows-hardware/drivers/install/creating-inf-files-for-multiple-platforms-and-operating-systems)」および「[国際対応の Inf ファイルの作成](https://docs.microsoft.com/windows-hardware/drivers/install/creating-international-inf-files)」を参照してください。

64ビットバージョンの Windows Vista 以降では、ファイルシステムドライバー (ファイルシステム、レガシフィルター、ミニフィルタードライバー) などの非 PnP (プラグアンドプレイ) ドライバーを含むすべてのカーネルモードコンポーネントが、読み込んで実行するために署名されている必要があります。 これらのバージョンの Windows オペレーティングシステムでは、次の一覧には、ファイルシステムフィルタードライバーに関連する情報が含まれています。

-   ファイルシステムドライバーを含む、PnP 以外のドライバーの INF ファイルに\[は、製造元\]または\[モデル\]のセクションを含める必要はありません。

-   [**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)コマンドラインツールは、WDK インストールディレクトリの\\bin\\selfsign ディレクトリにあります。このツールを使用すると、ドライバー SYS 実行可能ファイルに直接 "sign" を挿入できます。 パフォーマンス上の理由から、ブート開始ドライバーには、埋め込み署名が含まれている必要があります。

-   INF ファイルを指定すると、 [**Inf2Cat**](https://docs.microsoft.com/windows-hardware/drivers/devtest/inf2cat)コマンドラインツールを使用して、ドライバーパッケージのカタログ (.cat) ファイルを作成できます。 [WHQL](https://go.microsoft.com/fwlink/p/?linkid=8705)ロゴ署名を受け取ることができるのは、カタログファイルだけです。

-   管理者特権では、署名されていないドライバーを Windows Vista 以降の x64 ベースのシステムにインストールすることができます。 ただし、ドライバーは署名されていないため (そのため実行) に失敗します。

-   64ビットバージョンの Windows Vista の運転署名プロセスを含む、運転署名プロセスの詳細については、「[カーネルモードコード署名チュートリアル](https://go.microsoft.com/fwlink/p/?linkid=79445)」を参照してください。

-   カスタムカーネルモードの開発ツールを含む、すべてのカーネルモードコンポーネントに署名する必要があります。 詳細については、「[開発およびテスト中のドライバーへの署名 (Windows Vista 以降)](https://docs.microsoft.com/windows-hardware/drivers/install/signing-drivers-during-development-and-test--windows-vista-and-later-)」を参照してください。

INF ファイルを使用してレジストリから情報を読み取ったり、ユーザーモードアプリケーションを起動したりすることはできません。

INF ファイルを作成した後、通常はセットアップアプリケーションのソースコードを記述します。 セットアップアプリケーションは、ユーザーモードのセットアップ関数を呼び出して、INF ファイル内の情報にアクセスし、インストール操作を実行します。

独自のフィルタードライバーの INF ファイルを作成するには、サンプルファイルシステムフィルタードライバーの INF ファイルをテンプレートとして使用します。 [InfVerif](https://docs.microsoft.com/windows-hardware/drivers/devtest/infverif)ツールを使用して、INF ファイルの構文を確認できます。

ファイルシステムフィルタードライバーの INF ファイルには、通常、次のセクションが含まれています。

-   バージョン (必須)

-   DestinationDirs (省略可能ですが推奨)

-   SourceDisksNames (必須)

-   SourceDisksFiles (必須)

-   DefaultInstall (必須)

-   DefaultInstall (必須)

-   ServiceInstall (必須)

-   DefaultUninstall (省略可能)

-   DefaultUninstall. Services (省略可能)

-   文字列 (必須)

### <a name="span-idversion_section__required_spanspan-idversion_section__required_spanspan-idversion_section__required_spanversion-section-required"></a><span id="Version_Section__required_"></span><span id="version_section__required_"></span><span id="VERSION_SECTION__REQUIRED_"></span>Version セクション (必須)

[**Version**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)セクションでは、次のコード例に示すように、フィルターの種類によって決定されるクラスと GUID を指定します。

```cpp
[Version]
Signature   = "$WINDOWS NT$"
Class       = "ActivityMonitor"
ClassGuid   = {b86dff51-a31e-4bac-b3cf-e8cfe75c9fc2}
Provider    = %Msft%
DriverVer   = 08/28/2000,1.0.0.1
CatalogFile = 
```

次の表に、[[**バージョン**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)] セクションでファイルシステムフィルタードライバーによって指定される値を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エントリ</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>折本</strong></p></td>
<td align="left"><p>"$WINDOWS NT $"</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>クラス</strong></p></td>
<td align="left"><p>「<a href="file-system-filter-driver-classes-and-class-guids.md" data-raw-source="[File System Filter Driver Classes and Class GUIDs](file-system-filter-driver-classes-and-class-guids.md)">ファイルシステムフィルタードライバークラスとクラス guid」を</a>参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ClassGuid</strong></p></td>
<td align="left"><p>「<a href="file-system-filter-driver-classes-and-class-guids.md" data-raw-source="[File System Filter Driver Classes and Class GUIDs](file-system-filter-driver-classes-and-class-guids.md)">ファイルシステムフィルタードライバークラスとクラス guid」を</a>参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロバイダー</strong></p></td>
<td align="left"><p>独自の INF ファイルでは、Microsoft 以外のプロバイダーを指定する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>DriverVer</strong></p></td>
<td align="left"><p>「 <a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive" data-raw-source="[&lt;strong&gt;INF DriverVer directive&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)"><strong>INF DriverVer ディレクティブ</strong></a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>CatalogFile</strong></p></td>
<td align="left"><p>このエントリを空白のままにします。 将来、署名されたドライバーの WHQL が提供したカタログファイルの名前が含まれます。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddestinationdirs_section__optional_but_recommended_spanspan-iddestinationdirs_section__optional_but_recommended_spanspan-iddestinationdirs_section__optional_but_recommended_spandestinationdirs-section-optional-but-recommended"></a><span id="DestinationDirs_Section__optional_but_recommended_"></span><span id="destinationdirs_section__optional_but_recommended_"></span><span id="DESTINATIONDIRS_SECTION__OPTIONAL_BUT_RECOMMENDED_"></span>DestinationDirs セクション (省略可能ですが推奨)

[**Destinationdirs**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)セクションでは、フィルタードライバーとアプリケーションファイルのコピー先となるディレクトリを指定します。

このセクションと**Serviceinstall**セクションでは、システム定義の数値を使用して、既知のシステムディレクトリを指定できます。 これらの値の一覧については、「 [**INF DestinationDirs」セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)を参照してください。 次のコード例では、値 "12" は Drivers ディレクトリ (% windir%\\system32\\Drivers) を参照し、値 "10" は Windows ディレクトリ (% windir%) を参照します。

```cpp
[DestinationDirs]
DefaultDestDir             = 12
MyLegacyFilter.DriverFiles = 12
MyLegacyFilter.UserFiles   = 10,MyLegacyFilter
```

### <a name="span-idsourcedisksnames_section__required_spanspan-idsourcedisksnames_section__required_spanspan-idsourcedisksnames_section__required_spansourcedisksnames-section-required"></a><span id="SourceDisksNames_Section__required_"></span><span id="sourcedisksnames_section__required_"></span><span id="SOURCEDISKSNAMES_SECTION__REQUIRED_"></span>SourceDisksNames セクション (必須)

[**Sourcedisksnames**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section)セクションでは、使用する配布メディアを指定します。

次のコード例では、 [**Sourcedisksnames**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section)セクションに1つのディストリビューションメディアが一覧表示されます。 メディアの一意の識別子は1です。 メディアの名前は、INF ファイルの[**Strings**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section)セクションで定義されている% Disk1% トークンによって指定されます。

```cpp
[SourceDisksNames]
1 = %Disk1%
```

### <a name="span-idsourcedisksfiles_section__required_spanspan-idsourcedisksfiles_section__required_spanspan-idsourcedisksfiles_section__required_spansourcedisksfiles-section-required"></a><span id="SourceDisksFiles_Section__required_"></span><span id="sourcedisksfiles_section__required_"></span><span id="SOURCEDISKSFILES_SECTION__REQUIRED_"></span>SourceDisksFiles セクション (必須)

[**Sourcedisksfiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section)セクションでは、コピーするファイルの場所と名前を指定します。

次のコード例では、[ [**Sourcedisksfiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section) ] セクションに、ドライバー用にコピーされるファイルが一覧表示され、一意の識別子が 1 (この識別子は INF ファイルの[**Sourcedisksfiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section)セクションで定義されています) であるメディアでファイルが見つかることを指定しています。

```cpp
[SourceDisksFiles]
myLegacyFilter.exe = 1
myLegacyFilter.sys = 1
```

### <a name="span-iddefaultinstall_section__required_spanspan-iddefaultinstall_section__required_spanspan-iddefaultinstall_section__required_spandefaultinstall-section-required"></a><span id="DefaultInstall_Section__required_"></span><span id="defaultinstall_section__required_"></span><span id="DEFAULTINSTALL_SECTION__REQUIRED_"></span>DefaultInstall セクション (必須)

[**DefaultInstall**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-section)セクションでは、 [**CopyFiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)ディレクティブにより、ファイルシステムフィルタードライバーのドライバーファイルとユーザーアプリケーションファイルが、 [**destinationdirs**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)セクションで指定されている宛先にコピーされます。

**Note**   [**CopyFiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)ディレクティブは、カタログファイルまたは INF ファイル自体を参照してはならないことに注意してください。これらのファイルは、Setupapi.log によって自動的にコピーされます。

 

1つの INF ファイルを作成して、複数のバージョンの Windows オペレーティングシステムにドライバーをインストールすることができます。 この種類の INF ファイルは、オペレーティングシステムのバージョンごとに、追加の[**DefaultInstall**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-section)、 [**DefaultInstall**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-services-section)、 **Defaultuninstall**、および**defaultuninstall. services**セクションを作成することによって作成されます。 各セクションには、適用されるオペレーティングシステムのバージョンを指定する*装飾*(例、. ntx86、. ntia64、または nt) が付いています。 この種類の INF ファイルの作成の詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の Inf ファイルの作成](https://docs.microsoft.com/windows-hardware/drivers/install/creating-inf-files-for-multiple-platforms-and-operating-systems)」を参照してください。

次のコード例では、 [**CopyFiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)ディレクティブを使用して、INF ファイルの MyLegacyFilter ファイルおよび MyLegacyFilter セクションに一覧表示されているファイルをコピーします。

```cpp
[DefaultInstall]
OptionDesc = %MyLegacyFilterServiceDesc%
CopyFiles = MyLegacyFilter.DriverFiles, MyLegacyFilter.UserFiles
```

### <a name="span-iddefaultinstallservices_section__required_spanspan-iddefaultinstallservices_section__required_spanspan-iddefaultinstallservices_section__required_spandefaultinstallservices-section-required"></a><span id="DefaultInstall.Services_Section__required_"></span><span id="defaultinstall.services_section__required_"></span><span id="DEFAULTINSTALL.SERVICES_SECTION__REQUIRED_"></span>DefaultInstall セクション (必須)

DefaultInstall セクションには、特定のドライバーのサービスが読み込まれる方法とタイミングを制御する[**Addservice**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)ディレクティブが含まれてい[**ます。**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-services-section)

次のコード例では、 [**addservice**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)ディレクティブによって、MyLegacyFilter サービスがオペレーティングシステムに追加されます。 % MyLegacyFilterServiceName% トークンには、INF ファイルの[**Strings**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section)セクションで定義されているサービス名の文字列が含まれています。 MyLegacyFilter は、ドライバーの**Serviceinstall**セクションの例の名前です。

```cpp
[DefaultInstall.Services]
AddService = %MyLegacyFilterServiceName%,,MyLegacyFilter.Service
```

### <a name="span-idddk_serviceinstall_section_ifspanspan-idddk_serviceinstall_section_ifspanserviceinstall-section-required"></a><span id="ddk_serviceinstall_section_if"></span><span id="DDK_SERVICEINSTALL_SECTION_IF"></span>ServiceInstall セクション (必須)

**Serviceinstall**セクションでは、レジストリにサブキーまたは値の名前を追加し、値を設定します。 **Serviceinstall**セクションの名前は、 [**DefaultInstall**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-services-section)セクションの[**addservice**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)ディレクティブに含まれている必要があります。

次のコード例は、MyLegacyFilter サンプルドライバーの**Serviceinstall**セクションを示しています。

```cpp
[MyLegacyFilter.Service]
DisplayName    = %MyLegacyFilterServiceName%
Description    = %MyLegacyFilterServiceDesc%
ServiceBinary  = %12%\myLegacyFilter.sys
ServiceType    = 2 ;    SERVICE_FILE_SYSTEM_DRIVER
StartType      = 3 ;    SERVICE_DEMAND_START
ErrorControl   = 1 ;    SERVICE_ERROR_NORMAL
LoadOrderGroup = "FSFilter Activity Monitor"
AddReg         = MyLegacyFilter.AddRegistry
```

**DisplayName**エントリは、サービスの名前を指定します。 前の例では、サービス名の文字列は、INF ファイルの[**Strings**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section)セクションで定義されている% MyLegacyFilterServiceName% トークンによって指定されています。

**Description**エントリは、サービスを説明する文字列を指定します。 前の例では、この文字列は、INF ファイルの[**Strings**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section)セクションで定義されている% MyLegacyFilterServiceDesc% トークンによって指定されています。

**Servicebinary**エントリは、サービスの実行可能ファイルへのパスを指定します。 前の例では、値12は Drivers ディレクトリ (% windir%\\system32\\drivers) を示しています。

**ServiceType**エントリは、サービスの種類を指定します。 次の表に、 **ServiceType**に使用できる値と、対応するサービスの種類を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000001</p></td>
<td align="left"><p>SERVICE_KERNEL_DRIVER (デバイスドライバーサービス)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000002</p></td>
<td align="left"><p>SERVICE_FILE_SYSTEM_DRIVER (ファイルシステムまたはファイルシステムフィルタードライバーサービス)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000010</p></td>
<td align="left"><p>SERVICE_WIN32_OWN_PROCESS (独自のプロセスで実行される Microsoft Win32 サービス)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000020</p></td>
<td align="left"><p>SERVICE_WIN32_SHARE_PROCESS (プロセスを共有する Win32 サービス)</p></td>
</tr>
</tbody>
</table>

 

ファイルシステムフィルタードライバーの**ServiceType**エントリは、\_常\_に\_サービスファイルシステムドライバーに設定する必要があります。

**Starttype**エントリは、サービスをいつ開始するかを指定します。 次の表に、 **Starttype**とそれに対応する開始の種類に使用できる値を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
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

 

これらの開始の種類の詳細については、「[ドライバーが読み込まれるタイミングを決定する](what-determines-when-a-driver-is-loaded.md)」を参照してください。

ドライバーの開始の種類が [サービス\_ブート\_開始] (つまり、ドライバーがブート開始ドライバーである) の場合は、 **loadordergroup**エントリが、開発しているフィルターの種類に適していることを確認する必要もあります。 読み込み順序グループを選択するには、「[ファイルシステムフィルタードライバーの読み込み順序グループ](load-order-groups-for-file-system-filter-drivers.md)」を参照してください。 また、x64 ベースの Windows Vista システム以降では、ブート開始ドライバーのバイナリイメージファイルには、埋め込み署名が含まれている必要があります。 この要件により、システムブートのパフォーマンスが最適になります。 詳細については、「[カーネルモードコード署名のチュートリアル](https://go.microsoft.com/fwlink/p/?linkid=79445)」を参照してください。

ドライバーが読み込まれるタイミングを、 **Starttype**および**loadordergroup**のエントリがどのように決定するかについては、「[ドライバーが読み込まれるタイミング](what-determines-when-a-driver-is-loaded.md)を確認する方法」を参照してください。

**Errorcontrol**エントリは、システムの起動時にサービスを開始できなかった場合に実行するアクションを指定します。 次の表に、 **errorcontrol**に使用できる値と、それに対応するエラー制御値の一覧を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">アクション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000000</p></td>
<td align="left"><p>SERVICE_ERROR_IGNORE (エラーをログに記録し、システムの起動を続行します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000001</p></td>
<td align="left"><p>SERVICE_ERROR_NORMAL (エラーをログに記録し、ユーザーにメッセージを表示して、システムの起動を続行します)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000002</p></td>
<td align="left"><p>SERVICE_ERROR_SEVERE (レジストリの [前回の制御セット] に切り替えて、システムの起動を続行します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000003</p></td>
<td align="left"><p>SERVICE_ERROR_CRITICAL (システムスタートアップがレジストリの正常でないコントロールセットを使用していない場合は、[正常起動時] に切り替えて、もう一度やり直してください。 まだ起動できない場合は、バグチェックルーチンを実行します。 システムを起動するために必要なドライバーだけが、INF ファイルにこの値を指定する必要があります。)</p></td>
</tr>
</tbody>
</table>

 

**Loadordergroup**エントリは、開発中のファイルシステムフィルタードライバーの種類に適した読み込み順序グループに設定する必要があります。 読み込み順序グループを選択するには、「[ファイルシステムフィルタードライバーの読み込み順序グループ](load-order-groups-for-file-system-filter-drivers.md)」を参照してください。

[**AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)は、新しくインストールされたサービスのレジストリに格納される情報を含む、1つまたは複数の INF ライターで定義された**addregistry**セクションを参照します。

**注**  初期インストール後に INF ファイルを使用してドライバーをアップグレードする場合は、 **addregistry**セクションに含まれているエントリで、0x00000002 (FLG\_ADDREG\_NOCLOBBER) フラグを指定する必要があります。 このフラグを指定すると、後続の\\ファイル\\がインストールされるときに HKLM CurrentControlSet Services のレジストリエントリが保持されます。 次に例を示します。

 

```cpp
[ExampleFileSystem.AddRegistry]
HKR,Parameters,ExampleParameter,0x00010003,1
```

### <a name="span-iddefaultuninstall_section__optional_spanspan-iddefaultuninstall_section__optional_spanspan-iddefaultuninstall_section__optional_spandefaultuninstall-section-optional"></a><span id="DefaultUninstall_Section__optional_"></span><span id="defaultuninstall_section__optional_"></span><span id="DEFAULTUNINSTALL_SECTION__OPTIONAL_"></span>DefaultUninstall セクション (省略可能)

**Defaultuninstall**セクションは省略可能ですが、ドライバーをアンインストールできる場合は推奨されます。 このファイルには、ファイルとレジストリエントリを削除するための[**Delfiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delfiles-directive)ディレクティブと[**delfiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delreg-directive)ディレクティブが含まれています。

次のコード例では、 [**delfiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delfiles-directive)ディレクティブによって、ドライバーの INF ファイルの MyLegacyFilter ファイルおよび MyLegacyFilter セクションに記載されているファイルが削除されます。

```cpp
[DefaultUninstall]
DelFiles   = MyLegacyFilter.DriverFiles, MyLegacyFilter.UserFiles
DelReg     = MyLegacyFilter.DelRegistry
```

[**Delreg**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delreg-directive)ディレクティブは、アンインストールするサービスのレジストリから削除する情報を含む、1つまたは複数の INF ライターで定義された**delreg**セクションを参照します。

### <a name="span-iddefaultuninstallservices_section__optional_spanspan-iddefaultuninstallservices_section__optional_spanspan-iddefaultuninstallservices_section__optional_spandefaultuninstallservices-section-optional"></a><span id="DefaultUninstall.Services_Section__optional_"></span><span id="defaultuninstall.services_section__optional_"></span><span id="DEFAULTUNINSTALL.SERVICES_SECTION__OPTIONAL_"></span>DefaultUninstall. Services セクション (省略可能)

**Defaultuninstall. Services**セクションは省略可能ですが、ドライバーをアンインストールできる場合は推奨されます。 ファイルシステムフィルタードライバーのサービスを削除するための[**Delservice**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delservice-directive)ディレクティブが含まれています。

次のコード例では、 [**delservice**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delservice-directive)ディレクティブによって、オペレーティングシステムから MyLegacyFilter サービスが削除されます。

```cpp
[DefaultUninstall.Services]
DelService = MyLegacyFilter,0x200
```

**注**   [**delservice**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delservice-directive)ディレクティブでは、削除前にサービスを\_停止するように、常に 0x200 (SPSVCINST stopservice) フラグを指定する必要があります。

 

### <a name="span-idstrings_section__required_spanspan-idstrings_section__required_spanspan-idstrings_section__required_spanstrings-section-required"></a><span id="Strings_Section__required_"></span><span id="strings_section__required_"></span><span id="STRINGS_SECTION__REQUIRED_"></span>Strings セクション (必須)

[**Strings**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section)セクションでは、次の例に示すように、INF ファイルで使用される% strkey% トークンを定義します。

```cpp
[Strings]
Msft                      = "Microsoft Corporation"
MyLegacyFilterServiceDesc = "MyLegacyFilterFilter Driver"
MyLegacyFilterServiceName = "MyLegacyFilter"
MyLegacyFilterRegistry    = "system\currentcontrolset\services\MyLegacyFilter"
MyLegacyFilterMaxRecords  = "MaxRecords"
MyLegacyFilterMaxNames    = "MaxNames"
MyLegacyFilterDebugFlags  = "DebugFlags"
Disk1                     = "MyLegacyFilter Source Media"
```

ロケール固有の文字列を追加することで、単一の国際 INF ファイルを作成でき[**ます。**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section)INF ファイルの*LanguageID*セクション。 国際対応の INF ファイルの詳細については、「[国際対応の Inf ファイルの作成](https://docs.microsoft.com/windows-hardware/drivers/install/creating-international-inf-files)」を参照してください。

 

 




