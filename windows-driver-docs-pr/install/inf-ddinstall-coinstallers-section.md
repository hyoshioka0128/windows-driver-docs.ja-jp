---
title: INF DDInstall.CoInstallers セクション
description: CoInstallers セクションでは、1つまたは複数のデバイス固有の共同インストーラーを登録して、既存のデバイスクラスインストーラーの操作を補足します。
ms.assetid: 2deb16e1-632a-4169-b718-7e3501e64562
keywords:
- INF DDInstall. CoInstallers セクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DDInstall.CoInstallers Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88b6e3b29fd2b2081b19ad8117cda330ddb50777
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223260"
---
# <a name="inf-ddinstallcoinstallers-section"></a>INF DDInstall.CoInstallers セクション


**注**  ユニバーサルまたはモバイルのドライバーパッケージを作成する場合、このセクションは無効です。 「[ユニバーサル INF ファイルの使用」を](using-a-universal-inf-file.md)参照してください。

 

この省略可能なセクションでは、配布メディアに提供されている1つまたは複数のデバイス固有の共同インストーラーを登録して、既存のデバイスクラスインストーラーの操作を補足します。

```inf
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


<a href="" id="addreg-add-registry-section--add-registry-section----"></a>**AddReg =**<em>registry</em>\[-section **、**<em>add-section</em>\]...  
指定された共同インストーラーに関するレジストリ情報を格納する、1つまたは複数の INF ライターで定義された*レジストリセクション*を参照します。

このような add registry セクションで指定された**Hkr**は **..クラス\\**<em>setupclassguid</em>**\\**<em>デバイス id</em>レジストリパス (とも呼ばれます) のユーザー補助可能なドライバー。 "ソフトウェアキー"。 そのため、デバイス固有の共同インストーラーでは、このユーザーがアクセスできるデバイスごとの "ソフトウェア" サブキーの**CoInstallers32** value エントリを書き込み (または変更) します。

クラス固有の共同インストーラーでは、適切なの内容を変更することによって新しい共同インストーラーを登録し**ます。Codeviceinstallers\\**<em>setupclassguid</em>サブキー。 適切なレジストリ*Setupclassguid*サブキーのパスは、参照されるレジストリセクションで明示的に指定する必要があります。

詳細については、「 [**INF AddReg ディレクティブ**](inf-addreg-directive.md)」を参照してください。

<a href="" id="copyfiles--filename---file-list-section--file-list-section----"></a>**CopyFiles = @**<em>filename</em> | *ファイル-セクション*\[**、**<em>ファイルリスト-セクション</em>\]...  
ソースの共同インストーラーファイルを対象のコンピューター上の宛先に転送します。通常は、INF ファイル内の他の場所にある1つまたは複数の INF ライターで定義された*ファイルリストセクション*を参照します。 このようなファイルリストセクションでは、ソースメディアからターゲットの宛先ディレクトリにコピーされる共同インストーラーファイルを指定します。

ただし、共同インストーラーをインストールするシステム INF ファイルでは、 <em>ddinstall</em>でこのディレクティブを使用することはありません **。CoInstallers**セクション。

詳細については、「 [**INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)」を参照してください。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include =**<em>filename</em>**. .inf**\[**,**<em>filename2</em>**.inf**\]...  
このデバイスまたは[デバイスセットアップクラス](device-setup-classes.md)の共同インストーラーをインストールするために必要なセクションを含む、追加のシステム提供の INF ファイルを1つ以上指定します。 このエントリが指定されている場合は、通常、**必要**なエントリです。 (**インクルード**エントリとその使用に関する制限の詳細については、「[デバイスファイルのソースとターゲットの場所の指定](specifying-the-source-and-target-locations-for-device-files.md)」を参照してください)。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**必要な =**<em>inf-name</em>\[**,**<em>inf-name</em>\]...  
このデバイスのインストール中に処理する必要がある特定のセクションを指定します。 通常、このような名前付きセクションは、 <em>Ddinstall</em>**です。****インクルード**エントリに一覧表示されているシステム提供の INF ファイル内の CoInstallers セクション。 ただし、このような<em>Ddinstall</em>内で参照される任意のセクションを指定でき**ます。** インクルードされている INF の CoInstallers セクション。

**必要**なエントリを入れ子にすることはできません。 **必要**なエントリとその使用に関する制限の詳細については、「[デバイスファイルのソースとターゲットの場所の指定](specifying-the-source-and-target-locations-for-device-files.md)」を参照してください。

<a href="" id="delfiles-file-list-section--file-list-section----"></a>**Delfiles =**<em>ファイル</em>\[リスト-セクション **、**<em>ファイルリスト-セクション</em>\]...  
ターゲットから削除するファイルを指定するファイルリストセクションを参照します。 このディレクティブはほとんど使用されません。

詳細については、「 [**INF DelFiles ディレクティブ**](inf-delfiles-directive.md)」を参照してください。

<a href="" id="renfiles-file-list-section--file-list-section----"></a>**RenFiles =**<em>ファイル</em>\[**,** リスト-<em>セクション-セクション</em>\]...  
共同インストーラーのソースファイルがターゲットにコピーされる前に、名前を変更するファイルを指定するファイルリストセクションを参照します。 このディレクティブも使用されることはほとんどありません。

詳細については、「 [**INF RenFiles ディレクティブ**](inf-renfiles-directive.md)」を参照してください。

<a href="" id="delreg-del-registry-section--del-registry-section----"></a>**Delreg =**<em>del-registry-section</em>\[**,**<em>del-セクション</em>\]...  
1つまたは複数の INF ライター定義の削除を参照します *-section*s。 このセクションでは、レジストリから削除する必要がある、同じデバイスの以前のインストールの共同インストーラーに関する古いレジストリ情報を指定します。 このような delete registry セクションで指定された**Hkr**は、 **AddReg**エントリに対して既に説明したものと同じレジストリサブキーを指定します。 このディレクティブは、 <em>Ddinstall</em>ではほとんど使用され**ません。CoInstallers**セクション。

詳細については、「 [**INF DelReg ディレクティブ**](inf-delreg-directive.md)」を参照してください。

<a href="" id="bitreg-bit-registry-section--bit-registry-section----"></a>**Bitreg =**<em>ビットレジストリ-セクション</em>\[**、**<em>ビットレジストリ-セクション</em>\]...  
このエントリは、このセクションでは有効ですが、ほとんど使用されません。 このようなビットレジストリセクションで指定されている**Hkr**は、 **AddReg**エントリに対して既に説明したものと同じレジストリサブキーを指定します。

詳細については、「 [**INF BitReg ディレクティブ**](inf-bitreg-directive.md)」を参照してください。

<a href="" id="updateinis-update-ini-section--update-ini-section----"></a>**Updateinis =**<em>update-ini</em>\[-section **,**<em>.ini</em>\]...  
このエントリは、このセクションでは有効ですが、ほとんど使用されません。

詳細については、「 [**INF UpdateInis ディレクティブ**](inf-updateinis-directive.md)」を参照してください。

<a href="" id="updateinifields-update-inifields-section--update-inifields-section----"></a>**UpdateIniFields =**<em>inifields-section</em>\[**,**<em>inifields-section</em>\]...  
このエントリは、このセクションでは有効ですが、ほとんど使用されません。

詳細については、「 [**INF UpdateIniFields ディレクティブ**](inf-updateinifields-directive.md)」を参照してください。

<a href="" id="ini2reg-ini-to-registry-section--ini-to-registry-section----"></a>**Ini2Reg =**<em>ini</em>\[-セクション **、**<em>ini からレジストリへ</em>\]のセクション...  
このエントリは、このセクションでは有効ですが、ほとんど使用されません。

詳細については、「 [**INF Ini2Reg ディレクティブ**](inf-ini2reg-directive.md)」を参照してください。

<a name="remarks"></a>解説
-------

指定された*Ddinstall*セクションは、INF ファイルの "製造元別*モデル*" セクションのデバイス/モデル固有のエントリで参照されている必要があります。

INF に<em>Ddinstall</em>が含まれている場合 **。Coinstallers**セクションでは、プラットフォームによって修飾された非装飾的な*ddinstall*セクションごとに1つのが必要です。 **\[** たとえば、inf に**ntx86\] **セクション**\]** **\[** と**\[** <em>install セクション名</em><em>セクションが含ま</em>れていて、デバイス固有の共同インストーラーが登録されている場合、inf には ntx86 の両方が含まれている必要が<em>あります。</em>**Coinstallers\] **セクションと**\[**<em>インストールセクション名</em>を指定**します。Coinstallers\] **セクション。 システム定義の**nt**、 **ntx86**、. **ntia64**、. **ntamd64**、. **ntarm**、および**ntarm64**の各拡張機能の使用方法の詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の INF ファイルの作成](creating-inf-files-for-multiple-platforms-and-operating-systems.md)」を参照してください。

<em>Ddinstall</em>の各ディレクティブ **。CoInstallers** section は、複数の INF ライターで定義されたセクション名を参照できます。 ただし、追加の名前付きセクションは、それぞれコンマ (,) で区切られている必要があります。

各ディレクティブで作成されたセクション名は、INF ファイル内で一意である必要があります。また、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

共同インストーラーは、通常、追加の構成情報をレジストリに書き込むか、または INF の作成時には利用できないシステム固有の情報を動的に生成する必要があるその他のインストールタスクを実行する Win32 DLL です。 デバイス固有の共同インストーラーによって、OS のデバイスインストーラーまたはデバイスのインストール時に適切なクラスインストーラーのいずれかのインストール操作が補完されます。

共同インストーラーの記述方法と使用方法の詳細については、「[共同インストーラーの記述](writing-a-co-installer.md)」を参照してください。

### <a name="installing-co-installer-images"></a>共同インストーラーイメージのインストール

すべての共同インストーラーファイルを *% SystemRoot%\\system32*ディレクトリにコピーする必要があります。 INF の**CopyFiles**操作と同様に、出力先は inf ファイルの[**destinationdirs**](inf-destinationdirs-section.md)セクションにある名前付き*ファイルリストセクション*に対して、 *dirid*値**11**またはこの*dirid*値を**DefaultDestDir**エントリに指定することによって明示的に制御されます。

### <a name="registering-device-specific-co-installers"></a>デバイス固有の共同インストーラーの登録

1つ以上のデバイス固有の共同インストーラーを登録するには、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)型の値のエントリをレジストリに追加する必要があります。 次の一般的な形式を使用して、 [**AddReg**](inf-addreg-directive.md)ディレクティブで参照される*レジストリの追加セクション*を指定します。

```inf
[DDInstall.CoInstallers_DeviceAddReg]
 
