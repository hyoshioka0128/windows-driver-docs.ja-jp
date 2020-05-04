---
title: INF Manufacturer セクション
description: '[製造元] セクションでは、INF ファイルを使用してインストールできる1つまたは複数のデバイスの製造元を指定します。'
ms.assetid: c5128d0a-d581-4461-8eb9-5680b6b6ef38
keywords:
- INF の製造元セクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF Manufacturer Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48800a2794abf8caeaf5e90c94371b9e5c65aa26
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223142"
---
# <a name="inf-manufacturer-section"></a>INF Manufacturer セクション


[**製造元**] セクションでは、INF ファイルを使用してインストールできる1つまたは複数のデバイスの製造元を指定します。

```inf
[Manufacturer]

manufacturer-identifier
[manufacturer-identifier] 
[manufacturer-identifier] 
...
```

## <a name="entries"></a>エントリ


<a href="" id="manufacturer-identifier"></a>*製造元-識別子*  
製造元のデバイスモデルを識別する情報が含まれている製造元と INF セクションを一意に識別します。 各*製造元の識別子*のエントリは、別の行に存在し、次の形式を使用する必要があります。

```inf
manufacturer-name |
%strkey%=models-section-name |
%strkey%=models-section-name [,TargetOSVersion] [,TargetOSVersion] ...  (Windows XP and later versions of Windows)
```

これらのエントリは次のように定義されます。

<a href="" id="manufacturer-name"></a>*製造元-名前*  
デバイスの製造元を識別します。 INF には、同じ名前の対応する[**Inf*モデル*セクション**](inf-models-section.md)も含まれている必要があります。 製造元の名前の最大文字数は、LINE_LEN です。 (この方法で指定されたエントリはローカライズできません)。

<a href="" id="strkey-"></a>*strkey*   
製造元の名前を表す INF ファイル内で一意のトークンを指定します。 このような%*strkey*% token は、inf ファイルの[**inf 文字列セクション**](inf-strings-section.md)で定義されている必要があります。

<a href="" id="models-section-name"></a>*モデル-セクション名*  
INF ファイル内の製造元別[**Inf*モデル*セクション**](inf-models-section.md)に、inf ライターで定義されている名前を指定します。 この値は、INF ファイル内で一意である必要があります。また、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

<a href="" id="targetosversion"></a>*TargetOSVersion*  
さまざまな INF***モデル***セクションを使用できるターゲットオペレーティングシステムのバージョンを1つ以上指定します。 Windows は、実行されているオペレーティングシステムのバージョンに最も近い [INF***モデル***] セクションを選択します。

*TargetOSVersion*装飾の説明については、次の「**解説**」のセクションと、下記の例3の関連情報を参照してください。

**重要**: Windows SERVER 2003 SP1 以降では、inf ファイル**は、関連**付けられている inf***モデル***セクション名に加え、ntia64 または ntamd64 プラットフォーム拡張機能を使用して、モデルセクション名のエントリを修飾する必要があります。これにより、x86 以外のバージョンのオペレーティングシステムが指定されます。 これらのプラットフォーム拡張機能は、x86 ベースのオペレーティングシステムのバージョンの INF ファイル、または x64 ベースのアーキテクチャ用のファイルシステムドライバーの inf ファイルなどの非 PnP ドライバーの INF ファイルには必要ありません。

 

<a name="remarks"></a>解説
-------

1つまたは複数のデバイスをインストールするすべての INF ファイルには、"**製造元**" セクションが必要です。 通常、IHV/OEM が提供する INF ファイルでは、このセクションのエントリが1つだけ指定されています。 複数のエントリが指定されている場合は、各エントリが INF の別の行にある必要があります。

%*Strkey*%=*モデル-name*エントリを使用すると、国際対応の[inf ファイルの作成](creating-international-inf-files.md)に関するページおよび[**inf 文字列セクション**](inf-strings-section.md)のリファレンスページで説明されているように、国際市場向けの inf ファイルのローカライズが簡略化されます。

