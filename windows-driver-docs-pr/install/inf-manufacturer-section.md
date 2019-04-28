---
title: INF Manufacturer セクション
description: 製造元のセクションでは、INF ファイルを使用してインストールできる 1 つまたは複数のデバイスの製造元を識別します。
ms.assetid: c5128d0a-d581-4461-8eb9-5680b6b6ef38
keywords:
- 製造元の INF セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF Manufacturer Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ee959c01e9d4070aee4042ccc7951e53a19292f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378462"
---
# <a name="inf-manufacturer-section"></a>INF Manufacturer セクション


**製造元**セクションは、INF ファイルを使用してインストールできる 1 つまたは複数のデバイスの製造元を識別します。

```ini
[Manufacturer]

manufacturer-identifier
[manufacturer-identifier] 
[manufacturer-identifier] 
...
```

## <a name="entries"></a>エントリ


<a href="" id="manufacturer-identifier"></a>*製造元識別子*  
製造元および製造元のデバイス モデルを識別する情報を格納する INF セクションを一意に識別します。 各*製造元識別子*エントリが個別の行に存在し、次の形式を使用します。

```ini
manufacturer-name |
%strkey%=models-section-name |
%strkey%=models-section-name [,TargetOSVersion] [,TargetOSVersion] ...  (Windows XP and later versions of Windows)
```

これらのエントリの定義は次のとおりです。

<a href="" id="manufacturer-name"></a>*製造元の名前*  
デバイスの製造元を識別します。 INF では、対応するを含める必要がありますも[ **INF*モデル*セクション**](inf-models-section.md)の同じ名前です。 製造元の名前、文字の最大長は、LINE_LEN です。 (この方法で指定したエントリはローカライズできません。)

<a href="" id="strkey-"></a>*strkey*   
製造元の名前を表す INF ファイル内で一意で、トークンを指定します。 このような各 %*strkey*で % トークンを定義する必要があります、 [ **INF 文字列セクション**](inf-strings-section.md)の INF ファイル。

<a href="" id="models-section-name"></a>*models-section-name*  
製造元の INF ライター定義名を指定[ **INF*モデル*セクション**](inf-models-section.md) INF ファイル内で。 この値は、INF ファイル内で一意である必要があります、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、次を参照してください。 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)します。

<a href="" id="targetosversion"></a>*TargetOSVersion*  
1 つまたは複数のターゲット オペレーティング システムのバージョンを指定するさまざまな INF***モデル***セクションを使用できます。 Windows の選択、INF***モデル***実行されているオペレーティング システムのバージョンに最も近いセクション。

**注意**:上記の C++ コードでは、複数 TargetOSVersions は 1 つのエントリに表示されます。  これは、複数の TargetOSVersions を追加する正しい方法です。  別のエントリは、各ターゲットを表していません。  次の例 3 の関連情報を参照してください。


説明については、 *TargetOSVersion*の装飾は、次を参照してください。**解説**セクション。

**重要な**:  Windows Server 2003 SP1 以降、INF ファイルはモデルのセクション名のエントリを装飾する必要があります、 **INF 製造元セクション**、および関連付けられている INF***モデル***.ntia64 の名前のセクションまたはします。x86 以外を指定する ntamd64 プラットフォーム拡張機能は、オペレーティング システムのバージョンを対象します。 X86 ベースのターゲット オペレーティング システムのバージョンの INF ファイルまたは x64 ベースのアーキテクチャのファイル システム ドライバーの INF ファイルなどの非 PnP ドライバーの INF ファイルでは、これらのプラットフォーム拡張機能は必要はありません。

 

<a name="remarks"></a>コメント
-------

INF ファイルを 1 つまたは複数のデバイスをインストールする必要がありますが、**製造元**セクション。 通常、IHV と OEM 提供の INF ファイルはこのセクションでは 1 つのエントリのみを指定します。 複数のエントリが指定されている場合、INF の個別の行に各エントリがある必要があります。

% を使用して*strkey*%=*モデル セクション名*エントリには、国際市場向けの INF ファイルのローカライズが簡素化」の説明に従って[International INF の作成ファイル](creating-international-inf-files.md)とリファレンスのページの[ **INF 文字列セクション**](inf-strings-section.md)します。

