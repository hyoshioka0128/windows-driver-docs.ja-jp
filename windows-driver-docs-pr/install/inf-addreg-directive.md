---
title: INF AddReg ディレクティブ
description: AddReg ディレクティブを 1 つまたは複数 INF ライター定義を追加-レジストリのセクションでは変更またはレジストリ情報の作成に使用されるを参照します。
ms.assetid: e8162e20-0d8c-4400-9f4d-5f4abe81305b
keywords:
- INF AddReg ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF AddReg Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 984d3f8101b2f6f00c3a7a42013f62cce5407e22
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357517"
---
# <a name="inf-addreg-directive"></a>INF AddReg ディレクティブ


**AddReg**ディレクティブでは、1 つを参照またはより INF ライター-定義*追加レジストリ セクション*変更やレジストリ情報の作成に使用します。

```ini
[DDInstall] | 
[DDInstall.HW] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64]  (Windows XP and later versions of Windows) 
[ClassInstall32.ntarm]  (Windows 8 and later versions of Windows) 
[ClassInstall32.ntarm64]  (Windows 10 and later versions of Windows) 


[install-interface-section] | 
[service-install-section] | 
[event-log-install] | 
[add-interface-section]
AddReg=add-registry-section[,add-registry-section] ...
```

各*追加レジストリ セクション*以下を実行するエントリがあることができます。

-   場合によっては、初期値エントリで、新しいキーをレジストリに追加します。
-   既存のレジストリ キーに新しい値のエントリを追加します。
-   レジストリ内の特定のキーの値の既存のエントリを変更します。

という名前の各*追加レジストリ セクション*によって参照される、 **AddReg**ディレクティブは、次の形式。

```ini
[add-registry-section]
reg-root, [subkey],[value-entry-name],[flags],[value][,[value]]
reg-root, [subkey],[value-entry-name],[flags],[value][,[value]]
 ...
[[add-registry-section.security]
"security-descriptor-string"]
```

*追加レジストリ セクション*それぞれ別々 の行に任意の数のエントリを持つことができます。 INF を含めることも 1 つまたは複数のオプション<em>追加レジストリ セクション</em>**.security**セクションで、名前付き内で説明されているすべてのレジストリ値に適用されるセキュリティ記述子を指定する各*追加レジストリ セクション*します。

## <a name="entries"></a>エントリ


<a href="" id="reg-root"></a>*レジストリ ルート*  
このエントリで指定されたその他の値のレジストリ ツリーのルートを識別します。 値は次のいずれかになります。

<a href="" id="hkcr"></a>**HKCR**  
省略形**HKEY_CLASSES_ROOT**

<a href="" id="hkcu"></a>**HKCU**  
省略形**HKEY_CURRENT_USER**

<a href="" id="hklm"></a>**HKLM**  
省略形**HKEY_LOCAL_MACHINE**

<a href="" id="hku"></a>**HKU**  
省略形**HKEY_USERS**

<a href="" id="hkr"></a>**HKR**  
この省略形を使用して指定されているキーがこの INF セクションに関連付けられたレジストリ キーを基準との相対のルート**AddReg**ディレクティブが表示されたら、次の表に記載されています。

| INF セクションを含む AddReg ディレクティブ                        | HKR によって参照されるレジストリ キー                                                        |
|----------------------------------------------------------------|---------------------------------------------------------------------------------------|
| INF ***DDInstall*** |
| INF ***DDInstall *。ハードウェア** |
| INF *\[サービス-インストール セクション\]* セクション                      | **サービス**キー                                                                  |
| INF *\[インストール ログ イベントが\]* セクション                            | **EventLog**キー                                                                  |
| INF *\[追加インターフェイス セクション\]* セクション                        | デバイス インターフェイスのレジストリ キー                                                    |


**注**  **HKR**では使用できません、*追加レジストリ セクション*から参照されている、 [ **INF DefaultInstall セクション**](inf-defaultinstall-section.md)します。

 

