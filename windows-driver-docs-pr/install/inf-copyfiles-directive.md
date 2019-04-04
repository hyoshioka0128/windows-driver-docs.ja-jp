---
title: INF CopyFiles ディレクティブ
description: CopyFiles ディレクティブは、次のいずれかで行うことができます。
ms.assetid: 65756b1c-ea61-4bb4-90ac-4d96ceaf9665
keywords:
- INF CopyFiles ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF CopyFiles Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d5609c42f721688632bb6c70405057993588fa3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578138"
---
# <a name="inf-copyfiles-directive"></a>INF CopyFiles ディレクティブ


A **CopyFiles**ディレクティブは、次のいずれかで行うことができます。

-   既定のインストール先ディレクトリにソース メディアからコピーされる 1 つのファイルが発生します。
-   ソース メディアからコピー先にコピーするファイルの一覧を指定する各 INF で 1 つまたは複数のライター定義 INF セクションを参照します。

```ini
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

A **CopyFiles**いずれかのセクションでは、正式な構文のステートメントに示すように、ディレクティブを指定することができます。 このディレクティブは、INF セクションでは、次の中でも指定できます。

-   *追加インターフェイス セクション*、INF によって参照される[ **AddInterface** ](inf-addinterface-directive.md)ディレクティブで、 [ * **DDInstall *。インターフェイス**](inf-ddinstall-interfaces-section.md)セクション。
-   *インストール-section インターフェイス*、INF で参照されている[ **InterfaceInstall32** ](inf-interfaceinstall32-section.md)セクション

セクションによって参照される各名前付き、 **CopyFiles**ディレクティブは、次の形式の 1 つまたは複数のエントリ。

```ini
[file-list-section]
destination-file-name[,[source-file-name][,[unused][,flag]]]
...
```

INF-ライター定義*ファイルのセクション一覧*それぞれ別々 の行に任意の数のエントリを持つことができます。

各*ファイルのセクション一覧*省略可能であることができます関連付けられている<em>ファイルのセクション一覧</em>**.security**形式は次のセクション。

```ini
[file-list-section.security]
"security-descriptor-string"
```

## <a name="entries"></a>エントリ


<a href="" id="destination-file-name"></a>*destination-file-name*  
コピー先ファイルの名前を指定します。 ない場合は*ソース ファイル名*は、この仕様もソース ファイルの名前。

<a href="" id="source-file-name"></a>*ソース ファイル名*  
ソース ファイルの名前を指定します。 ファイルのコピー操作のソースと変換先のファイル名が同じ場合*ソース ファイル名*を省略できます。

<a href="" id="unused"></a>*未使用*  
このエントリは Windows 2000 以降のバージョンの Windows でサポートされていません。

<a href="" id="flag"></a>*フラグ*  
特定のソース ファイルを先にコピーする方法 (またはかどうか) を制御する、またはセクションのエントリの 10 進値として 16 進表記で表されるこれらのオプションのフラグを使用できます。 次のシステム定義のフラグの 1 つまたは複数の (論理和) 値を指定できます。 ただし、これらのフラグの一部は相互に排他的です。

<a href="" id="0x00000001---copyflg-warn-if-skip--"></a>**0x00000001** (COPYFLG_WARN_IF_SKIP)   
ファイルをコピーしていないユーザーが選択した場合は、警告を送信します。 このフラグは、次は、相互に排他的では、両方はデジタル署名されている INF ファイルに関連するではありません。

<a href="" id="0x00000002--copyflg-noskip-"></a>**0x00000002** (COPYFLG_NOSKIP)  
ファイルのコピーをスキップするユーザーは許可されません。 場合、このフラグが含まれる、[ドライバー パッケージ](driver-packages.md)署名されます。

<a href="" id="0x00000004--copyflg-noversioncheck-"></a>**0x00000004** (COPYFLG_NOVERSIONCHECK)  
ファイルのバージョンを無視し、保存先ディレクトリに既存のファイルに記述します。 このフラグは、次の 2 つは相互に排他的です。 このフラグは、デジタル署名された INF ファイルには関係ありません。

<a href="" id="0x00000008--copyflg-force-file-in-use-"></a>**0x00000008** (COPYFLG_FORCE_FILE_IN_USE)  
使用中のファイルの動作を強制: 現在開いている場合に、同じ名前の既存のファイルをコピーしないでください。 代わりに、名前を変更して、[次へ]、再起動が発生するときに使用できるように、一時テーブル名を指定したソース ファイルをコピーします。

<a href="" id="0x00000010--copyflg-no-overwrite-"></a>**0x00000010** (COPYFLG_NO_OVERWRITE)  
保存先ディレクトリに既存のファイルを同じ名前のソース ファイルで置換操作を行います。 このフラグは、他のフラグと組み合わせることはできません。

<a href="" id="0x00000020--copyflg-no-version-dialog--"></a>**0x00000020** (COPYFLG_NO_VERSION_DIALOG)   
書き込みませんソース ファイルの保存先ディレクトリにファイルを既存のファイルがソース ファイルより新しい場合。

新しいチェックが実行 VS_VERSIONINFO ファイル バージョン リソースから抽出されたファイルのバージョンを使用します。 詳細については、「 https://docs.microsoft.com/windows/desktop/menurc/version-information」を参照してください。 ターゲット ファイルは、実行可能ファイルまたはリソースのイメージはありません。 または、ファイルにファイルのバージョン情報が含まれていない、し、デバイスのインストールが想定するターゲット ファイルは古い。 

<a href="" id="0x00000040---copyflg-overwrite-older-only-"></a>**0x00000040** (COPYFLG_OVERWRITE_OLDER_ONLY)  
先にファイルが新しいバージョンに置き換えられる場合にのみ、インストール先ディレクトリにソース ファイルをコピーします。 このフラグは、デジタル署名された INF ファイルには関係ありません。 バージョン チェックでは、COPYFLG_NO_VERSION_DIALOG で説明したものと同じ手順を使用します。

<a href="" id="0x00000400--copyflg-replaceonly--"></a>**0x00000400** (COPYFLG_REPLACEONLY)   
ファイルが既に保存先ディレクトリに存在する場合にのみ、ソース ファイルをコピー先ディレクトリにコピーします。

<a href="" id="0x00000800--copyflg-nodecomp--"></a>**0x00000800** (あります)   
(Windows 7 以降)インストール先ディレクトリに圧縮した場合は、ソース ファイルを展開せず、ソース ファイルをコピーします。

<a href="" id="0x00001000--copyflg-replace-boot-file-"></a>**0x00001000** (COPYFLG_REPLACE_BOOT_FILE)  
このファイルは、システムのローダーで必要です。 ユーザーに、システムの再起動を求められます。

<a href="" id="0x00002000--copyflg-noprune-"></a>**0x00002000** (COPYFLG_NOPRUNE)  
最適化の結果として、この操作は削除しないでください。

たとえば、Windows は、ファイルが既に存在するためには、ファイルのコピー操作が必要ないことを判断する可能性があります。 ただし、操作は必須であり、最適化をオーバーライドし、ファイル操作を実行する Windows に指示する、INF のライターが認識しています。

このフラグを使用するには、INF でも指定されている場合、ファイルがコピーされることを確認と[ **DelFiles** ](inf-delfiles-directive.md)ディレクティブまたは、INF [ **RenFiles** ](inf-renfiles-directive.md)ディレクティブ。

<a href="" id="0x00004000--copyflg-in-use-rename-"></a>**0x00004000** (COPYFLG_IN_USE_RENAME)  
場合は、変換先ファイルが使用されているために、ソース ファイルをコピーできません、コピー先ファイルの名前を変更先のファイルをソース ファイルをコピーし、変換先の名前が変更されたファイルを削除します。 コピー先ファイルの名前を変更することはできない場合、は、次のシステムの再起動中にコピー操作を完了します。 変換先の名前が変更されたファイルを削除できない場合、次のシステムの再起動中に、変換先の名前が変更されたファイルを削除します。

<a href="" id="security-descriptor-string"></a>*セキュリティ記述子の文字列*  
名前付きによってコピーされたすべてのファイルに適用する、セキュリティ記述子を指定*ファイルのセクション一覧*します。 *セキュリティ記述子の文字列*DACL を指定するトークンを含む文字列です (**d:**) セキュリティ コンポーネント。

セキュリティ記述子文字列については、[セキュリティ記述子定義言語 (Windows)](https://msdn.microsoft.com/library/windows/desktop/aa379567)を参照してください。 セキュリティ記述子文字列の形式の詳細については、セキュリティ記述子定義言語 (Windows) を参照してください。

場合、<em>ファイルのセクション一覧</em>**.security**セクションが指定されていない、ファイルがファイルのコピー先ディレクトリのセキュリティ特性を継承します。

場合、<em>ファイルのセクション一覧</em>**.security**セクションを指定すると、デバイスおよびシステム サービス パックのインストールとアップグレードが発生することができるように、次の ACE を含める必要があります。

-   (A;GA;;この SY) は、ローカル システムにすべてのアクセスを付与します。
-   (A;GA;;この BA) は、組み込みの管理者のすべてのアクセスを付与します。

*いない*特権を持たないユーザーに書き込みアクセスを許可する ACE 文字列を指定します。

セキュリティ記述子を指定する方法の詳細については、[セキュリティで保護されたデバイスのインストールを作成する](creating-secure-device-installations.md)を参照してください。

<a name="remarks"></a>コメント
-------

Windows のみをコピー、[ドライバー パッケージ](driver-packages.md)ファイルについては、INF ドライバーのインストールの一部として移行先の位置に**CopyFiles**ディレクティブ。 ファイルをコピーするときに、オペレーティング システムによって自動的に、必要な場合、一時ファイル名を生成し、次回オペレーティング システムを起動したとき、コピーされたソース ファイルの名前を変更します。

INF ファイル ライターは、INF を使用して、ソース メディアからコピーされるファイルのパスの指定を指定する必要がありますも[ **SourceDisksNames** ](inf-sourcedisksnames-section.md)セクションと、INF [ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)ソース メディアの INF ファイルを基準には、各ソース ファイルのパスを明示的に指定するセクション。

コピー操作のコピー先がによって制御される、 [ **INF DestinationDirs セクション**](inf-destinationdirs-section.md)します。 このセクションでは、としては、次のように、すべてのファイル コピー操作の出力先を制御します。

- 場合によって参照される名前付きセクションを**CopyFiles**ディレクティブ対応するエントリを持つ、 [ **DestinationDirs** ](inf-destinationdirs-section.md)のエントリを明示的に指定する同じの INF セクション名前付きセクションに記載されているすべてのファイルがコピー先ターゲット先ディレクトリ。 名前付きセクションが表示されていない場合、 **DestinationDirs**セクションで、Windows は、 **DefaultDestDir**内のエントリ、 **DestinationDirs** INF ファイルのセクション。
- 場合、 **CopyFiles**ディレクティブを使用して、 **@** <em>filename</em>構文では、Windows を使用して、 **DefaultDestDir** 内のエントリ**DestinationDirs** INF ファイルのセクション。

次の点は、INF に適用**CopyFiles**ディレクティブ。

- すべて*ファイルのセクション一覧*名は、INF ファイルに固有である必要がありますが、それを参照できます**CopyFiles**、 [ **DelFiles**](inf-delfiles-directive.md)、または[**RenFiles** ](inf-renfiles-directive.md)他の場所で同じ INF ファイルのディレクティブ。 セクション名が記載されている一般的な規則に従う必要があります[INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)します。
- いずれかで指定されているファイル名、 **@** <em>filename</em>または*ファイルのセクション一覧*エントリは、ソース メディア上のファイルの正確な名前である必要があります。 % を使用することはできません*strkey*% トークン ファイル名を指定します。 % の詳細については*strkey*% のトークンを参照してください[ **INF 文字列セクション**](inf-strings-section.md)します。
- **CopyFiles**ディレクティブが修飾をサポートしていません、*ファイルのセクション一覧*システム定義のプラットフォームの拡張機能の名前 (**.nt**、 **.ntx86**、 **.ntia64**、または **.ntamd64**)。
- 使用しない**CopyFiles** INF ファイルをコピーするディレクティブ。 詳細については、[INF ファイルのコピー](copying-inf-files.md)を参照してください。

Windows Vista 以降では、次の点にも適用されます、INF **CopyFiles**ディレクティブ。

-   DIFx ツールが内のドライバー パッケージをプレインストールする場合、[ドライバー ストア](driver-store.md)、それらのみからファイルをコピー ドライバ パッケージ ソースのドライバー ストアにファイルに対応する INF 場合**CopyFiles**ディレクティブ。
-   Windows のアップグレードの一環として、Windows のみをコピーするドライバー パッケージ ファイル、[ドライバー ストア](driver-store.md)ファイルについては、INF ドライバーの移行の一部として**CopyFiles**ディレクティブ。

<a name="examples"></a>使用例
--------

この例では、どのように[ **SourceDisksNames**](inf-sourcedisksnames-section.md)、 [ **SourceDisksFiles**](inf-sourcedisksfiles-section.md)、および[ **DestinationDirs** ](inf-destinationdirs-section.md)セクションでは、単純なデバイスのドライバーの INF の処理で発生したファイルのコピー (およびファイルの削除) 操作のパスを指定します。 (同じ INF が例として、以前使用されたも[**バージョン**](inf-version-section.md)、 **SourceDisksNames**、および**SourceDisksFiles**セクションです)。

```ini
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

