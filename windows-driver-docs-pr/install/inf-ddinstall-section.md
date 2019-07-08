---
title: INF DDInstall セクション
description: 各モデルあたり DDInstall セクションには、省略可能な DriverVer ディレクティブが含まれていて、図では、最も頻繁に指定した INF ディレクティブ、CopyFiles および AddReg、INF ファイルで追加の名前付きセクションを参照する 1 つまたは複数のディレクティブが最初に表示します。
ms.assetid: 79cba88d-fda1-4b91-bf51-98afd7224bc9
keywords:
- INF DDInstall セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DDInstall Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 963c2a4eb2ea79c2467e61f922166f0206090092
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385916"
---
# <a name="inf-ddinstall-section"></a>INF DDInstall セクション


各ごとのモデル*DDInstall*セクションが含まれていますが、省略可能な**DriverVer**ディレクティブ追加を参照する 1 つまたは複数のディレクティブの名前をここに、最も頻繁に INF ファイルのセクションINF のディレクティブを指定した**CopyFiles**と**AddReg**、最初に表示されています。

セクションでには、これらのディレクティブによって参照されるには、ドライバー ファイルをインストールして、特定のデバイスやドライバー固有の情報をレジストリに書き込むのための手順が含まれます。

```ini
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


<a href="" id="driverver-mm-dd-yyyy--x-y-v-z--"></a>**DriverVer=** <em>mm/dd/yyyy</em>\[ **,** <em>x.y.v.z</em>\]   
この項目のバージョン情報を指定します、[ドライバー パッケージ](driver-packages.md)します。

このエントリを指定する方法については、次を参照してください。 [ **INF DriverVer ディレクティブ**](inf-driverver-directive.md)します。

<a href="" id="copyfiles--filename---file-list-section--file-list-section-----"></a>**CopyFiles=@** <em>filename</em> | *file-list-section*\[ **,** <em>file-list-section</em>\] ...  
このディレクティブは、先のソース メディアからコピーされる 1 つの名前付きファイルを指定しますか、または 1 つまたは複数 INF ライター定義のセクションでは、先に転送するため、元のメディアのデバイス関連のファイルを指定するを参照します。 **CopyFiles**ディレクティブは省略可能では、ほとんどには存在*DDInstall*セクション。

**DefaultDestDir**内のエントリ、 [ **DestinationDirs** ](inf-destinationdirs-section.md) INF のセクションがコピーされる 1 つのファイルの保存先を指定します。 [ **SourceDisksNames** ](inf-sourcedisksnames-section.md)と[ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)セクション、またはで指定された追加の INF、 **LayoutFile**エントリのこの INF の[**バージョン**](inf-version-section.md)セクションで、ドライバー ファイルの配布メディアの場所を指定します。

詳細については、次を参照してください。 [ **INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)します。

<a href="" id="copyinf-filename1-inf--filename2-inf----"></a>**CopyINF =** <em>filename1</em> **.inf**\[ **、** <em>filename2</em> **.inf**\]...  
(Windows XP 以降)このディレクティブは、ターゲット システムにコピーする INF ファイルを指定します。

詳細については、次を参照してください。 [ **INF CopyINF ディレクティブ**](inf-copyinf-directive.md)します。

<a href="" id="addreg-add-registry-section--add-registry-section----"></a>**AddReg=** <em>add-registry-section</em>\[ **,** <em>add-registry-section</em>\]...  
このディレクティブは、1 つまたは複数 INF ライター定義のセクションでは新しいサブキー、場合によっては、初期値エントリで指定されているまたは既存のキーの値のエントリが変更されたレジストリに書き込まれるを参照します。

**HKR**追加レジストリ セクション内の仕様を指定、 **.クラス\\** <em>SetupClassGUID</em> **\\** <em>デバイス インスタンス id</em>ユーザーからアクセス可能なドライバーのレジストリ パス。 この種類の**HKR**仕様とも呼ばれる、します。 「ソフトウェア キー」です。

詳細については、次を参照してください。 [ **INF AddReg ディレクティブ**](inf-addreg-directive.md)します。

<a href="" id="addproperty-add-registry-section--add-registry-section----"></a>**AddProperty =** <em>追加レジストリ セクション</em>\[ **、** <em>追加レジストリ セクション</em>\].  
(Windows Vista 以降)変更を 1 つまたは複数の INF ファイルでセクションを参照して[デバイス プロパティ](device-properties.md)デバイス インスタンスに設定されています。 使用する必要があります、 [ **INF AddProperty ディレクティブ**](inf-addproperty-directive.md) Windows Vista またはそれ以降のバージョンの Windows オペレーティング システムを新たに導入されたデバイス インスタンス プロパティを設定するだけです。

デバイス インスタンス プロパティ以前 Windows Server 2003、Windows XP、または Windows 2000 で導入された、対応するレジストリ エントリの値がある、使用する続行する必要があります[ **INF AddReg ディレクティブ**](inf-addreg-directive.md)デバイス インスタンスのプロパティを設定します。 システム定義プロパティとカスタム プロパティに次のガイドラインが適用されます。 使用する方法についての詳細、 **AddProperty**ディレクティブを参照してください[INF AddProperty ディレクティブと INF DelProperty ディレクティブを使用して](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)します。

<a href="" id="include-filename1-inf--filename2-inf----"></a>**含める =** <em>filename1</em> **.inf**\[ **、** <em>filename2</em> **.inf**\]...  
この省略可能なエントリでは、1 つまたは複数追加システムが指定した INF ファイルをこのデバイスやドライバーをインストールするために必要なセクションが含まれているを指定します。 通常、このエントリが指定されている場合は、**必要がある**エントリ。

たとえば、このエントリが次のよう指定、システムのカーネル ストリーミング サポートに依存しているデバイス ドライバー用のシステム INF ファイル。

```ini
Include= ks.inf[, [kscaptur.inf,] [ksfilter.inf]]...
```

詳細については、 **Include**エントリと、その使用に関する制限事項を参照してください。[デバイス ファイルのソースとターゲットの場所を指定する](specifying-the-source-and-target-locations-for-device-files.md)します。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**必要な =** <em>inf セクション名</em>\[ **、** <em>inf セクション名</em>\].  
この省略可能なエントリでは、このデバイスのインストール中に処理する必要があるシステム提供の INF ファイル内のセクションを指定します。 通常、このような名前付きセクションは、 *DDInstall* (または<em>DDInstall</em> **.** <em>xxx</em>) 内に記載されている INF ファイルの 1 つのセクション、 **Include**エントリ。 ただし、このような内で参照されている任意のセクションがあります、 *DDInstall*または<em>DDInstall</em> **.** <em>xxx</em>の含まれる INF セクション。

上記のあるデバイス ドライバーの INF ファイルなど、 **Include**エントリは次のようにこのエントリを指定します。

```ini
Needs= KS.Registration[, KSCAPTUR.Registration | KSCAPTUR.Registration.NT, MSPCLOCK.Installation]
```

**必要がある**エントリを入れ子にすることはできません。 詳細については、**必要がある**エントリと、その使用に関する制限事項を参照してください。[デバイス ファイルのソースとターゲットの場所を指定する](specifying-the-source-and-target-locations-for-device-files.md)します。

<a href="" id="delfiles-file-list-section--file-list-section----"></a>**Delfiles =** <em>ファイルのセクション一覧</em>\[ **、** <em>ファイルのセクション一覧</em>\].  
このディレクティブは、1 つまたは複数 INF ライター定義のセクションでは削除するターゲット上のファイルの一覧を参照します。

詳細については、次を参照してください。 [ **INF DelFiles ディレクティブ**](inf-delfiles-directive.md)します。

<a href="" id="renfiles-file-list-section--file-list-section----"></a>**Renfiles =** <em>ファイルのセクション一覧</em>\[ **、** <em>ファイルのセクション一覧</em>\].  
このディレクティブは、1 つまたは複数 INF ライター定義のセクションではデバイスに関連するソース ファイルがターゲット コンピューターにコピーされる前に、変換先の名前を変更するファイルのリストを参照します。

詳細については、次を参照してください。[**INF RenFiles ディレクティブ**](inf-renfiles-directive.md)します。

<a href="" id="delreg-del-registry-section--del-registry-section----"></a>**DelReg=** <em>del-registry-section</em>\[ **,** <em>del-registry-section</em>\]...  
このディレクティブは、1 つまたは複数 INF ライター定義のセクションでは、デバイスのインストール中に、レジストリから削除するエントリを指定では、どのキーと値を参照します。

通常、このディレクティブは、INF は、このデバイスの以前のインストールからの古いレジストリ エントリをクリーンアップする必要がありますと、アップグレードを処理するために使用します。

**HKR** delete レジストリ セクション内の指定を指定、 **.クラス\\** <em>SetupClassGUID</em> **\\** <em>デバイス インスタンス id</em>ユーザーからアクセス可能なドライバーのレジストリ パス。 この種類の**HKR**仕様とも呼ばれる、します。 「ソフトウェア キー」です。

詳細については、次を参照してください。 [ **INF してディレクティブ**](inf-delreg-directive.md)します。

<a href="" id="delproperty-add-registry-section--add-registry-section----"></a>**DelProperty=** <em>add-registry-section</em>\[ **,** <em>add-registry-section</em>\]...  
(Windows Vista 以降)削除する 1 つまたは複数の INF ファイルでセクションを参照して[デバイス プロパティ](device-properties.md)デバイス インスタンスに設定されています。 使用する必要があります、 [ **INF DelProperty ディレクティブ**](inf-delproperty-directive.md) Windows Vista または Windows の以降のバージョンを新たに導入されたデバイス インスタンス プロパティを削除するだけです。

デバイス インスタンス プロパティ以前 Windows Server 2003、Windows XP、または Windows 2000 で導入された、対応するレジストリ エントリの値がある、使用する続行する必要があります[ **INF してディレクティブ**](inf-delreg-directive.md)デバイス インスタンスのプロパティを削除します。 システム定義プロパティとカスタム プロパティに次のガイドラインが適用されます。 使用する方法についての詳細、 **DelProperty**ディレクティブを参照してください[INF AddProperty ディレクティブと INF DelProperty ディレクティブを使用して](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)します。

<a href="" id="featurescore-featurescore"></a>**FeatureScore =** <em>featurescore</em>  
**警告**  、 **FeatureScore**ディレクティブが処理されるで直接指定した場合のみ、 **\[DDInstall\]** セクション。

 

(Windows Vista 以降)このディレクティブは、ドライバーをドライバーがサポートする機能に基づく、順位付けの追加条件を提供します。 特徴のスコアを定義できますなど、[デバイス セットアップ クラス](device-setup-classes.md)クラスに固有の条件に基づいてドライバーを識別するためです。

ドライバーが順位付けされる方法の詳細については、次を参照してください。[どの Windows ランクのドライバー (Windows Vista 以降)](how-setup-ranks-drivers--windows-vista-and-later-.md)します。

このディレクティブの詳細については、次を参照してください。 [ **INF FeatureScore ディレクティブ**](inf-featurescore-directive.md)します。

**注**  が、 *DDInstall*セクションが複数含めることができます**FeatureScore**セクションのエントリでは、最初のエントリのみが処理されます。

 

<a href="" id="bitreg-bit-registry-section--bit-registry-section----"></a>**BitReg =** <em>ビットのレジストリ セクション</em>\[ **、** <em>ビットのレジストリ セクション</em>\].  
このディレクティブは、1 つまたは複数 INF ライター定義を既存のレジストリ値のエントリの型のセクションを参照[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)変更されます。

**HKR**ビット レジストリのセクションで仕様を指定、 **.クラス\\** <em>SetupClassGUID</em> **\\** <em>デバイス インスタンス id</em>ユーザーからアクセス可能なドライバーのレジストリ パス。 この種類の**HKR**仕様とも呼ばれる、します。 「ソフトウェア キー」です。

詳細については、次を参照してください。 [ **INF BitReg ディレクティブ**](inf-bitreg-directive.md)します。

<a href="" id="logconfig-log-config-section--log-config-section----"></a>**LogConfig=** <em>log-config-section</em>\[ **,** <em>log-config-section</em>\]...  
このディレクティブは、ルート列挙デバイスか、または手動でインストールされているデバイスに対して、INF 内で 1 つまたは複数のライター定義 INF セクションを参照します。 これらの名前のセクションでは、このような「検出」または手動でインストールされているデバイスの INF に、デバイスが正常に機能が必要 bus 相対ハードウェア リソースの 1 つまたは複数の論理構成を指定します。 ソフトウェア構成可能でないこのような手動でインストールされているデバイスの INF する必要があります、 <em>DDInstall</em>**します。FactDef**セクション。

**LogConfig**ディレクティブを使用すると、プラグ アンド プレイ (PnP) デバイスをインストールすることはありません。 ただし、使用することができます、 [ **INF DDInstall.LogConfigOverride セクション**](inf-ddinstall-logconfigoverride-section.md) PnP デバイス用のオーバーライド構成を提供します。

このディレクティブは、関連するすべての上位レベル (試行) ドライバーとコンポーネントではありません。

詳細については、次を参照してください。 [ **INF LogConfig ディレクティブ**](inf-logconfig-directive.md)します。

<a href="" id="profileitems-profile-items-section--profile-items-section----"></a>**ProfileItems =** <em>プロファイル-section 項目</em>\[ **、** <em>プロファイル-section 項目</em>\].  
(Microsoft Windows 2000 および Windows の以降のバージョン)このディレクティブは、1 つまたは複数 INF ライター定義のセクションでは追加、または [スタート] メニューから削除する項目を説明するを参照します。

詳細については、次を参照してください。 [ **INF ProfileItems ディレクティブ**](inf-profileitems-directive.md)します。

<a href="" id="updateinis-update-ini-section--update-ini-section----"></a>**UpdateInis =** <em>update-section ini</em>\[ **、** <em>update-section ini</em>\].  
使用頻度の低いこのディレクティブは、1 つを参照またはソース INI を指定する、多くの INF ライター定義セクションのファイルから特定のセクションまたはこのようなセクション内の行のインストール時に、同じ名前の変換先の INI ファイルに読み込むことができます。 必要に応じて、同じ名前の指定したソースの INI ファイルからの先に既存の INI ファイルの変更の 1 行ずつ更新 ini セクションで指定できます。

詳細については、次を参照してください。 [ **INF UpdateInis ディレクティブ**](inf-updateinis-directive.md)します。

<a href="" id="updateinifields-update-inifields-section--update-inifields-section----"></a>**UpdateIniFields =** <em>update-section inifields</em>\[ **、** <em>update-section inifields</em>\].  
使用頻度の低いこのディレクティブは、1 つまたは複数 INF ライター定義のセクションでは、デバイスに固有の INI ファイルの行を内の変更を指定するを参照します。

詳細については、次を参照してください。 [ **INF UpdateIniFields ディレクティブ**](inf-updateinifields-directive.md)します。

<a href="" id="ini2reg-ini-to-registry-section--ini-to-registry-section----"></a>**Ini2Reg =** <em>セクション レジストリ ini</em>\[ **、** <em>セクション レジストリ ini</em>\].  
これは、ディレクティブの参照セクションまたは、ソース メディアに、デバイスに固有の INI ファイルの行は 1 つまたは複数のライター定義 INF セクションは、レジストリに移動するのにはほとんど使用されません。

詳細については、次を参照してください。 [ **INF Ini2Reg ディレクティブ**](inf-ini2reg-directive.md)します。

<a href="" id="registerdlls-register-dll-section--register-dll-section----"></a>**RegisterDlls =** <em>レジスタ-section dll</em>\[ **、** <em>レジスタ-section dll</em>\].  
このディレクティブは、OLE コントロールは、自己登録を必要とするファイルを指定するために使用する 1 つまたは複数の INF セクションを参照します。

詳細については、次を参照してください。 [ **INF RegisterDlls ディレクティブ**](inf-registerdlls-directive.md)します。

<a href="" id="unregisterdlls-unregister-dll-section--unregister-dll-section----"></a>**UnregisterDlls =** <em>の登録を解除 dll セクション</em>\[ **、** <em>の登録を解除 dll セクション</em>\].  
このディレクティブは、OLE コントロールは、(自己の削除) を自己登録解除を必要とするファイルを指定するために使用する 1 つまたは複数の INF セクションを参照します。

詳細については、次を参照してください。 [ **INF UnregisterDlls ディレクティブ**](inf-unregisterdlls-directive.md)します。

<a href="" id="excludeid-device-identification-string--device-identification-string----"></a>**ExcludeID =** <em>デバイスの識別文字列</em>\[ **、** <em>デバイスの識別文字列</em>\].  
**警告**  、 **ExcludeID**ディレクティブが処理されるで直接指定した場合のみ、 **\[DDInstall\]** セクション。

 

(Windows XP 以降)このディレクティブを 1 つまたは複数のデバイスの識別文字列を指定します (どちらか[ハードウェア Id](hardware-ids.md)または[互換性 Id](compatible-ids.md))。 *DDInstall*セクションがデバイスをインストールしていない[デバイス Id](device-ids.md)ハードウェア Id または互換性のある Id 一覧のいずれかに一致します。

<a href="" id="reboot"></a>**再起動**  
このディレクティブは、呼び出し元にインストールが完了したら、システムを再起動するメッセージを表示することを示します。

詳細については、次を参照してください。 [ **INF 再起動ディレクティブ**](inf-reboot-directive.md)します。

<a name="remarks"></a>コメント
-------

Windows Driver Kit (WDK) のドキュメント全体で用語*DDInstall*を参照するために使用する*インストール セクション名*プラットフォーム拡張機能の有無。 そのため、"*DDInstall*セクション"意味"、INF の形式で名前付きセクション\[*インストール セクション名*\]または\[ <em>インストール セクション名</em>* *.nt * * * xxx*\]"。 名前を作成するときに*DDInstall*セクションなど、デバイスに固有のプレフィックスを含める必要があります **\[WDMPNPB003_Device\]** または **\[GPR400 します。Install.NT\]** します。

各*DDInstall* - 製造元でデバイス/モデルに固有のエントリでは、セクションを参照する必要があります[ **INF*モデル*セクション**](inf-models-section.md)の INF ファイル。

ソース メディアからの転送に関連付けられているファイルがないデバイスを除く別のオペレーティング システム プラットフォームで WDM ドライバーをインストールする INF ファイルは少なくとも 1 つ、次のことがあります*DDInstall*セクション。

- <em>インストール セクション名</em> **.ntx86**セクション デバイス/ドライバーのインストールが x86 ベースのプラットフォームに固有のエントリを指定します。
- <em>インストール セクション名</em> **.ntia64**セクション デバイス/ドライバーのインストールは Itanium ベースのプラットフォームに固有のエントリを指定します。
- <em>インストール セクション名</em> **.ntamd64**セクション デバイス/ドライバーのインストールは x64 ベースのプラットフォームに固有のエントリを指定します。
- <em>インストール セクション名</em> **.ntarm**セクション デバイス/ドライバーのインストールは ARM ベースのプラットフォームに固有のエントリを指定します。
- <em>インストール セクション名</em> **.ntarm64**セクション ARM64 ベースのプラットフォームに固有のデバイスとドライバーのインストール用のエントリを指定します。


- *インストール セクション名*または<em>インストール セクション名</em> **.nt**特定に固有ではないデバイスとドライバーのインストール用のエントリを指定するセクションハードウェア プラットフォームです。

詳細については、システム定義を使用する方法についての **.nt**、 **.ntx86**、 **.ntia64**、 **.ntamd64**、 **.ntarm**、および **.ntarm64** 、拡張機能を参照してください[INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](creating-inf-files-for-multiple-platforms-and-operating-systems.md)します。

Windows 2000 以降、ドライバーをインストールする INF ファイルがある必要があります[ **DDInstall.Services** ](inf-ddinstall-services-section.md)セクションでは、レジストリに格納されるデバイスとドライバーのレジストリ情報を指定する **.\\CurrentControlSet\\サービス**ツリー。 デバイスによっては、含めることもできます 1 つまたは複数<em>DDInstall</em>**します。HW**、 <em>DDInstall</em>**します。CoInstallers**、 <em>DDInstall</em>**します。インターフェイス**、や<em>DDInstall</em>**します。LogConfigOverride**セクション。

各ディレクティブを*DDInstall*セクションでは、複数のセクション名を参照できます。 ただし、各追加の名前付きセクションは、コンマ (,) で区切る必要があります。

各セクション名は、INF ファイル内で一意である必要があり、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、次を参照してください。 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)します。

すべて**AddReg**ディレクティブで指定された、 *DDInstall*セクションはについて上限または下限フィルター ドライバーに関する情報を格納するために使用できない追加レジストリ セクションを参照すると見なされます。多機能デバイス、またはについてドライバーに依存しないが、デバイスに固有のパラメーター。 デバイス/ドライバー INF は、この種の情報をレジストリに格納する必要がある場合に、使用する必要があります、 **AddReg**ディレクティブでは、装飾されていないと装飾<em>DDInstall</em>**します。HW**参照別に存在する場合のセクションは INF ライター定義*追加レジストリ セクション*します。

に応じて、[デバイス セットアップ クラス](device-setup-classes.md)に指定されている、 [ **INF バージョン セクション**](inf-version-section.md)で追加のクラスに固有のディレクティブを指定できます、 *DDInstall*セクション。 クラスに固有のディレクティブの詳細については、次のトピックを参照してください。

-   [Windows SideShow と互換性のあるデバイスの INF ファイルを構築](https://docs.microsoft.com/windows-hardware/drivers/)
-   [ネットワークの INF ファイルで DDInstall セクション](https://docs.microsoft.com/windows-hardware/drivers/network/ddinstall-services-section-in-a-network-inf-file)
-   [静止画像デバイスの INF ファイル](https://docs.microsoft.com/windows-hardware/drivers/image/inf-files-for-still-image-devices)
-   [WIA デバイスの INF ファイル](https://docs.microsoft.com/windows-hardware/drivers/image/inf-files-for-wia-devices)
-   [ネットワーク コンポーネントのインストール要件](https://docs.microsoft.com/windows-hardware/drivers/network/installation-requirements-for-network-components)
-   [INF ファイルで WDF ディレクティブの指定](https://docs.microsoft.com/windows-hardware/drivers/wdf/specifying-wdf-directives-in-inf-files)

<a name="examples"></a>使用例
--------

この例の拡張、 *DDInstall*セクションでは、 **Ser_Inst**と**Inp_Inst**します。 これらのセクションの例では参照、 [ **INF*モデル*セクション**](inf-models-section.md)します。

```ini
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

