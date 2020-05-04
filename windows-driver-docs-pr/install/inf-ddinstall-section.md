---
title: INF DDInstall セクション
description: 各モデルの DDInstall セクションには、省略可能な DriverVer ディレクティブ、および INF ファイル内の追加の名前付きセクションを参照するディレクティブが1つ以上含まれています。ここでは、最も頻繁に指定される INF ディレクティブである CopyFiles と AddReg が最初に示されています。
ms.assetid: 79cba88d-fda1-4b91-bf51-98afd7224bc9
keywords:
- INF DDInstall セクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DDInstall Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8042f2955545e77775f9ee2e298b8630afa19b5e
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223230"
---
# <a name="inf-ddinstall-section"></a>INF DDInstall セクション


各モデルの*Ddinstall*セクションには、省略可能な**DriverVer**ディレクティブ、および inf ファイル内の追加の名前付きセクションを参照するディレクティブが1つ以上含まれています。ここでは、最も頻繁に指定される Inf ディレクティブである**CopyFiles**と**AddReg**が最初に示されています。

これらのディレクティブで参照されるセクションには、ドライバーファイルをインストールし、デバイス固有またはドライバー固有の情報をレジストリに書き込むための手順が含まれています。

```inf
[install-section-name] | 
[install-section-name.nt] | 
[install-section-name.ntx86] | 
[install-section-name.ntia64] |  (Windows XP and later versions of Windows)
[install-section-name.ntamd64]  (Windows XP and later versions of Windows)

[DriverVer=mm/dd/yyyy[,x.y.v.z] ]
[CopyFiles=@filename | file-list-section[,file-list-section] ...]
[CopyINF=filename1.inf[,filename2.inf]...]   (Windows XP and later versions of Windows)
[AddReg=add-registry-section[,add-registry-section]...]
[AddProperty=add-registry-section[,add-registry-section]...]  (Windows Vista and later versions of Windows)
[Include=filename1.inf[,filename2.inf]...]
[Needs=inf-section-name[,inf-section-name]...]
[Delfiles=file-list-section[,file-list-section]...]
[Renfiles=file-list-section[,file-list-section]...]
[DelReg=del-registry-section[,del-registry-section]...]
[DelProperty=add-registry-section[,add-registry-section]...]  (Windows Vista and later versions of Windows)
[FeatureScore=featurescore]...  (Windows Vista and later versions of Windows)
[BitReg=bit-registry-section[,bit-registry-section]...]
[LogConfig=log-config-section[,log-config-section]...]
[ProfileItems=profile-items-section[,profile-items-section]...]  (Microsoft Windows 2000 and later versions of Windows)
[UpdateInis=update-ini-section[,update-ini-section]...]
[UpdateIniFields=update-inifields-section[,update-inifields-section]...]
[Ini2Reg=ini-to-registry-section[,ini-to-registry-section]...]
[RegisterDlls=register-dll-section[,register-dll-section]...]
[UnregisterDlls=unregister-dll-section[,unregister-dll-section]...]
[ExcludeID=device-identification-string[,device-identification-string]...]...  ((Windows XP and later versions of Windows)
[Reboot]
```

## <a name="entries"></a>エントリ


<a href="" id="driverver-mm-dd-yyyy--x-y-v-z--"></a>**DriverVer =**<em>mm/dd/yyyy</em>\[**,**<em>x-y. z</em>\]   
この省略可能なエントリは、[ドライバーパッケージ](driver-packages.md)のバージョン情報を指定します。

このエントリを指定する方法の詳細については、「 [**INF DriverVer ディレクティブ**](inf-driverver-directive.md)」を参照してください。

<a href="" id="copyfiles--filename---file-list-section--file-list-section-----"></a>**CopyFiles = @**<em>filename</em> | *ファイル-セクション*\[**、**<em>ファイルリスト-セクション</em>\] ...  
このディレクティブは、ソースメディアから宛先にコピーする1つの名前付きファイルを指定します。または、ソースメディア上のデバイス関連ファイルを転送先に転送するように指定する、1つまたは複数の INF ライターで定義されたセクションを参照します。 **CopyFiles**ディレクティブは省略可能ですが、ほとんどの*ddinstall*セクションに存在します。

