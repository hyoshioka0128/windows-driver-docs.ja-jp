---
title: INF DDInstall.CoInstallers セクション
description: 共同インストーラーのセクションでは、既存のデバイス クラスのインストーラーの操作を補足する 1 つまたは複数のデバイス固有共同インストーラーを登録します。
ms.assetid: 2deb16e1-632a-4169-b718-7e3501e64562
keywords:
- INF DDInstall.CoInstallers セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DDInstall.CoInstallers Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca20eaff3c1cd2635149ffd883b9a1bd9c510adb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557763"
---
# <a name="inf-ddinstallcoinstallers-section"></a>INF DDInstall.CoInstallers セクション


**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このセクションが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

このオプションのセクションでは、1 つまたは複数デバイス固有 co-installer 配布メディアに既存のデバイス クラスのインストーラーの操作を補足する登録します。

```ini
[install-section-name.CoInstallers] |
[install-section-name.nt.CoInstallers] | 
[install-section-name.ntx86.CoInstallers] | 
[install-section-name.ntarm.CoInstallers] | (Windows 8 and later versions of Windows)
[install-section-name.ntarm64.CoInstallers] | (Windows 10 version 1709 and later versions of Windows)
[install-section-name.ntia64.CoInstallers] |  (Windows XP and later versions of Windows)
[install-section-name.ntamd64.CoInstallers]  (Windows XP and later versions of Windows)
  
AddReg=add-registry-section[,add-registry-section]... 
CopyFiles=@filename | file-list-section[,file-list-section]...
[Include=filename.inf[,filename2.inf]...]
[Needs=inf-section-name[,inf-section-name]...]
[DelFiles=file-list-section[,file-list-section]...]
[RenFiles=file-list-section[,file-list-section]...]
[DelReg=del-registry-section[,del-registry-section]...] 
[BitReg=bit-registry-section[,bit-registry-section]...]
[UpdateInis=update-ini-section[,update-ini-section]...]
[UpdateIniFields=update-inifields-section[,update-inifields-section]...]
[Ini2Reg=ini-to-registry-section[,ini-to-registry-section]...]
... 
```

## <a name="entries"></a>エントリ


<a href="" id="addreg-add-registry-section--add-registry-section----"></a>**AddReg=**<em>add-registry-section</em>\[**,**<em>add-registry-section</em>\]...  
1 つを参照またはより INF ライター-定義*追加レジストリ セクション*について指定された共同インストーラー レジストリ情報を格納する s。

**HKR**などで指定された追加レジストリ セクションを指定、 **.クラス\\**<em>SetupClassGUID</em>**\\**<em>デバイス インスタンス id</em>ユーザーがアクセスできるドライバーのレジストリ パスとして別名をします。 「ソフトウェア キー」です。 そのため、デバイスに固有の共同インストーラーをし書き込みます (または変更します)、 **CoInstallers32**このユーザーがアクセスできるデバイス/ドライバー「ソフトウェア」サブキー内のエントリの値します。

クラスに固有の共同インストーラーを適切な内容を変更することによって新しい co-installer を登録 **.CoDeviceInstallers\\**<em>SetupClassGUID</em>サブキー。 適切なレジストリのパス*SetupClassGUID*セクションでは、参照先の追加-レジストリのサブキーを明示的に指定する必要があります。

詳細については、次を参照してください。 [ **INF AddReg ディレクティブ**](inf-addreg-directive.md)します。

<a href="" id="copyfiles--filename---file-list-section--file-list-section----"></a>**CopyFiles=@**<em>filename</em> | *file-list-section*\[**,**<em>file-list-section</em>\]...  
ソース共同インストーラー ファイル転送先に対象のコンピューターに通常 1 つを参照することでより INF ライターの定義または*ファイルのセクション一覧*INF ファイルで別の場所。 このようなファイル リスト セクションでは、ソース メディアから、ターゲットのインストール先ディレクトリにコピーする共同インストーラー ファイルを指定します。

ただし、共同インストーラーをインストールするシステム INF ファイルは、このディレクティブを決してを使用する<em>DDInstall</em>**します。CoInstallers**セクション。

詳細については、次を参照してください。 [ **INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)します。