HKR,,CoInstallers32,0x00010000,"DevSpecificCoInstall.dll
   [,DevSpecificEntryPoint]"[,"DevSpecific2CoInstall.dll
      [,DevSpecific2EntryPoint]"...] 
```

**Hkr**エントリは INF ファイル内の単一行として一覧表示され、各デバイス固有の共同インストーラー DLL には一意の名前を付ける必要があります。 リストされている共同インストーラーが登録されると、システムのデバイスインストーラーは、そのデバイスのインストールプロセスの後続の手順でそれらを呼び出します。

オプションの*DevCoDeviceInstall*が省略されている場合は、既定の**CoDeviceInstall**ルーチン名が共同インストーラー DLL のエントリポイントとして使用されます。

詳細については、「[デバイス固有の共同インストーラーの登録](registering-a-device-specific-co-installer.md)」を参照してください。

### <a name="registering-device-class-co-installers"></a>デバイスクラスの共同インストーラーの登録

1つ以上のデバイスクラスのレジストリへのインストーラーに対して、値エントリ (およびセットアップクラスのサブキーがまだ存在しない場合) を追加するには、 [**AddReg**](inf-addreg-directive.md)ディレクティブで参照される*レジストリの追加セクション*の一般的な形式を次に示します。

```inf
[DDInstall.CoInstallers_ClassAddReg]
 