下に格納されているドライバー情報の詳細については、 **HKEY_LOCAL_MACHINE**ルートは、「[レジストリ ツリーとデバイスとドライバーのキー](registry-trees-and-keys.md)します。

<a href="" id="subkey"></a>*サブキー*  
このオプションの値の形式を % として*strkey*% のトークンで定義されている、 [**文字列**](inf-strings-section.md)セクション、INF または下のレジストリ パスとして、指定された*reg ルート*(<em>key1</em>**\\**<em>key2</em>**\\**<em>key3</em>...)、次のいずれかを指定します。

-   指定されたレジストリ パスの最後に、レジストリに追加する新しいサブキー。
-   既存のサブキーを (指定したサブキーの既存の名前付きの値のエントリの値を置き換える可能性があります)、このエントリで指定された追加の値を記述します。
-   両方の新しいサブキーの初期値エントリと共にレジストリに追加します。

<a href="" id="value-entry-name"></a>*value-entry-name*  
この省略可能な値か、指定された (既存) で既存の値のエントリの名前*サブキー*を追加する新しい値のエントリの名前を作成しますまたは、指定した*サブキー*それが既に存在するか、新しいキーがあるかどうか、。レジストリに追加します。 この値を表現できるとして **"**<em>文字列を引用符で囲まれた</em>**"** または % として*strkey*INF ので定義されている % トークン[**文字列**](inf-strings-section.md)セクション。 (これを文字列型の値を省略した場合、*値のエントリ名*このキーの値のエントリを「名前」既定値です)。

オペレーティング システム サポートの一部のシステム定義された特別な*値のエントリ名*キーワード。 末尾を参照してください。**解説**詳細についてはします。

<a href="" id="flags"></a>*フラグ*  
この省略可能な 16 進値、下位ワードのシステム定義の上位ワード フラグの論理和のビットマスク値、値のエントリのデータ型を定義および追加レジストリ操作を制御として表されます。

これらのフラグのビットマスク値は次のとおりです。

<a href="" id="0x00000001--flg-addreg-binvaluetype---"></a>**0x00000001** (FLG_ADDREG_BINVALUETYPE)   
指定された値は、「生」データです。 (この値は、FLG_ADDREG_TYPE_BINARY と同じです)。

<a href="" id="0x00000002--flg-addreg-noclobber---"></a>**0x00000002** (FLG_ADDREG_NOCLOBBER)   
指定した値が既存の値のエントリの値を置換するを防ぐ。

<a href="" id="0x00000004--flg-addreg-delval-"></a>**0x00000004** (FLG_ADDREG_DELVAL)  
削除、指定された*サブキー*レジストリ、または指定された削除から*値のエントリ名*指定されたレジストリから*サブキー*します。

<a href="" id="0x00000008--flg-addreg-append--"></a>**0x00000008** (FLG_ADDREG_APPEND)   
追加を指定した*値*の既存のエントリは名前付きの値。 このフラグは FLG_ADDREG_TYPE_MULTI_SZ も設定されている場合にのみ有効です。 指定した文字列値は既に存在する場合は追加されません。

<a href="" id="0x00000010--flg-addreg-keyonly-"></a>**0x00000010** (FLG_ADDREG_KEYONLY)  
作成、特定*サブキー*、れた指定された値、エントリの名前と値は無視されます。

<a href="" id="0x00000020--flg-addreg-overwriteonly--"></a>**0x00000020** (FLG_ADDREG_OVERWRITEONLY)   
指定されたにリセット*値*場合にのみ、指定した*値、エントリの名前*に既に存在する、特定*サブキー*。

<a href="" id="0x00001000--flg-addreg-64bitkey--"></a>**0x00001000** (FLG_ADDREG_64BITKEY)   
(Windows XP および Windows の以降のバージョン。)64 ビットのレジストリで指定された変更を加えます。 指定しない場合は、ネイティブのレジストリに変更が行わします。