<a href="" id="include-filename-inf--filename2-inf----"></a>**含める =**<em>filename</em>**.inf**\[**、**<em>filename2</em>**.inf**\]...  
1 つまたは複数追加システムが指定した INF ファイルをこのデバイスの共同インストーラーをインストールするために必要なセクションが含まれているを指定しますまたは[デバイス セットアップ クラス](device-setup-classes.md)します。 通常、このエントリが指定されている場合は、**必要がある**エントリ。 (の詳細については、 **Include**エントリと、その使用に関する制限事項を参照してください。[デバイス ファイルのソースとターゲットの場所を指定する](specifying-the-source-and-target-locations-for-device-files.md))。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**必要な =**<em>inf セクション名</em>\[**、**<em>inf セクション名</em>\].  
このデバイスのインストール中に処理する必要がある特定のセクションを指定します。 通常、このような名前付きセクションは、 <em>DDInstall</em>**します。CoInstallers**セクションに記載されているシステム指定の INF ファイル内で、 **Include**エントリ。 ただし、このような内で参照されている任意のセクションがあります、 <em>DDInstall</em>**します。CoInstallers**の含まれる INF セクション。

**必要がある**エントリを入れ子にすることはできません。 詳細については、**必要がある**エントリと、その使用に関する制限事項を参照してください。[デバイス ファイルのソースとターゲットの場所を指定する](specifying-the-source-and-target-locations-for-device-files.md)します。

<a href="" id="delfiles-file-list-section--file-list-section----"></a>**DelFiles =**<em>ファイルのセクション一覧</em>\[**、**<em>ファイルのセクション一覧</em>\].  
ターゲットから削除するファイルを指定するファイル リスト セクションを参照します。 このディレクティブはほとんど使用されません。

詳細については、次を参照してください。 [ **INF DelFiles ディレクティブ**](inf-delfiles-directive.md)します。

<a href="" id="renfiles-file-list-section--file-list-section----"></a>**RenFiles=**<em>file-list-section</em>\[**,**<em>file-list-section</em>\]...  
共同インストーラーのソース ファイルがターゲットにコピーされる前に名前を変更する変換先のファイルを指定するファイル リスト セクションを参照します。 このディレクティブもほとんど使用しません。

詳細については、次を参照してください。 [ **INF RenFiles ディレクティブ**](inf-renfiles-directive.md)します。

<a href="" id="delreg-del-registry-section--del-registry-section----"></a>**DelReg=**<em>del-registry-section</em>\[**,**<em>del-registry-section</em>\]...  
1 つまたは複数 INF-ライターの定義を参照して*delete-section レジストリ*秒。 このようなセクションでは、レジストリから削除する必要がある同じデバイスの以前のインストールの共同インストーラーに関する古いレジストリ情報を指定します。 **HKR**指定にすでに説明した同じレジストリ サブキーを削除レジストリ セクションなどで指定された、 **AddReg**エントリ。 このディレクティブは使用が非常にまれな<em>DDInstall</em>**します。CoInstallers**セクション。

詳細については、次を参照してください。 [ **INF してディレクティブ**](inf-delreg-directive.md)します。

<a href="" id="bitreg-bit-registry-section--bit-registry-section----"></a>**BitReg =**<em>ビットのレジストリ セクション</em>\[**、**<em>ビットのレジストリ セクション</em>\].  
このエントリでは、このセクションでは有効ですが、ほとんど使用されません。 **HKR**などで指定されたビット レジストリ セクション指定と同じレジストリ サブキーの既に説明したとおり、 **AddReg**エントリ。

詳細については、次を参照してください。 [ **INF BitReg ディレクティブ**](inf-bitreg-directive.md)します。

<a href="" id="updateinis-update-ini-section--update-ini-section----"></a>**UpdateInis =**<em>update-section ini</em>\[**、**<em>update-section ini</em>\].  
このエントリでは、このセクションでは有効ですが、ほとんど使用されません。

詳細については、次を参照してください。 [ **INF UpdateInis ディレクティブ**](inf-updateinis-directive.md)します。

<a href="" id="updateinifields-update-inifields-section--update-inifields-section----"></a>**UpdateIniFields =**<em>update-section inifields</em>\[**、**<em>update-section inifields</em>\].  
このエントリでは、このセクションでは有効ですが、ほとんど使用されません。

詳細については、次を参照してください。 [ **INF UpdateIniFields ディレクティブ**](inf-updateinifields-directive.md)します。

<a href="" id="ini2reg-ini-to-registry-section--ini-to-registry-section----"></a>**Ini2Reg =**<em>セクション レジストリ ini</em>\[**、**<em>セクション レジストリ ini</em>\].  
このエントリでは、このセクションでは有効ですが、ほとんど使用されません。

詳細については、次を参照してください。 [ **INF Ini2Reg ディレクティブ**](inf-ini2reg-directive.md)します。

