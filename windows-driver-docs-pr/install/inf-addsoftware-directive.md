---
title: INF AddSoftware ディレクティブ
description: AddSoftware ディレクティブは、スタンドアロンソフトウェアのインストールについて説明します。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 26de0aa0f35add9159a49f457fb76c9786b7dd56
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223276"
---
# <a name="inf-addsoftware-directive"></a>INF AddSoftware ディレクティブ

各**addsoftware**ディレクティブは、スタンドアロンソフトウェアのインストールについて説明します。  このディレクティブは、**ソフトウェアコンポーネント**セットアップクラスの INF ファイルで使用します。 ソフトウェアコンポーネントの詳細については、「[コンポーネント INF ファイルの使用](using-a-component-inf-file.md)」を参照してください。  このディレクティブは、Windows 10 バージョン1703以降でサポートされています。

有効なインストールの種類は、[ターゲットプラットフォーム](../develop/windows-10-editions-for-universal-drivers.md)によって異なります。 たとえば、デスクトップでは MSI インストーラーとセットアップ Exe がサポートされています。  **注**: 種類2はユニバーサルドライバーでサポートされています。種類1はデスクトップのみです。

ソフトウェアコンポーネントの INF ファイルで**Addsoftware**を指定すると、デバイスのインストール後にインストールされるソフトウェアがシステムによってキューに追加されます。  ソフトウェアがインストールされるかどうかは保証されません。
参照されているソフトウェアのインストールに失敗した場合、参照元のソフトウェアコンポーネントが更新されると、システムによって再試行されます。

**Addsoftware**ディレクティブは、 [**INF *ddinstall*内で使用されます。ソフトウェア**](inf-ddinstall-software-section.md)セクション。

```inf
[DDInstall.Software]
AddSoftware=SoftwareName,[flags],software-install-section
```

## <a name="entries"></a>エントリ

*SoftwareName*

インストールするソフトウェアの名前を指定します。  この名前は、ソフトウェアを一意に識別します。  **Addsoftware**ディレクティブの処理では、任意のドライバーパッケージの**addsoftware**ディレクティブによって、同じ名前でインストールされた以前のソフトウェアに対してバージョンがチェックされます。  SoftwareName の前に、ベンダー名を付けることをお`ContosoControlPanel`勧めします。たとえば、のようにします。

*flags*

1つまたは複数の (論理和) フラグを指定します。

**0x00000000**  
**Addsoftware**ディレクティブは1回だけ処理されます。

**0x00000001**  
**Addsoftware**ディレクティブは、同じ一意の*SoftwareName*を持つ**addsoftware**を指定するコンポーネントデバイスごとに1回処理されます。

*ソフトウェア-インストール-セクション*

ソフトウェアのインストールに関する情報を含む INF ライターで定義されたセクションを参照します。
    
## <a name="remarks"></a>解説

各 INF ライターで作成されたセクション名は、INF ファイル内で一意である必要があります。また、セクション名を定義するための一般的な規則に従う必要があります。  これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

**Addsoftware**ディレクティブは、INF ファイル内の別の場所にある*software-install セクション*を参照する必要があります。  各セクションには、次の形式があります。

```inf
[software-install-section]

SoftwareType=type-code
[SoftwareBinary=path-to-binary]
[SoftwareArguments=argument[, argument] …]
[SoftwareVersion=w.x.y.z]
[SoftwareID=pfn://x.y.z]
```

