---
title: INF CopyFiles ディレクティブ
description: CopyFiles ディレクティブは、次のいずれかの操作を実行できます。
ms.assetid: 65756b1c-ea61-4bb4-90ac-4d96ceaf9665
keywords:
- INF CopyFiles ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF CopyFiles Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10d704ae9a3031a5771b2c1fcdfdcebdd211d91c
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223266"
---
# <a name="inf-copyfiles-directive"></a>INF CopyFiles ディレクティブ


**CopyFiles**ディレクティブは、次のいずれかを実行できます。

-   ソースメディアから既定のコピー先ディレクトリに1つのファイルがコピーされます。
-   INF 内の1つまたは複数の INF ライターで定義されたセクションを参照します。各セクションは、ソースメディアから宛先にコピーするファイルのリストを指定します。

```inf
[DDInstall] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64]  (Windows XP and later versions of Windows)
[ClassInstall32.ntarm]  (Windows 8 and later versions of Windows)
[ClassInstall32.ntarm64]  (Windows 10 and later versions of Windows)


  
CopyFiles=@filename | file-list-section[, file-list-section]... 
```

**CopyFiles**ディレクティブは、正式な構文ステートメントに示されている任意のセクション内で指定できます。 このディレクティブは、次のいずれかの INF セクション内で指定することもできます。

-   Ddinstall * で INF [**addinterface**](inf-addinterface-directive.md)ディレクティブによって参照される、*インターフェイスの追加セクション*[です。 *インターフェイス](inf-ddinstall-interfaces-section.md)セクション。
-   INF [**InterfaceInstall32**](inf-interfaceinstall32-section.md)セクションで参照される*インストールインターフェイスセクション*

**CopyFiles**ディレクティブによって参照される各名前付きセクションには、次の形式の1つ以上のエントリがあります。

```inf
[file-list-section]
destination-file-name[,[source-file-name][,[unused][,flag]]]
...
```

INF ライターで定義された*ファイルリストセクション*では、任意の数のエントリを個別の行に含めることができます。

各*ファイルリストセクション*には、次の形式のオプションで、関連付けられた<em>ファイルの一覧</em>のセクションを含めることができ**ます。**

```inf
[file-list-section.security]
"security-descriptor-string"
```

## <a name="entries"></a>エントリ


<a href="" id="destination-file-name"></a>*変換先-ファイル名*  
コピー先ファイルの名前を指定します。 *ソースファイル名*が指定されていない場合、この指定はソースファイルの名前でもあります。

<a href="" id="source-file-name"></a>*ソース-ファイル名*  
ソースファイルの名前を指定します。 ファイルのコピー操作に使用するソースファイルとターゲットファイルの名前が同じ場合は、*ソースファイル名*を省略できます。

<a href="" id="unused"></a>*未使用*  
このエントリは、windows 2000 以降のバージョンの Windows ではサポートされなくなりました。

<a href="" id="flag"></a>*誤り*  
これらの省略可能なフラグは、16進表記で表現されるか、またはセクションエントリの10進値として使用して、特定のソースファイルがコピー先にコピーされる方法 (またはそのか) を制御できます。 次のシステム定義フラグの1つまたは複数の (論理和) 値を指定できます。 ただし、これらのフラグの一部は相互に排他的です。

<a href="" id="0x00000001---copyflg-warn-if-skip--"></a>**0x00000001** (COPYFLG_WARN_IF_SKIP)   
ユーザーがファイルをコピーしないことを選択した場合は、警告を送信します。 このフラグと次のフラグは相互に排他的であり、デジタル署名されている INF ファイルには関係ありません。

<a href="" id="0x00000002--copyflg-noskip-"></a>**0x00000002** (COPYFLG_NOSKIP)  
ユーザーがファイルのコピーをスキップすることを許可しません。 このフラグは、[ドライバーパッケージ](driver-packages.md)が署名されている場合に暗黙的に示されます。

<a href="" id="0x00000004--copyflg-noversioncheck-"></a>**0x00000004** (COPYFLG_NOVERSIONCHECK)  
ファイルのバージョンを無視し、インポート先のディレクトリにある既存のファイルを上書きします。 このフラグと次の2つのフラグは相互に排他的です。 このフラグは、デジタル署名された INF ファイルには関係ありません。