INF の[**Destinationdirs**](inf-destinationdirs-section.md)セクションの**DefaultDestDir**エントリは、コピーする1つのファイルのコピー先を指定します。 [**Sourcedisksnames**](inf-sourcedisksnames-section.md)セクションと[**Sourcedisksnames**](inf-sourcedisksfiles-section.md)セクション、またはこの Inf[**バージョン**](inf-version-section.md)セクションの**layoutfile**エントリに指定されている追加の inf は、ドライバーファイルの配布メディア上の場所を提供します。

詳細については、「 [**INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)」を参照してください。

<a href="" id="copyinf-filename1-inf--filename2-inf----"></a>**Copyinf =**<em>filename1</em>**.inf**\[**,**<em>filename2</em>\]**...**  
(Windows XP 以降)このディレクティブを使用すると、指定した INF ファイルがターゲットシステムにコピーされます。

詳細については、「 [**INF Copyinf ディレクティブ**](inf-copyinf-directive.md)」を参照してください。

<a href="" id="addreg-add-registry-section--add-registry-section----"></a>**AddReg =**<em>registry</em>\[-section **、**<em>add-section</em>\]...  
このディレクティブは、1つまたは複数の INF ライターで定義されたセクションを参照します。このセクションでは、新しいサブキー (場合によっては初期値のエントリを含む) がレジストリに書き込まれるか、既存のキーの値エントリが変更されます。

このような add registry セクションでは、 **Hkr**仕様で **..クラス\\**<em>setupclassguid</em>**\\**<em>デバイスのインスタンス id</em>レジストリパスユーザー補助ドライバー。 この種類の**Hkr**仕様は、とも呼ばれます。 "ソフトウェアキー"。

詳細については、「 [**INF AddReg ディレクティブ**](inf-addreg-directive.md)」を参照してください。

<a href="" id="addproperty-add-registry-section--add-registry-section----"></a>**Addproperty =**<em>registry</em>\[-section **、**<em>add-section</em>\]...  
(Windows Vista 以降)デバイスインスタンスに設定されている[デバイスプロパティ](device-properties.md)を変更する1つ以上の INF ファイルセクションを参照します。 Windows Vista 以降のバージョンの Windows オペレーティングシステムに新しく追加されたデバイスインスタンスプロパティを設定する場合にのみ、 [**INF AddProperty ディレクティブ**](inf-addproperty-directive.md)を使用する必要があります。

Windows Server 2003、Windows XP、または Windows 2000 で以前に導入され、対応するレジストリエントリ値を持つデバイスインスタンスプロパティについては、引き続き[**INF AddReg ディレクティブ**](inf-addreg-directive.md)を使用して、デバイスインスタンスのプロパティを設定する必要があります。 これらのガイドラインは、システム定義のプロパティとカスタムプロパティに適用されます。 **Addproperty**ディレクティブの使用方法の詳細については、「 [Inf addproperty ディレクティブと Inf Delproperty ディレクティブの使用](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)」を参照してください。

<a href="" id="include-filename1-inf--filename2-inf----"></a>**Include =**<em>filename1</em>**.inf**\[**,**\]<em>filename2</em>**...**  
このオプションのエントリは、このデバイスやドライバーをインストールするために必要なセクションを含む、システムによって提供される追加の1つ以上の INF ファイルを指定します。 このエントリが指定されている場合は、通常、**必要**なエントリです。

たとえば、システムのカーネルストリーミングサポートに依存するデバイスドライバーのシステム INF ファイルでは、次のようにこのエントリを指定します。

```inf
Include= ks.inf[, [kscaptur.inf,] [ksfilter.inf]]...
```

