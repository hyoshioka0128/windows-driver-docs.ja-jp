---
title: InfVerif エラー 1330
description: InfVerif (InfVerif.exe) は、ドライバーの INF ファイルをテストするのに使用できるツールです。 INF 構文の問題の報告、だけでなく、ツールは、INF ファイルがユニバーサルを報告します。
ms.assetid: 6F565E1C-C6FC-4637-B476-FE4E4672CCC3
ms.date: 03/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: c55513476815ed35ab8931318b7491fc3a7c8b93
ms.sourcegitcommit: 56599ec634b3a731f2d13dff686be3b7b95390e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2019
ms.locfileid: "58419570"
---
# <a name="infverif-error-1330---1333"></a>InfVerif エラー 1330 1333

InfVerif エラー 1330 では、1 つのコピー先ファイルが複数のソース ファイルによって上書きされます機能のエラーを防ぐのに役立ちます。 例:

```command
[CopyFiles.A]
DesiredFileName1,SourceFile1A ; Used by DDInstallSection A

[CopyFiles.B]
DesiredFileName1,SourceFile1B ; Used by DDInstallSection B
```

ときに複数[DDInstall セクション](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)さまざまなソース ファイルを使用して 1 つの宛先ファイルをコピー、 [CopyFiles](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)ディレクティブ、これら**CopyFiles**が競合する場合、**DDInstall セクション**すべて同じシステムで処理を取得します。 この例では、かどうか 2 つの異なるデバイスを使用している同じドライバーが別のインストールのセクションでは、またはオフラインでのドライバーの一部のイメージングと展開シナリオでです。 複数のソース ファイルをさまざまなので、 **DDInstall セクション**同じの正確な 1 つの宛先ファイルのさまざまな異なるソース ファイルにコピー **DDInstall のセクションでは**上書き他の最後のファイルがコピーされるように配置先となる、期待される結果ができない可能性があります。

## <a name="cases"></a>場合

このドキュメントでは、古い構文を次の場合、機能のエラーを削除するメソッドを更新する方法に関するガイダンスを提供します。 すべての場合は、各 INF に固有の他の理由が存在する可能性がありますに、以下に示します。

* 異なる**DDInstall セクション**1 つのサービスのバイナリのサービス名の変更

* 異なる**DDInstall セクション**ドライバーまたはユーザー モード アプリケーションがアクセス先ファイルの場所にコピーを取得するソース ファイルの名前を変更

### <a name="different-ddinstall-sections-rename-a-service-binary-for-one-service"></a>異なる**DDInstall セクション**1 つのサービスのバイナリのサービス名の変更

次のコードは、別の方法の例**DDInstall セクション**1 つのサービスのバイナリのサービスの名前を変更します。

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

このコードを更新するには、異なるバイナリのさまざまなサービス名を作成します。

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

### <a name="different-ddinstall-sections-rename-a-source-file-to-get-copied-over-to-a-destination-file-location-accessed-by-the-driver-or-a-user-mode-application"></a>異なる**DDInstall セクション**ドライバーまたはユーザー モード アプリケーションがアクセス先ファイルの場所にコピーを取得するソース ファイルの名前を変更

この場合、ドライバーは、動的ファイルの場所として使用されている固定ファイルの場所にアクセスします。 1 つの動的変数の複数のソース ファイルを追跡するには、使用することができます、 [AddReg](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)実行時に取得できるパスを格納する HKR エントリ。 これが機能**AddReg**デバイスを基準とした HKR エントリが格納されます。

**AddReg** HKR エントリを選択するソース ファイルをコピーする 1 つの宛先ファイルではなく、ソース ファイルのファイルの場所を指定します。

```command
[A.AddReg]
HKR,, FileName1Path, "%13%\SourceFile1A"

[B.AddReg]
HKR,, FileName1Path, "%13%\SourceFile1B"
```

固定ファイルの場所をアクセスではなく、対象のファイルの場所は、デバイス上の設定から取得できます。 ターゲット ファイルの場所は、INF によってレジストリ値に格納されているし、ドライバーの API 呼び出しを使用して取得します。

によって、INF 値をプロビジョニングするを使用して、 [INF AddReg ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)HKR を使用して*reg ルート*内のエントリ、*追加レジストリ セクション*から参照されている、 [INF DDInstall セクション](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)または[INF DDInstall.HW セクション](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)します。

レジストリ値は、1 つの宛先ファイルの場所ではなく、ターゲット ファイルの追跡維持、ため、ドライバーは、それらのファイルを異なる方法でアクセスする必要があります。 ターゲット ファイルにアクセスするには、ドライバーは、レジストリ値を開き、そのソース ファイルの場所を返すには、次の Api のいずれかを呼び出すようになりましたが必要。