HKLM,System\CurrentControlSet\Control
    \CoDeviceInstallers,{SetupClassGUID},
       0x00010008,"DevClssCoInst.dll[,DevClssEntryPoint]" 
 ...
```

このような add registry セクションの各エントリは、INF ファイル内で1行として表示されます。また、指定された各クラスの共同インストーラー DLL には一意の名前を付ける必要があります。 指定された共同インストーラーを複数の[デバイスセットアップクラス](device-setup-classes.md)で使用する必要がある場合、この add registry セクションには複数のエントリを含めることができ、それぞれに適切な*setupclassguid*値が設定されます。

このような補助デバイスクラスの共同インストーラーでは、既存のクラスインストーラーに対して既に登録されている共同インストーラーを置き換えることはできません。 したがって、クラスの共同インストーラーには一意の名前を付ける必要があります。また、指定された[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)型の値は、 **{**<em>setupclassguid</em>**}** サブキーに既に存在している場合は、クラス固有の共同インストーラーエントリ (*フラグ*値**0x0010008**の**8**によって示されます) に追加する必要があります。

**メモ** 同じ名前の共同インストーラーが既に登録されている場合、 [setupapi.log](setupapi.md)関数は、重複する<em>Devclsscoinstall</em>**.dll**を値エントリに追加することはありません。

 

補助的なデバイスクラスの共同インストーラーの INF は、右クリックでインストールするか、 **Setupinstallfrominfsection**を呼び出すことによってアクティブにすることができます。

<a name="examples"></a>例
--------

この例は、 *Ddinstall*を示しています。IrDA シリアルネットワークアダプターについては、 **CoInstallers**セクションを参照してください。 システムが提供するこれらの IrDA (シリアル) Nic 用の INF は、システム IrDA クラスインストーラーに共同インストーラーを提供します。

```inf
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

前の PNP<strong>。R.CoInstallers</strong>セクションは、インストーラー固有の*追加レジストリ*セクションのみを参照しています。 このシステムが提供する INF は IrDA ネットワークデバイスのセットをインストールするため、 [**CopyFiles**](inf-copyfiles-directive.md)ディレクティブはありません。 この INF ファイルは、すべてのシステム INF ファイルと同様に、[**バージョン**](inf-version-section.md)セクションの**layoutfile**エントリを使用して、共同インストーラーファイルを変換先に転送します。

すべての<em>Ddinstall</em>に注意**してください。** IHV または OEM によって提供される INF の CoInstallers セクションには、 **CopyFiles**ディレクティブと共に[**sourcedisksnames**](inf-sourcedisksnames-section.md)および[**sourcedisksnames**](inf-sourcedisksfiles-section.md)セクションもあります。

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

**Updateinis の**
[**バージョン**](inf-version-section.md)

 

 






