---
title: InfVerif エラー 1330
description: InfVerif (InfVerif) は、ドライバーの INF ファイルをテストするために使用できるツールです。 Inf 構文の問題を報告するだけでなく、INF ファイルがユニバーサルであるかどうかが報告されます。
ms.assetid: 6F565E1C-C6FC-4637-B476-FE4E4672CCC3
ms.date: 03/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: 32d53db49eadac6ac822d96b74a3b5a008ca50b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839555"
---
# <a name="infverif-error-1330---1333"></a>InfVerif エラー 1330 ~ 1333

InfVerif Error 1330 を使用すると、1つの宛先ファイルが複数のソースファイルによって上書きされる場合に、機能エラーを防ぐことができます。 次に、例を示します。

```command
[CopyFiles.A]
DesiredFileName1,SourceFile1A ; Used by DDInstallSection A

[CopyFiles.B]
DesiredFileName1,SourceFile1B ; Used by DDInstallSection B
```

複数の[Ddinstall セクション](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)で、 [copyfiles](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)ディレクティブを使用して異なるソースファイルを1つのターゲットファイルにコピーする場合、 **ddinstall セクション**がすべて同じシステムで処理されると、これらの**CopyFiles**が競合する可能性があります。 この例として、2つの異なるデバイスが同じドライバーを使用していて、インストールセクションが異なる場合や、オフラインのドライバーイメージングおよび展開シナリオがある場合が挙げられます。 異なる**ddinstall セクション**からの複数のソースファイルが同一の同一の単一のターゲットファイルにコピーされるため、異なる**ddinstall セクション**の異なるソースファイルが、コピーされた最後のファイルである変換先に配置されます。予期しない結果になる可能性があります。

## <a name="cases"></a>場合

このドキュメントでは、次の場合に機能エラーを削除するメソッドに古い構文を更新する方法に関するガイダンスを提供します。 すべてのケースが以下に記載されているわけではありません。各 INF に固有の他の理由が考えられます。

* 異なる**Ddinstall セクション**で、1つのサービスのサービスバイナリの名前を変更する

* 異なる**Ddinstall セクション**異なるソースファイルの名前を変更して、ドライバーまたはユーザーモードアプリケーションがアクセスするターゲットファイルの場所にコピーします。

### <a name="different-ddinstall-sections-rename-a-service-binary-for-one-service"></a>異なる**Ddinstall セクション**で、1つのサービスのサービスバイナリの名前を変更する

次のコードは、1つのサービスに対して、異なる**Ddinstall セクション**がサービスバイナリの名前を変更する方法の例です。

```command
[DDInstallSection_A]
CopyFiles = CopyFiles.A

[DDInstallSection_B]
CopyFiles = CopyFiles.B

[CopyFiles.A]
ServiceBinaryFile, ServiceBinaryA

[CopyFiles.B]
ServiceBinaryFile, ServiceBinaryB

[DDInstallSection_A.Services]
AddService = ServiceName, 0x00000002, ServiceName_Install

[DDInstallSection_B.Services]
AddService = ServiceName, 0x00000002, ServiceName_Install

[ServiceName_Install]
ServiceType    = 1
StartType      = 3
ErrorControl   = 0
ServiceBinary  = %12%\ServiceBinaryFile
```

このコードを更新するには、バイナリごとに異なるサービス名を作成します。

```command
[DDInstallSection_A]
CopyFiles = CopyFiles.A

[DDInstallSection_B]
CopyFiles = CopyFiles.B

[CopyFiles.A]
ServiceBinaryA

[CopyFiles.B]
ServiceBinaryB

[DDInstallSection_A.Services]
AddService = ServiceName1, 0x00000002, ServiceName1_Install

[DDInstallSection_B.Services]
AddService = ServiceName2, 0x00000002, ServiceName2_Install

[ServiceName1_Install]
ServiceType    = 1
StartType      = 3
ErrorControl   = 0
ServiceBinary  = %12%\ServiceBinaryA

[ServiceName2_Install]
ServiceType    = 1
StartType      = 3
ErrorControl   = 0
ServiceBinary  = %12%\ServiceBinaryB
```