INF ファイルに*製造元名*の形式で1つ以上のエントリが指定されている場合、これらの各エントリは、inf 内の他の場所にある対応する***モデル***セクションの名前を暗黙的に指定します。

このセクションでは、各システムが提供する INF ファイルの**製造元**セクションを目次として考えることができます。このセクションでは、[デバイスセットアップクラス](device-setup-classes.md)のすべての製造元のデバイスモデルのインストールを設定します。 INF ファイルの [**製造元**] セクション内の各エントリには、製造元の名前に対して、簡単にローカライズ可能な%*strkey*% トークンと、製造元別の一意の***モデル***セクション名の両方が指定されています。

[**製造元**] セクションの [*モデル-セクション名*] エントリは、対象のオペレーティングシステムのバージョンを指定するように装飾できます。 さまざまなバージョンのオペレーティングシステムに対して、異なる[**INF*モデル*セクション**](inf-models-section.md)を指定できます。 指定されたバージョンは、INF***モデル***セクションが使用されているオペレーティングシステムのバージョンを示します。 バージョンが指定されていない場合、Windows では、すべてのバージョンのオペレーティングシステムに対して指定された***モデル***セクションを使用します。

Windows XP から Windows 10 バージョン1511の場合、 *TargetOSVersion*デコレーションの形式は次のようになります。

```inf
nt[Architecture][.[OSMajorVersion][.[OSMinorVersion][.[ProductType][.SuiteMask]]]]
```
Windows 10 バージョン 1607 (ビルド14310以降) では、 *TargetOSVersion*デコレーションの形式は次のようになります。
```inf
nt[Architecture][.[OSMajorVersion][.[OSMinorVersion][.[ProductType][.[SuiteMask][.[BuildNumber]]]]]
```

各フィールドは次のように定義されます。

<a href="" id="nt"></a>**r**  
ターゲットオペレーティングシステムが NT ベースであることを指定します。 Windows 2000 以降のバージョンの Windows はすべて NT ベースです。

<a href="" id="architecture"></a>*構造*  
ハードウェアプラットフォームを識別します。 指定する場合は、 **x86**、 **ia64**、 **amd64**、 **arm**、または**arm64**にする必要があります。

Windows Server 2003 SP1 より前では、*アーキテクチャ*が指定されていない場合、関連する INF***モデル***セクションは任意のハードウェアプラットフォームで使用できます。

Windows Server 2003 SP1 以降では、[ [**INF*モデル*] セクション**](inf-models-section.md)で、x86 以外のターゲットオペレーティングシステムバージョンのアーキテクチャを指定する必要があります。 アーキテクチャは、x86 ベースのオペレーティングシステムバージョンの場合は、[INF***モデル***] セクションの名前で省略できます。

<a href="" id="osmajorversion"></a>*OSMajorVersion*  
オペレーティングシステムのメジャーバージョン番号を表す番号。 次の表は、Windows オペレーティングシステムのメジャーバージョンを定義しています。

| Windows のバージョン        | メジャー バージョン |
|------------------------|---------------|
| Windows 10             | 10            |
| Windows Server 2012 R2 | 6             |
| Windows 8.1            | 6             |
| Windows Server 2012    | 6             |
| Windows 8              | 6             |
| Windows Server 2008 R2 | 6             |
| Windows 7              | 6             |
| Windows Server 2008    | 6             |
| Windows Vista          | 6             |
| Windows Server 2003 R2 | 5             |
| Windows Server 2003    | 5             |
| Windows XP             | 5             |
| Windows 2000           | 5             |

 

<a href="" id="osminorversion"></a>*OSMinorVersion*  
オペレーティングシステムのマイナーバージョン番号を表す番号。 次の表は、Windows オペレーティングシステムのマイナーバージョンを定義しています。