<a href="" id="0x00000008--copyflg-force-file-in-use-"></a>**0x00000008** (COPYFLG_FORCE_FILE_IN_USE)  
ファイルの使用時の動作を強制する: 現在開いている場合は、同じ名前の既存のファイルをコピーしません。 代わりに、指定されたソースファイルを一時的な名前でコピーして、次回の再起動時に名前を変更して使用できるようにします。

<a href="" id="0x00000010--copyflg-no-overwrite-"></a>**0x00000010** (COPYFLG_NO_OVERWRITE)  
コピー先のディレクトリにある既存のファイルを、同じ名前のソースファイルに置き換えることはできません。 このフラグを他のフラグと組み合わせることはできません。

<a href="" id="0x00000020--copyflg-no-version-dialog--"></a>**0x00000020** (COPYFLG_NO_VERSION_DIALOG)   
既存のファイルがソースファイルより新しい場合は、コピー先のディレクトリにソースファイルを含むファイルを書き込まないでください。

新しいチェックは、VS_VERSIONINFO ファイルバージョンリソースから抽出されたファイルバージョンを使用して行われます。 詳細については、「https://docs.microsoft.com/windows/desktop/menurc/version-information」を参照してください。 ターゲットファイルが実行可能ファイルまたはリソースイメージでない場合、またはファイルにファイルバージョン情報が含まれていない場合、デバイスのインストールでは、ターゲットファイルが古いことが前提となります。 

<a href="" id="0x00000040---copyflg-overwrite-older-only-"></a>**0x00000040** (COPYFLG_OVERWRITE_OLDER_ONLY)  
コピー先のファイルが新しいバージョンで置き換えられている場合にのみ、コピー先のディレクトリにソースファイルをコピーします。 このフラグは、デジタル署名された INF ファイルには関係ありません。 バージョンチェックでは、上記の COPYFLG_NO_VERSION_DIALOG で説明した手順と同じ手順を使用します。

<a href="" id="0x00000400--copyflg-replaceonly--"></a>**0x00000400** (COPYFLG_REPLACEONLY)   
コピー先のディレクトリにファイルが既に存在する場合にのみ、コピー先のディレクトリにソースファイルをコピーします。

<a href="" id="0x00000800--copyflg-nodecomp--"></a>**0x00000800** (COPYFLG_NODECOMP)   
(Windows 7 以降)ソースファイルが圧縮されている場合は、圧縮を解除せずにコピー先ディレクトリにソースファイルをコピーします。

<a href="" id="0x00001000--copyflg-replace-boot-file-"></a>**0x00001000** (COPYFLG_REPLACE_BOOT_FILE)  
このファイルは、システムローダーによって要求されます。 システムの再起動を求めるメッセージがユーザーに表示されます。

<a href="" id="0x00002000--copyflg-noprune-"></a>**0x00002000** (COPYFLG_NOPRUNE)  
最適化の結果として、この操作を削除しないでください。

たとえば、ファイルが既に存在しているために、ファイルのコピー操作が不要であると判断した場合があります。 ただし、INF のライターは、操作が必要であることを認識し、その最適化をオーバーライドしてファイル操作を実行するように Windows に指示します。

このフラグを使用して、ファイルが INF [**Delfiles**](inf-delfiles-directive.md)ディレクティブまたは inf [**RenFiles**](inf-renfiles-directive.md)ディレクティブでも指定されている場合に、ファイルがコピーされるようにすることができます。

<a href="" id="0x00004000--copyflg-in-use-rename-"></a>**0x00004000** (COPYFLG_IN_USE_RENAME)  
コピー先ファイルが使用されているためにソースファイルをコピーできない場合は、コピー先ファイルの名前を変更し、ソースファイルをコピー先ファイルにコピーして、名前を変更したファイルを削除します。 コピー先ファイルの名前を変更できない場合は、次回のシステム再起動時にコピー操作を完了します。 名前を変更したコピー先ファイルを削除できない場合は、次のシステムの再起動時に、名前を変更したコピー先ファイルを削除します。