<a name="remarks"></a>注釈
-------

指定した*DDInstall* - 製造元でデバイス/モデルに固有のエントリでは、セクションを参照する必要があります*モデル*INF ファイルのセクション。

INF が含まれている場合、 <em>DDInstall</em>**します。Coinstallers**セクションで、必要がありますいずれかのプラットフォームで修飾された、装飾されていない各*DDInstall*セクション。 たとえば、INF、含まれている場合、 **\[**<em>インストール セクション名</em>**.ntx86\]** セクションおよび **\[**<em>インストール セクション名</em>**\]** セクションと、デバイスに固有の co-installer を登録しますその後、INF は、両方を含める必要があります、  **。\[**<em>インストール セクション名</em>**.ntx86 します。Coinstallers\]** セクションおよび**\[**<em>インストール セクション名</em>**します。Coinstallers\]** セクション。 詳細については、システム定義を使用する方法についての **.nt**、 **.ntx86**、 **.ntia64**、 **.ntamd64**、 **.ntarm**、および **.ntarm64** 、拡張機能を参照してください[INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](creating-inf-files-for-multiple-platforms-and-operating-systems.md)します。

各ディレクティブを<em>DDInstall</em>**します。CoInstallers**セクションは、1 つ以上の INF ライター定義セクション名を参照できます。 ただし、各追加の名前付きセクションは、コンマ (,) で区切る必要があります。

各セクションのディレクティブが作成した名前は、INF ファイル内で一意である必要があり、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、次を参照してください。 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)します。

共同インストーラーは、する通常のレジストリに追加の構成情報を書き込むか、つまり使用できない、INF の作成時に動的に生成された、システム固有の情報を必要とするその他のインストール タスクを実行する Win32 DLL です。 デバイスに固有の共同インストーラーは、そのデバイスがインストールされている場合に、OS のデバイスのインストーラーのか、適切なクラスのインストーラーのインストールの操作を補足します。

書き込みと共同インストーラーを使用する方法の詳細については、次を参照してください。[共同インストーラーの作成](writing-a-co-installer.md)です。

### <a name="installing-co-installer-images"></a>共同インストーラー イメージのインストール

すべての共同インストーラー ファイルをコピーする必要があります、 *%systemroot%\\system32*ディレクトリ。 などの任意の INF **CopyFiles**操作、変換先が明示的に制御を名前付き*ファイルのセクション一覧*で、 [ **DestinationDirs** ](inf-destinationdirs-section.md)によって INF ファイルのセクション、 *dirid*値**11**またはこれを指定して*dirid*値、 **DefaultDestDir**エントリ。

### <a name="registering-device-specific-co-installers"></a>デバイスに固有の co-installer を登録します。

1 つまたは複数のデバイスに固有の共同インストーラーを登録する場合は、追加する必要があります、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-レジストリへのエントリの値を入力します。 指定、*追加レジストリ セクション*によって参照される、 [ **AddReg** ](inf-addreg-directive.md)ディレクティブを次の一般的な形式を使用しています。

```ini
[DDInstall.CoInstallers_DeviceAddReg]
 
HKR,,CoInstallers32,0x00010000,"DevSpecificCoInstall.dll
   [,DevSpecificEntryPoint]"[,"DevSpecific2CoInstall.dll
      [,DevSpecific2EntryPoint]"...] 
```

**HKR**エントリが、INF ファイル内の単一行として表示されており、各指定されたデバイスに応じた共同インストーラー DLL は、一意の名前をいる必要があります。 表示されている共同インストーラーが登録されると、システムのデバイスのインストーラー呼び出し元のインストール プロセスの以降の各ステップでそのデバイスの。

場合、省略可能な*DevSpecificEntryPoint*を省略すると、既定の**CoDeviceInstall**ルーチンの名前は、共同インストーラー DLL のエントリ ポイントとして使用されます。

詳細については、次を参照してください。[登録デバイスに固有の共同インストーラー](registering-a-device-specific-co-installer.md)します。

### <a name="registering-device-class-co-installers"></a>デバイス クラス co-installer を登録します。

値エントリ (とそれが既に存在しない場合、セットアップ クラス サブキー) を追加する、レジストリへの 1 つまたは複数のデバイス クラス co-installer を*追加レジストリ セクション*によって参照される、 [ **AddReg**](inf-addreg-directive.md)ディレクティブは、次の一般的な形式。

```ini
[DDInstall.CoInstallers_ClassAddReg]
 
HKLM,System\CurrentControlSet\Control
    \CoDeviceInstallers,{SetupClassGUID},
       0x00010008,"DevClssCoInst.dll[,DevClssEntryPoint]" 
 ...
```

