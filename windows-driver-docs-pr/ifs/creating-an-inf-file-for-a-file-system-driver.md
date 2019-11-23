---
title: ファイル システム ドライバー用の INF ファイルの作成
description: ファイル システム ドライバー用の INF ファイルの作成
ms.assetid: 4b67159f-a5a5-46da-9500-a9c6b6995da4
keywords:
- INF ファイル WDK ファイルシステム、作成
- Setupapi.log WDK ファイルシステム
- 文字列セクション WDK ファイルシステム
- DefaultUninstall セクション WDK ファイルシステム
- ServiceInstall セクション WDK ファイルシステム
- DefaultInstall セクション WDK ファイルシステム
- SourceDisksNames セクション WDK ファイルシステム
- DestinationDirs セクション WDK ファイルシステム
- WDK のファイル システムのバージョン
- INF ファイルの作成 (WDK ファイルシステム)
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 06340df1d9191a9c1375f999d546ba1e38174a97
ms.sourcegitcommit: 2a1c24db881ed843498001493c3ce202c9aa03f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2019
ms.locfileid: "74128486"
---
# <a name="creating-an-inf-file-for-a-file-system-driver"></a>ファイル システム ドライバー用の INF ファイルの作成

Windows セットアップおよびデバイスインストーラーサービス (総称して「 [setupapi.log](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)」といいます) は、Windows セットアップとドライバーのインストールを制御する機能を提供します。 インストールプロセスは INF ファイルによって制御されます。

ファイルシステムドライバーの INF ファイルには、Setupapi.log がドライバーのインストールに使用する指示が記載されています。 INF ファイルは、ドライバーを実行するために必要なファイル、およびドライバーファイルのソースディレクトリと宛先ディレクトリを指定するテキストファイルです。 INF ファイルには、Setupapi.log によってレジストリに格納されるドライバー構成情報 (ドライバーの開始の種類や読み込み順序グループなど) も含まれています。