### <a name="different-ddinstall-sections-rename-a-source-file-to-get-copied-over-to-a-destination-file-location-accessed-by-the-driver-or-a-user-mode-application"></a>異なる**Ddinstall セクション**異なるソースファイルの名前を変更して、ドライバーまたはユーザーモードアプリケーションがアクセスするターゲットファイルの場所にコピーします。

この場合、ドライバーは、動的なファイルの場所として使用されている固定のファイルの場所にアクセスしています。 複数のソースファイルを追跡する1つの動的変数を使用するには、 [AddReg](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive) hkr エントリを使用して、実行時に取得できるパスを格納します。 これは、 **AddReg** hkr エントリがデバイスに対して相対的に格納されているために機能します。

**AddReg** hkr エントリは、ソースファイルのコピー先ファイルを1つだけ選択するのではなく、ソースファイルのファイルの場所を指定します。

```command
[A.AddReg]
HKR,, FileName1Path, "%13%\SourceFile1A"

[B.AddReg]
HKR,, FileName1Path, "%13%\SourceFile1B"
```

固定ファイルの場所にアクセスするのではなく、デバイス上の設定からターゲットファイルの場所を取得できます。 ターゲットファイルの場所は、INF によってレジストリ値に格納され、ドライバーの API 呼び出しを通じて取得されます。

INF を使用して値をプロビジョニングするには、inf [DDInstall セクション](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)または[inf DDINSTALL. HW セクション](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)から参照されている AddReg*セクション*で、hkr *Reg ルート*エントリを使用して[inf](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)を使用します。

レジストリ値は、1つの対象ファイルの場所ではなく、ターゲットファイルを追跡するため、ドライバーはこれらのファイルに異なる方法でアクセスする必要があります。 ターゲットファイルにアクセスするために、ドライバーは次のいずれかの Api を呼び出して、レジストリ値を開き、そのソースファイルの場所を返すようにする必要があります。

#### <a name="wdm"></a>WDM

* [**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)

#### <a name="wdf"></a>WDF

* [**WdfDeviceOpenRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceopenregistrykey)

* [**WdfFdoInitOpenRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitopenregistrykey)

#### <a name="other-user-mode-code"></a>その他のユーザーモードコード

* [**CM_Open_DevNode_Key**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_open_devnode_key)

