---
title: INF DefaultInstall セクション
description: Inf ファイルの DefaultInstall セクションは、ユーザーが INF ファイル名を右クリックした後に [インストール] メニュー項目を選択した場合にアクセスされます。
ms.assetid: 41412124-38d9-43c0-9954-d34b242a3922
keywords:
- INF DefaultInstall セクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DefaultInstall Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cab49fa5d2250cbf76d9651efe50998b28750da8
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223212"
---
# <a name="inf-defaultinstall-section"></a>INF DefaultInstall セクション


**注**  ユニバーサルまたはモバイルのドライバーパッケージを作成する場合、このセクションは無効であるため、使用しないでください。  代わりに、[ [**INF 製造元] セクション**](inf-manufacturer-section.md)のみを使用してください。  INF で**DefaultInstall**と**Manufacturer**の両方のセクションを使用すると、Universal inf の検証エラーが発生し、インストールの動作に一貫性がなくなる可能性があります。  「[ユニバーサル INF ファイルの使用」を](using-a-universal-inf-file.md)参照してください。

 

Inf ファイルの**DefaultInstall**セクションは、ユーザーが inf ファイル名を右クリックした後に [インストール] メニュー項目を選択した場合にアクセスされます。

```inf
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


<a href="" id="copyfiles--filename---file-list-section--file-list-section-----"></a>**CopyFiles = @**<em>filename</em> | *ファイル-セクション*\[**、**<em>ファイルリスト-セクション</em>\] ...  
この省略可能なディレクティブは、ソースメディアから宛先にコピーする1つの名前付きファイルを指定するか、またはソースメディアから転送先に転送するファイルを指定する1つ以上の INF ライターで定義されたセクションを参照します。

INF の**Destinationdirs**セクションの**DefaultDestDir**エントリは、コピーする1つのファイルのコピー先を指定します。 **Sourcedisksnames**セクションと**Sourcedisksnames**セクション、またはこの Inf**バージョン**セクションの**layoutfile**エントリに指定されている追加の inf は、ドライバーファイルの配布メディア上の場所を提供します。

詳細については、「 [**INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)」を参照してください。

<a href="" id="copyinf-filename1-inf--filename2-inf----"></a>**Copyinf =**<em>filename1</em>**.inf**\[**,**<em>filename2</em>\]**...**  
(Windows XP 以降のバージョンの Windows)。このディレクティブを使用すると、指定した INF ファイルがターゲットシステムにコピーされます。

詳細については、「 [**INF Copyinf ディレクティブ**](inf-copyinf-directive.md)」を参照してください。

<a href="" id="addreg-add-registry-section--add-registry-section----"></a>**AddReg =**<em>registry</em>\[-section **、**<em>add-section</em>\]...  
このディレクティブは、1つまたは複数の INF ライターで定義されたセクションを参照します。このセクションでは、新しいサブキー (場合によっては初期値のエントリを含む) がレジストリに書き込まれるか、既存のキーの値エントリが変更されます。

詳細については、「 [**INF AddReg ディレクティブ**](inf-addreg-directive.md)」を参照してください。

<a href="" id="include-filename1-inf--filename2-inf----"></a>**Include =**<em>filename1</em>**.inf**\[**,**\]<em>filename2</em>**...**  
このオプションのエントリは、このデバイスやドライバーをインストールするために必要なセクションを含む、システムによって提供される追加の1つ以上の INF ファイルを指定します。 このエントリが指定されている場合は、通常、**必要**なエントリです。

たとえば、システムのカーネルストリーミングサポートに依存するデバイスドライバーのシステム INF ファイルでは、次のようにこのエントリを指定します。

```inf
Include= ks.inf[,[kscaptur.inf,][ksfilter.inf]]
```

**インクルード**エントリとその使用に関する制限の詳細については、「[デバイスファイルのソースとターゲットの場所の指定](specifying-the-source-and-target-locations-for-device-files.md)」を参照してください。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**必要な =**<em>inf-name</em>\[**,**<em>inf-name</em>\]...  
この省略可能なエントリは、このデバイスのインストール中に処理する必要がある、システムが提供する INF ファイル内のセクションを指定します。 通常、このような名前付きセクションは、 *ddinstall* (または<em>ddinstall</em>) です **。**<em>xxx</em>)**インクルード**エントリに一覧表示されているいずれかの INF ファイル内のセクション。 ただし、このような*ddinstall*または<em>ddinstall</em>内で参照される任意のセクションを指定でき**ます。** 含まれている INF の<em>xxx</em>セクション。

たとえば、上記の**Include**エントリを含むデバイスドライバーの INF ファイルでは、このエントリを次のように指定します。

```inf
Needs= KS.Registration[,KSCAPTUR.Registration | 
                        KSCAPTUR.Registration.NT,MSPCLOCK.Installation]
