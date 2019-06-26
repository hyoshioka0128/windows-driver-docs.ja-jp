---
title: 更新プログラム ドライバー パッケージの作成
description: このトピックでは、更新プログラムのドライバー パッケージの作成に関する情報を提供し、INF ファイルの例の設定と構成を提供します。
ms.assetid: 9018900A-3670-4C78-9094-1DDAB82847DD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe270c24069362210c958e4241e623ef45bfeb89
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353994"
---
# <a name="authoring-an-update-driver-package"></a>更新プログラム ドライバー パッケージの作成


必要がある更新プログラムのペイロード、ESRT で説明されている各ファームウェア リソース バンドルされ、ファームウェアの他のリソースに限定せず、独自のバージョン管理スキームを維持することを許可するための独自のドライバー パッケージの配布の更新プログラムがあることはできません同じ周期で更新されます。

次の例は、ドライバーのサンプル ファームウェア リソースの更新を対象とするパッケージ INF ファイルの定義、{SYSTEM\_ファームウェア} からテーブル 2 のバージョン 1 からバージョン 2 への更新で ESRT 例では、リソース。 参照用に、仮定システムの GUID が割り当てられている\_ファームウェア リソースは 6bd4efb9-23cc-4b4a-ac37-016517413e9a します。

```INF
[Version]
Signature   = "$WINDOWS NT$"
Provider    = %Provider%
Class       = Firmware
ClassGuid   = {f2e7dd72-6468-4e36-b6f1-6488f42c1b52}
DriverVer   = 01/01/2012,2.0.0.0
CatalogFile = catalog.cat
PnpLockdown = 1

[Manufacturer]
%MfgName% = Firmware,NTarm

[Firmware.NTarm]
%FirmwareDesc% = Firmware_Install,UEFI\RES_{6bd4efb9-23cc-4b4a-ac37-016517413e9a}

[Firmware_Install.NT]
CopyFiles = Firmware_CopyFiles

[Firmware_CopyFiles]
firmware.bin

[Firmware_Install.NT.Hw]
AddReg = Firmware_AddReg

[Firmware_AddReg]
HKR,,FirmwareId,,{6bd4efb9-23cc-4b4a-ac37-016517413e9a}
HKR,,FirmwareVersion,%REG_DWORD%,0x00000002
HKR,,FirmwareFilename,,{6bd4efb9-23cc-4b4a-ac37-016517413e9a}\firmware.bin

[SourceDisksNames]
1 = %DiskName%

[SourceDisksFiles]
firmware.bin = 1

[DestinationDirs]
DefaultDestDir = %DIRID_WINDOWS%,Firmware\{6bd4efb9-23cc-4b4a-ac37-016517413e9a}

[Strings]
; localizable
Provider     = "Contoso Ltd."
MfgName      = "Fabrikam Inc."
FirmwareDesc = "Fabrikam System Firmware 2.0"
DiskName     = "Firmware Update"

; non-localizable
DIRID_WINDOWS = 10
REG_DWORD     = 0x00010001
```

次のセクションで、設定のカスタマイズを変更します。

```INF
[Version]
DriverVer --> The date on which this driver package was authored; the Driver version of this driver package. Driver version in this driver package must be greater than the current driver version
CatalogFile --> Name of the catalog file

firmware.bin --> Change all instances of firmware.bin with the name of the firmware image name

[Manufacturer]
%MfgName% = Firmware,NTarm
[Firmware.NTarm] --> Change the architecture. 
For x86, it should be NTx86
For AMD64, it should be NTamd64

[Firmware.NTarm]
%FirmwareDesc% = Firmware_Install,UEFI\RES_{6bd4efb9-23cc-4b4a-ac37-016517413e9a} --> The GUID of the firmware resource

[Firmware_AddReg]
HKR,,FirmwareId,,{6bd4efb9-23cc-4b4a-ac37-016517413e9a} --> The GUID of the firmware resource
HKR,,FirmwareVersion,%REG_DWORD%,0x00000002 --> Version of the firmware for the update
HKR,,FirmwareFilename,,{6bd4efb9-23cc-4b4a-ac37-016517413e9a}\firmware.bin --> The subdirectory named after the GUID of the firmware resource and the firmware image name

[DestinationDirs]
DefaultDestDir = %DIRID_WINDOWS%,Firmware\{6bd4efb9-23cc-4b4a-ac37-016517413e9a} --> The full destination path for the firmware image file based under a subdirectory named after the GUID of the firmware resource within the %SystemRoot%\Firmware directory

[Strings]
; localizable
Modify any strings here [optional]
```