INF ファイルを 1 つまたは複数のエントリを指定する場合、*製造元名*形式では、このような各エントリに対応する名前を暗黙的に指定する***モデル***他の場所で、INF セクション。

各システムが指定した INF ファイルの考えられる**製造元**用のデバイス モデルのすべての製造元のインストールをこのセクションに設定するために、目次としてセクション、[デバイス セットアップ クラス](device-setup-classes.md). INF ファイルの各エントリ**製造元**セクションでは、どちらも、簡単にローカライズ可能な % を指定します*strkey*、製造元とを一意にする-、-INF あたり-の製造元の名前の % トークン***モデル。*** セクション名。

*モデル セクション名*内のエントリ、**製造元**セクションは、ターゲット オペレーティング システムのバージョンを指定する修飾できます。 異なる[ **INF*モデル*セクション**](inf-models-section.md)オペレーティング システムの異なるバージョンを指定できます。 指定されたバージョンがオペレーティング システムのバージョンを示すため、INF***モデル***セクションが使用されています。 Windows を使用して、指定したバージョンが指定されていない場合***モデル***セクションのすべてのオペレーティング システムのすべてのバージョン。

Windows 10、バージョン 1511 の形式の Windows XP の*TargetOSVersion*の装飾は、次のようにします。

```ini
nt[Architecture][.[OSMajorVersion][.[OSMinorVersion][.[ProductType][.SuiteMask]]]]
```
以降では、Windows 10 バージョン 1607 (ビルド 14310 およびそれ以降) 形式の*TargetOSVersion*の装飾は、次のようにします。
```ini
nt[Architecture][.[OSMajorVersion][.[OSMinorVersion][.[ProductType][.[SuiteMask][.[BuildNumber]]]]]
```

各フィールドの定義は次のとおりです。

<a href="" id="nt"></a>**nt**  
対象のオペレーティング システムでは、NT ベースを指定します。 Windows 2000 および以降のバージョンの Windows NT ベースのすべてが。

<a href="" id="architecture"></a>*アーキテクチャ*  
ハードウェア プラットフォームを識別します。 指定する場合、この必要がありますで**x86**、 **ia64**、 **amd64**、 **arm**、または**arm64**します。

Windows Server 2003 SP1 より前場合*アーキテクチャ*が指定されていない、関連付けられている INF***モデル***セクションは、任意のハードウェア プラットフォームで使用できます。

Windows Server 2003 SP1 以降、アーキテクチャで指定されなければなりません[ **INF*モデル*セクション**](inf-models-section.md) x86 以外の名前は、オペレーティング システムのバージョンを対象します。 アーキテクチャは INF で省略可能な***モデル***セクション x86 ベースのターゲット バージョンのオペレーティング システムの名前。

<a href="" id="osmajorversion"></a>*OSMajorVersion*  
オペレーティング システムのメジャー バージョン番号を表す数値。 次の表では、Windows オペレーティング システムのメジャー バージョンを定義します。

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
オペレーティング システムのマイナー バージョン番号を表す数値。 次の表では、Windows オペレーティング システムのマイナー バージョンを定義します。

| Windows のバージョン        | ［マイナー バージョン］ |
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
VER_NT_xxxx フラグの 1 つを表す数で定義*Winnt.h*次のようします。

**0x0000001** (VER_NT_WORKSTATION)

**0x0000002** (VER_NT_DOMAIN_CONTROLLER)

**0x0000003** (VER_NT_SERVER)

製品の種類が指定されている場合、INF ファイルは、オペレーティング システムが指定された製品の種類と一致する場合にのみに使用されます。 場合は、INF は、単一のオペレーティング システムのバージョンでは、複数の製品の種類をサポートしている複数*TargetOSVersion*エントリが必要です。

<a href="" id="suitemask"></a>*SuiteMask*  
定義されている VER_SUITE_xxxx フラグの 1 つ以上の組み合わせを表す番号*Winnt.h*します。 これらのフラグを以下に示します。

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