| Windows のバージョン        | マイナー バージョン |
|------------------------|---------------|
| Windows 10             | 0             |
| Windows Server 2012 R2 | 3             |
| Windows 8.1            | 3             |
| Windows Server 2012    | 2             |
| Windows 8              | 2             |
| Windows Server 2008 R2 | 1             |
| Windows 7              | 1             |
| Windows Server 2008    | 0             |
| Windows Vista          | 0             |
| Windows Server 2003 R2 | 2             |
| Windows Server 2003    | 2             |
| Windows XP             | 1             |
| Windows 2000           | 0             |

 

<a href="" id="producttype"></a>*ProductType*  
次のように、 *winnt.h*で定義されている VER_NT_xxxx フラグのいずれかを表す数値。

**0x0000001** (VER_NT_WORKSTATION)

**0x0000002** (VER_NT_DOMAIN_CONTROLLER)

**0x0000003** (VER_NT_SERVER)

製品の種類が指定されている場合は、オペレーティングシステムが指定した製品の種類と一致する場合にのみ、INF ファイルが使用されます。 INF が1つのオペレーティングシステムバージョンに対して複数の種類の製品をサポートしている場合は、複数の*TargetOSVersion*エントリが必要です。

<a href="" id="suitemask"></a>*SuiteMask*  
*Winnt.h*で定義されている1つ以上の VER_SUITE_xxxx フラグの組み合わせを表す数値。 これらのフラグには、次のものがあります。

**0x00000001** (VER_SUITE_SMALLBUSINESS)

**0x00000002** (VER_SUITE_ENTERPRISE)

**0x00000004** (VER_SUITE_BACKOFFICE)

**0x00000008** (VER_SUITE_COMMUNICATIONS)

**0x00000010** (VER_SUITE_TERMINAL)

**0x00000020** (VER_SUITE_SMALLBUSINESS_RESTRICTED)

**0x00000040** (VER_SUITE_EMBEDDEDNT)

**0x00000080** (VER_SUITE_DATACENTER)

**0x00000100** (VER_SUITE_SINGLEUSERTS)

**0x00000200** (VER_SUITE_PERSONAL)

**0x00000400** (VER_SUITE_SERVERAPPLIANCE)

1つまたは複数の suite マスク値を指定すると、オペレーティングシステムが指定されたすべての製品スイートと一致する場合にのみ、INF が使用されます。 INF が1つのオペレーティングシステムバージョンに対して複数の製品スイートの組み合わせをサポートしている場合は、複数の*TargetOSVersion*エントリが必要です。

<a href="" id="buildnumber"></a>*隣*  
ビルド14310以降で、セクションが適用される Windows 10 リリースの OS ビルド番号の最小値を表す数値。

ビルド番号は、特定の OS メジャー/マイナーバージョンに対してのみ相対的であると見なされ、将来の OS メジャー/マイナーバージョンに対してはリセットされる可能性があります。*TargetOSVersion*デコレーションによって指定されたビルド番号は、 *TargetOSVersion*の os メジャー/マイナーバージョンが現在の Os (または altplatforminfo) バージョンと完全に一致する場合にのみ評価されます。現在の OS バージョンが、 *TargetOSVersion*デコレーション (osmajorversion, OSMinorVersion) によって指定された os バージョンよりも大きい場合、指定されたビルド番号に関係なく、セクションは適用可能と見なされます。 同様に、現在の OS バージョンが*TargetOSVersion*デコレーションによって指定された os バージョンよりも小さい場合、セクションは適用されません。

ビルド番号が指定されている場合、 *TargetOSVersion*デコレーションの os バージョンと種類は、両方とも、このデコレーションが最初に導入された Windows 10 ビルド14310の os バージョンとビルド番号よりも大きい必要があります。  以前のバージョンのオペレーティングシステムでは、これらの変更がないと (たとえば、Windows 10 ビルド 10240)、不明な装飾は解析されないため、これらの以前のビルドを対象とすることによって、その OS が有効な装飾をまったく考慮しないようにすることができます。