<a href="" id="0x00002000--flg-addreg-keyonly-common-"></a>**0x00002000** (FLG_ADDREG_KEYONLY_COMMON)  
(Windows XP および Windows の以降のバージョン。)これは、FLG_ADDREG_KEYONLY と同じですが、内でも、 *del-section レジストリ*の[ **INF してディレクティブ**](inf-delreg-directive.md)します。

<a href="" id="0x00004000--flg-addreg-32bitkey-"></a>**0x00004000** (FLG_ADDREG_32BITKEY)  
(Windows XP および Windows の以降のバージョン。)32 ビットのレジストリで指定された変更を加えます。 指定しない場合は、ネイティブのレジストリに変更が行わします。

<a href="" id="0x00000000--flg-addreg-type-sz-"></a>**0x00000000** (FLG_ADDREG_TYPE_SZ)  
指定された値または値が型の[REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)します。

**注**  フラグの値は、任意の r から省略できますので、この値は、指定した値エントリの既定の型*例: ルート =* 行、*追加レジストリ セクション*で動作します。この型の値のエントリ。

 

<a href="" id="0x00010000--flg-addreg-type-multi-sz-"></a>**0x00010000** (FLG_ADDREG_TYPE_MULTI_SZ)  
レジストリの種類が、指定された値のエントリや値[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)します。 次の値フィールドには、コンマで区切られた文字列のリストを指定できます。 この仕様では、指定された文字列値の任意の NULL 終端記号は必要ありません。

<a href="" id="0x00020000--flg-addreg-type-expand-sz--"></a>**0x00020000** (FLG_ADDREG_TYPE_EXPAND_SZ)   
特定*値のエントリ名*や*値*のレジストリの種類は[REG_EXPAND_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)します。

<a href="" id="0x00010001--flg-addreg-type-dword---flg-addreg-type-dword-"></a>**0x00010001** (FLG_ADDREG_TYPE_DWORD) (FLG_ADDREG_TYPE_DWORD)  
特定*値のエントリ名*や*値*のレジストリの種類は[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)します。

<a href="" id="0x00020001--flg-addreg-type-none-"></a>**0x00020001** (FLG_ADDREG_TYPE_NONE)  
特定*値のエントリ名*や*値*のレジストリの種類は[REG_NONE](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)します。