このような追加のレジストリ セクション内の各エントリが、INF ファイル内の単一行として表示され、各クラスの指定された共同インストーラー DLL は、一意の名前をいる必要があります。 1 つ以上の指定された共同インストーラーを使用する場合[デバイス セットアップ クラス](device-setup-classes.md)、この追加レジストリ セクションはそれぞれ、適切な 1 つ以上のエントリを持つことができます*SetupClassGUID*値。

このような追加のデバイス クラス共同インストーラーは、既存のクラスのインストーラーの場合は、既に登録されている共同インストーラーを置き換えるいない必要があります。 そのため、クラスの共同インストーラーが一意の名前をいる必要があります、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-指定した型の値を追加する必要があります (によって示される、 **8**で、*フラグ*値**0x0010008**) 共同インストーラーをクラスに固有のエントリに存在する場合、既にに存在する、 **{**<em>SetupClassGUID</em>**}** サブキー。

**注**、 [SetupAPI](setupapi.md)関数は重複することはありません追加<em>DevClssCoInstall</em>**.dll**同じ名前の共同インストーラーが既にある場合、値のエントリを登録されています。

 

右クリックしてインストールして、または呼び出しを通じて、補足のデバイス クラスの共同インストーラーの INF をアクティブにできる**SetupInstallFromInfSection**します。

<a name="examples"></a>例
--------

この例では、 *DDInstall*.**CoInstallers** IrDA シリアルのネットワーク アダプターのセクション。 これらの IrDA (シリアル) Nic のシステム提供の INF には、システム IrDA クラスのインストーラーに共同インストーラーが用意されています。

```ini
; DDInstall section
[PNP.NT]
AddReg=ISIR.reg, Generic.reg, Serial.reg
PromptForPort=0     ; This is handled by IRCLASS.DLL
LowerFilters=SERIAL ; This is handled by IRCLASS.DLL
BusType=14
Characteristics=0x4 ; NCF_PHYSICAL 

; ... PNP.NT.Services section omitted here
[PNP.NT.CoInstallers]
AddReg = ISIR.CoInstallers.reg 
; ...

[IRSIR.reg]
HKR, Ndi, HelpText, 0, %IRSIR.Help%
HKR, Ndi, Service, 0, "IRSIR"
HKR, Ndi\Interfaces, DefUpper, 0, "ndisirda"
HKR, Ndi\Interfaces, DefLower, 0, "nolower"
HKR, Ndi\Interfaces, UpperRange, 0, "ndisirda"
HKR, Ndi\Interfaces, LowerRange, 0, "nolower"

[Generic.reg]
HKR,,InfraredTransceiverType,0,"0"

[Serial.reg]
HKR,,SerialBased,0, "0"

[ISIR.CoInstallers.reg]
HKR,,CoInstallers32,0x00010000,"IRCLASS.dll,IrSIRClassCoInstaller"

; ... Services and Event Log registry sections omitted here
[Strings]
; ...
IRSIR.Help = "An IrDA serial infrared device is a built-in COM port or 
external transceiver which transmits infrared pulses. This NDIS 
miniport driver installs as a network adapter and binds to the FastIR 
protocol."
```

上記の PNP<strong>します。NT します。CoInstallers</strong>セクションは、共同 installer 固有のみ参照*追加レジストリ*セクション。 ある[ **CopyFiles** ](inf-copyfiles-directive.md)ディレクティブにこのシステムが指定した INF ためには、一連のネットワーク デバイスの IrDA をインストールします。 この INF ファイルを使用して、すべてのシステム INF ファイルと同様、 **LayoutFile**エントリでその[**バージョン**](inf-version-section.md)共同インストーラー ファイルを先に転送するセクション。

注意<em>DDInstall</em>**します。CoInstallers** 、IHV および OEM によって提供される、INF セクションがあります、 **CopyFiles**ディレクティブと共に、 [ **SourceDisksNames** ](inf-sourcedisksnames-section.md)と[ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)セクション。

## <a name="see-also"></a>関連項目


[**AddReg**](inf-addreg-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[**DelFiles**](inf-delfiles-directive.md)

[**DelReg**](inf-delreg-directive.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**Ini2Reg**](inf-ini2reg-directive.md)

[**RenFiles**](inf-renfiles-directive.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**UpdateIniFields**](inf-updateinifields-directive.md)

**UpdateInis**
[**バージョン**](inf-version-section.md)

 

 






