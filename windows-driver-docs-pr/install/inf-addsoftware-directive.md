---
title: INF AddSoftware ディレクティブ
description: AddSoftware ディレクティブでは、スタンドアロンのソフトウェアのインストールについて説明します。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8c757b95faf9047b1d06f66f79197d72f8a90b87
ms.sourcegitcommit: 7e0ac000726f8e79d9eb8b9991a2c698f9472507
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2019
ms.locfileid: "65531266"
---
# <a name="inf-addsoftware-directive"></a>INF AddSoftware ディレクティブ

各**AddSoftware**ディレクティブがスタンドアロンのソフトウェアのインストールについて説明します。  INF ファイルでこのディレクティブを使用して、 **SoftwareComponent**クラスをセットアップします。 ソフトウェア コンポーネントの詳細については、次を参照してください。[コンポーネントの INF ファイルを使用して](using-a-component-inf-file.md)します。  Windows 10 バージョン 1703 以降では、このディレクティブはサポートされます。

有効なインストールの種類によって異なります、[ターゲット プラットフォーム](../develop/windows-10-editions-for-universal-drivers.md)します。 たとえば、デスクトップには、インストーラーの MSI と Exe のセットアップがサポートしています。  **注意**:種類 2 がユニバーサル ドライバーでサポートされている、種類 1 がデスクトップ専用です。

ソフトウェア コンポーネントの INF ファイルを指定すると**AddSoftware**、システム キュー ソフトウェアをデバイスのインストール後にインストールします。  または、ソフトウェアをインストールする場合、保証はありません。
参照されているソフトウェアは、インストールに失敗した場合、参照元のソフトウェア コンポーネントが更新されたときにで、システムがもう一度しようとします。

**AddSoftware**内ディレクティブの使用、 [ **INF *DDInstall*します。ソフトウェア**](inf-ddinstall-software-section.md)セクション。

```ini
[DDInstall.Software]
AddSoftware=SoftwareName,[flags],software-install-section
```

## <a name="entries"></a>エントリ

*SoftwareName*

インストールするソフトウェアの名前を指定します。  この名前は、ソフトウェアを一意に識別します。  処理、 **AddSoftware**ディレクティブは、インストールによって同じ名前の前のソフトウェアに対してバージョンを確認します。、 **AddSoftware** 、ドライバー パッケージからディレクティブ。  たとえば、ベンダーの名前を持つ SoftwareName を付けることをお勧めします。`ContosoControlPanel`します。

*flags*

1 つまたは複数の (論理和) フラグを指定します。

**0x00000000**  
**AddSoftware**ディレクティブが 1 回だけ処理されます。

**0x00000001**  
**AddSoftware**ディレクティブを指定するデバイスをコンポーネントごとに 1 回処理**AddSoftware**と同じ一意*SoftwareName*します。

*software-install-section*

ソフトウェアをインストールするための情報を含む INF ライター定義のセクションを参照します。
    
## <a name="remarks"></a>コメント

各 INF ライター作成セクション名は、INF ファイル内で一意である必要があり、セクション名を定義するための一般的な規則に従う必要があります。  これらの規則の詳細については、次を参照してください。 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)します。

**AddSoftware**ディレクティブは名前付き参照する必要があります*ソフトウェアのインストール-セクション*INF ファイルで別の場所。  このような各セクションでは、次の形式があります。

```ini
[software-install-section]

SoftwareType=type-code
[SoftwareBinary=path-to-binary]
[SoftwareArguments=argument[, argument] …]
[SoftwareVersion=w.x.y.z]
[SoftwareID=pfn://x.y.z]
```