```

**必要**なエントリを入れ子にすることはできません。 (**必要**なエントリとその使用に関する制限の詳細については、「[デバイスファイルのソースとターゲットの場所の指定](specifying-the-source-and-target-locations-for-device-files.md)」を参照してください)。

<a href="" id="delfiles-file-list-section--file-list-section----"></a>**Delfiles =**<em>ファイル</em>\[リスト-セクション **、**<em>ファイルリスト-セクション</em>\]...  
このディレクティブは、削除するターゲット上のファイルを一覧表示する1つ以上の INF ライターで定義されたセクションを参照します。

詳細については、「 [**INF DelFiles ディレクティブ**](inf-delfiles-directive.md)」を参照してください。

<a href="" id="renfiles-file-list-section--file-list-section----"></a>**Renfiles =**<em>ファイル</em>\[**,** リスト-<em>セクション-セクション</em>\]...  
このディレクティブは、デバイス関連のソースファイルをターゲットコンピューターにコピーする前に、コピー先で名前を変更する1つ以上の INF ライター定義セクションを参照します。

詳細については、「 [**INF RenFiles ディレクティブ**](inf-renfiles-directive.md)」を参照してください。

<a href="" id="delreg-del-registry-section--del-registry-section----"></a>**Delreg =**<em>del-registry-section</em>\[**,**<em>del-セクション</em>\]...  
このディレクティブは、デバイスのインストール中にレジストリから削除されるキーと値のエントリが指定されている、1つまたは複数の INF ライターで定義されたセクションを参照します。

通常、このディレクティブは、INF がこのデバイスの以前のインストールから古いレジストリエントリをクリーンアップする必要がある場合に、アップグレードを処理するために使用されます。 このような削除レジストリセクションでは、 **Hkr**仕様で **..クラス\\**<em>setupclassguid</em>**\\**<em>デバイスのインスタンス id</em>レジストリパスユーザー補助ドライバー。 この種類の**Hkr**仕様は、とも呼ばれます。 "ソフトウェアキー"。

詳細については、「 [**INF DelReg ディレクティブ**](inf-delreg-directive.md)」を参照してください。

<a href="" id="bitreg-bit-registry-section--bit-registry-section----"></a>**Bitreg =**<em>ビットレジストリ-セクション</em>\[**、**<em>ビットレジストリ-セクション</em>\]...  
このディレクティブは、 [REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)型の既存のレジストリ値のエントリが変更される、1つまたは複数の INF ライターで定義されたセクションを参照します。 詳細については、「 [**INF AddReg ディレクティブ**](inf-addreg-directive.md)」を参照してください。

このようなビットレジストリセクションでは、 **Hkr**仕様で **..クラス\\**<em>setupclassguid</em>**\\**<em>デバイスのインスタンス id</em>レジストリパスユーザー補助ドライバー。 この種類の**Hkr**仕様は、とも呼ばれます。 "ソフトウェアキー"。

詳細については、「 [**INF BitReg ディレクティブ**](inf-bitreg-directive.md)」を参照してください。

<a href="" id="profileitems-profile-items-section--profile-items-section----"></a>**Profileitems =**<em>profile-items-section</em>\[**,**<em>profile-section</em>\]...  
このディレクティブは、[スタート] メニューに追加または削除する項目を記述する1つ以上の INF ライターで定義されたセクションを参照します。

詳細については、「 [**INF ProfileItems ディレクティブ**](inf-profileitems-directive.md)」を参照してください。

<a href="" id="updateinis-update-ini-section--update-ini-section----"></a>**Updateinis =**<em>update-ini</em>\[-section **,**<em>.ini</em>\]...  
使用頻度の低いディレクティブは、1つまたは複数の INF ライターで定義されたセクションを参照しています。この場合、そのセクション内の特定のセクションまたは行を、インストール時に同じ名前の宛先 INI ファイルに読み込むソース INI ファイルを指定します。 必要に応じて、同じ名前の指定したソース INI ファイルから、コピー先の既存の INI ファイルを変更することもできます。これは、.ini セクションで指定できます。

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

<a name="remarks"></a>解説
-------

**DefaultInstall**セクションは、デバイスのインストールには使用できません。 **DefaultInstall**セクションは、デバイスノード (*devnode*) に関連付けられていないクラスフィルタードライバー、クラス共同インストーラー、ファイルシステムフィルター、およびカーネルドライバーサービスのインストールに対してのみ使用してください。

**注**  ドライバーパッケージがデジタル署名されている場合は、[ドライバーパッケージ](driver-packages.md)の inf ファイルに inf **DefaultInstall**セクションを含めないでください。 ドライバーパッケージの署名の詳細については、「[ドライバーの署名](driver-signing.md)」を参照してください。

 

**DefaultInstall**セクションの指定は省略可能です。 INF ファイルに**DefaultInstall**セクションが含まれていない場合は、ファイル名を右クリックして [インストール] を選択すると、エラーメッセージが表示されます。

**注**   [***ddinstall***](inf-ddinstall-section.md)セクションとは異なり、 **DefaultInstall**セクションには[**DriverVer**](inf-driverver-directive.md)または[**logconfig**](inf-logconfig-directive.md)ディレクティブを含めることはできません。

 

*デバイスインストールアプリケーション*から**DefaultInstall**セクションをインストールするには、次の**installhinfsection**呼び出しを使用します。

```inf
InstallHinfSection(NULL,NULL,TEXT("DefaultInstall 132 path-to-inf\infname.inf"),0); 
```

**Installhinfsection**の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

システム定義の**nt**、 **ntx86**、. **ntia64**、. **ntamd64**、. **ntarm**、および**ntarm64**の各拡張機能の使用方法の詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の INF ファイルの作成](creating-inf-files-for-multiple-platforms-and-operating-systems.md)」を参照してください。

<a name="examples"></a>例
--------

次の例は、一般的な**DefaultInstall**セクションを示しています。

```inf
[DefaultInstall]
CopyFiles=MyAppWinFiles, MyAppSysFiles, @SRSutil.exe
AddReg=MyAppRegEntries
```

この例では、ユーザーが INF ファイル名を右クリックした後に [インストール] を選択すると、 **DefaultInstall**セクションが実行されます。

## <a name="see-also"></a>関連項目


[***DDInstall***](inf-ddinstall-section.md)

[**DriverVer**](inf-driverver-directive.md)

[**LogConfig**](inf-logconfig-directive.md)

 

 