*TargetOSVersion*装飾の詳細については、「[プラットフォーム拡張機能とオペレーティングシステムバージョンの組み合わせ](combining-platform-extensions-with-operating-system-versions.md)」を参照してください。

**重要**  windows XP 以降のバージョンの windows を対象とするオペレーティングシステムのプラットフォーム拡張機能を使用して、**製造元**および[***モデル***](inf-models-section.md)セクションの*モデルセクション名*のエントリを常に修飾することを強くお勧めします。 X86 ベースのハードウェアプラットフォームでは、 **nt**プラットフォーム拡張機能を使用しないでください。代わりに、 **ntx86**を使用してください。

 

INF に文字飾り付きの**製造元**セクションのエントリが含まれている場合は、オペレーティングシステムの装飾に一致する名前を持つ[**inf*モデル*のセクション**](inf-models-section.md)も含まれている必要があります。 たとえば、INF に次の**製造元**セクションが含まれているとします。

**% FooCorp% = FooMfg、NTx86....0x80、NTamd64**

次に、INF には次の名前の[**Inf*モデル*セクション**](inf-models-section.md)も含まれている必要があります。

-   **\[FooMfg.NTx86....0x80\]**

    この名前は、x86 ベースのハードウェアプラットフォーム上の windows XP およびそれ以降のバージョンの Windows のデータセンタースイートに適用されます。

-   **\[FooMfg.NTamd64\]**

    この名前は、x64 ベースのハードウェアプラットフォーム上の windows XP およびそれ以降のバージョンの Windows のすべての製品の種類とスイートに適用されます。

インストール中、Windows は次の方法で[**INF*モデル*セクション**](inf-models-section.md)を選択します。

1.  Windows が、データセンター製品スイートを含む x86 ベースバージョンのオペレーティングシステム (windows XP 以降のバージョン) で実行されている場合、windows は** \[FooMfg... NTx86 を選択します。0x80\] ** ***モデル***セクション。
2.  Windows が、すべての製品スイートについて x64 ベースバージョンのオペレーティングシステム (windows XP 以降のバージョン) で実行されている場合、windows は** \[FooMfg\] ** ***モデル***セクションを選択します。

INF が Windows XP より前のバージョンのオペレーティングシステムで使用する場合は、 ** \[FooMfg\]** という名前の非装飾***モデル***セクションも含まれている必要があります。

INF で複数の製造元がサポートされている場合は、製造元ごとにこれらの規則に従う必要があります。

*TargetOSVersion*デコレーションのその他の例を次に示します。

-   **% FooCorp% = FooMfg、NTx86**

    この例では、結果として得られる INF***モデル***セクション名は** \[FooMfg. NTx86\]** であり、任意の x86 バージョンのオペレーティングシステム (Windows XP 以降) に適用されます。

-   **% FooCorp% = FooMfg, NT. 7.8**

    この例では、バージョン7.8 以降のオペレーティングシステムでは、結果として得られる INF***モデル***セクション名は** \[FooMfg\]** です。 Windows XP などの以前のバージョンのオペレーティングシステムでは、 ** \[FooMfg\] **が使用されます。

セットアップで使用する INF***モデル***セクションの選択は、次の規則に基づいています。

-   いくつかのオペレーティングシステムのバージョン番号またはマイナーバージョンの inf [***モデル*セクション**](inf-models-section.md)が inf に含まれている場合、Windows では、インストールが実行されているオペレーティングシステムのバージョンよりも高いバージョン番号を使用します。
-   オペレーティングシステムのバージョンに一致する [INF***モデル***] セクションにも、製品の種類や製品スイートの装飾が含まれている場合、Windows は実行中のオペレーティングシステムに最も近いセクションを選択します。

たとえば、windows が Windows XP で実行されている場合 (バージョン 5.1)、Data Center 製品スイートは含まれていません。次のエントリが**製造元**のセクションにあります。

**% FooCorp% = FooMfg、nt、nt. 5、NT 5.5、NT...0x80**