次の表では、さまざまなドライバー パッケージの INF セクションと、上記のサンプル ドライバー パッケージ INF ファイルの定義を参照するようフィールドについて説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>セクション/フィールド</th>
<th>値</th>
<th>Comment</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>[バージョン]</strong></td>
<td></td>
<td>ドライバー パッケージのバージョン管理情報を定義します。</td>
</tr>
<tr class="even">
<td>プロバイダー</td>
<td><p>プロバイダーの % = Contoso inc.</p>
<p>([文字列] セクションではローカライズされます)</p></td>
<td>全体のファームウェア リソースの更新プログラムのドライバー パッケージのプロバイダー/ベンダーを識別します。</td>
</tr>
<tr class="odd">
<td>クラス/ClassGuid</td>
<td><p>ファームウェア/</p>
<p>{f2e7dd72-6468-4e36-b6f1-6488f42c1b52}</p></td>
<td>ドライバー パッケージの日付を指定します。 日、バージョンする必要があります両方反映日付とリソースの実際のファームウェア更新プログラムのバージョンにできるだけ PnP デバイス インストールのシステムが、システムで使用できる最適なドライバー パッケージを正確に選択できることを確認するためにします。</td>
</tr>
<tr class="even">
<td>CatalogFile</td>
<td>catalog.cat</td>
<td>記号ドライバー パッケージの INF ファイルとすべてのファームウェアが関連付けられているリソースにバイナリが更新される、関連するカタログ ファイルを指定します。</td>
</tr>
<tr class="odd">
<td>PnpLockdown</td>
<td>1</td>
<td>関連のないアプリケーションによって、外部から変更されてからインストールされているドライバー ファイルを保護するために、PnP ドライバー ファイルのロックダウン メカニズムを使用できます。 ファームウェアのリソースの更新プログラムは、リソースのイメージ ファイルのファームウェアは PnP システムのコントロールの外部で改ざんがいることはできません確認する、この設定を有効に常にする必要があります。</td>
</tr>
<tr class="even">
<td><strong>[製造元]</strong></td>
<td></td>
<td>すべて個別のドライバーの製造元/ベンダー ファームウェア リソースの更新プログラムの定義を一覧表示します。 各製造元の行を指定して、[&lt;モデル&gt;] セクションし、そのサポートされているターゲット プラットフォームを識別します。</td>
</tr>
<tr class="odd">
<td><p>MfgName %</p></td>
<td><p>Fabrikam Inc.</p>
<p>([文字列] セクションではローカライズされます)</p></td>
<td>リソースのファームウェア更新プログラムの製造元/ベンダーを識別します。 プロバイダーのフィールドと同じ可能性があります。</td>
</tr>
<tr class="even">
<td></td>
<td><p>ファームウェア、</p>
<p>NTarm</p></td>
<td>識別、&lt;モデル&gt;] セクションをターゲットのドライバーのプラットフォームを含むこのドライバー パッケージでサポートされているファームウェアのリソースにデバイスを定義します。 この例で、ドライバーがのみ NT の ARM ベースのプラットフォームの対象、および [&lt;モデル&gt;] セクションでは [Firmware.NTarm]。</td>
</tr>
<tr class="odd">
<td><strong>[Firmware.NTarm]</strong></td>
<td></td>
<td>[&lt;モデル&gt;] セクションの ARM ベースの NT プラットフォーム更新プログラムが定義されているすべてのファームウェア リソースにデバイスを一覧表示します。 各ハードウェア モデルの行を指定して、[&lt;DDInstall&gt;] セクションとその関連するハードウェア ID の一致。</td>
</tr>
<tr class="even">
<td>FirmwareDesc %</td>
<td><p>Fabrikam システム ファームウェア 2.0</p>
<p>([文字列] セクションではローカライズされます)</p></td>
<td>リソースのファームウェアの更新について説明します。 これは、デバイス マネージャーに関連付けられているファームウェア リソース デバイス インスタンスを表示するために使用する主な説明文字列とその他のデバイスに関連する UI。 このため、説明は、ファームウェアのベンダーとバージョンを含めることができます。</td>
</tr>
<tr class="odd">
<td></td>
<td><p>Firmware_Install、</p>
<p>UEFI\RES_ {RESOURCE_GUID}</p></td>
<td>識別、[&lt;DDInstall&gt;] UEFI\RES_ {RESOURCE_GUID} のハードウェア ID で識別されるデバイスのインスタンスを対象とするリソースのファームウェアの更新のインストールを格納しているセクションの手順 RESOURCE_GUID は、更新されているファームウェアのリソースの GUID です。</td>
</tr>
<tr class="even">
<td><p><strong>[Firmware_Install.NT]</strong></p>
<p>CopyFiles = Firmware_CopyFiles</p>
<p><strong>[Firmware_CopyFiles]</strong></p>
<p>...</p></td>
<td></td>
<td>[&lt;DDInstall&gt;] リソースのファームウェア更新プログラムのインストールを含むセクションの手順します。 ファームウェアのリソースの更新プログラムのファームウェアのリソースの更新プログラムの場所にコピーするファームウェア リソース イメージ ファイルのみを定義します。 この例で、[&lt;DDInstall&gt;] セクションでは [Firmware_Install.NT]。</td>
</tr>
<tr class="odd">
<td><em>firmware.bin</em></td>
<td></td>
<td>コピーするファームウェアのリソース更新のイメージ ファイルを指定します。 以下の詳細については、このファイルがコピーされます [DestinationDirs] セクションを参照してください。</td>
</tr>
<tr class="even">
<td><p><strong>[Firmware_Install.NT.Hw]</strong></p>
<p>AddReg Firmware_AddReg を =</p>
<p><strong>[Firmware_AddReg]</strong></p>
<p>...</p></td>
<td></td>
<td>[&lt;DDInstall&gt;します。リソースのファームウェア更新のハードウェアに固有のインストール手順を含む Hw] セクション。 ファームウェア リソースの更新プログラムはターゲット デバイスのインスタンスのデバイスのハードウェア キーの下に設定されているレジストリ値の形式で使用このファームウェア リソース更新の構成情報を定義します。</td>
</tr>
<tr class="odd">
<td>FirmwareId</td>
<td>{RESOURCE_GUID}</td>
<td>ファームウェアのファームウェアのリソースの GUID を更新します。 指定する必要がありますが、同じファームウェア リソース、UEFI\RES_ {RESOURCE_GUID} ハードウェア ID に埋め込まれている GUID であるに注意してくださいここでは、スタンドアロンの値、PnP システムはすべてのハードウェア Id、デバイスの厳密に使用される非透過の文字列として扱いますため/。ドライバーの一致する目的。</td>
</tr>
<tr class="even">
<td>FirmwareVersion</td>
<td>0x00000002</td>
<td>ファームウェアの REG_DWORD 値として指定されたリソース更新のファームウェアのバージョン。</td>
</tr>
<tr class="odd">
<td>FirmwareFilename</td>
<td>{RESOURCE_GUID}&lt;em&gt;firmware.bin</em></td>
<td>ファームウェアのリソース更新プログラムの更新カプセルのイメージ ファイル名のファームウェアのファイル名。 このパスは、{RESOURCE_GUID} は、ファームウェアの特定のリソースの対象となるすべてのファームウェア イメージのファイルを整理するために使用するサブディレクトリを表すように %SystemRoot%\Firmware ディレクトリに対して相対的なは。</td>
</tr>
<tr class="even">
<td><strong>[SourceDisksNames]</strong></td>
<td></td>
<td>すべて個別のドライバー パッケージ ソース ディスクの場所のファームウェア更新リソースの画像ファイルなどの関連するドライバー ファイルが含まれているを一覧表示します。</td>
</tr>
<tr class="odd">
<td>1</td>
<td><p>%DiskName% = Firmware Update</p>
<p>([文字列] セクションではローカライズされます)</p></td>
<td>任意の番号付きのドライバー パッケージのソース ディスク ID とその説明の名前を指定します。 オプションのドライバー パッケージの相対的なサブディレクトリが指定されていない、ドライバー ファイルのファームウェア リソース更新のイメージ ファイルと同様に、このディスクの ID に関連付けられているが、INF ファイルの横にある有効期限が必要です。</td>
</tr>
<tr class="even">
<td><strong>[SourceDisksFiles]</strong></td>
<td></td>
<td>ドライバー パッケージによって参照されるすべてのドライバー ファイルを一覧表示し、[SourceDisksNames] セクションから、ディスク ID にリンクします。</td>
</tr>
<tr class="odd">
<td><em>firmware.bin</em></td>
<td>1</td>
<td>確立、 <em>firmware.bin</em>プライマリ ディスクの ID にリンクさせることにより、ドライバー パッケージの一部として、リソースの更新イメージ ファームウェア ファイル このドライバー ファイルがそのディスクを基準とした有効期限が必要ですので省略可能なファイル固有のサブディレクトリを指定しない ID のサブディレクトリでは、この例では、INF ファイルの横にある右。</td>
</tr>
<tr class="even">
<td><strong>[DestinationDirs]</strong></td>
<td></td>
<td>ドライバー パッケージによって参照されるすべてのドライバー ファイルのターゲットのコピー先のディレクトリを一覧表示します。</td>
</tr>
<tr class="odd">
<td>DefaultDestDir</td>
<td><p>%DIRID_WINDOWS%,Firmware&lt;/p&gt;
<p>{RESOURCE_GUID}</p></td>
<td>後の %systemroot%\firmware、場所 DIRID_WINDOWS (10) が、基本の %systemroot% ディレクトリを表し、{RESOURCE_GUID} は、サブディレクトリを表す名前にするには、このドライバー パッケージによってコピーされたすべてのドライバー ファイルの既定のインストール先ディレクトリを指定します、ファームウェアのリソース GUID。</td>
</tr>
<tr class="even">
<td><strong>[Strings]</strong></td>
<td></td>
<td>すべての間接的な文字列トークン (トークン % の %) のキー/値のマッピングを定義します。ドライバー パッケージ INF ファイル。 文字列のトークンの使用により、特定のロケールを導入することで簡単にローカライズするドライバー パッケージ INF ファイル [文字列&lt;。LanguageID&gt;] セクションでします。 REG_DWORD など、数値定数の値を定義するための文字列のトークン置換を使用することもできます。</td>
</tr>
<tr class="odd">
<td>プロバイダー</td>
<td>"Contoso Ltd."</td>
<td>文字列のトークンのキー/値マッピングの例です。</td>
</tr>
</tbody>
</table>



