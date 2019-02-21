---
title: INF DefaultInstall セクション
description: INF ファイルの DefaultInstall セクションは、INF ファイル名を右クリックして、"Install"メニュー項目を選択した場合にアクセスします。
ms.assetid: 41412124-38d9-43c0-9954-d34b242a3922
keywords:
- INF DefaultInstall セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DefaultInstall Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e88d0693ed72ea338b7a7287838bb9b7d168bb17
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551100"
---
# <a name="inf-defaultinstall-section"></a>INF DefaultInstall セクション


**注**  ここでは無効ですしユニバーサルまたはモバイルのドライバー パッケージを作成する場合は使用できません。  代わりに、のみを使用して、 [ **INF 製造元セクション**](inf-manufacturer-section.md)します。  両方を使用して**DefaultInstall**と**製造元**セクションでは、INF でユニバーサル INF 検証エラーが発生し、一貫性のないインストールの動作につながることができます。  参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

INF ファイルの**DefaultInstall** INF ファイル名を右クリックして、"Install"メニュー項目を選択した場合、セクションにアクセスします。

```ini
[DefaultInstall] | 
[DefaultInstall.nt] | 
[DefaultInstall.ntx86] | 
[DefaultInstall.ntarm] | (Windows 8 and later versions of Windows)
[DefaultInstall.ntarm64]  (Windows 10 version 1709 and later versions of Windows)
[DefaultInstall.ntia64] | (Windows XP and later versions of Windows)
[DefaultInstall.ntamd64]  (Windows XP and later versions of Windows)
 
[CopyFiles=@filename | file-list-section[,file-list-section] ...]
[CopyINF=filename1.inf[,filename2.inf]...]
[AddReg=add-registry-section[,add-registry-section]...]
[Include=filename1.inf[,filename2.inf]...]
[Needs=inf-section-name[,inf-section-name]...]
[Delfiles=file-list-section[,file-list-section]...]
[Renfiles=file-list-section[,file-list-section]...]
[DelReg=del-registry-section[,del-registry-section]...]
[BitReg=bit-registry-section[,bit-registry-section]...]
[ProfileItems=profile-items-section[,profile-items-section]...]
[UpdateInis=update-ini-section[,update-ini-section]...]
[UpdateIniFields=update-inifields-section[,update-inifields-section]...]
[Ini2Reg=ini-to-registry-section[,ini-to-registry-section]...]
[RegisterDlls=register-dll-section[,register-dll-section]...]
[UnregisterDlls=unregister-dll-section[,unregister-dll-section]...] ...
```

## <a name="entries"></a>エントリ


<a href="" id="copyfiles--filename---file-list-section--file-list-section-----"></a>**CopyFiles=@**<em>filename</em> | *file-list-section*\[**,**<em>file-list-section</em>\] ...  
この省略可能なディレクティブは先に、ソース メディアからコピーされる 1 つの名前付きファイルを指定します。 または、1 つまたは複数 INF ライター定義のセクションでは、ソース メディアから先に転送するファイルを指定するを参照します。

**DefaultDestDir**内のエントリ、 **DestinationDirs** INF のセクションがコピーされる 1 つのファイルの保存先を指定します。 **SourceDisksNames**と**SourceDisksFiles**セクション、またはで指定された追加の INF、 **LayoutFile**エントリのこの INF の**バージョン**セクションで、ドライバー ファイルの配布メディアの場所を指定します。

詳細については、次を参照してください。 [ **INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)します。

<a href="" id="copyinf-filename1-inf--filename2-inf----"></a>**CopyINF =**<em>filename1</em>**.inf**\[**、**<em>filename2</em>**.inf**\]...  
(Windows XP および Windows の以降のバージョン。)このディレクティブは、ターゲット システムにコピーする INF ファイルを指定します。

詳細については、次を参照してください。 [ **INF CopyINF ディレクティブ**](inf-copyinf-directive.md)します。

<a href="" id="addreg-add-registry-section--add-registry-section----"></a>**AddReg=**<em>add-registry-section</em>\[**,**<em>add-registry-section</em>\]...  
このディレクティブは、1 つまたは複数 INF ライター定義のセクションでは新しいサブキー、場合によっては、初期値エントリで指定されているまたは既存のキーの値のエントリが変更されたレジストリに書き込まれるを参照します。

詳細については、次を参照してください。 [ **INF AddReg ディレクティブ**](inf-addreg-directive.md)します。

<a href="" id="include-filename1-inf--filename2-inf----"></a>**含める =**<em>filename1</em>**.inf**\[**、**<em>filename2</em>**.inf**\]...  
この省略可能なエントリでは、1 つまたは複数追加システムが指定した INF ファイルをこのデバイスやドライバーをインストールするために必要なセクションが含まれているを指定します。 通常、このエントリが指定されている場合は、**必要がある**エントリ。

たとえば、このエントリが次のよう指定、システムのカーネル ストリーミング サポートに依存しているデバイス ドライバー用のシステム INF ファイル。

```ini
Include= ks.inf[,[kscaptur.inf,][ksfilter.inf]]
```