#### <a name="wdm"></a>WDM

* [**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceregistrykey)

#### <a name="wdf"></a>WDF

* [**WdfDeviceOpenRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceopenregistrykey)

* [**WdfFdoInitOpenRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitopenregistrykey)

#### <a name="other-user-mode-code"></a>その他のユーザー モード コード

* [**CM_Open_DevNode_Key**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_open_devnode_key)

> [!NOTE]
> この例では、INF ペイロード ファイルのコピー先では、ソリューションは影響しません。  ただし、ベスト プラクティスを使用する例では、使用[DIRID](https://docs.microsoft.com/windows-hardware/drivers/install/using-dirids) 13 ことにより、高速化するためが少ないファイルのコピーをインストールします。  参照してください"[を使用して DIRIDs](https://docs.microsoft.com/windows-hardware/drivers/install/using-dirids)「と」[ドライバー ストアから実行](https://docs.microsoft.com/windows-hardware/drivers/develop/universal-driver-scenarios#run-from-the-driver-store)"詳細についてはします。

次のコード例では、古い構文を使用する、INF を更新する方法を示します。

### <a name="details-for-different-source-files-mapped-to-one-destination-file"></a>1 つのコピー先ファイルにマップされている別のソース ファイルの詳細

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
<td></br>ファイルを手動で移動する場所を選択します。</td>
</tr>
<tr>
<td><pre>[CopyFiles.A]
DesiredFileName1,SourceFile1A ; HW Version A
DesiredFileName2,SourceFile2A ; HW Version A</br>
[CopyFiles.B]
DesiredFileName1,SourceFile1B ; HW Version B
DesiredFileName2,SourceFile2B ; HW Version B
</pre></td>
<td></br><u>ファイルのコピーのテクニック</u>:ファイルの名前を変更して DDInstall セクションがインストールされているため、ドライバーにリンク先ファイルのパスにコピーを取得するソース ファイルを取得します。

DDInstall のすべてのセクションのすべてのファイルをインストールする前にコピーする場合は、これは機能しません。
</td>
</tr>
</tbody>
</table>

### <a name="details-for-udating-by-using-addreg-hkr-entries"></a>Udating AddReg HKR エントリを使用しての詳細

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
<td></br>ベスト プラクティスは、ストア ディレクトリ (Dirid 13) のままに、ドライバー内のすべて</td>
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

<td></br>インストールに必要なファイルを追跡するには、各 DDInstall Section.HW AddReg セクションを追加します。

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
<td></br>複数のソース ファイル場所が 1 つのレジストリ値にマップします。 HKR AddReg DDInstall または DDInstall.HW セクションから、デバイスの設定に格納されているため、これは機能します。  このドライバー パッケージにデバイスをインストールすると、ときにのみ使用する DDInstall セクションでは、のいずれかの HKR AddReg の 1 つだけが使用され、競合されませんので。
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
<td></br>すべてのファイル、独自の場所に対応されないように機能のエラーと INF パス InfVerif。
</br>
DestinationDirs に付属している Dirid 13 ファイルの名前を変更するのに CopyFiles を使用しないでください。

</td>
</tr>
</tbody>
</table>

### <a name="accessing-the-file-location-from-the-driver-pseudo-code"></a>ドライバー (擬似コード) から、ファイルの場所へのアクセス

```command
Before (Fixed Filename):
    OpenFile(Path\DesiredFileName1)

After (Dynamic Filename):
    OpenDeviceRegistryKey(Device, &KeyHandle)
    RegistryKeyQueryValue(KeyHandle, FileNamePath1, &SourceFile)
    OpenFile(SourceFile)
```

### <a name="accessing-the-file-location-from-user-mode"></a>ユーザー モードから、ファイルの場所へのアクセス

ターゲット ファイルからユーザー モードにアクセスするときは、デバイス コンテキスト、ドライバーがあることはできません。 ここでは、追加のステップを追加する必要があります。 キー ハンドルを開く前にファイルの読み込みに何を示すレジストリ値を格納しているデバイスを検索します。

これは、[リンク](https://docs.microsoft.com/en-us/windows-hardware/drivers/develop/universal-driver-scenarios#run-from-the-driver-store)をデバイスを検索して Dirid 13 を使用して、ベスト プラクティスについては、ユーザー モードで、レジストリの場所を識別するハンドルを開くデバイス一覧をフィルター処理する方法を示します。

## <a name="errors-1331---1333"></a>エラー 1331 1333

エラー 1331 1333 はすべて、同じ問題がレジストリに関連するレジストリ値をサービス内で値しそれぞれのサービスします。 エラー 1330 1331 1333 のエラーを解決する方法はカバーのドキュメントの例です。