>[!NOTE]
>参照してください[ **SoftwareType** ](#software-install-section-softwaretype)セクション エントリと値の制約についてはします。

使用してをインストールしたソフトウェア**AddSoftware**サイレント モードで (またはサイレント モードで) インストールされている必要があります。 つまり、ユーザー インターフェイスでくユーザーに表示されません、インストール中にします。

使用してをインストールしたソフトウェア**AddSoftware**は**いない**仮想ソフトウェア コンポーネントのデバイスまたはその親デバイスをアンインストールする場合にアンインストールされます。 ソフトウェアは、UWP アプリではない場合 (つまり使用している**AddSoftware**値は 1 です)、ユーザーでは、レジストリでトレースを離れることがなくアンインストール簡単にかどうかを確認してください。 次の手順に従います。

* MSI インストーラーを使用している場合のセットアップ、[プログラムの追加/削除](https://msdn.microsoft.com/library/windows/desktop/aa368032)アプリケーションの Windows インストーラー パッケージ内のエントリ。
* カスタム EXE (ローカルのデバイスの設定を補足する) ではなくそのインストール グローバル レジストリ/ファイルの状態を使用している場合は、使用、 [Uninstall レジストリ キー](https://msdn.microsoft.com/library/windows/desktop/aa372105)します。 

## <a name="software-install-section-softwaretype"></a>[ソフトウェアのインストール-セクション]:SoftwareType

`SoftwareType={type-code}`

**SoftwareType**必要なエントリであり、ソフトウェアのインストールの種類を指定します。

値が 1 の関連付けられているソフトウェアが、MSI、EXE またはバイナリであることを示します。  この値が設定されている場合、 **SoftwareBinary**エントリも必要です。  Windows 10 s. 1 の値がサポートされていません  

場合**SoftwareType**を 1 に設定されている**SoftwareBinary**と **%softwareversion**も、必要ですが、 **SoftwareArguments** (フラグを設定**AddSoftware**ディレクティブ) は省略可能です。 

Windows 10 バージョン 1709 以降、2 の値は、関連するソフトウェアを Microsoft Store のリンクを示します。  グラフィカル ユーザー インターフェイスを持たないデバイス固有のソフトウェアのみの値 1 を使用します。  グラフィカル要素を持つデバイスに固有のアプリがある場合は、Microsoft Store での元ドライバーを参照する必要がありますを使用して**SoftwareType** 2。

場合**SoftwareType** 2 に設定されている**SoftwareID**は必須であり、フラグ (で、 **AddSoftware**ディレクティブ) は省略可能です。 場合**SoftwareType** 2 に設定されている**SoftwareBinary**と **%softwareversion**は使用されません。

>[!NOTE]
>種類 2 の AddSoftware ディレクティブを使用して、コンポーネント INF を使用する必要はありません。  ディレクティブは、任意の INF で正常に使用できます。  ただし、型の 1 の AddSoftware ディレクティブは、コンポーネント INF から使用する必要があります。

デバイスに関連付けられていないソフトウェアを配布するのに AddSoftware を使用しないでください。 たとえば、AddSoftware で PC の OEM 固有のユーティリティ プログラムをインストールする必要がありますされません。
代わりに、次のオプションのいずれかを使用し、Windows 10 の OEM イメージにアプリをプレインストールします。

* Win32 アプリをプレインストールするには、監査モードと、アプリのインストールを起動します。 詳細については、次を参照してください。[監査モードの概要](https://docs.microsoft.com/windows-hardware/manufacture/desktop/audit-mode-overview)します。
* Microsoft Store (UWP) アプリをプレインストールするには、次を参照してください[Preinstallable デスクトップ デバイス アプリ。](https://docs.microsoft.com/windows-hardware/customize/preinstall/preinstallable-apps-for-windows-10-desktop)

ユニバーサル Windows プラットフォーム (UWP) アプリとドライバーのペアリングの詳細については、次を参照してください。[ユニバーサル Windows プラットフォーム (UWP) アプリでのドライバーをペアリング](pairing-app-and-driver-versions.md)と[ハードウェア サポート アプリ (HSA)。Steps for Driver Developers (ハードウェア サポート アプリ (HSA): ドライバー開発者向け手順)](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)」をご覧ください。

## <a name="software-install-section-softwarebinary"></a>[ソフトウェアのインストール-セクション]:SoftwareBinary

`SoftwareBinary={filename}`

実行可能ファイルへのパスを指定します。  システムでは、次のようなコマンドラインが生成されます。

`MSI: msiexec /i "<SoftwareBinary>” ALLUSERS=1 /quiet /qn /promptrestart [<SoftwareArguments>]`

`EXE: <SoftwareBinary> [<SoftwareArguments>]`

このエントリを使用する必要がありますして追加した場合、実行可能ファイル、DriverStore に指定する、 [INF CopyFiles ディレクティブ](inf-copyfiles-directive.md)で、 **DestinationDirs** 13 の値。

>[!NOTE]
>参照してください[ **SoftwareType** ](#software-install-section-softwaretype)上の制約については**SoftwareBinary**エントリと値。

## <a name="software-install-section-softwarearguments"></a>[ソフトウェアのインストール-セクション]:SoftwareArguments

`SoftwareArguments={argument1[, argument2[, … argumentN]]}`

コマンドラインに追加する拡張機能に固有の引数を指定します。  システムが生成されたコマンドラインに単に通過するコマンドライン引数を指定できます。  呼ばれる特殊な文字列を指定することもできます。*ランタイム コンテキスト変数*します。  ランタイム コンテキスト変数を指定するときに、システムに変換しますデバイス固有の値が生成されたコマンドラインに追加する前にします。  混在させるし、ランタイム コンテキスト変数とリテラル文字列引数と一致できます。  サポートされているランタイム コンテキスト変数は次のとおりです。

`<<DeviceInstanceID>>`

ソフトウェア コンポーネントのデバイス インスタンス ID を持つ、上記の文字列が置き換えられます。

例:

```ini
    [DDInstall.Software]
    AddSoftware=ContosoControlPanel,,Contoso_ControlPanel_Software

    [Contoso_ControlPanel_Software]
    SoftwareType=1
    SoftwareBinary=ContosoControlPanel.exe
    SoftwareArguments=<<DeviceInstanceID>>
    SoftwareVersion=1.0.0.0
```

次のようなコマンド ラインで上記の例の結果。

`<DriverStorePath>\ContosoControlPanel.exe PCI\VEN_0000&DEV_0001&SUBSYS_00000000&REV_00\0123`

場合 SoftwareArguments には、複数の引数が含まれています。

```ini
    SoftwareArguments=arg1,<<DeviceInstanceID>>,arg2
```

上記の結果:

`<DriverStorePath>\ContosoControlPanel.exe arg1 PCI\VEN_0000&DEV_0001&SUBSYS_00000000&REV_00\0123 arg2`

>[!NOTE]
>参照してください[ **SoftwareType** ](#software-install-section-softwaretype)上の制約については**SoftwareArguments**エントリと値。

## <a name="software-install-section-softwareversion"></a>[ソフトウェアのインストール-セクション]:SoftwareVersion

`SoftwareVersion={w.x.y.z}`

ソフトウェアのバージョンを指定します。  各値は 65535 を超えることはできません。  システムに重複が検出した場合**SoftwareName**、チェック、 **%softwareversion**前に対して **%softwareversion**。  大きい場合は、Windows は、ソフトウェアを実行します。

>[!NOTE]
>参照してください[ **SoftwareType** ](#software-install-section-softwaretype)上の制約については **%softwareversion**エントリと値。

## <a name="software-install-section-softwareid"></a>[ソフトウェアのインストール-セクション]:SoftwareID

`SoftwareID={x.y.z}`

Microsoft Store の識別子と識別子の型を指定します。  現時点では、のみパッケージ ファミリ名 (PFN) をサポートします。  PFN を使用してフォームを使用してユニバーサル Windows プラットフォーム (UWP) アプリを参照する`pfn://<x.y.z>`します。

>[!NOTE]
>参照してください[ **SoftwareType** ](#software-install-section-softwaretype)上の制約については**SoftwareID**エントリと値。

## <a name="see-also"></a>関連項目

* [コンポーネントの INF ファイルを使用して](using-a-component-inf-file.md)します。
* [INF DDInstall.Software セクション](inf-ddinstall-software-section.md)
* [INF AddComponent ディレクティブ](inf-addcomponent-directive.md)
* [ユニバーサル Windows プラットフォーム (UWP) アプリとドライバーのペアリング](pairing-app-and-driver-versions.md)
* [ハードウェア サポート アプリ (HSA):ドライバー開発者向け手順](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)