**インクルード**エントリとその使用に関する制限の詳細については、「[デバイスファイルのソースとターゲットの場所の指定](specifying-the-source-and-target-locations-for-device-files.md)」を参照してください。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**必要な =**<em>inf-name</em>\[**,**<em>inf-name</em>\]...  
この省略可能なエントリは、このデバイスのインストール中に処理する必要がある、システムが提供する INF ファイル内のセクションを指定します。 通常、このような名前付きセクションは、 *ddinstall* (または<em>ddinstall</em>) です **。**<em>xxx</em>)**インクルード**エントリに一覧表示されているいずれかの INF ファイル内のセクション。 ただし、このような*ddinstall*または<em>ddinstall</em>内で参照される任意のセクションを指定でき**ます。** 含まれている INF の<em>xxx</em>セクション。

たとえば、上記の**Include**エントリを含むデバイスドライバーの INF ファイルでは、このエントリを次のように指定します。

```inf
Needs= KS.Registration[, KSCAPTUR.Registration | KSCAPTUR.Registration.NT, MSPCLOCK.Installation]
```

**必要**なエントリを入れ子にすることはできません。 **必要**なエントリとその使用に関する制限の詳細については、「[デバイスファイルのソースとターゲットの場所の指定](specifying-the-source-and-target-locations-for-device-files.md)」を参照してください。

<a href="" id="delfiles-file-list-section--file-list-section----"></a>**Delfiles =**<em>ファイル</em>\[リスト-セクション **、**<em>ファイルリスト-セクション</em>\]...  
このディレクティブは、削除するターゲット上のファイルを一覧表示する1つ以上の INF ライターで定義されたセクションを参照します。

詳細については、「 [**INF DelFiles ディレクティブ**](inf-delfiles-directive.md)」を参照してください。

<a href="" id="renfiles-file-list-section--file-list-section----"></a>**Renfiles =**<em>ファイル</em>\[**,** リスト-<em>セクション-セクション</em>\]...  
このディレクティブは、デバイス関連のソースファイルをターゲットコンピューターにコピーする前に、コピー先で名前を変更する1つ以上の INF ライター定義セクションを参照します。

詳細については、「[**INF RenFiles ディレクティブ**](inf-renfiles-directive.md)」を参照してください。

<a href="" id="delreg-del-registry-section--del-registry-section----"></a>**Delreg =**<em>del-registry-section</em>\[**,**<em>del-セクション</em>\]...  
このディレクティブは、デバイスのインストール中にレジストリから削除されるキーと値のエントリが指定されている、1つまたは複数の INF ライターで定義されたセクションを参照します。

通常、このディレクティブは、INF がこのデバイスの以前のインストールから古いレジストリエントリをクリーンアップする必要がある場合に、アップグレードを処理するために使用されます。

このような削除レジストリセクションでは、 **Hkr**仕様で **..クラス\\**<em>setupclassguid</em>**\\**<em>デバイスのインスタンス id</em>レジストリパスユーザー補助ドライバー。 この種類の**Hkr**仕様は、とも呼ばれます。 "ソフトウェアキー"。

詳細については、「 [**INF DelReg ディレクティブ**](inf-delreg-directive.md)」を参照してください。

<a href="" id="delproperty-add-registry-section--add-registry-section----"></a>**Delproperty =**<em>add</em>\[-registry-section **,**<em>add</em>\]...  
(Windows Vista 以降)デバイスインスタンスに設定されている[デバイスプロパティ](device-properties.md)を削除する1つ以上の INF ファイルセクションを参照します。 Windows Vista 以降のバージョンの Windows に新しく追加されたデバイスインスタンスプロパティを削除する場合にのみ、 [**INF DelProperty ディレクティブ**](inf-delproperty-directive.md)を使用する必要があります。

Windows Server 2003、Windows XP、または Windows 2000 で以前に導入され、対応するレジストリエントリ値を持つデバイスインスタンスプロパティについては、引き続き[**INF DelReg ディレクティブ**](inf-delreg-directive.md)を使用してデバイスインスタンスのプロパティを削除する必要があります。 これらのガイドラインは、システム定義のプロパティとカスタムプロパティに適用されます。 **Delproperty**ディレクティブの使用方法の詳細については、「 [Inf addproperty ディレクティブと Inf Delproperty ディレクティブの使用](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)」を参照してください。

