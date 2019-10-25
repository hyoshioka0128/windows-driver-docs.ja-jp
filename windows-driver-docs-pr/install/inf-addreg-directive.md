---
title: INF AddReg ディレクティブ
description: AddReg ディレクティブは、レジストリ情報を変更または作成するために使用される、1つまたは複数の INF ライターで定義されたレジストリセクションを参照します。
ms.assetid: e8162e20-0d8c-4400-9f4d-5f4abe81305b
keywords:
- INF AddReg ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF AddReg Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb1d4a1c5c69358427001ea822bcafa7616bcee3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837479"
---
# <a name="inf-addreg-directive"></a>INF AddReg ディレクティブ


**AddReg**ディレクティブは、レジストリ情報を変更または作成するために使用される、1つまたは複数の INF ライターで定義された*レジストリセクション*を参照します。

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

各 [*レジストリの追加] セクション*には、次の操作を実行するためのエントリがあります。

-   新しいキー (場合によっては、初期値のエントリを含む) をレジストリに追加します。
-   既存のレジストリキーに新しい値のエントリを追加します。
-   レジストリ内の特定のキーの既存の値エントリを変更します。

**AddReg**ディレクティブによって参照される各名前付き*追加レジストリセクション*の形式は次のとおりです。

```ini
[add-registry-section]
reg-root, [subkey],[value-entry-name],[flags],[value][,[value]]
reg-root, [subkey],[value-entry-name],[flags],[value][,[value]]
 ...
[[add-registry-section.security]
"security-descriptor-string"]
```

*レジストリセクション*には、任意の数のエントリを含めることができます。各エントリは個別の行にあります。 INF には、1つまたは複数のオプションの<em>add レジストリセクション</em>を含めることもでき**ます。セキュリティ**セクションでは、それぞれのセキュリティ記述子を指定します。これらのセクションには、指定した*レジストリ*値で記述されているすべてのレジストリ値に適用されます。

## <a name="entries"></a>Entries


<a href="" id="reg-root"></a>*reg-ルート*  
このエントリに指定されている他の値のレジストリツリーのルートを識別します。 値は次のいずれかになります。

<a href="" id="hkcr"></a>**HKCR**  
**HKEY_CLASSES_ROOT**の略称

<a href="" id="hkcu"></a>**HKCU**  
**HKEY_CURRENT_USER**の省略形

<a href="" id="hklm"></a>**HKLM**  
**HKEY_LOCAL_MACHINE**の省略形

<a href="" id="hku"></a>**HKU**  
**HKEY_USERS**の省略形

<a href="" id="hkr"></a>**HKR**  
相対ルート。この省略形を使用して指定されたキーは、次の表に示すように、この**AddReg**ディレクティブが表示される INF セクションに関連付けられているレジストリキーを基準としています。

| AddReg ディレクティブを含む INF セクション                        | HKR によって参照されるレジストリキー                                                        |
|----------------------------------------------------------------|---------------------------------------------------------------------------------------|
| INF ***Ddinstall*** |
| INF ***Ddinstall *。HW** |
| INF *\[サービス-インストールセクション\]* セクション                      | **サービス**キー                                                                  |
| INF *\[イベントログ-インストール\]* セクション                            | **EventLog**キー                                                                  |
| INF *\[\]セクションの追加*                        | デバイスインターフェイスのレジストリキー                                                    |


**注**  **Hkr**は、 [**INF DefaultInstall セクション**](inf-defaultinstall-section.md)から参照される*レジストリの追加セクション*では使用できません。

 

**HKEY_LOCAL_MACHINE**ルートの下に格納されているドライバー情報の詳細については、「[デバイスとドライバーのレジストリツリーとキー](registry-trees-and-keys.md)」を参照してください。

<a href="" id="subkey"></a>*サブキー*  
この省略可能な値。 INF の[**Strings**](inf-strings-section.md)セクションで定義された%*strkey*% token として、または指定された*reg ルート*(<em>key1</em> **\\** <em>key2</em> **\\** <em>key3</em>...) の下のレジストリパスとして形成されます。では、次のいずれかを指定します。

-   指定されたレジストリパスの最後にレジストリに追加される新しいサブキー。
-   このエントリに指定されている追加の値が書き込まれる既存のサブキー (場合によっては、指定されたサブキーの既存の名前付きの値エントリの値を置き換えることがあります)。
-   レジストリに新しいサブキーを追加し、その初期値のエントリと共に追加します。