詳細については、 **Include**エントリと、その使用に関する制限事項を参照してください。[デバイス ファイルのソースとターゲットの場所を指定する](specifying-the-source-and-target-locations-for-device-files.md)します。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**必要な =**<em>inf セクション名</em>\[**、**<em>inf セクション名</em>\].  
この省略可能なエントリでは、このデバイスのインストール中に処理する必要があるシステム提供の INF ファイル内のセクションを指定します。 通常、このような名前付きセクションは、 *DDInstall* (または<em>DDInstall</em>**.**<em>xxx</em>) 内に記載されている INF ファイルの 1 つのセクション、 **Include**エントリ。 ただし、このような内で参照されている任意のセクションがあります、 *DDInstall*または<em>DDInstall</em>**.**<em>xxx</em>の含まれる INF セクション。

上記のあるデバイス ドライバーの INF ファイルなど、 **Include**エントリは次のようにこのエントリを指定します。

```ini
Needs= KS.Registration[,KSCAPTUR.Registration | 
                        KSCAPTUR.Registration.NT,MSPCLOCK.Installation]
```

**必要がある**エントリを入れ子にすることはできません。 (の詳細については、**必要がある**エントリと、その使用に関する制限事項を参照してください。[デバイス ファイルのソースとターゲットの場所を指定する](specifying-the-source-and-target-locations-for-device-files.md))。

<a href="" id="delfiles-file-list-section--file-list-section----"></a>**Delfiles =**<em>ファイルのセクション一覧</em>\[**、**<em>ファイルのセクション一覧</em>\].  
このディレクティブは、1 つまたは複数 INF ライター定義のセクションでは削除するターゲット上のファイルの一覧を参照します。

詳細については、次を参照してください。 [ **INF DelFiles ディレクティブ**](inf-delfiles-directive.md)します。

<a href="" id="renfiles-file-list-section--file-list-section----"></a>**Renfiles =**<em>ファイルのセクション一覧</em>\[**、**<em>ファイルのセクション一覧</em>\].  
このディレクティブは、1 つまたは複数 INF ライター定義のセクションではデバイスに関連するソース ファイルがターゲット コンピューターにコピーされる前に、変換先の名前を変更するファイルのリストを参照します。

詳細については、次を参照してください。 [ **INF RenFiles ディレクティブ**](inf-renfiles-directive.md)します。

<a href="" id="delreg-del-registry-section--del-registry-section----"></a>**DelReg=**<em>del-registry-section</em>\[**,**<em>del-registry-section</em>\]...  
このディレクティブは、1 つまたは複数 INF ライター定義のセクションでは、デバイスのインストール中に、レジストリから削除するエントリを指定では、どのキーと値を参照します。

通常、このディレクティブは、INF は、このデバイスの以前のインストールからの古いレジストリ エントリをクリーンアップする必要がありますと、アップグレードを処理するために使用します。 **HKR** delete レジストリ セクション内の指定を指定、 **.クラス\\**<em>SetupClassGUID</em>**\\**<em>デバイス インスタンス id</em>ユーザーからアクセス可能なドライバーのレジストリ パス。 この種類の**HKR**仕様とも呼ばれる、します。 「ソフトウェア キー」です。

詳細については、次を参照してください。 [ **INF してディレクティブ**](inf-delreg-directive.md)します。

<a href="" id="bitreg-bit-registry-section--bit-registry-section----"></a>**BitReg =**<em>ビットのレジストリ セクション</em>\[**、**<em>ビットのレジストリ セクション</em>\].  
このディレクティブは、1 つまたは複数 INF ライター定義を既存のレジストリ値のエントリの型のセクションを参照[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)変更されます。 詳細については、次を参照してください。 [ **INF AddReg ディレクティブ**](inf-addreg-directive.md)します。

**HKR**ビット レジストリのセクションで仕様を指定、 **.クラス\\**<em>SetupClassGUID</em>**\\**<em>デバイス インスタンス id</em>ユーザーからアクセス可能なドライバーのレジストリ パス。 この種類の**HKR**仕様とも呼ばれる、します。 「ソフトウェア キー」です。

詳細については、次を参照してください。 [ **INF BitReg ディレクティブ**](inf-bitreg-directive.md)します。

<a href="" id="profileitems-profile-items-section--profile-items-section----"></a>**ProfileItems =**<em>プロファイル-section 項目</em>\[**、**<em>プロファイル-section 項目</em>\].  
このディレクティブは、1 つまたは複数 INF ライター定義のセクションでは追加、または [スタート] メニューから削除する項目を説明するを参照します。

詳細については、次を参照してください。 [ **INF ProfileItems ディレクティブ**](inf-profileitems-directive.md)します。

<a href="" id="updateinis-update-ini-section--update-ini-section----"></a>**UpdateInis =**<em>update-section ini</em>\[**、**<em>update-section ini</em>\].  
使用頻度の低いこのディレクティブは、1 つを参照またはソース INI を指定する、多くの INF ライター定義セクションのファイルから特定のセクションまたはこのようなセクション内の行のインストール時に、同じ名前の変換先の INI ファイルに読み込むことができます。 必要に応じて、同じ名前の指定したソースの INI ファイルからの先に既存の INI ファイルの変更の 1 行ずつ更新 ini セクションで指定できます。