<a href="" id="featurescore-featurescore"></a>**特長コア =**<em>特長コア</em>  
**警告**  - **[ \[ddinstall\] ** ] セクションで直接指定されている場合にのみ、[領域の**コア**] ディレクティブが処理されます。

 

(Windows Vista 以降)このディレクティブは、ドライバーがサポートする機能に基づくドライバーの追加の順位付け条件を提供します。 たとえば、クラス固有の条件に基づいてドライバーを区別する[デバイスセットアップクラス](device-setup-classes.md)に対して、機能スコアが定義されている場合があります。

ドライバーの順位付けの詳細については、「Windows がドライバーをランク付けする[方法 (Windows Vista 以降)](how-setup-ranks-drivers--windows-vista-and-later-.md)」を参照してください。

このディレクティブの詳細については、「 [**INF の特長コアディレクティブ**](inf-featurescore-directive.md)」を参照してください。

**注**   *ddinstall*セクションには複数の使用可能な**コア**エントリを含めることができますが、セクションでは最初のエントリのみが処理されます。

 

<a href="" id="bitreg-bit-registry-section--bit-registry-section----"></a>**Bitreg =**<em>ビットレジストリ-セクション</em>\[**、**<em>ビットレジストリ-セクション</em>\]...  
このディレクティブは、 [REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)型の既存のレジストリ値のエントリが変更される、1つまたは複数の INF ライターで定義されたセクションを参照します。

このようなビットレジストリセクションでは、 **Hkr**仕様で **..クラス\\**<em>setupclassguid</em>**\\**<em>デバイスのインスタンス id</em>レジストリパスユーザー補助ドライバー。 この種類の**Hkr**仕様は、とも呼ばれます。 "ソフトウェアキー"。

詳細については、「 [**INF BitReg ディレクティブ**](inf-bitreg-directive.md)」を参照してください。

<a href="" id="logconfig-log-config-section--log-config-section----"></a>**Logconfig =**<em>log-config-section</em>\[logs-セクション **、**<em>ログ</em>\]の構成-セクション...  
このディレクティブは、INF 内で、ルートで列挙されたデバイスまたは手動でインストールされたデバイスの1つまたは複数の INF ライターで定義されたセクションを参照します。 これらの名前付きセクションでは、このような "検出" または手動でインストールされたデバイスの INF によって、デバイスが動作するために必要なバス相対ハードウェアリソースの1つ以上の論理構成が指定されます。 このような手動でインストールされたデバイスの INF には、ソフトウェアで構成できるものではなく、 <em>Ddinstall</em>も必要です **。FactDef**セクション。

**Logconfig**ディレクティブは、プラグアンドプレイ (PnP) デバイスのインストールには使用されません。 ただし、 [**INF DDInstall. LogConfigOverride セクション**](inf-ddinstall-logconfigoverride-section.md)を使用して、PnP デバイスの上書き構成を指定することができます。

このディレクティブは、すべての上位レベル (デバイス以外) のドライバーとコンポーネントには関係ありません。

詳細については、「 [**INF LogConfig ディレクティブ**](inf-logconfig-directive.md)」を参照してください。

<a href="" id="profileitems-profile-items-section--profile-items-section----"></a>**Profileitems =**<em>profile-items-section</em>\[**,**<em>profile-section</em>\]...  
(Microsoft Windows 2000 以降のバージョンの Windows)このディレクティブは、[スタート] メニューに追加または削除する項目を記述する1つ以上の INF ライターで定義されたセクションを参照します。

詳細については、「 [**INF ProfileItems ディレクティブ**](inf-profileitems-directive.md)」を参照してください。

<a href="" id="updateinis-update-ini-section--update-ini-section----"></a>**Updateinis =**<em>update-ini</em>\[-section **,**<em>.ini</em>\]...  
使用頻度の低いディレクティブは、1つまたは複数の INF ライターで定義されたセクションを参照しています。この場合、そのセクション内の特定のセクションまたは行を、インストール時に同じ名前の宛先 INI ファイルに読み込むソース INI ファイルを指定します。 必要に応じて、同じ名前の特定のソース INI ファイルから、コピー先の既存の INI ファイルに対する1行ずつの変更を、更新プログラム INI セクションで指定できます。