<a href="" id="security-descriptor-string"></a>*セキュリティ記述子-文字列*  
名前付き*ファイルリストセクション*によってコピーされるすべてのファイルに適用されるセキュリティ記述子を指定します。 *セキュリティ記述子文字列*は、DACL (**D:**) セキュリティコンポーネントを示すトークンを含む文字列です。

セキュリティ記述子の文字列の詳細については、「[セキュリティ記述子定義言語 (Windows)](https://docs.microsoft.com/windows/desktop/SecAuthZ/security-descriptor-definition-language)」を参照してください。 セキュリティ記述子文字列の形式の詳細については、「セキュリティ記述子定義言語 (Windows)」を参照してください。

<em>ファイルリスト-セクション</em>**. security**セクションが指定されていない場合、ファイルは、ファイルのコピー先となるディレクトリのセキュリティ特性を継承します。

<em>ファイルリスト-section</em>**. security**セクションが指定されている場合、デバイスとシステムサービスパックのインストールとアップグレードが発生するように、次の ACE が含まれている必要があります。

-   (A;;GA、;、SY) −ローカルシステムへのすべてのアクセスを許可します。
-   (A;;GA、;、BA: 組み込みの管理者へのすべてのアクセスを許可します。

権限*のないユーザー*に書き込みアクセス権を付与する ACE 文字列を指定しないでください。

セキュリティ記述子を指定する方法の詳細については、「セキュリティ[で保護されたデバイスのインストールの作成](creating-secure-device-installations.md)」を参照してください。

<a name="remarks"></a>解説
-------

ファイルに INF **CopyFiles**ディレクティブが含まれている場合にのみ、ドライバーのインストールの一部として[ドライバーパッケージ](driver-packages.md)がコピー先の場所にコピーされます。 ファイルをコピーすると、オペレーティングシステムは必要に応じて自動的に一時ファイル名を生成し、次にオペレーティングシステムが起動されたときに、コピーされたソースファイルの名前を変更します。

また、inf ファイルライターは、INF [**Sourcedisksnames**](inf-sourcedisksnames-section.md)セクションと Inf [**Sourcedisksnames**](inf-sourcedisksfiles-section.md)セクションを使用して、ソースメディアからコピーされるファイルのパス仕様を指定する必要があります。これにより、ソースメディア内の inf ファイルに対して相対的に各ソースファイルのパスが明示的に指定されます。

コピー操作の送信先は、 [**INF DestinationDirs セクション**](inf-destinationdirs-section.md)によって制御されます。 このセクションでは、次のように、すべてのファイルコピー操作の対象を制御します。

- **CopyFiles**ディレクティブによって参照される名前付きセクションに、同じ INF の[**destinationdirs**](inf-destinationdirs-section.md)セクション内に対応するエントリがある場合、そのエントリは、指定されたセクションに示されているすべてのファイルのコピー先となるターゲットディレクトリを明示的に指定します。 名前付きセクションが**destinationdirs**セクションに表示されていない場合、WINDOWS は INF ファイルの**Destinationdirs**セクションの**DefaultDestDir**エントリを使用します。
- **CopyFiles**ディレクティブで**@** <em>filename</em>構文を使用する場合、Windows は INF ファイルの**destinationdirs**セクションの**DefaultDestDir**エントリを使用します。

INF の**CopyFiles**ディレクティブには、次の点が適用されます。

- すべての*ファイルリストセクション*名は inf ファイルに対して一意である必要がありますが、同じ inf ファイル内の他の場所では、 **CopyFiles**、 [**Delfiles**](inf-delfiles-directive.md)、または[**RenFiles**](inf-renfiles-directive.md)ディレクティブで参照できます。 セクション名は、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」で説明されている一般的な規則に従う必要があります。
- ファイル**@**<em>名または</em>*ファイルリストセクション*のエントリに指定されたファイル名は、ソースメディア上のファイルの正確な名前である必要があります。 %*Strkey*% トークンを使用してファイル名を指定することはできません。 %*Strkey*% トークンの詳細については、「 [**INF Strings」セクション**](inf-strings-section.md)を参照してください。
- **CopyFiles**ディレクティブでは、システム定義のプラットフォーム拡張機能 (**. nt**、 **ntx86**、 **ntia64**、または**ntamd64**) を使用した*ファイルリストセクション*名の装飾はサポートされていません。
- **CopyFiles**ディレクティブを使用して INF ファイルをコピーしないでください。 詳細については、「 [INF ファイルのコピー](copying-inf-files.md)」を参照してください。

Windows Vista 以降では、次の点が INF の**CopyFiles**ディレクティブにも適用されます。

-   DIFx ツールによってドライバー[ストア](driver-store.md)にドライバーパッケージがプレインストールされると、ファイルに対応する INF **CopyFiles**ディレクティブがある場合にのみ、ドライバーパッケージソースからドライバーストアにファイルがコピーされます。
-   Windows のアップグレードの一環として、ファイルに INF **CopyFiles**ディレクティブがある場合にのみ、ドライバーの移行の一部としてドライバーパッケージファイルがドライバー[ストア](driver-store.md)にコピーされます。

<a name="examples"></a>例
--------

この例では、 [**Sourcedisksnames**](inf-sourcedisksnames-section.md)、 [**sourcedisksnames**](inf-sourcedisksfiles-section.md)、および[**destinationdirs**](inf-destinationdirs-section.md)の各セクションで、単純なデバイスドライバーの INF を処理するときに発生するコピーファイル (およびファイルの削除) 操作のパスを指定する方法を示します。 (同じ INF は、前の[**バージョン**](inf-version-section.md)、 **sourcedisksnames**、および**sourcedisksnames**セクションの例としても使用されていました)。

```inf
[SourceDisksNames]
1 = %Floppy_Description%,,,\WinNT


[SourceDisksFiles.x86]
aha154x.sys = 2,\x86 ; on distribution disk 2, in subdir \WinNT\x86

[DestinationDirs]
DefaultDestDir = 12  ; DIRID_DRIVERS 
                     ; == \System32\Drivers on Windows platforms
; ... Manufacturer and Models sections omitted here


DelFiles= AHA154X.DelFiles
 ; defines a delete-files section not shown here
; ... some other directives and sections omitted here

[AHA154X.NTx86]
CopyFiles=@AHA154x.SYS 
; ... some other directives and sections omitted here
; ...
```

この例では、 **CopyFiles** [ *ddinstall * で CopyFiles ディレクティブを使用する方法を示します。](inf-ddinstall-coinstallers-section.md)システムデバイスタイプ固有のクラスインストーラーの inf 処理を補完する2つのデバイス固有の共同インストーラーを提供するデバイスドライバーの inf の CoInstallers セクション。

```inf
[DestinationDirs]
XxDev_Coinstallers_CopyFiles = 11  ; DIRID_SYSTEM
; ... other file-list entries and DefaultDestDirs omitted here

; ... Manufacturer, Models, and DDInstall sections omitted here

[XxDev_Install.CoInstallers] 
CopyFiles=XxDev_Coinstallers_CopyFiles
; ... AddReg omitted here

[XxDev_Coinstallers_CopyFiles]
XxPreInst.dll   ; dev-specific co-installer run before class installer
XxPostInst.dll  ; run after class installer (post processing)
```

前の例で示したように、新しいデバイス固有の共同インストーラーの名前は、プロバイダーの名前 (ここでは*Xx*と表示されます) と、そのような各共同インストーラー DLL ( *Preinst.exe*と*postinst*として示されています) を使用して作成できます。

INF **CopyFiles**ディレクティブの使用方法のその他の例については、Windows driver KIT (WDK) の*src*ディレクトリに含まれているデバイスドライバーのサンプルの inf ファイルを参照してください。

## <a name="see-also"></a>関連項目


[**AddInterface**](inf-addinterface-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。CoInstallers**](inf-ddinstall-coinstallers-section.md)

[***DDInstall *。インターフェイス**](inf-ddinstall-interfaces-section.md)

[**DelFiles**](inf-delfiles-directive.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**RenFiles**](inf-renfiles-directive.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**文字列**](inf-strings-section.md)

[**バージョン**](inf-version-section.md)

 

 