INF ファイルとその作成方法の詳細については、「 [Inf ファイル](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)および inf ファイルの作成」[セクションと「ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)」を参照してください。 ドライバーの署名に関する一般的な情報については、「[ドライバーの署名](https://docs.microsoft.com/windows-hardware/drivers/install/driver-signing)」を参照してください。

1つの INF ファイルを作成して、複数のバージョンの Windows オペレーティングシステムにドライバーをインストールすることができます。 このような INF ファイルの作成の詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の Inf ファイルの作成](https://docs.microsoft.com/windows-hardware/drivers/install/creating-inf-files-for-multiple-platforms-and-operating-systems)」および「[国際対応の Inf ファイルの作成](https://docs.microsoft.com/windows-hardware/drivers/install/creating-international-inf-files)」を参照してください。

64ビットバージョンの Windows Vista 以降では、ファイルシステムドライバー (ファイルシステム、レガシフィルター、ミニフィルタードライバー) などの非 PnP (プラグアンドプレイ) ドライバーを含むすべてのカーネルモードコンポーネントが、読み込んで実行するために署名されている必要があります。 これらのバージョンの Windows オペレーティングシステムでは、次の一覧に、ファイルシステムドライバーに関連する情報を示します。

- ファイルシステムドライバーを含む、PnP 以外のドライバーの INF ファイルには、\[の製造元\] または \[モデル\] セクションを含める必要はありません。

- [**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)コマンドラインツール (WDK インストールディレクトリの \bin\SelfSign ディレクトリにあります) を使用して、ドライバー SYS 実行可能ファイルに "sign" を直接埋め込むことができます。 パフォーマンス上の理由から、ブート開始ドライバーには、埋め込み署名が含まれている必要があります。

- INF ファイルを指定すると、 [**Inf2Cat**](https://docs.microsoft.com/windows-hardware/drivers/devtest/inf2cat)コマンドラインツールを使用して、ドライバーパッケージのカタログ (.cat) ファイルを作成できます。 [WHQL](https://go.microsoft.com/fwlink/p/?linkid=8705)ロゴ署名を受け取ることができるのは、カタログファイルだけです。

- 管理者特権では、署名されていないドライバーを Windows Vista 以降の x64 ベースのシステムにインストールすることができます。 ただし、ドライバーは署名されていないため (そのため実行) に失敗します。

- 64ビットバージョンの Windows Vista の運転署名プロセスを含む、運転署名プロセスの詳細については、「[カーネルモードコード署名チュートリアル](https://go.microsoft.com/fwlink/p/?linkid=79445)」を参照してください。

- カスタムカーネルモードの開発ツールを含む、すべてのカーネルモードコンポーネントに署名する必要があります。 詳細については、「[開発およびテスト中のドライバーへの署名 (Windows Vista 以降)](https://docs.microsoft.com/windows-hardware/drivers/install/signing-drivers-during-development-and-test--windows-vista-and-later-)」を参照してください。

INF ファイルを使用してレジストリから情報を読み取ったり、ユーザーモードアプリケーションを起動したりすることはできません。

INF ファイルを作成した後、通常はセットアップアプリケーションのソースコードを記述します。 セットアップアプリケーションは、ユーザーモードのセットアップ関数を呼び出して、INF ファイル内の情報にアクセスし、インストール操作を実行します。

独自のファイルシステムドライバーの INF ファイルを作成するには、次の情報をガイドとして使用します。 [ChkINF](https://docs.microsoft.com/windows-hardware/drivers/devtest/chkinf)ツールを使用して、INF ファイルの構文を確認できます。

一般に、ファイルシステムドライバーの INF ファイルには、次のセクションが含まれています。

- バージョン (必須)

- DestinationDirs (省略可能ですが推奨)

- SourceDisksNames (必須)

- SourceDisksFiles (必須)

- DefaultInstall (必須)

- DefaultInstall (必須)

- ServiceInstall (必須)

- DefaultUninstall (省略可能)

- DefaultUninstall. Services (省略可能)

- 文字列 (必須)

### <a name="version-section-required"></a>Version セクション (必須)

[[**バージョン**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)] セクションでは、次のコード例に示すように、ドライバーのバージョン情報を指定します。

```cpp
[Version]
Signature   = "$WINDOWS NT$"
Provider    = %Msft%
DriverVer   = 08/28/2000,1.0.0.1
CatalogFile =
```

次の表に、[[**バージョン**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)] セクションでファイルシステムフィルタードライバーによって指定される値を示します。

| エントリ | Value |
| ----- | ----- |
| **折本** | "$WINDOWS NT $" |
| **Provider** | 独自の INF ファイルでは、Microsoft 以外のプロバイダーを指定する必要があります。 |
| **DriverVer** | 「 [ **INF DriverVer ディレクティブ**」を参照してください。](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive) |
| **CatalogFile** | このエントリを空白のままにします。 将来、署名されたドライバーの WHQL が提供したカタログファイルの名前が含まれます。 |

### <a name="destinationdirs-section-optional-but-recommended"></a>DestinationDirs セクション (省略可能ですが推奨)

[**Destinationdirs**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)セクションでは、ファイルシステムドライバーファイルのコピー先のディレクトリを指定します。

このセクションで、 **ServiceInstall** セクションで、システム定義の数値を使用してよく知られているシステムのディレクトリを指定することができます。 これらの値の一覧については、「 [**INF DestinationDirs」セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)を参照してください。 次のコード例では、値 "12" は Drivers ディレクトリ (%windir%\system32\drivers) を参照します。

```cpp
[DestinationDirs]
DefaultDestDir = 12
ExampleFileSystem.DriverFiles = 12
```

### <a name="sourcedisksnames-section-required"></a>SourceDisksNames セクション (必須)

[**Sourcedisksnames**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section)セクションでは、使用する配布メディアを指定します。

次のコード例では、 [**Sourcedisksnames**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section)セクションに、ファイルシステムドライバー用の1つの配布メディアが一覧表示されます。 メディアの一意の識別子は1です。 メディアの名前は、INF ファイルの**Strings**セクションで定義されている% Disk1% トークンによって指定されます。

```cpp
[SourceDisksNames]
1 = %Disk1%
```

### <a name="sourcedisksfiles-section-required"></a>SourceDisksFiles セクション (必須)

[**Sourcedisksfiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section)セクションでは、コピーするファイルの場所と名前を指定します。

次のコード例では、[ [**Sourcedisksfiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section) ] セクションに、ファイルシステムドライバー用にコピーするファイルが一覧表示され、一意の識別子が 1 (この識別子は INF ファイルの[**Sourcedisksfiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section)セクションで定義されています) であるメディアでファイルが見つかることを指定します。

```cpp
[SourceDisksFiles]
examplefilesystem.sys = 1
```

### <a name="defaultinstall-section-required"></a>DefaultInstall セクション (必須)

[ **DefaultInstall** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-section) セクションで、 [ **CopyFiles** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)ディレクティブは、先に、ファイル システム ドライバーのドライバー ファイルをコピーします。指定された、 [ **DestinationDirs** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)セクション。

> [!NOTE]
> [**CopyFiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)ディレクティブは、カタログファイルまたは INF ファイル自体を参照することはできません。これらのファイルは、Setupapi.log によって自動的にコピーされます。

1つの INF ファイルを作成して、複数のバージョンの Windows オペレーティングシステムにドライバーをインストールすることができます。 この種類の INF ファイルは、オペレーティングシステムのバージョンごとに、追加の[**DefaultInstall**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-section)、 [**DefaultInstall**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-services-section)、 **Defaultuninstall**、および**defaultuninstall. services**セクションを作成することによって作成されます。 各セクションには、適用されるオペレーティングシステムのバージョンを指定する*装飾*(例、. ntx86、. ntia64、または nt) が付いています。 この種類の INF ファイルの作成の詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の Inf ファイルの作成](https://docs.microsoft.com/windows-hardware/drivers/install/creating-inf-files-for-multiple-platforms-and-operating-systems)」を参照してください。

次のコード例では、 [**CopyFiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)ディレクティブを使用して、INF ファイルの "ファイルシステム. driverfiles" セクションに一覧表示されているファイルをコピーします。

```cpp
[DefaultInstall]
OptionDesc = %ServiceDesc%
CopyFiles = ExampleFileSystem.DriverFiles

[ExampleFileSystem.DriverFiles]
examplefilesystem.sys
```

### <a name="defaultinstallservices-section-required"></a>DefaultInstall セクション (必須)

DefaultInstall セクションには、特定のドライバーのサービスが読み込まれる方法とタイミングを制御する[**Addservice**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)ディレクティブが含まれてい[**ます。** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-services-section)

次のコード例では、 [**Addservice**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)ディレクティブによってファイルシステムサービスがオペレーティングシステムに追加されます。 % ServiceName% トークンには、INF ファイルの**Strings**セクションで定義されているサービス名の文字列が含まれています。 例 Filesystem. Service は、ファイルシステムドライバーの**Serviceinstall**セクションの名前です。

```cpp
[DefaultInstall.Services]
AddService = %ServiceName%,,ExampleFileSystem.Service
```

### <a name="serviceinstall-section-required"></a>ServiceInstall セクション (必須)

**Serviceinstall**セクションでは、レジストリにサブキーまたは値の名前を追加し、値を設定します。 **Serviceinstall**セクションの名前は、 [**DefaultInstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-services-section)の[**addservice ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)に含まれている必要があります。

次のコード例は、ファイルシステムドライバーの**Serviceinstall**セクションを示しています。

```cpp
[ExampleFileSystem.Service]
DisplayName    = %ServiceName%
Description    = %ServiceDesc%
ServiceBinary  = %12%\examplefilesystem.sys
ServiceType    = 2 ;    SERVICE_FILE_SYSTEM_DRIVER
StartType      = 1 ;    SERVICE_SYSTEM_START
ErrorControl   = 1 ;    SERVICE_ERROR_NORMAL
LoadOrderGroup = "File System"
AddReg         = ExampleFileSystem.AddRegistry
```

**DisplayName**エントリは、サービスの名前を指定します。 前の例では、サービス名の文字列は、INF ファイルの**Strings**セクションで定義されている% ServiceName% トークンによって指定されています。

**Description**エントリは、サービスを説明する文字列を指定します。 前の例では、この文字列は、INF ファイルの**Strings**セクションで定義されている% servicedesc% token によって指定されています。

**Servicebinary**エントリは、サービスの実行可能ファイルへのパスを指定します。 前の例では、値12は Drivers ディレクトリ (%windir%\system32\drivers) を表しています。

**ServiceType**エントリは、サービスの種類を指定します。 次の表に、 **ServiceType**に使用できる値と、対応するサービスの種類を示します。

| Value | 説明 |
| ----- | ----------- |
| 0x00000001 | SERVICE_KERNEL_DRIVER (デバイスドライバーサービス) |
| 0x00000002 | SERVICE_FILE_SYSTEM_DRIVER (ファイルシステムまたはファイルシステムフィルタードライバーサービス) |
| 0x00000010 | SERVICE_WIN32_OWN_PROCESS (独自のプロセスで実行される Microsoft Win32 サービス) |
| 0x00000020 | SERVICE_WIN32_SHARE_PROCESS (プロセスを共有する Win32 サービス) |

**ServiceType**エントリは、ファイルシステムドライバーの場合は常に SERVICE_FILE_SYSTEM_DRIVER に設定する必要があります。

**Starttype**エントリは、サービスをいつ開始するかを指定します。 次の表に、 **Starttype**とそれに対応する開始の種類に使用できる値を示します。

| Value | 説明 |
| ----- | ----------- |
| ― | SERVICE_BOOT_START |
| 0x00000001 | SERVICE_SYSTEM_START |
| 0x00000002 | SERVICE_AUTO_START |
| 0x00000003 | SERVICE_DEMAND_START |
| 0x00000004 | SERVICE_DISABLED |

これらの開始の種類の詳細については、「[ドライバーが読み込まれるタイミング](what-determines-when-a-driver-is-loaded.md)を決定するには」を参照してください。

X64 ベースの Windows Vista システム以降では、ブート開始ドライバーのバイナリイメージファイル (開始の種類が SERVICE_BOOT_START のドライバー) には、埋め込まれた署名が含まれている必要があります。 この要件により、システムブートのパフォーマンスが最適になります。 詳細については、「[カーネルモードコード署名のチュートリアル](https://go.microsoft.com/fwlink/p/?linkid=79445)」を参照してください。

ドライバーが読み込まれるタイミングを、 **Starttype**および**loadordergroup**のエントリがどのように決定するかについては、「[ドライバーが読み込まれるタイミング](what-determines-when-a-driver-is-loaded.md)を確認する方法」を参照してください。

**Errorcontrol**エントリは、システムの起動時にサービスを開始できなかった場合に実行するアクションを指定します。 次の表に、 **errorcontrol**に使用できる値と、それに対応するエラー制御値の一覧を示します。

| Value | 説明 |
| ----- | ----------- |
| ― | SERVICE_ERROR_IGNORE (エラーをログに記録し、システムの起動を続行します。) |
| 0x00000001 | SERVICE_ERROR_NORMAL (エラーをログに記録し、ユーザーにメッセージを表示して、システムの起動を続行します)。 |
| 0x00000002 | SERVICE_ERROR_SEVERE (レジストリの [前回の制御セット] に切り替え、システムの起動を続行します。 |
| 0x00000003 | SERVICE_ERROR_CRITICAL (システムスタートアップがレジストリの正常でないコントロールセットを使用していない場合は、[正常起動時] に切り替えて、もう一度やり直してください。 まだ起動できない場合は、バグチェックルーチンを実行します。 システムを起動するために必要なドライバーだけが、INF ファイルにこの値を指定する必要があります。) |

ファイルシステムドライバーの場合は、 **Loadordergroup**エントリを常に "file system" に設定する必要があります。 これは、ファイルシステムフィルタードライバーまたはファイルシステムミニフィルタードライバーに対して指定されているものとは異なります。この場合、 **Loadordergroup**エントリは、ファイルシステムフィルターの読み込み順序グループのいずれかに設定されます。 ファイルシステムフィルタードライバーとファイルシステムミニフィルタードライバーに使用される読み込み順序グループの詳細については、「[ファイルシステムフィルタードライバーの読み込み順序](load-order-groups-for-file-system-filter-drivers.md)グループ」および「[ミニフィルタードライバーの](load-order-groups-and-altitudes-for-minifilter-drivers.md)ための負荷の増加」を参照してください。

[**AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)は、新しくインストールされたサービスのレジストリに格納される情報を含む、1つまたは複数の INF ライターで定義された**addregistry**セクションを参照します。

**注**   初期インストール後に、ドライバーのアップグレードに INF ファイルが使用される場合は、 **addregistry**セクションに含まれているエントリで、0x00000002 (FLG_ADDREG_NOCLOBBER) フラグを指定する必要があります。 このフラグを指定すると、後続のファイルがインストールされたときに HKLM\CurrentControlSet\Services のレジストリエントリが保持されます。 次に、例を示します。

```cpp
[ExampleFileSystem.AddRegistry]
HKR,Parameters,ExampleParameter,0x00010003,1
```

### <a name="defaultuninstall-section-optional"></a>DefaultUninstall セクション (省略可能)

**Defaultuninstall**セクションは省略可能ですが、ドライバーをアンインストールできる場合は推奨されます。 このファイルには、ファイルとレジストリエントリを削除するための[**Delfiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delfiles-directive)ディレクティブと[**delfiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delreg-directive)ディレクティブが含まれています。

次のコード例では、 [**delfiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delfiles-directive)ディレクティブを使用して、INF ファイルの "ファイルシステム. driverfiles" セクションに一覧表示されているファイルを削除します。

```cpp
[DefaultUninstall]
DelFiles   = ExampleFileSystem.DriverFiles
DelReg     = ExampleFileSystem.DelRegistry
```

[**Delreg**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delreg-directive)ディレクティブは、アンインストールするサービスのレジストリから削除する情報を含む、1つまたは複数の INF ライターで定義された**delreg**セクションを参照します。

### <a name="defaultuninstallservices-section-optional"></a>DefaultUninstall. Services セクション (省略可能)

**Defaultuninstall. Services**セクションは省略可能ですが、ドライバーをアンインストールできる場合は推奨されます。 ファイルシステムドライバーのサービスを削除するための[**Delservice**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delservice-directive)ディレクティブが含まれています。

次のコード例では、 [**Delservice**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delservice-directive)ディレクティブを使用して、ファイルシステムドライバーのサービスをオペレーティングシステムから削除します。

```cpp
[DefaultUninstall.Services]
DelService = %ServiceName%,0x200
```

> [!NOTE]
> [**Delservice**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delservice-directive)ディレクティブは、削除前にサービスを停止するように、常に 0x200 (SPSVCINST_STOPSERVICE) フラグを指定する必要があります。

> [!NOTE]
> ファイルシステム製品には、完全にはアンインストールできない特定のクラスがあります。 このような状況では、アンインストールできる製品のコンポーネントをアンインストールして、アンインストールできないコンポーネントをインストールしたままにすることができます。 このような製品の例として、Microsoft 単一インスタンスストア (SIS) 機能があります。

### <a name="strings-section-required"></a>Strings セクション (必須)

[**Strings**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section)セクションでは、INF ファイルで使用される% strkey% トークンを定義します。

たとえば、ファイルシステムドライバーでは、次の文字列が INF ファイルに定義されています。

```cpp
[Strings]
Msft        = "Microsoft Corporation"
ServiceDesc = "Example File System Driver"
ServiceName = "ExampleFileSystem"
ParameterPath = "SYSTEM\CurrentControlSet\Services\ExampleFileSystem\Parameters"
Disk1       = "Example File System Driver CD"
```

ロケール固有の**文字列**を追加することで、単一の国際 INF ファイルを作成できます。INF ファイルの*LanguageID*セクション。 国際対応の INF ファイルの詳細については、「[国際対応の Inf ファイルの作成](https://docs.microsoft.com/windows-hardware/drivers/install/creating-international-inf-files)」を参照してください。