>[!NOTE]
>セクションのエントリと値に対する制約の詳細については、「[**ソフトウェアの種類**](#software-install-section-softwaretype)」を参照してください。

**Addsoftware**を使用してインストールされたソフトウェアは、サイレント (または静か) でインストールする必要があります。 つまり、インストール時にユーザーに表示されるユーザーインターフェイスを使用することはできません。

仮想ソフトウェアコンポーネントデバイスまたはその親デバイスがアンインストールされている場合、 **Addsoftware**を使用してインストールされたソフトウェアはアンインストールされ**ません**。 ソフトウェアが UWP アプリではない場合 (つまり、値が1の**Addsoftware**を使用している場合) は、レジストリにトレースを残すことなく、ユーザーが簡単にアンインストールできることを確認してください。 そのためには次を行います。

* MSI インストーラーを使用している場合は、アプリケーションの Windows インストーラーパッケージに [[プログラムの追加と削除](https://docs.microsoft.com/windows/desktop/Msi/configuring-add-remove-programs-with-windows-installer)] エントリを設定します。
* ローカルのデバイス設定を補完するのではなく、グローバルレジストリ/ファイルの状態をインストールするカスタム EXE を使用している場合は、 [Uninstall レジストリキー](https://docs.microsoft.com/windows/desktop/Msi/uninstall-registry-key)を使用します。 

## <a name="software-install-section-softwaretype"></a>[software-install-section]: ソフトウェアの種類

`SoftwareType={type-code}`

Software **type**ソフトウェアのインストールの種類を指定します。必須のエントリです。

値1は、関連付けられているソフトウェアが MSI または EXE バイナリであることを示します。  この値が設定されている場合は、[**ソフトウェアバイナリ**] エントリも必要です。  Windows 10 S では、値1はサポートされていません。  

[**ソフトウェアの種類**] が1に設定されている場合は、**ソフトウェアのバイナリ**とソフトウェアの**バージョン**も必要ですが、ソフトウェアの**引数**とフラグ ( **addsoftware**ディレクティブ内) は省略可能です。 

Windows 10 バージョン1709以降、値2は、関連付けられているソフトウェアが Microsoft Store リンクであることを示します。  グラフィカルユーザーインターフェイスを持たないデバイス固有のソフトウェアに対してのみ、値1を使用します。  グラフィック要素を持つデバイス固有のアプリがある場合は、Microsoft Store から取得され、ドライバーは**ソフトウェアの種類**2 を使用してそれを参照する必要があります。

[**ソフトウェアの種類**] が2に設定されている場合、[ソフトウェア**id** ] は必須であり、フラグ ( **addsoftware**ディレクティブ内) は省略可能です。 [**ソフトウェアの種類**] が2に設定されている場合、**ソフトウェアのバイナリ**と**ソフトウェアのバージョン**は使用されません。

>[!NOTE]
>AddSoftware ディレクティブの Type 2 を使用する場合、コンポーネントの INF を利用する必要はありません。  ディレクティブは、どの INF でも正常に使用できます。  ただし、型1の AddSoftware ディレクティブは、コンポーネント INF から使用する必要があります。

デバイスに関連付けられていないソフトウェアを配布する場合は、AddSoftware を使用しないでください。 たとえば、OEM 固有の PC ユーティリティプログラムは、AddSoftware と共にインストールしないでください。
代わりに、次のいずれかのオプションを使用して、Windows 10 の OEM イメージにアプリをプレインストールします。

* Win32 アプリをプレインストールするには、監査モードで起動し、アプリをインストールします。 詳細については、「[監査モードの概要](https://docs.microsoft.com/windows-hardware/manufacture/desktop/audit-mode-overview)」を参照してください。
* Microsoft Store (UWP) アプリをプレインストールするには、「[デスクトップデバイスのインストール前のアプリ](https://docs.microsoft.com/windows-hardware/customize/preinstall/preinstallable-apps-for-windows-10-desktop)」を参照してください。

ドライバーとユニバーサル Windows プラットフォーム (UWP) アプリのペアリングの詳細については、「[ドライバーとユニバーサル Windows プラットフォーム (uwp) アプリ](pairing-app-and-driver-versions.md)および[ハードウェアサポートアプリ (HSA): ドライバー開発者向けの手順](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)」を参照してください。

## <a name="software-install-section-softwarebinary"></a>[software-install-section]: ソフトウェアバイナリ

`SoftwareBinary={filename}`

実行可能ファイルへのパスを指定します。  システムは、次のようなコマンドラインを生成します。

`MSI: msiexec /i "<SoftwareBinary>” ALLUSERS=1 /quiet /qn /promptrestart [<SoftwareArguments>]`

`EXE: <SoftwareBinary> [<SoftwareArguments>]`

このエントリを使用する場合、実行可能ファイルを DriverStore に追加する必要があります。これを行うには、 **Destinationdirs**値13を指定して[INF CopyFiles ディレクティブ](inf-copyfiles-directive.md)を指定します。

>[!NOTE]
>**ソフトウェアのバイナリ**エントリと値に対する制約の詳細については、「[**ソフトウェアの種類**](#software-install-section-softwaretype)」を参照してください。

## <a name="software-install-section-softwarearguments"></a>[software-install-section]: ソフトウェアの引数

`SoftwareArguments={argument1[, argument2[, … argumentN]]}`

コマンドラインに追加する拡張機能固有の引数を指定します。  生成されたコマンドラインにシステムが単に渡すコマンドライン引数を指定できます。  *ランタイムコンテキスト変数*と呼ばれる特殊な文字列を指定することもできます。  ランタイムコンテキスト変数を指定すると、生成されたコマンドラインに追加される前に、システムによってその変数がデバイス固有の値に変換されます。  リテラル文字列の引数とランタイムコンテキストの変数を組み合わせることができます。  サポートされているランタイムコンテキスト変数は次のとおりです。

`<<DeviceInstanceID>>`

上記の文字列は、ソフトウェアコンポーネントのデバイスインスタンス ID で置き換えられます。

次に例を示します。

```inf
    [DDInstall.Software]
    AddSoftware=ContosoControlPanel,,Contoso_ControlPanel_Software

    [Contoso_ControlPanel_Software]
    SoftwareType=1
    SoftwareBinary=ContosoControlPanel.exe
    SoftwareArguments=<<DeviceInstanceID>>
    SoftwareVersion=1.0.0.0
```

上記の例では、次のようなコマンドラインが生成されます。

`<DriverStorePath>\ContosoControlPanel.exe PCI\VEN_0000&DEV_0001&SUBSYS_00000000&REV_00\0123`

パラメーターに複数の引数が含まれている場合:

```inf
    SoftwareArguments=arg1,<<DeviceInstanceID>>,arg2
```

上記の結果は次のようになります。

`<DriverStorePath>\ContosoControlPanel.exe arg1 PCI\VEN_0000&DEV_0001&SUBSYS_00000000&REV_00\0123 arg2`

>[!NOTE]
>**ソフトウェアの引数**のエントリと値に対する制約の詳細については、「[**ソフトウェアの種類**](#software-install-section-softwaretype)」を参照してください。

## <a name="software-install-section-softwareversion"></a>[ソフトウェア-インストール-セクション]: ソフトウェアのバージョン

`SoftwareVersion={w.x.y.z}`

ソフトウェアのバージョンを指定します。  各値は65535を超えることはできません。  システムが重複する**SoftwareName**を検出すると、以前の**バージョンのソフトウェア**に対して**ソフトウェアのバージョン**がチェックされます。  それより大きい場合は、Windows によってソフトウェアが実行されます。

>[!NOTE]
>**ソフトウェアのバージョン**のエントリと値に対する制約の詳細については、「[**ソフトウェアの種類**](#software-install-section-softwaretype)」を参照してください。

## <a name="software-install-section-softwareid"></a>[software-install-section]: ソフトウェア Id

`SoftwareID={x.y.z}`

Microsoft Store 識別子と識別子の種類を指定します。  現時点では、パッケージファミリ名 (PFN) のみがサポートされています。  PFN を使用して、フォーム`pfn://<x.y.z>`を使用してユニバーサル WINDOWS プラットフォーム (UWP) アプリを参照します。

>[!NOTE]
>**ソフトウェア id**のエントリと値に対する制約の詳細については、「[**ソフトウェアの種類**](#software-install-section-softwaretype)」を参照してください。

## <a name="see-also"></a>参照

* [コンポーネントの INF ファイルを使用](using-a-component-inf-file.md)します。
* [INF DDInstall.Software セクション](inf-ddinstall-software-section.md)
* [INF AddComponent ディレクティブ](inf-addcomponent-directive.md)
* [ドライバーとユニバーサル Windows プラットフォーム (UWP) アプリとのペアリング](pairing-app-and-driver-versions.md)
* [ハードウェアサポートアプリ (HSA): ドライバー開発者向けの手順](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)