1 つまたは複数のスイート マスク値を指定する場合、INF は、オペレーティング システムには、すべての指定された製品スイートが一致する場合にのみ使用されます。 場合は、INF は、単一のオペレーティング システムのバージョンでは、複数の製品スイートの組み合わせをサポートしている複数*TargetOSVersion*エントリが必要です。

<a href="" id="buildnumber"></a>*BuildNumber*  
最小の OS を表す数値はビルドのセクションが該当する、ビルド 14310 以降、またはそれ以降を Windows 10 のリリース番号です。

ビルド番号では、いくつか特定の OS メジャー/マイナー バージョンのみを基準としたと見なされます、将来の OS メジャー/マイナー バージョンをリセットすることがあります。  任意で指定された数のビルド、 *TargetOSVersion*装飾が OS のメジャー/マイナー バージョンの場合にのみ評価される、 *TargetOSVersion*現在の OS (または AltPlatformInfo) のバージョンを正確に一致します。  現在の OS バージョンがで指定された OS バージョンよりも大きい場合、 *TargetOSVersion*装飾 (OSMajorVersion、OSMinorVersion) セクションが指定されたビルド番号に関係なく適用できると見なされます。 同様に、現在の OS バージョンがで指定された OS バージョンよりも小さいかどうか*TargetOSVersion*の装飾は、セクションは適用されません。

ビルド番号は、指定した場合、OS のバージョンとの BuildNumber、 *TargetOSVersion*装飾する必要があります OS バージョンよりも大きくして、Windows 10 ビルドこの装飾が初めて導入された 14310 のビルド番号。  ターゲットのビルド前の試行が実際に妨げるその OS 検討、装飾のすべての有効なこれらの変更 (Windows 10 ビルド 10240 など) することがなく、オペレーティング システムの以前のバージョンは、不明な装飾を解析できません。

詳細については、 *TargetOSVersion*の装飾を参照してください[プラットフォーム拡張機能バージョンのオペレーティング システムと組み合わせて](combining-platform-extensions-with-operating-system-versions.md)します。

**重要な**  常に装飾ことを強くお勧め*モデル セクション名*内のエントリ、**製造元**と[ ***モデル***](inf-models-section.md)プラットフォーム拡張機能は、ターゲットのオペレーティング システムを含むセクションでは Windows XP または Windows の以降のバージョン。 X86 ベースのハードウェア プラットフォームでの使用を避ける必要があります、 **.nt**プラットフォーム拡張機能と使用 **.ntx86**代わりにします。

 

INF が含まれている場合**製造元**装飾セクション エントリも含める必要があります[ **INF*モデル*セクション**](inf-models-section.md)名前を持つオペレーティング システムの飾り付けに一致します。 例では、INF に、次が含まれている場合、**製造元**セクション。

**%FooCorp%=FooMfg, NTx86....0x80, NTamd64**

INF に含める必要がありますも[ **INF*モデル*セクション**](inf-models-section.md)で次の名前。

-   **\[FooMfg.NTx86....0x80\]**

    この名前は、Windows XP のデータ センターのスイートで、Windows の x86 ベースのハードウェア プラットフォームでの以降のバージョンに適用されます。

-   **\[FooMfg.NTamd64\]**

    この名前は、すべての商品の種類と Windows XP のスイートと x64 ベースのハードウェア プラットフォームでの以降のバージョンの Windows に適用されます。

インストール中に、Windows の選択、 [ **INF*モデル*セクション**](inf-models-section.md)次のように。

1.  Windows が x86 ベースのバージョンのデータ センターの製品スイートを含むオペレーティング システム (Windows XP またはそれ以降のバージョン) で実行している場合に、Windows が選択、 **\[FooMfg.NTx86.0x80\]** ***モデル***セクション。
2.  Windows が x64 ベース バージョンのすべての製品スイートのオペレーティング システム (Windows XP またはそれ以降のバージョン) で実行している場合に、Windows が選択、 **\[FooMfg.NTamd64\]** ***モデル***セクション。

Windows XP より前のオペレーティング システムのバージョンで使用するため、INF する場合、含める必要があります、装飾されていない***モデル***という名前のセクション **\[FooMfg\]** します。