<a href="" id="value-entry-name"></a>*値-エントリ名*  
この省略可能な値は、指定された (既存の)*サブキー*の既存の値エントリに名前を付けるか、または指定した*サブキー*に追加される新しい値エントリの名前を作成します (既に存在しているか、レジストリに追加する新しいキーであるかを示します)。 この値は、 **"** <em>引用符で囲ま</em>れた文字列 **"** として、または INF の [[**文字列**](inf-strings-section.md)] セクションで定義されている%*strkey*% token として表すことができます。 (文字列型の値に対してこれが省略されている場合、このキーの既定の "名前のない" 値エントリが*エントリ名*として指定されます)。

オペレーティングシステムでは、システム定義の特別な*値のエントリ名*のキーワードがサポートされています。 詳細については、この**解説**の末尾を参照してください。

<a href="" id="flags"></a>*示す*  
この省略可能な16進値は、システム定義の小さい単語と上位のフラグ値のビットマスクとして表現され、値エントリのデータ型を定義したり、レジストリの追加操作を制御したりします。

これらの各フラグのビットマスク値は次のとおりです。

<a href="" id="0x00000001--flg-addreg-binvaluetype---"></a>**0x00000001** (FLG_ADDREG_BINVALUETYPE)   
指定された値は "raw" データです。 (この値は FLG_ADDREG_TYPE_BINARY と同じです)。

<a href="" id="0x00000002--flg-addreg-noclobber---"></a>**0x00000002** (FLG_ADDREG_NOCLOBBER)   
指定された値によって既存の値エントリの値が置換されないようにします。

<a href="" id="0x00000004--flg-addreg-delval-"></a>**0x00000004** (FLG_ADDREG_DELVAL)  
指定された*サブキー*をレジストリから削除するか、指定された*エントリ名*を指定したレジストリ*サブキー*から削除します。

<a href="" id="0x00000008--flg-addreg-append--"></a>**0x00000008** (FLG_ADDREG_APPEND)   
指定された値を既存の名前付きの値エントリの*値*に追加します。 このフラグは、FLG_ADDREG_TYPE_MULTI_SZ も設定されている場合にのみ有効です。 指定された文字列値は、既に存在する場合は追加されません。

<a href="" id="0x00000010--flg-addreg-keyonly-"></a>**0x00000010** (FLG_ADDREG_KEYONLY)  
指定された*サブキー*を作成しますが、指定された値のエントリ名や値を無視します。

<a href="" id="0x00000020--flg-addreg-overwriteonly--"></a>**0x00000020** (FLG_ADDREG_OVERWRITEONLY)   
指定された*値-エントリ名*が指定した*サブキー*に既に存在する場合にのみ、指定された*値*にリセットします。

<a href="" id="0x00001000--flg-addreg-64bitkey--"></a>**0x00001000** (FLG_ADDREG_64BITKEY)   
(Windows XP 以降のバージョンの Windows)。64ビットレジストリで、指定された変更を行います。 指定しない場合、ネイティブレジストリに変更が加えられます。

<a href="" id="0x00002000--flg-addreg-keyonly-common-"></a>**0x00002000** (FLG_ADDREG_KEYONLY_COMMON)  
(Windows XP 以降のバージョンの Windows)。これは FLG_ADDREG_KEYONLY と同じですが、 [**INF DelReg ディレクティブ**](inf-delreg-directive.md)の*del-registry セクション*でも機能します。

<a href="" id="0x00004000--flg-addreg-32bitkey-"></a>**0x00004000** (FLG_ADDREG_32BITKEY)  
(Windows XP 以降のバージョンの Windows)。32ビットレジストリで、指定された変更を行います。 指定しない場合、ネイティブレジストリに変更が加えられます。

<a href="" id="0x00000000--flg-addreg-type-sz-"></a>**0x00000000** (FLG_ADDREG_TYPE_SZ)  
指定された値のエントリまたは値は、 [REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)型になります。

この値は、指定された値エントリの既定の型である  **ことに注意**してください。したがって、この型の値のエントリに対して動作する、 *add registry-section*では、flags 値を任意の r (*ルート = 行)* から省略できます。

 

<a href="" id="0x00010000--flg-addreg-type-multi-sz-"></a>**0x00010000** (FLG_ADDREG_TYPE_MULTI_SZ)  
指定された値のエントリまたは値は、レジストリの種類が[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)です。 次の値フィールドは、コンマで区切られた文字列のリストにすることができます。 この仕様では、特定の文字列値に対して NULL 終端文字は必要ありません。