重要とその他のファームウェア イメージのすべての潜在的な競合を回避するために各ファームウェア リソースの更新画像ファイルのバージョンの一意の名前を使用するファイル、どちらも、独自と他のファームウェアのベンダーから。 たとえば、 *firmware.bin*上記から割り当てる必要がありますを両方のベンダーの名前とバージョンの制約を満たすために次の名前。*Fabrikam システム ファームウェア 2.0.bin*します。

同じ Windows システム イメージに配置したときの OEM/IHV カスタマイズのために使用可能性のある、指定したファームウェアのリソース更新イメージ バリアントが競合しないことを確認するにはお勧め各ファームウェアを個別のリソース更新イメージがあります。%systemroot% 内のサブディレクトリの下でメンテナンス\\ファームウェア ディレクトリ。 このサブディレクトリは、ターゲットのファームウェア リソース GUID いずれかの後に名前必要があります。 次のファームウェア リソース更新イメージ パスが配置の制約を満たすなど: %systemroot%\\ファームウェア\\{6bd4efb9-23cc-4b4a-ac37-016517413e9a}\\Fabrikam システム ファームウェア 2.0.bin します。

## <a name="test-signing-the-firmware-driver-package"></a>ファームウェアのドライバー パッケージに署名をテストします。


ドライバー パッケージ INF ファイルおよびファームウェア ペイロード バイナリは、準備ができたら後、は、カタログ ファイルを生成するためにドライバー パッケージ全体を署名する必要があります。 このカタログ ファイルは、有効性と INF ファイルおよびファームウェアのペイロードのバイナリに安全にファームウェアのリソースの更新を開始する Windows を有効にするには、ドライバー パッケージ内に含まれる信頼性の保証が重要になります。