> [!NOTE]
> この例では、INF ペイロードがファイルを保存する場所はソリューションに影響しません。  ただし、ベストプラクティスを使用するために、この例では[Dirid](https://docs.microsoft.com/windows-hardware/drivers/install/using-dirids) 13 を使用します。これは、より短いファイルコピーでより高速なインストールを提供するためです。  詳細については、「[DIRIDs の使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-dirids)」および「[ドライバーストアからの実行](https://docs.microsoft.com/windows-hardware/drivers/develop/universal-driver-scenarios#run-from-the-driver-store)」を参照してください。

次のコード例は、古い構文を使用する INF を更新する方法を示しています。

### <a name="details-for-different-source-files-mapped-to-one-destination-file"></a>1つのターゲットファイルにマップされているさまざまなソースファイルの詳細

<table>
<thead>
<tr>
<th>ソース コード</th>
<th>Comment</th>
</tr>
</thead>
<tbody>
<tr><td><pre>[DestinationDirs]
CopyFiles.A = 12
CopyFiles.B = 12</br>
[DDInstallSection_A]
CopyFiles  = CopyFiles.A</br>
[DDInstallSection_B]
CopyFiles = CopyFiles.B
</td>
</pre>
<td></br>ファイルを手動で移動する場所を選択する</td>
</tr>
<tr>
<td><pre>[CopyFiles.A]
DesiredFileName1,SourceFile1A ; HW Version A
DesiredFileName2,SourceFile2A ; HW Version A</br>
[CopyFiles.B]
DesiredFileName1,SourceFile1B ; HW Version B
DesiredFileName2,SourceFile2B ; HW Version B
</pre></td>
<td></br><u>ファイルコピー手法</u>: インストールする Ddinstall セクションによって、ドライバーがリンクされているターゲットファイルパスにコピーされるソースファイルが選択されるように、ファイルの名前を変更します。

これは、すべての DDInstall セクションのすべてのファイルがインストール前にコピーされる場合には機能しません。
</td>
</tr>
</tbody>
</table>

### <a name="details-for-udating-by-using-addreg-hkr-entries"></a>AddReg HKR エントリを使用した udating の詳細

<table>
<thead>
<tr>
<th>ソース コード</th>
<th>Comment</th>
</tr>
</thead>
<tbody>
<tr>
<td><pre>[DestinationDirs]
CopyFiles.A = 13
CopyFiles.B = 13
</td>
</pre>
<td></br>すべてをドライバーストアディレクトリ (Dirid 13) に残しておくことをお勧めします。</td>
</tr>
<tr>
<td><pre>[DDInstallSection_A]
CopyFiles = CopyFiles.A</br>
[DDInstallSection_A.HW]
AddReg = A.AddReg</br>
[DDInstallSection_B]
CopyFiles = CopyFiles.B</br>
[DDInstallSection_B.HW]
AddReg = B.AddReg  

</pre></td>

<td></br>各 DDInstall セクションの AddReg セクションを追加して、そのインストールに必要なファイルを追跡します。

</td>
</tr>

<tr>
<td><pre>[A.AddReg]
HKR,, FileName1Path, "%13%\SourceFile1A"
HKR,, FileName2Path, "%13%\SourceFile2A"</br>
[B.AddReg]
HKR,, FileName1Path, "%13%\SourceFile1A"
HKR,, FileName2Path, "%13%\SourceFile2A"

</pre></td>
<td></br>1つのレジストリ値にマップされた複数のソースファイルの場所。 これは、DDInstall または DDInstall. HW セクションからの HKR AddReg がデバイス設定に格納されているために機能します。  このドライバーパッケージと共にインストールされるデバイスは、DDInstall セクションの1つのみを使用するので、HKR AddReg の1つだけが使用され、競合は発生しません。
</td>
</tr>

<tr>
<td><pre>[CopyFiles.A]
SourceFile1A ; HW Version A
SourceFile2A ; HW Version A</br>
[CopyFiles.B]
SourceFile1B ; HW Version B
SourceFile2B ; HW Version B
</pre></td>
<td></br>すべてのファイルが独自の場所にマップされるため、機能エラーや INF が InfVerif に合格することはありません。
</br>
対象のファイルの名前を変更するには、CopyFiles を使用しないでください。

</td>
</tr>
</tbody>
</table>

### <a name="accessing-the-file-location-from-the-driver-pseudo-code"></a>ドライバーからのファイルの場所へのアクセス (擬似コード)

```command
Before (Fixed Filename):
    OpenFile(Path\DesiredFileName1)

After (Dynamic Filename):
    OpenDeviceRegistryKey(Device, &KeyHandle)
    RegistryKeyQueryValue(KeyHandle, FileNamePath1, &SourceFile)
    OpenFile(SourceFile)
```

### <a name="accessing-the-file-location-from-user-mode"></a>ユーザーモードからのファイルの場所へのアクセス

ユーザーモードからターゲットファイルにアクセスするときに、ドライバーが持っているデバイスコンテキストがありません。 この場合は、追加の手順を追加する必要があります。 キーハンドルを開く前に、読み込むファイルを示すレジストリ値を含むデバイスを見つけます。

デバイスリストをフィルター処理してデバイスを検索し、ユーザーモードでレジストリの場所のハンドルを開く方法については、「[ドライバーストアからの実行](https://docs.microsoft.com/windows-hardware/drivers/develop/universal-driver-scenarios#run-from-the-driver-store)」を参照してください。

## <a name="errors-1331---1333"></a>エラー 1331 ~ 1333

エラー 1331-1333 はすべて同じ問題ですが、レジストリ値、サービス内のレジストリ値、およびサービスに関連しています。 エラー1330のドキュメントに記載されている例では、1331-1333 エラーを解決する方法を説明しています。