詳細については、「 [**INF UpdateInis ディレクティブ**](inf-updateinis-directive.md)」を参照してください。

<a href="" id="updateinifields-update-inifields-section--update-inifields-section----"></a>**UpdateIniFields =**<em>inifields-section</em>\[**,**<em>inifields-section</em>\]...  
使用頻度の低いディレクティブは、1つまたは複数の INF ライターで定義されたセクションを参照します。このセクションでは、デバイス固有の INI ファイルの行に含まれる変更が指定されています。

詳細については、「 [**INF UpdateIniFields ディレクティブ**](inf-updateinifields-directive.md)」を参照してください。

<a href="" id="ini2reg-ini-to-registry-section--ini-to-registry-section----"></a>**Ini2Reg =**<em>ini</em>\[-セクション **、**<em>ini からレジストリへ</em>\]のセクション...  
使用頻度の低いディレクティブは、1つまたは複数の INF ライターで定義されたセクションを参照します。このセクションでは、ソースメディアで提供される、デバイス固有の INI ファイルのセクションや行をレジストリに移動します。

詳細については、「 [**INF Ini2Reg ディレクティブ**](inf-ini2reg-directive.md)」を参照してください。

<a href="" id="registerdlls-register-dll-section--register-dll-section----"></a>**Registerdlls =**<em>register</em>\[-セクション **、**<em>register-section</em>\]...  
このディレクティブは、OLE コントロールであり、自己登録が必要なファイルを指定するために使用される1つ以上の INF セクションを参照します。

詳細については、「 [**INF RegisterDlls ディレクティブ**](inf-registerdlls-directive.md)」を参照してください。

<a href="" id="unregisterdlls-unregister-dll-section--unregister-dll-section----"></a>**Unregisterdlls =**<em>登録解除-セクション</em>\[**の**<em>登録解除-セクション</em>\]...  
このディレクティブは、OLE コントロールであり、自己登録解除 (自己削除) を必要とするファイルを指定するために使用される1つ以上の INF セクションを参照します。

詳細については、「 [**INF UnregisterDlls ディレクティブ**](inf-unregisterdlls-directive.md)」を参照してください。

<a href="" id="excludeid-device-identification-string--device-identification-string----"></a>**Excludeid =**<em>デバイス id-文字列</em>\[**、**<em>デバイス識別文字列</em>\]...  
**警告**   **excludeid**ディレクティブは、 ** \[\] ddinstall**セクションで直接指定されている場合にのみ処理されます。

 

(Windows XP 以降)このディレクティブは、1つまたは複数のデバイス id 文字列 ([ハードウェア id](hardware-ids.md)または[互換性 id](compatible-ids.md)) を指定します。 [ *Ddinstall* ] セクションでは、一覧表示されているハードウェア id または互換性 id のいずれかに一致する[デバイス id](device-ids.md)を持つデバイスはインストールされません。

<a href="" id="reboot"></a>**再起動**  
このディレクティブは、インストールの完了後に、呼び出し元にシステムの再起動を求めるメッセージが表示されることを示します。

詳細については、「 [**INF Reboot ディレクティブ**](inf-reboot-directive.md)」を参照してください。

<a name="remarks"></a>解説
-------

Windows Driver Kit (WDK) のドキュメント全体を通じて、 *Ddinstall*という用語を使用して、プラットフォーム拡張の有無に関係なく、*インストールセクション名*を参照します。 このため、"*ddinstall* section" は、"INF 内の名前付きセクション" を\[意味します。これは、形式の*インストールセクション名*\]または\[<em>インストールセクション</em>*名 *. nt **\]* * xxx "です。 *Ddinstall*セクションに名前を作成する場合は、 ** \[\] WDMPNPB003_Device**や** \[GPR400 などのデバイス固有のプレフィックスを含める必要があります。NT\]をインストールします**。

各*Ddinstall*セクションは、inf ファイルの「製造元別の[**inf*モデル*」セクション**](inf-models-section.md)にある、デバイス/モデル固有のエントリで参照されている必要があります。