自己テスト目的でドライバー パッケージに署名する手順は以下に列挙します。 この手順は、テスト目的でのみに注意してください。 、運用環境では、ファームウェアの更新プログラムのドライバー パッケージに署名するため、パートナー センターに送信する必要があります。 運用環境用のファームウェア ドライバー パッケージに署名する手順については、次を参照してください。 [Certifying と更新プログラム パッケージを署名](certifying-and-signing-the-update-package.md)します。

1.  最新の Windows SDK と Windows Driver Kit をインストールします。 これは、makecert、pvk2pfx inf2cat と signtool のツールを次の %] の [でインストールされます\\Program Files (x86)\\Windows キット\\&lt;*バージョン*&gt; \\bin\\x86。
2.  テスト証明書を作成するには、次のコマンドを実行します。

    ```console
    makecert.exe -r -pe -a sha256 -eku 1.3.6.1.5.5.7.3.3 -n CN=Foo -sv fwu.pvk fwu.cer
    pvk2pfx.exe -pvk fwu.pvk -spc fwu.cer -pi <Password entered during makecert prompt> -spc fwu.cer -pfx fwu.pfx
    ```

    詳細については、次を参照してください。 [ **MakeCert**](https://docs.microsoft.com/windows-hardware/drivers/devtest/makecert)します。

3.  カタログ ファイルを作成するには、次のコマンドを実行します。

    ```console
    Inf2Cat.exe /driver:"." /os:8_x64
    ```

    */Driver*引数は、INF の場所を指します。 値を変更、 */os*のファームウェアのドライバー パッケージの対象となる OS に応じて引数。 詳細については、次を参照してください。 [ **Inf2Cat**](https://docs.microsoft.com/windows-hardware/drivers/devtest/inf2cat)します。

    セキュリティ カタログとドライバーの詳細については、次を参照してください。[カタログ ファイルとデジタル署名](https://docs.microsoft.com/windows-hardware/drivers/install/catalog-files)と[PnP ドライバー パッケージのカタログ ファイルを作成する](https://docs.microsoft.com/windows-hardware/drivers/install/creating-a-catalog-file-for-a-pnp-driver-package)します。

4.  カタログ ファイルの署名には、次のコマンドを実行します。

    ```console
    signtool sign /fd sha256 /f fwu.pfx /p <Password entered during makecert prompt> delta.cat
    ```

    詳細については、次を参照してください。 [ **SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)します。

5.  テスト システムでは、テスト証明書をインストールします。
    1.  Fwu.cer ファイルをダブルクリックし、選択、**証明書のインストール**オプション。
    2.  証明書のインストール中に、次のオプションを選択します。
        -   ストアの場所選択**ローカル マシン**します。
        -   証明書ストアを参照して選択**信頼されたルート証明機関**します。

6.  セキュア ブート ファームウェアと BIOS オプションを無効にします。
7.  テストは、OS ローダーは、カタログが実稼働署名された場合でもに、起動中のファームウェア イメージ ファイル (firmware.bin) を読み込むことができます、BCD オプションで署名を有効にします。 管理者特権で次のコマンドを実行します。

    ```console
    bcdedit /set testsigning on
    ```

ドライバー パッケージを署名すると、後にインストールできますを使用して、次のメカニズムのいずれか。

-   **デバイス マネージャー**します。 手動テストでは、デバイス マネージャーは、ファームウェア リソースのデバイスを検索およびファームウェア リソースの更新を開始するには、ドライバーを更新しての使いやすいインターフェイスを提供します。
    1.  接続でデバイスの表示中にデバイスの種類、または「Microsoft UEFI 対応のシステム」のデバイス の下の表示中に「ファームウェア」クラスの下の目的のファームウェア リソース デバイスを見つけます。
    2.  ファームウェアのリソースのデバイスを右クリックし、「Update ドライバー ソフトウェア…」を選択します。オプション。
    3.  見つけてファームウェア リソース デバイス上に新しいファームウェア リソース更新ドライバー パッケージをインストールするには、"コンピューターでドライバー ソフトウェアを参照する オプションを使用します。 この操作は指定したファームウェア リソースの更新プログラムのドライバー パッケージは、すべて既存ファームウェア リソース更新ドライバー パッケージを Windows のドライバー ストアに追加する前にファームウェア リソースのデバイスに既にする可能性がありますよりも新しい実際ことを確認し、インストールを開始しています。
-   **pnputil**します。 自動テストの pnputil コマンド ライン ユーティリティさせるのに管理者特権を持つコマンド プロンプトからファームウェア リソースの更新プログラムのドライバー パッケージを Windows のドライバー ストアにインポートし、適用可能なすべてのファームウェアでデバイスのインストールを開始現在を使用している、古いファームウェア リソース バージョンは、現在インストールされているドライバー パッケージの INF ファイルの DriverVer やサードの不足によって確立されると、リソースにデバイスでは、提供されたドライバー パッケージの INF ファイルを完全パーティします。 たとえば、次のコマンド ラインを使用して追加し、x: をインストールする\\firmware.inf:

    ```console
    pnputil -i -a X:\firmware.inf
    ```

    **注**pnputil ツールは Windows 10 Mobile でサポートされていません。



リソースのファームウェアの更新がファームウェア リソース デバイスに正常にインストールとしてファームウェアの現在のバージョンより新しいバージョンであるファームウェア リソースの更新を提供し、デバイスが完了するには、システムの再起動を待機する、操作を更新します。 この状態のデバイスには、システムにより、デバイスからの起動し、再起動が実行されるまで、安定した状態に復元されているデバイスの問題を維持することで再起動する必要があるが示されます。

## <a name="validating-the-status-of-the-firmware-update"></a>ファームウェア更新の状態を検証しています


ファームウェア ドライバー パッケージが正常にインストールされている、PnP 場合は、更新プログラムを適用するためにシステム再起動を要求します。 再起動後、更新の状態を検証することができます。 更新の状態は、次のレジストリ キーの下で管理されます。HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\FirmwareResources\\{リソース\_GUID}。

リソース\_GUID は (ESRT) から更新されたリソースの GUID です。

"LastAttemptStatus"レジストリ値では、場所、値が 0 の成功を示し、0 以外の値は、失敗を表します、ファームウェアの更新の状態を示します。 このレジストリ キーの値は、OS ローダーを ESRT から LastAttemptStatus の値に基づいて設定 NTSTATUS コードです。 次の表は、NTSTATUS コードに対応するを LastAttemptStatus コードをマップします。

| LastAttemptStatus                        | コード | NTSTATUS                        | コード       |
|------------------------------------------|------|---------------------------------|------------|
| 成功                                  | 0    | ステータス\_成功                 | 0x00000000 |
| エラー:失敗しました。                      | 1    | ステータス\_失敗            | 0xC0000001 |
| エラー:リソース不足            | 2    | ステータス\_不十分\_リソース | 0xC000009A |
| エラー:バージョンが正しくありません。                 | 3    | ステータス\_リビジョン\_が一致しません      | 0xC0000059 |
| エラー:無効なイメージ形式              | 4    | ステータス\_無効な\_イメージ\_形式  | 0xC000007B |
| エラー:認証エラー              | 5    | ステータス\_アクセス\_が拒否されました          | 0xC0000022 |
| エラー:接続されていない AC の電源イベント     | 6    | ステータス\_POWER\_状態\_が無効です   | 0xC00002D3 |
| エラー:不足しているバッテリの電源イベント | 7    | ステータス\_不十分\_電源     | 0xC00002DE |



ファームウェア リソース [デバイス] ノードのハードウェア ID プロパティは、ファームウェアのバージョン、XXX は新しいファームウェアのバージョンの変更を反映もする必要があります。

-   UEFI\\RES\_{リソース\_GUID} &AMP; REV\_XXX

ファームウェアの更新に失敗した場合は、失敗したファームウェアの更新を再試行できます。

-   デバイス マネージャーでは、ファームウェアのノードを展開し、ファームウェア リソース デバイスを右クリックし、クリックして**ドライバー ソフトウェアの更新**します。
-   をクリックして**参照コンピューターでドライバー ソフトウェア**、し、次へ のページの **コンピューター上のデバイス ドライバーの一覧から選択できるように**。
-   以前は、インストールされている同じドライバーを選択し、[ok] をクリックします。

次回の再起動後は、OS ローダーはファームウェアのドライバー パッケージのペイロードを使用した UpdateCapsule() に呼び出します。

## <a name="related-topics"></a>関連トピック

[ESRT テーブルの定義](esrt-table-definition.md)  

[プラグ アンド プレイ デバイス](plug-and-play-device.md)  

[更新プログラムの処理](processing-updates.md)  

[UEFI 環境からデバイス I/O](device-i-o-from-the-uefi-environment.md)  

[シームレスな危機防止と回復](seamless-crisis-prevention-and-recovery.md)  

[ファームウェアの更新状態](firmware-update-status.md)  