この例ではどのように、 **CopyFiles**にディレクティブを使用することができます、 [ * **DDInstall *。CoInstallers** ](inf-ddinstall-coinstallers-section.md)のシステム デバイスの種類に固有のクラスのインストーラーの INF 処理を補完する、2 つのデバイスに固有の共同のインストーラーを提供するデバイス ドライバーを INF セクション。

```ini
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

前の例からわかるように、新しいデバイスに固有の共同インストーラーの名前は、プロバイダーの名前から構築できます (に示すここでは、 *Xx*) と各このような共同インストーラー DLL の使用目的 (示すようにここでは、 *PreInst*と*PostInst*)。

例については、INF を使用する方法の追加**CopyFiles**ディレクティブを参照してください、INF ファイルに含まれるデバイス ドライバーのサンプルについては、 *src* Windows Driver Kit (WDK) のディレクトリ。

## <a name="see-also"></a>関連項目


[**AddInterface**](inf-addinterface-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。共同インストーラー**](inf-ddinstall-coinstallers-section.md)

[***DDInstall *。インターフェイス**](inf-ddinstall-interfaces-section.md)

[**DelFiles**](inf-delfiles-directive.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**RenFiles**](inf-renfiles-directive.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**文字列**](inf-strings-section.md)

[**バージョン**](inf-version-section.md)

 

 