この場合、Windows は** \[FooMfg\]** という名前の[**INF*モデル*セクション**](inf-models-section.md)を検索します。 Windows では、windows XP のデータセンターバージョンで実行されている場合は** \[FooMfg\] **セクションも使用します。これは、特定のバージョン番号が製品の種類とスイートマスクよりも優先されるためです。

INF で特定のオペレーティングシステムのバージョン、製品の種類、またはスイートを明示的に除外する場合は、[空の[**Inf*モデル*] セクション**](inf-models-section.md)を作成します。 たとえば、 ** \[FooMfg\] **という名前の空のセクションには、x86 ベースのオペレーティングシステムバージョン6.0 以降でのインストールが禁止されています。

<a name="examples"></a>例
--------

この例では、単一の IHV の INF に対する一般的な**製造元**のセクションを示します。

```inf
[Manufacturer]
%Mfg%=Contoso        ; Models section == Contoso

[Contoso]

; ...
[Strings]
Mfg = "Contoso, Ltd."
```

次の例は、デバイスクラス固有のインストーラーの INF に一般的に使用されている**製造元**セクションの一部を示しています。

```inf
[Manufacturer]
%CONTOSO%=Contoso_Section
; several entries omitted here for brevity
%FABRIKAM%=Fabrikam_Section
%ADATUM%=Adatum_Section
```

次の例は、x86 プラットフォーム、Windows XP 以降に固有の**製造元**セクションを示しています。

```inf
[Manufacturer]
%foo%=foosec,NTx86.5.1

[foosec.NTx86.5.1]
```

次の例は、x64 プラットフォーム、Windows 10 ビルド14393、およびそれ以降に固有の**製造元**セクションを示しています。

```inf
[Manufacturer]
%foo%=foosec,NTamd64.10.0...14393

[foosec.NTamd64.10.0...14393]
```

次の2つの例は、さまざまな OS 固有の INF*モデル*セクションで構成されたスケルトンファイルを示しています。

例 1:

```inf
[Manufacturer]
%MyName% = MyName,NTx86.5.1
.
[MyName]
%MyDev% = InstallA,hwid
.
[MyName.NTx86.5.1]
%MyDev% = InstallB,hwid
.
[InstallA]   ; Windows 2000 
.
.
[InstallB]   ; Windows XP and later, x86 only
.
```

例 2:

```inf
[Manufacturer]
%MyName% = MyName,NTx86.6.0,NTx86.5.1,
.
[MyName.NTx86.6.0] ; Empty section, so this INF does not support
.                  ; NT 6.0 and later.
.
[MyName.NTx86.5.1] ; Used for NT 5.1 and later
.                  ; (but not NT 6.0 and later due to the NTx86.6.0 entry)
%MyDev% = InstallB,hwid
.
[MyName]           ; Empty section, so this INF does not support
.                  ; Win2000
.
```

例 3: 

```inf
[Manufacturer]
%MyMfg% = MyMfg, NTamd64.6.1, NTamd64.10.0, NTamd64.10.0...14310
.
[MyMfg.NTamd64.6.1]          ; Used for Windows 7 and later
.                            ; (but not for Windows 10 and later due to the NT.10.0 entry)
.
[MyMfg.NTamd64.10.0]         ; Used for Windows 10
.                            ; (but not for Windows 10 build 14393 and later due to the NT.10.0...14393 entry)
.
[MyMfg.NTamd64.10.0...14393] ; Used for Windows 10 build 14393 and later
.
.
```
**注**: 複数の TargetOSVersions を指定する場合は、次の例に示すように、1つのエントリに文字列を結合します。  各ターゲットを個別のエントリとして表すことはできません。 

## <a name="see-also"></a>関連項目


[プラットフォーム拡張機能とオペレーティング システム バージョンを組み合わせる](combining-platform-extensions-with-operating-system-versions.md)

[***モデル***](inf-models-section.md)

[**文字列**](inf-strings-section.md)

 

 