INF では、複数のメーカーをサポートする場合、これらのルールが各製造元の後にする必要があります。

その他の例を次に*TargetOSVersion*装飾します。

-   **%FooCorp% = FooMfg, NTx86**

    この例では、結果の INF で***モデル***セクション名は **\[FooMfg.NTx86\]** は、x86 の適用とオペレーティング システムのバージョン (Windows XP またはそれ以降)。

-   **%FooCorp% = FooMfg, NT.7.8**

    Version 7.8 と以降のオペレーティング システム、結果の INF に、この例では***モデル***セクション名は **\[FooMfg.NT.7.8\]** します。 以前のバージョンの Windows XP など、オペレーティング システムの**\[FooMfg.NT\]** 使用されます。

どの INF のセットアップの選択***モデル***を使用するセクションは、次の規則に基づきます。

-   INF が含まれている場合[ **INF*モデル*セクション**](inf-models-section.md)の主要ないくつかの場合、またはオペレーティング システムのバージョン番号のマイナー Windows 使用セクションには、最上位のバージョン番号をインストールを配置に時間がオペレーティング システムのバージョンよりも高いではありません。
-   場合、INF***モデル***を Windows が実行中のオペレーティング システムに最も一致するセクションを選択して、オペレーティング システムのバージョンに一致するセクションでは、製品の種類や製品スイートの装飾にも含まれます。

たとえば、Windows せず、データ センター製品スイートでは、Windows XP (バージョン 5.1) で実行されているして次のエントリが見つかるとします、**製造元**セクション。

**%FooCorp%=FooMfg, NT, NT.5, NT.5.5, NT....0x80**

ここでは Windows、 [ **INF*モデル*セクション**](inf-models-section.md)という **\[FooMfg.NT.5\]** します。 Windows を使用しても、 **\[FooMfg.NT.5\]** セクション、Windows XP のデータ センターのバージョンで実行する場合のため、特定のバージョン番号、製品の種類とスイートのマスクよりも優先されます。

空の作成、INF、特定のオペレーティング システムのバージョン、製品の種類、またはスイートを明示的に除外する場合は、 [ **INF*モデル*セクション**](inf-models-section.md)します。 という名前の空のセクションなど**\[FooMfg.NTx86.6.0\]** バージョン 6.0 以降のオペレーティング システムの x86 ベースのインストールを禁止します。

<a name="examples"></a>使用例
--------

この例では、**製造元**の 1 つの IHV、INF を一般的なセクションです。

```ini
[Manufacturer]
%Mfg%=Contoso        ; Models section == Contoso

[Contoso]

; ...
[Strings]
Mfg = "Contoso, Ltd."
```

次の例の一部を示しています、**製造元**デバイス クラス固有のインストーラーの INF を一般的なセクション。

```ini
[Manufacturer]
%CONTOSO%=Contoso_Section
; several entries omitted here for brevity
%FABRIKAM%=Fabrikam_Section
%ADATUM%=Adatum_Section
```

次の例は、**製造元**x86 に固有のセクション プラットフォームでは、Windows XP 以降。

```ini
[Manufacturer]
%foo%=foosec,NTx86.5.1

[foosec.NTx86.5.1]
```

次の例は、**製造元**x64 に固有のセクションのプラットフォーム、Windows 10 ビルド 14393 以降。

```ini
[Manufacturer]
%foo%=foosec,NTamd64.10.0...14393

[foosec.NTamd64.10.0...14393]
```

次の 2 つの例は、さまざまな OS 固有の INF のスケルトンの INF ファイルを表示する*モデル*セクション。

例 1:

```ini
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

```ini
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

```ini
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
**注意**:複数 TargetOSVersions を指定するときに文字列にまとめて 1 つのエントリでこの例のようにです。  別のエントリは、各ターゲットを表していません。 

## <a name="see-also"></a>関連項目


[オペレーティング システムのバージョンとプラットフォームの拡張機能を組み合わせること](combining-platform-extensions-with-operating-system-versions.md)

[***モデル***](inf-models-section.md)

[**文字列**](inf-strings-section.md)

 

 