<a href="" id="value"></a>*値*  
指定した新しい値を必要に応じて指定*値のエントリ名*特定のレジストリ キーに追加します。 このような*値*という名前で追加する値、既存のキー値のエントリを既存の「置換」値を指定できます (*フラグ*値**0x00010008**) を既存の名前[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-新しいの既存のキーを既存のキーに書き込まれる新しい値のエントリまたは初期値のエントリの値のエントリを入力*サブキー*レジストリに追加します。

このような式を*値*に指定されたレジストリの種類によって異なります、*フラグ*、次のようにします。

-   レジストリの文字列型の値を表すことがいずれかを"*文字列を引用符で囲まれた*"または % として*strkey*% のトークンで定義されている、 [**文字列**](inf-strings-section.md)セクションINF ファイルです。 このような INF 指定の値を各文字列の最後に終端の NULL を含める必要はありません。
-   数値型のレジストリ値は、(0 x 表記を使用して) によって 16 進数または 10 進数として表現できます。

<a href="" id="security-descriptor-string"></a>*セキュリティ記述子の文字列*  
名前付きによって作成されたすべてのレジストリ エントリに適用する、セキュリティ記述子を指定*追加レジストリ セクション*します。 *セキュリティ記述子の文字列*DACL を指定するトークンを含む文字列です (**d:**) セキュリティ コンポーネント。

場合、<em>追加レジストリ セクション</em>**.security**セクションが指定されていない、レジストリ エントリが親のキーのセキュリティ設定を継承します。

場合、<em>追加レジストリ セクション</em>**.security**セクションを指定すると、デバイスおよびシステム サービス パックのインストールとアップグレードが発生することができるように、次の ACE を含める必要があります。

-   (A;GA;;この SY) は、ローカル システムにすべてのアクセスを付与します。
-   (A;GA;;この BA) は、組み込みの管理者のすべてのアクセスを付与します。

*いない*特権を持たないユーザーに書き込みアクセスを許可する ACE 文字列を指定します。

セキュリティ記述子文字列については、次を参照してください。[セキュリティ記述子定義言語 (Windows)](https://msdn.microsoft.com/library/windows/desktop/aa379567)します。 セキュリティ記述子文字列の形式の詳細については、セキュリティ記述子定義言語 (Windows) を参照してください。

セキュリティ記述子を指定する方法の詳細については、次を参照してください。[セキュリティで保護されたデバイスのインストールを作成する](creating-secure-device-installations.md)します。

<a name="remarks"></a>注釈
-------

**AddReg**上記の正式な構文のステートメントで次のセクションのいずれかのディレクティブを指定できます。 このディレクティブは、INF ライター定義の次のセクションのいずれかも指定できます。

-   A*サービス-インストール セクション*または*インストール ログ イベントが*セクションによって参照される、 [ **AddService** ](inf-addservice-directive.md)ディレクティブで、 [ **INF *DDInstall*します。サービス セクション**](inf-ddinstall-services-section.md)します。
-   *追加インターフェイス セクション*によって参照される、 [ **AddInterface** ](inf-addinterface-directive.md)ディレクティブで、 [ **INF *DDInstall*.インターフェイス セクション**](inf-ddinstall-interfaces-section.md)します。
-   *インストール-section インターフェイス*で参照されている、 [ **INF InterfaceInstall32 セクション**](inf-interfaceinstall32-section.md)します。

各*追加レジストリ セクション*名は、INF ファイルに固有である必要がありますが、それを参照できます**AddReg**同じ INF の他のセクション ディレクティブ。 各セクション名に記載されているセクションの名前の定義の一般的な規則に従う必要があります[INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)します。

**注**  下位のビット フラグの値の下位ワードの文字データやバイナリ データを区別します。

 

レジストリの種類の定義済みの reg _ 1 つ以外の数を表す*XXX*の上位ワードで新しい種類の番号を指定する種類を*フラグ*FLG_ADDREG_BINVALUETYPE その下位のワードでの論理和。 このようなデータを*値*コンマで区切られたバイトのシーケンスとしてバイナリ形式で指定する必要があります。 たとえば、値のエントリとして 0x38 などの新しいレジストリ データ型のデータの 16 バイトを格納するセクション エントリの追加レジストリは次のような。

```ini
HKR,,MYValue,0x00380001,1,0,2,3,4,5,6,7,8,9,A,B,C,D,E,F
```

この方法は、数値型の値ではなく新しいレジストリの種類の定義に使用できます[REG_EXPAND_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)、 [REG_NONE](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)、または[REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)します。 これらの種類の詳細については、次を参照してください。[レジストリ値の型](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)します。

### <a name="special-value-entry-name-keywords"></a>特別な*値のエントリ名*キーワード

HKR で使用するための特別なキーワードが定義されている**AddReg**エントリ。 これらのキーワードを使用するエントリの形式は次のとおりです。

```ini
[HKR,,DeviceCharacteristics,0x10001,characteristics] 
[HKR,,DeviceType,0x10001,device-type] 
[HKR,,Security,,security-descriptor-string] 
[HKR,,UpperFilters,0x10000,service-name] 
[HKR,,LowerFilters,0x10000,service-name] 
[HKR,,Exclusive,0x10001,exclusive-device] 
[HKR,,EnumPropPages32,,"prop-provider.dll,provider-entry-point"]
[HKR,,LocationInformationOverride,,"text-string"] 
[HKR,,ResourcePickerTags,,"text-string"] 
[HKR,,ResourcePickerExceptions,,"text-string"] ,
```

以下に示します、HKR **AddReg**これらの特別なキーワードを使用して、エントリ。

<a href="" id="devicecharacteristics"></a>**DeviceCharacteristics**  
A **DeviceCharacteristics** HKR **AddReg**エントリは、デバイスの特性を指定します。 *特性*値は 1 つまたは複数のこれはまたはを使用しての結果である数値\*ファイルで定義されている特徴値*Wdm.h*と*Ntddk.h*.

INF では、次の値のみを指定できます。

```ini
#define FILE_REMOVABLE_MEDIA            0x00000001
#define FILE_READ_ONLY_DEVICE           0x00000002
#define FILE_FLOPPY_DISKETTE            0x00000004
#define FILE_WRITE_ONCE_MEDIA           0x00000008
#define FILE_DEVICE_SECURE_OPEN         0x00000100
```

これらの値については、次を参照してください。 [ **IoCreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548397)します。

使用して指定されている特徴値を**DeviceCharacteristics**エントリへの各呼び出しで指定されているものは論理和**IoCreateDevice**デバイス スタックでデバイス オブジェクトを作成します。 OR 演算は、すべてのデバイス オブジェクトが追加された後、デバイスを開始する前に発生します。

*特性*値 (ゼロの値を含む) には、クラスが関連付けられているインストーラー INF で指定された任意のクラス全体のデバイスの特性がよりも優先されます。

デバイスの特性の詳細については、次を参照してください。[デバイスの特性を指定する](https://msdn.microsoft.com/library/windows/hardware/ff563818)します。

<a href="" id="devicetype"></a>**DeviceType**  
A **DeviceType** HKR **AddReg**エントリは、デバイスのデバイスの種類を指定します。 デバイスの種類には、FILE_DEVICE_ の数値*XXX*で定義された定数*Wdm.h*または*Ntddk.h*します。 0x10001 のフラグの値は、デバイスの種類の値があるを指定します、 [REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)します。 詳細については、次を参照してください。[デバイスの種類の指定](https://msdn.microsoft.com/library/windows/hardware/ff563821)します。

クラス インストーラー INF はすべて、またはすべてのデバイス クラスのほとんどに適用されるデバイスの種類を指定する必要があります。 たとえば、FILE_DEVICE_CD_ROM 型の場合、クラス内のデバイスは、指定、*デバイスの種類*0x02 になります。 デバイスの INF の値を指定する場合**DeviceType**、存在する場合は、クラスのインストーラーによって設定された値をオーバーライドします。 クラスまたはデバイスの INF が指定されている場合、 **DeviceType**値、PnP マネージャーを適用するには、その型、*物理デバイス オブジェクト (PDO)* バス ドライバーによって作成します。

<a href="" id="security"></a>**セキュリティ**  
A**セキュリティ**HKR **AddReg**エントリは、デバイスのセキュリティ記述子を指定します。 *セキュリティ記述子の文字列*DACL を指定するトークンを含む文字列です (**d:**) セキュリティ コンポーネント。

クラス インストーラー INF では、デバイス クラスのセキュリティ記述子を指定できます。 デバイスの INF には、クラスのセキュリティをオーバーライドする個々 のデバイスのセキュリティ記述子を指定できます。 クラスまたはデバイスの INF が指定されている場合、*セキュリティ記述子の文字列*、PnP マネージャー デバイスのすべてのオブジェクトに、記述子の伝達 ( *DOs*) デバイス。 関数のデバイス オブジェクトが含まれます (*FDO*) 省略可能な*DOs をフィルター処理*、および PDO します。

セキュリティ記述子文字列の形式の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

セキュリティ記述子を指定する方法の詳細については、次を参照してください。[セキュリティで保護されたデバイスのインストールを作成する](creating-secure-device-installations.md)します。

<a href="" id="upperfilters"></a>**再**  
**再**HKR **AddReg** PnP 上フィルター ドライバーを指定します。 このエントリで、 [ * **DDInstall *。HW** ](inf-ddinstall-hw-section.md)セクションが 1 つまたは複数のデバイス固有の上位フィルター ドライバーを定義します。 [ **ClassInstall32** ](inf-classinstall32-section.md) ] セクションで、このエントリが 1 つまたは複数のクラス全体にわたる上フィルター ドライバーを定義します。

<a href="" id="lowerfilters"></a>**LowerFilters**  
A **LowerFilters** HKR **AddReg** PnP 低いフィルター ドライバーを指定します。 このエントリで、 <em>DDInstall</em>**します。ハードウェア セクション**1 つまたは複数のデバイスに固有の低いフィルター ドライバーを定義します。 **ClassInstall32**  セクションで、このエントリが 1 つまたは複数のクラス全体にわたる低いフィルター ドライバーを定義します。

<a href="" id="exclusive"></a>**排他的**  
**排他**HKR **AddReg**エントリが存在し、「1」に設定されている場合を指定します、デバイスがある、*排他デバイス*します。 それ以外の場合、デバイスは扱われませんに排他的です。 詳細については、次を参照してください。[デバイス オブジェクトに排他アクセスを指定する](https://msdn.microsoft.com/library/windows/hardware/ff563827)します。

<a href="" id="enumproppages32"></a>**EnumPropPages32**  
**EnumPropPages32** HKR **AddReg**エントリは、ダイナミック リンク ライブラリの名前を指定します (*DLL*) ファイルをデバイス固有のプロパティ ページのプロバイダー。 名前も指定します、 **ExtensionPropSheetPageProc** DLL によって実装されるコールバック関数。 プロパティ ページと機能の詳細については、Windows 7 および .NET Framework 4.0 用 Microsoft Windows ソフトウェア開発キット (SDK) を参照してください。

**重要な**  両方の DLL の名前と**ExtensionPropSheetPageProc**コールバック関数をまとめて引用符で囲む必要があります ("")。

 

<a href="" id="locationinformationoverride"></a>**LocationInformationOverride**  
(Windows XP および Windows の以降のバージョン)A **LocationInformationOverride** HKR **AddReg**エントリは、デバイスの物理的な場所を説明するテキスト文字列を指定するために使用できます。 これは、上書き、 **LocationInformation**への応答で、デバイスのバス ドライバーを提供する文字列、 [ **IRP_MN_QUERY_DEVICE_TEXT** ](https://msdn.microsoft.com/library/windows/hardware/ff551674)要求。

<a href="" id="resourcepickertags"></a>**ResourcePickerTags**  
A **ResourcePickerTags** HKR **AddReg**エントリは、デバイスのリソース ピッカーのタグを指定します。

<a href="" id="resourcepickerexceptions"></a>**ResourcePickerExceptions**  
A **ResourcePickerExceptions** HKR **AddReg**エントリをデバイスに許可されるリソースの競合を指定します。

<a name="examples"></a>例
--------

**AddReg**ディレクティブによって参照される INF ライター定義のセクションで、この例では、(SCSI) Miniport_EventLog_AddReg セクションを参照する、 **AddService**ディレクティブで、 <em>DDInstall</em>**します。サービス**のこの INF セクション。

```ini
[Miniport_EventLog_AddReg]
HKR,,EventMessageFile,0x00020000,"%%SystemRoot%%\System32\IoLogMsg.dll" 
; double quotation marks delimiters in preceding entry prevent truncation 
; if line wraps
 
HKR,,TypesSupported,0x00010001,7 
```

## <a name="see-also"></a>関連項目


[**AddInterface**](inf-addinterface-directive.md)

[**AddService**](inf-addservice-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。共同インストーラー**](inf-ddinstall-coinstallers-section.md)

[***DDInstall *。ハードウェア**](inf-ddinstall-hw-section.md)

[***DDInstall *。インターフェイス**](inf-ddinstall-interfaces-section.md)

[***DDInstall *。サービス**](inf-ddinstall-services-section.md)

[**DelReg**](inf-delreg-directive.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**文字列**](inf-strings-section.md)

 

 