次の例では、プラットフォーム拡張機能を使用する一般的な図を提供します。

```ini
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

次の例は、 *DDInstall*さまざまなオペレーティング システム プラットフォームでデバイスのオーディオ システム提供されている WDM ドライバーをインストールする INF ファイルのセクション。

```ini
[WDMPNPB003_Device.NT]
DriverVer=01/14/1999,5.0
Include=ks.inf, wdmaudio.inf
Needs=KS.Registration, WDMAUDIO.Registration.NT
LogConfig=SB16.LC1,SB16.LC2,SB16.LC3,SB16.LC4,SB16.LC5 
; a few log-config-sections omitted here for brevity
CopyFiles=MSSB16.CopyList
AddReg=WDM_SB16.AddReg
```

次の例は、上の参照セクションでは、**必要がある**システムが指定したエントリ*ks.inf*と*wdmaudio.inf*ファイル。 前の例では、これらのファイルがで指定された、 **Includes**エントリ。 オペレーティング システムのインストーラーのデバイスやメディア クラスのインストーラーがこのデバイスを処理する場合<em>インストール セクション名</em> **.nt**  セクションで、次の 2 つのセクションではこれらをも処理します。

```ini
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

[* **DDInstall *。共同インストーラー**](inf-ddinstall-coinstallers-section.md)

[* **DDInstall*.FactDef**](inf-ddinstall-factdef-section.md)

[* **DDInstall *。ハードウェア**](inf-ddinstall-hw-section.md)

[* **DDInstall *。インターフェイス**](inf-ddinstall-interfaces-section.md)

[* **DDInstall*.LogConfigOverride**](inf-ddinstall-logconfigoverride-section.md)

[* **DDInstall *。サービス**](inf-ddinstall-services-section.md)

[**DefaultInstall**](inf-defaultinstall-section.md)

[**DefaultInstall.Services**](inf-defaultinstall-services-section.md)

[**DelProperty**](inf-delproperty-directive.md)

[**FeatureScore**](inf-featurescore-directive.md)

 

 