詳細については、次を参照してください。 [ **INF UpdateInis ディレクティブ**](inf-updateinis-directive.md)します。

<a href="" id="updateinifields-update-inifields-section--update-inifields-section----"></a>**UpdateIniFields =**<em>update-section inifields</em>\[**、**<em>update-section inifields</em>\].  
使用頻度の低いこのディレクティブは、1 つまたは複数 INF ライター定義のセクションでは、デバイスに固有の INI ファイルの行を内の変更を指定するを参照します。

詳細については、次を参照してください。 [ **INF UpdateIniFields ディレクティブ**](inf-updateinifields-directive.md)します。

<a href="" id="ini2reg-ini-to-registry-section--ini-to-registry-section----"></a>**Ini2Reg =**<em>セクション レジストリ ini</em>\[**、**<em>セクション レジストリ ini</em>\].  
これは、ディレクティブの参照セクションまたは、ソース メディアに、デバイスに固有の INI ファイルの行は 1 つまたは複数のライター定義 INF セクションは、レジストリに移動するのにはほとんど使用されません。

詳細については、次を参照してください。 [ **INF Ini2Reg ディレクティブ**](inf-ini2reg-directive.md)します。

<a href="" id="registerdlls-register-dll-section--register-dll-section----"></a>**RegisterDlls =**<em>レジスタ-section dll</em>\[**、**<em>レジスタ-section dll</em>\].  
このディレクティブは、OLE コントロールは、自己登録を必要とするファイルを指定するために使用する 1 つまたは複数の INF セクションを参照します。

詳細については、次を参照してください。 [ **INF RegisterDlls ディレクティブ**](inf-registerdlls-directive.md)します。

<a href="" id="unregisterdlls-unregister-dll-section--unregister-dll-section----"></a>**UnregisterDlls =**<em>の登録を解除 dll セクション</em>\[**、**<em>の登録を解除 dll セクション</em>\].  
このディレクティブは、OLE コントロールは、(自己の削除) を自己登録解除を必要とするファイルを指定するために使用する 1 つまたは複数の INF セクションを参照します。

詳細については、次を参照してください。 [ **INF UnregisterDlls ディレクティブ**](inf-unregisterdlls-directive.md)します。

<a name="remarks"></a>注釈
-------

**DefaultInstall**デバイスのインストール用のセクションでは使用しないでください。 使用**DefaultInstall**クラスをインストールするためだけのセクションではドライバー、クラスの共同インストーラー、ファイル システム フィルター、およびデバイス ノードに関連付けられているサービスをカーネル ドライバーをフィルター処理 (*devnode*).

**注**  、INF ファイルの[ドライバー パッケージ](driver-packages.md)、INF を含めることはできません**DefaultInstall**セクションへのデジタル署名のドライバー パッケージがある場合。 ドライバー パッケージに署名に関する詳細については、次を参照してください。[ドライバーの署名](driver-signing.md)します。

 

提供する、 **DefaultInstall**セクションは省略可能です。 INF ファイルが含まれていない場合、 **DefaultInstall**  セクションで、表示されるエラー メッセージ、ファイル名を右クリックしてにより発生した後に「インストール」を選択します。

**注**  とは異なり、 [ ***DDInstall*** ](inf-ddinstall-section.md) ] セクションで、 **DefaultInstall**セクションを含めることはできません[ **DriverVer** ](inf-driverver-directive.md)または[ **LogConfig** ](inf-logconfig-directive.md)ディレクティブ。

 

インストールする、 **DefaultInstall**セクションから、*デバイス インストール アプリケーション*、に対する次の呼び出しを使用して、 **InstallHinfSection**:

```ini
InstallHinfSection(NULL,NULL,TEXT("DefaultInstall 132 path-to-inf\infname.inf"),0); 
```

詳細については**InstallHinfSection**、Microsoft Windows SDK のドキュメントを参照してください。

詳細については、システム定義を使用する方法についての **.nt**、 **.ntx86**、 **.ntia64**、 **.ntamd64**、 **.ntarm**、および **.ntarm64** 、拡張機能を参照してください[INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](creating-inf-files-for-multiple-platforms-and-operating-systems.md)します。

<a name="examples"></a>例
--------

次の例は、一般的な**DefaultInstall**セクション。

```ini
[DefaultInstall]
CopyFiles=MyAppWinFiles, MyAppSysFiles, @SRSutil.exe
AddReg=MyAppRegEntries
```

この例で、 **DefaultInstall**セクション INF ファイル名を右クリックしてユーザーが [インストール] を選択した場合に実行されます。

## <a name="see-also"></a>関連項目


[***DDInstall***](inf-ddinstall-section.md)

[**DriverVer**](inf-driverver-directive.md)

[**LogConfig**](inf-logconfig-directive.md)

 

 