<a href="" id="0x00020000--flg-addreg-type-expand-sz--"></a>**0x00020000** (FLG_ADDREG_TYPE_EXPAND_SZ)   
指定された*値-エントリ名*または*値*は、レジストリの種類[REG_EXPAND_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)です。

<a href="" id="0x00010001--flg-addreg-type-dword---flg-addreg-type-dword-"></a>**0x00010001** (FLG_ADDREG_TYPE_DWORD) (FLG_ADDREG_TYPE_DWORD)  
指定された*値-エントリ名*または*値*は、レジストリの種類[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)です。

<a href="" id="0x00020001--flg-addreg-type-none-"></a>**0x00020001** (FLG_ADDREG_TYPE_NONE)  
指定された*値-エントリ名*または*値*は、レジストリの種類[REG_NONE](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)です。

<a href="" id="value"></a>*数値*  
必要に応じて、指定されたレジストリキーに追加する、指定された*値-エントリ名*の新しい値を指定します。 このよう*な値*には、既存のキーに含まれる既存の名前付きの値のエントリの "置換" 値、既存のキーの既存の名前付きの[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)型の値のエントリに追加する値 (*フラグ*値**0x00010008**)、新しい値を指定できます。既存のキーに書き込むエントリ、またはレジストリに追加する新しい*サブキー*の初期値のエントリ。

このような*値*の式は、次のように、*フラグ*に指定されたレジストリの種類によって異なります。

-   レジストリ文字列型の値は、"引用符で囲まれた*文字列*" として、または INF ファイルの[**文字列**](inf-strings-section.md)セクションで定義されている%*strkey*% token として表すことができます。 このような INF 指定値では、各文字列の末尾に NULL 終端記号を含める必要はありません。
-   レジストリの数値型の値は、16進数 (0x 表記を使用) または10進数として表すことができます。

<a href="" id="security-descriptor-string"></a>*セキュリティ記述子-文字列*  
指定された*レジストリセクション*によって作成されるすべてのレジストリエントリに適用されるセキュリティ記述子を指定します。 *セキュリティ記述子文字列*は、DACL (**D:** ) セキュリティコンポーネントを示すトークンを含む文字列です。

<em>Add registry-section</em> **. security**セクションが指定されていない場合、レジストリエントリは親キーのセキュリティ設定を継承します。

<em>Add registry-section</em> **. security**セクションが指定されている場合、デバイスとシステムサービスパックのインストールとアップグレードが発生するように、次の ACE が含まれている必要があります。