ソースメディアから転送されるファイルが関連付けられていないデバイスを除き、異なるオペレーティングシステムプラットフォームに WDM ドライバーをインストールする INF ファイルには、次の*Ddinstall*セクションの少なくとも1つが必要です。

- X86 ベースのプラットフォームに固有のデバイス/ドライバーのインストールのエントリを指定する**ntx86** <em>セクション。</em>
- Itanium ベースのプラットフォームに固有のデバイス/ドライバーのインストールのエントリを指定する**ntia64** <em>セクション。</em>
- X64 ベースのプラットフォームに固有のデバイス/ドライバーのインストールのエントリを指定する**ntamd64** <em>セクション。</em>
- ARM ベースのプラットフォームに固有のデバイス/ドライバーのインストールのエントリを指定する、 <em>install section-name</em>**. ntarm**セクション。
- ARM64 ベースのプラットフォームに固有のデバイスまたはドライバーのインストールのエントリを指定する**ntarm64** <em>セクション。</em>


- 特定のハードウェアプラットフォームに固有ではないデバイスまたはドライバーのインストールのエントリを指定する、*インストールセクション名*または<em>インストールセクション-name</em>**. nt**セクション。

システム定義の**nt**、 **ntx86**、. **ntia64**、. **ntamd64**、. **ntarm**、および**ntarm64**の各拡張機能の使用方法の詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の INF ファイルの作成](creating-inf-files-for-multiple-platforms-and-operating-systems.md)」を参照してください。

Windows 2000 以降では、ドライバーをインストールする INF ファイルには、 [**Ddinstall. Services**](inf-ddinstall-services-section.md)セクションが必要です。これにより、デバイスまたはドライバーのレジストリ情報をレジストリに保存するように指定できます.. **.CurrentControlSet\\ \\** デバイスによっては、1つまたは複数の<em>Ddinstall</em>を使用することもでき**ます。HW**、 <em>ddinstall</em>**。CoInstallers**、 <em>ddinstall</em>**。インターフェイス**、または<em>ddinstall</em>**。LogConfigOverride**セクション。

*Ddinstall*セクション内の各ディレクティブは、複数のセクション名を参照できます。 ただし、追加の名前付きセクションは、それぞれコンマ (,) で区切られている必要があります。

各セクション名は、INF ファイル内で一意である必要があります。また、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

*Ddinstall*セクションで指定されているすべての**AddReg**ディレクティブは、追加レジストリセクションを参照することを前提としています。このセクションは、上位または下位フィルタードライバーに関する情報を格納するために使用することはできず、多機能デバイスについて、またはドライバーに依存しないものの、デバイス固有のパラメーターです。 デバイス/ドライバーの INF がこの種類の情報をレジストリに格納する必要がある場合は、 **AddReg**ディレクティブを、非装飾で修飾された<em>ddinstall</em>で使用する必要があり**ます。ハードウェア**セクション (存在する場合) は、別の INF ライターで定義された*レジストリセクション*を参照します。

[ [**INF バージョン] セクション**](inf-version-section.md)で指定された[デバイスセットアップクラス](device-setup-classes.md)に応じて、追加のクラス固有のディレクティブを*ddinstall*セクションで指定できます。 クラス固有のディレクティブの詳細については、次のトピックを参照してください。