-   (A;;GA、;、SY) −ローカルシステムへのすべてのアクセスを許可します。
-   (A;;GA、;、BA: 組み込みの管理者へのすべてのアクセスを許可します。

権限*のないユーザー*に書き込みアクセス権を付与する ACE 文字列を指定しないでください。

セキュリティ記述子の文字列の詳細については、「[セキュリティ記述子定義言語 (Windows)](https://docs.microsoft.com/windows/desktop/SecAuthZ/security-descriptor-definition-language)」を参照してください。 セキュリティ記述子文字列の形式の詳細については、「セキュリティ記述子定義言語 (Windows)」を参照してください。

セキュリティ記述子を指定する方法の詳細については、「セキュリティ[で保護されたデバイスのインストールの作成](creating-secure-device-installations.md)」を参照してください。

<a name="remarks"></a>解説
-------

**AddReg**ディレクティブは、上記の仮構文ステートメントに示されているいずれかのセクションの下で指定できます。 このディレクティブは、次の INF ライターで定義されたセクションのいずれかで指定することもできます。

-   INF Ddinstall で[**addservice**](inf-addservice-directive.md)ディレクティブによって参照される、*サービスのインストール*セクションまたは*イベントログのインストール*セクション[ **。サービスセクション**](inf-ddinstall-services-section.md)。
-   INF Ddinstall で[**addinterface**](inf-addinterface-directive.md)ディレクティブによって参照される、*インターフェイスの追加セクション* [ **。インターフェイスセクション**](inf-ddinstall-interfaces-section.md)。
-   [**INF InterfaceInstall32 セクション**](inf-interfaceinstall32-section.md)で参照される*インストールインターフェイスセクション*。

各*add registry セクション*名は inf ファイルに対して一意である必要がありますが、同じ inf の他のセクションの**AddReg**ディレクティブで参照できます。 各セクション名は、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」で説明されているセクション名を定義するための一般的な規則に従う必要があります。

フラグ値の下位ワードの下位ビットによって、文字データとバイナリデータが区別さ  **ことに注意**してください。

 

定義済みの REG_*XXX*型以外の種類のレジストリを表すには、小さい単語の FLG_ADDREG_BINVALUETYPE と共に、*フラグ*の上位ワードに新しい型番号を指定します。 このような*値*のデータは、コンマで区切られたバイトのシーケンスとしてバイナリ形式で指定する必要があります。 たとえば、新しいレジストリデータ型の16バイトのデータ (0x38 など) を値エントリとして格納する場合、[レジストリの追加] セクションのエントリは次のようになります。

```ini
HKR,,MYValue,0x00380001,1,0,2,3,4,5,6,7,8,9,A,B,C,D,E,F
```

この手法は、値に対して新しいレジストリの種類を定義するために使用できますが、 [REG_EXPAND_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)、 [REG_NONE](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)、または[REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)型の値には使用できません。 これらの型の詳細については、「[レジストリ値の型](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)」を参照してください。

### <a name="special-value-entry-name-keywords"></a>特別な*値-エントリ名*のキーワード

特別なキーワードは、HKR **AddReg**エントリで使用するために定義されています。 これらのキーワードを使用するエントリの形式は次のとおりです。

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

次に、これらの特殊なキーワードを使用する HKR **AddReg**のエントリについて説明します。

<a href="" id="devicecharacteristics"></a>**DeviceCharacteristics**  
**DeviceCharacteristics** Hkr **AddReg**エントリは、デバイスの特性を指定します。 *特性*値は、FILE_ および*Ntddk*で定義されている1つ*以上の*\* ファイル特性値に対して or を使用した結果の数値です。

INF で指定できる値は次のとおりです。

```ini
#define FILE_REMOVABLE_MEDIA            0x00000001
#define FILE_READ_ONLY_DEVICE           0x00000002
#define FILE_FLOPPY_DISKETTE            0x00000004
#define FILE_WRITE_ONCE_MEDIA           0x00000008
#define FILE_DEVICE_SECURE_OPEN         0x00000100
```

これらの値の詳細については、「 [**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)」を参照してください。

**DeviceCharacteristics**エントリを使用して指定される特性値は、デバイススタックにデバイスオブジェクトを作成する**IoCreateDevice**の各呼び出しで指定された値との間にあります。 または操作は、すべてのデバイスオブジェクトが追加された後、デバイスが起動される前に発生します。

*特性*値 (ゼロの値を含む) は、関連付けられているクラスインストーラーの INF に指定されたクラス全体のデバイスの特性をオーバーライドします。

デバイスの特性の詳細については、「[デバイスの特性の指定](https://docs.microsoft.com/windows-hardware/drivers/kernel/specifying-device-characteristics)」を参照してください。

<a href="" id="devicetype"></a> **(Devicetype**  
**(Devicetype** Hkr **AddReg**エントリは、デバイスのデバイスの種類を指定します。 デバイスの種類は、 *Wdm*または*Ntddk*で定義されている FILE_DEVICE_*XXX*定数の数値です。 フラグ値0x10001 は、デバイスの種類の値が[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)であることを指定します。 詳細については、「[デバイスの種類の指定](https://docs.microsoft.com/windows-hardware/drivers/kernel/specifying-device-types)」を参照してください。

クラスインストーラーの INF では、クラス内のデバイスのすべて、またはほぼすべてに適用されるデバイスの種類を指定する必要があります。 たとえば、クラス内のデバイスの種類が FILE_DEVICE_CD_ROM である場合は、*デバイスの種類*として0x02 を指定します。 デバイス INF で **(devicetype**の値が指定されている場合は、クラスインストーラーによって設定された値がオーバーライドされます (存在する場合)。 クラスまたはデバイスの INF で **(devicetype**値が指定されている場合、PnP マネージャーは、デバイスのバスドライバーによって作成された*物理デバイスオブジェクト (PDO)* にその種類を適用します。

<a href="" id="security"></a>**保護**  
**Security** Hkr **AddReg**エントリは、デバイスのセキュリティ記述子を指定します。 *セキュリティ記述子文字列*は、DACL (**D:** ) セキュリティコンポーネントを示すトークンを含む文字列です。

クラスインストーラー INF は、デバイスクラスのセキュリティ記述子を指定できます。 デバイスの INF では、個々のデバイスのセキュリティ記述子を指定して、クラスのセキュリティをオーバーライドできます。 クラスまたはデバイス INF で*セキュリティ記述子文字列*が指定されている場合、PnP マネージャーはデバイスのすべてのデバイスオブジェクト ( *DOs*) に記述子を伝達します。 これには、関数デバイスオブジェクト (*FDO*)、オプションの*フィルター DOS*、および PDO が含まれます。

セキュリティ記述子文字列の形式の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

セキュリティ記述子を指定する方法の詳細については、「セキュリティ[で保護されたデバイスのインストールの作成](creating-secure-device-installations.md)」を参照してください。

<a href="" id="upperfilters"></a>**UpperFilters**  
**UpperFilters** Hkr **AddReg**エントリは、PnP 上位フィルタードライバーを指定します。 このエントリは[***ddinstall * にあります。HW** ](inf-ddinstall-hw-section.md)セクションでは、デバイス固有の上位フィルタードライバーを1つ以上定義します。 [**ClassInstall32**](inf-classinstall32-section.md)セクションでは、このエントリはクラス全体の上位フィルタードライバーを1つ以上定義します。

<a href="" id="lowerfilters"></a>**LowerFilters**  
**LowerFilters** Hkr **AddReg**エントリは、PnP 下位フィルタードライバーを指定します。 このエントリは、 <em>Ddinstall</em>に含ま**れています。HW セクションで**は、デバイス固有の下位フィルタードライバーを1つ以上定義します。 **ClassInstall32**セクションでは、このエントリは1つ以上のクラス全体の下位フィルタードライバーを定義します。

<a href="" id="exclusive"></a>**外税**  
**排他**Hkr **AddReg**エントリが存在し、"1" に設定されている場合は、デバイスが*排他デバイス*であることを指定します。 それ以外の場合、デバイスは排他として扱われません。 詳細については、「[デバイスオブジェクトへの排他アクセスの指定](https://docs.microsoft.com/windows-hardware/drivers/kernel/specifying-exclusive-access-to-device-objects)」を参照してください。

<a href="" id="enumproppages32"></a>**EnumPropPages32**  
**EnumPropPages32** Hkr **AddReg**エントリは、デバイス固有のプロパティページプロバイダーであるダイナミックリンクライブラリ (*DLL*) ファイルの名前を指定します。 また、DLL によって実装される**Extensionpropsheet Pageproc** callback 関数の名前も指定します。 プロパティページおよび関数の詳細については、Microsoft Windows Software Development Kit (SDK) for Windows 7 および .NET Framework 4.0 を参照してください。

**重要**  DLL と**Extensionpropsheet pageproc** callback 関数の名前は、両方とも引用符 ("") で囲む必要があります。

 

<a href="" id="locationinformationoverride"></a>**LocationInformationOverride**  
(Windows XP 以降のバージョンの Windows)**Locationinformationoverride** Hkr **AddReg** entry を使用すると、デバイスの物理的な場所を記述するテキスト文字列を指定できます。 これは、デバイスのバスドライバーが[**IRP_MN_QUERY_DEVICE_TEXT**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-text)要求に応答して提供する**locationinformation**文字列をオーバーライドします。

<a href="" id="resourcepickertags"></a>**ResourcePickerTags**  
**ResourcePickerTags** Hkr **AddReg**エントリは、デバイスのリソースピッカータグを指定します。

<a href="" id="resourcepickerexceptions"></a>**ResourcePickerExceptions**  
**ResourcePickerExceptions** Hkr **AddReg**エントリは、デバイスで許可されるリソースの競合を指定します。

<a name="examples"></a>例
--------

**AddReg**ディレクティブは、この例の (SCSI) Miniport_EventLog_AddReg セクションを参照しています。この例では、 <em>Ddinstall</em>で**addservice**ディレクティブによって参照されている INF ライター定義セクションの下に**あります。** この INF のサービスセクション。

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

[***Ddinstall *.CoInstallers**](inf-ddinstall-coinstallers-section.md)

[***Ddinstall *.HW**](inf-ddinstall-hw-section.md)

[***Ddinstall *.インターフェイス**](inf-ddinstall-interfaces-section.md)

[***Ddinstall *.サービス**](inf-ddinstall-services-section.md)

[**DelReg**](inf-delreg-directive.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**Strings**](inf-strings-section.md)

 

 