-   [Windows SideShow と互換性のあるデバイス用の INF ファイルを構築する](https://docs.microsoft.com/windows-hardware/drivers/)
-   [ネットワーク INF ファイル内の DDInstall セクション](https://docs.microsoft.com/windows-hardware/drivers/network/ddinstall-services-section-in-a-network-inf-file)
-   [静止画像デバイスの INF ファイル](https://docs.microsoft.com/windows-hardware/drivers/image/inf-files-for-still-image-devices)
-   [WIA デバイスの INF ファイル](https://docs.microsoft.com/windows-hardware/drivers/image/inf-files-for-wia-devices)
-   [ネットワーク コンポーネントのインストール要件](https://docs.microsoft.com/windows-hardware/drivers/network/installation-requirements-for-network-components)
-   [INF ファイルでの WDF ディレクティブの指定](https://docs.microsoft.com/windows-hardware/drivers/wdf/specifying-wdf-directives-in-inf-files)

<a name="examples"></a>例
--------

この例では、 *Ddinstall*セクション、 **Ser_Inst**および**Inp_Inst**の展開を示します。 これらのセクションについては、 [**「INF*モデル***](inf-models-section.md)の例」セクションを参照してください。

```inf
[Ser_Inst]
CopyFiles=Ser_CopyFiles, mouclass_CopyFiles

[Ser_CopyFiles]
sermouse.sys

[mouclass_CopyFiles] ; section name referenced by > 1 CopyFiles
mouclass.sys

[Inp_Inst]
CopyFiles=Inp_CopyFiles, mouclass_CopyFiles

[Inp_CopyFiles]
inport.sys
```

次の例では、プラットフォーム拡張機能を使用する一般的な例を示します。

```inf
[Manufacturer]
%MSFT% = Microsoft

[Microsoft]
%Device.DeviceDesc% = DeviceInstall, HWID
[DeviceInstall.NTx86]
;
; This section is used for installations on x86 systems.
;
...
[DeviceInstall.NTx86.Services]
;
; Services installation for x86 systems.
;
...
[DeviceInstall.NT]
;
; This section is used for installations on systems (all other architectures).
;
...
[DeviceInstall.NT.Services]
;
; Services installation for systems (all other architectures).
;
...
```

次の例は、システムによって提供される、オーディオデバイス用の WDM ドライバーをさまざまなオペレーティングシステムプラットフォームにインストールする INF ファイルの*Ddinstall*セクションを示しています。

```inf
[WDMPNPB003_Device.NT]
DriverVer=01/14/1999,5.0
Include=ks.inf, wdmaudio.inf
Needs=KS.Registration, WDMAUDIO.Registration.NT
LogConfig=SB16.LC1,SB16.LC2,SB16.LC3,SB16.LC4,SB16.LC5 
; a few log-config-sections omitted here for brevity
CopyFiles=MSSB16.CopyList
AddReg=WDM_SB16.AddReg
```

次の例では、システムによって提供される*ks*ファイルと*wdmaudio*ファイルで、上記の**必要**なエントリによって参照されるセクションを示します。 前の例では、これらのファイルは**インクルード**エントリで指定されています。 オペレーティングシステムのデバイスインストーラーまたはメディアクラスインストーラーが、このデバイスの<em>インストールセクション名</em>**. nt**セクションを処理するときに、次の2つのセクションも処理されます。

```inf
[KS.Registration]
; following AddReg= is actually a single line in the ks.inf file
AddReg=ProxyRegistration,CategoryRegistration,\
    TopologyNodeRegistration,PlugInRegistration,PinNameRegistration,\
    DeviceRegistration 
CopyFiles=KSProxy.Files,KSDriver.Files

[WDMAUDIO.Registration.NT]
AddReg=WDM.AddReg
CopyFiles=WDM.CopyFiles.Sys, WDM.CopyFiles.Drv
;
; INF-writer-defined add-registry and file-list sections
; referenced by preceding directives are omitted here for brevity
;
```

## <a name="see-also"></a>関連項目


[**AddProperty**](inf-addproperty-directive.md)

[***DDInstall *。CoInstallers**](inf-ddinstall-coinstallers-section.md)

[***DDInstall *。FactDef**](inf-ddinstall-factdef-section.md)

[***DDInstall *。ハードウェア**](inf-ddinstall-hw-section.md)

[***DDInstall *。インターフェイス**](inf-ddinstall-interfaces-section.md)

[***DDInstall *。LogConfigOverride**](inf-ddinstall-logconfigoverride-section.md)

[***DDInstall *。サーヴィス**](inf-ddinstall-services-section.md)

[**DefaultInstall**](inf-defaultinstall-section.md)

[**DefaultInstall**](inf-defaultinstall-services-section.md)

[**DelProperty**](inf-delproperty-directive.md)

[**FeatureScore**](inf-featurescore-directive.md)

 

 






