---
title: INF AddPowerSetting ディレクティブ
description: AddPowerSetting ディレクティブは、電源設定情報の変更または作成に使用される1つ以上のセクションを参照します。
ms.assetid: 0231ba90-5de4-4f5a-83bb-0f73be4b23ae
keywords:
- INF AddPowerSetting ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF AddPowerSetting Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8738f4b0a98f94843ea39daf2ad87c5f0bdf2b9
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223114"
---
# <a name="inf-addpowersetting-directive"></a>INF AddPowerSetting ディレクティブ


**Addpowersetting**ディレクティブは、電源設定情報の変更または作成に使用される1つ以上のセクションを参照します。 各 [パワー設定の*追加] セクション*では、電源設定、電源設定に使用できる値、電源設定のフレンドリ名、電源設定の説明を定義します。 また、[パワー*設定の追加] セクション*では、各電源設定パーソナリティの既定値も指定します。 電源設定と電源設定個性の詳細については、「[デバイスパフォーマンス状態の管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-device-performance-states)」を参照してください。

```inf
[DDInstall] | 
[DDInstall.HW] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows Vista)
[ClassInstall32.ntamd64]  (Windows Vista)
[ClassInstall32.ntarm] 
[ClassInstall32.ntarm64]  



AddPowerSetting=add-power-setting-section[,add-power-setting-section]
```

一般に、*追加-設定-セクション*には次のディレクティブが含まれています。

-   **サブグループ**ディレクティブ。
-   **設定**ディレクティブ
-   2つ以上の**値**ディレクティブまたは1つの**ValueRange**ディレクティブの一覧。
-   6つの**既定**のディレクティブのセット。

*パワー設定の追加セクション*は、次の2つの形式のいずれかを使用します。

-   許容される電源設定値を2つ以上の不連続値のセットとして定義できる場合は、次のように、**値**ディレクティブの一覧を使用して、使用可能な値を指定します。

    ```inf
    [add-power-setting-section]

    [SubGroup = {subgroup-guid}] | SubGroup = {subgroup-guid}, subgroup-name, subgroup-description, subgroup-icon
    Setting = {setting-guid}, [setting-name],[setting-description],[setting-icon]
    Value = value-index, value-name,[value-description], value-flags, value-data 
    Value = value-index, value-name,[value-description], value-flags, value-data
    [Value = value-index, value-name,[value-description], value-flags, value-data
    ...
    Value = value-index, value-name,[value-description], value-flags, value-data]

    (Six required Default directives, each one of which has the following form)
    Default = power-scheme-personality-GUID, AC/DC-index, default-setting-index | default-setting-value 
    ...
    ```

-   許容される電源設定値を、指定した範囲内の負でない整数値のインクリメントシーケンスとして定義することが最適な場合は、次のように、1つの**ValueRange**ディレクティブを使用して、許可される値を指定します。

    ```inf
    [add-power-setting-section]

    [SubGroup = {subgroup-guid}] | 
    SubGroup = {subgroup-guid}, subgroup-name, subgroup-description, subgroup-icon
    Setting = {setting-guid}, [setting-name],[setting-description],[setting-icon]
    ValueRange = range-minimum-value, range-maximum-value, range-increment, [range-unit-label] 

    (Six required Default directives, each one of which has the following form)
    Default = power-scheme-personality-GUID, AC/DC-index, default-setting-index | default-setting-value 
    ...
    ```

## <a name="entries"></a>エントリ


**メモ**  *値データ*のエントリを除き、文字列値を指定する次のすべてのエントリでは、「 [addpowersetting 文字列エントリ値を指定](#specifying-an-addpowersetting-string-entry-value)する」で説明されている方法のいずれかで文字列を指定できます。

 

<a href="" id="subgroup"></a>**グループ**  
サブグループは、論理的に関連する電源設定をグループ化します。

システム定義のサブグループを指定するには **、サブグループディレクティブを**含め、*サブグループ guid*エントリだけを指定します。 システム定義サブグループは、 *Wdm*で定義されている GUID_*Xxx*_SUBGROUP と NO_SUBGROUP_GUID の定数によって表されます。

たとえば、GUID_VIDEO_SUBGROUP は、電源設定パーソナリティのビデオ電源設定を含むサブグループを表します。 NO_SUBGROUP_GUID 定数は、論理的にサブグループに属していない設定のコレクションを表します。 **サブグループ**ディレクティブが含まれていない場合、既定では、どのサブグループにも論理的に属していない設定のコレクションに設定が追加されます。

新しいサブグループを定義するには、**サブ**グループディレクティブを含め、必要なエントリ (*サブグループ-guid*、*サブグループ名*、*サブグループ、説明*、*サブグループ)* を指定します。 新しいサブグループの GUID は一意である必要があり、その他のエントリは可能な限りわかりやすいものにする必要があります。

<a href="" id="subgroup-guid"></a>*サブグループ-guid*  
必須エントリは、サブグループを識別する GUID を指定します。 このエントリの形式は **{**<em>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</em>**}** です。ここで、"X" は16進数字です。

たとえば、システム定義定数 GUID_VIDEO_SUBGROUP の値は {7516B95F-F776-4464-8C53-06167F40CC99} です。 この GUID は、電源設定パーソナリティのビデオ電源設定が含まれているサブグループを表します。

<a href="" id="subgroup-name"></a>*サブグループ名*  
電源設定のサブグループ名を指定する文字列。 サブグループがシステム定義のサブグループである場合、このエントリを指定することはできません。 サブグループが新規の場合は、このエントリが必要です。

<a href="" id="subgroup-description"></a>*サブグループ-説明*  
ユーザーに対して、電源サブグループを説明する文字列。 サブグループがシステム定義のサブグループである場合、このエントリを指定することはできません。 サブグループが新規の場合は、このエントリが必要です。

<a href="" id="subgroup-icon"></a>*サブグループ-アイコン*  
アイコンリソースへの参照。 サブグループがシステム定義のサブグループである場合、このエントリを指定することはできません。 サブグループが新規の場合は、このエントリが必要です。

アイコンリソースは、言語に依存しないレジストリ値として指定する必要があります。 言語に依存しないレジストリ値を指定する方法については、「 [AddPowerSetting 文字列エントリ値の指定](#specifying-an-addpowersetting-string-entry-value)」を参照してください。

<a href="" id="setting"></a>**設定**  
**設定**ディレクティブは、セクション内の他のすべてのエントリが適用される設定を識別します。 アドオンの追加セクションでは、1つの**設定**ディレクティブが必要です。また、設定ディレクティブは、[パワー設定の追加] セクション**で1つ**しか指定できません。 INF ファイルで複数の設定が定義されている場合は、それぞれの設定を独自の [電源設定] セクションで定義する必要があります。

**設定**ディレクティブに関連付けられているエントリを次に示します。

<a href="" id="setting-guid"></a>*設定-guid*  
電源設定を表す GUID を指定する必須のエントリです。 このエントリの形式は **{**<em>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</em>**}** です。ここで、各 "X" は16進数字です。

たとえば、次に示すのはカスタム GUID 値 {BFC0D9E9-549C-483D-AD2A-3D90C98A8B03} です。

<a href="" id="setting-name"></a>*設定-名前*  
電源設定のフレンドリ名を含む文字列を指定する、省略可能なエントリです。 コントロールパネルの [**電源オプション**] には、この表示名がユーザーに表示されます。

<a href="" id="setting-description"></a>*設定-説明*  
ユーザーに対して電源設定を説明する文字列と、その設定がシステムの電源とパフォーマンスに与える影響を指定する、省略可能なエントリです。

<a href="" id="setting-icon"></a>*設定-アイコン*  
アイコンリソースへの参照である省略可能なエントリ。 アイコンリソースは、言語に依存しないレジストリ値で指定する必要があります。

言語に依存しないレジストリ値を指定する方法については、「 [AddPowerSetting 文字列エントリ値の指定](#specifying-an-addpowersetting-string-entry-value)」を参照してください。

<a href="" id="value"></a>**数値**  
**値**ディレクティブは、電源設定に使用できる値を定義します。 値を2つ以上の値のセットとして定義できる場合**は、値ディレクティブを**使用する必要があります。各値は、値固有のカスタムデータ型を持つことができます。 このような場合は、追加-設定-セクションに2つ以上の**値**ディレクティブが含まれている必要があります。 ユーザーは、コントロールパネルの [**電源オプション**] でこれらの値のいずれかを選択して、電源設定を構成できます。

許容される電源設定値が、範囲内で負でない整数のインクリメントされたセットとして記述されている場合は、 **Value**ディレクティブの代わりに**ValueRange**ディレクティブを使用して、使用可能な電源設定値を指定します。

<a href="" id="value-index"></a>*値-インデックス*  
0以上の一意のインデックス値を指定し、対応する設定値を参照するために使用される、必須のエントリです。 コントロールパネルの [**電源オプション**] には、対応するインデックス値の順にユーザーの電源設定値が表示されます。

<a href="" id="value-name"></a>*値-名前*  
対応する設定値のフレンドリ名を指定する文字列を提供する必須のエントリです。 コントロールパネルの [**電源オプション**] には、ユーザーに対する電源設定値のフレンドリ名が表示されます。

<a href="" id="value-description"></a>*値-説明*  
ユーザーに対して、電源設定の値、および設定値がシステムの電源とパフォーマンスに与える影響について説明する文字列を提供する、省略可能なエントリ。

<a href="" id="value-flags"></a>*値-フラグ*  
次の表に示すように、対応する値データのエントリのデータ型を指定する必須のエントリです。

| フラグ値 | データ型   |
|------------|-------------|
| 0x00000001 | [REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types) |
| 0x00010001 | [REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)  |
| 0x00000000 | [REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)     |

 

<a href="" id="value-data"></a>*値-データ*  
対応する設定値のデータを提供する必須のエントリ。次に示すように、対応する*値フラグ*エントリによって指定されるデータ型によって異なります。

-   [REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)値は、0x 表記を使用して16進数形式で指定できます。または、0x 表記のないペアの16進数値のコンマ区切りのリストとして指定することもできます。

    たとえば、次のエントリは同等です。0xFEDCBA9876543210 と、ペアになっている16進数字のコンマ区切りのリスト: FE、DC、BA、98、76、54、32、10。

-   [REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)値は、16進数形式 (0x 表記を使用) または10進数形式で指定できます。
-   [REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)値は、二重引用符 ("*引用符で*囲まれた文字列") で囲まれた文字列、または Inf ファイルの inf[**文字列**](inf-strings-section.md)セクションで定義されている%*strkey*% token としてのみ表現できます。

**メモ**  ローカライズできないため、文字列値は使用しないでください。 代わりに、型[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)または[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)の値を使用してください。

 

<a href="" id="valuerange"></a>**ValueRange**  
許容される電源設定値が、指定された範囲内の負でない整数値のインクリメントシーケンスとして最も適切に定義される場合は、 **ValueRange**ディレクティブを使用します。 電源マネージャーは、コントロールパネルの [**電源オプション**] でユーザーが選択した設定が、これらの許可されている値のいずれかであることを検証します。 許容される値のセットは、許容される最小値、最大許容値、および範囲内で許容される値間のインクリメントによって決定されます。 値は次を満たす場合に許可されます。

```inf
range-minimum-value + k*range-increment
```

*範囲の最小値*が0以上で、 *k*と*範囲のインクリメント*が1以上で、値が*範囲の最大値*以下である場合は、値が1以上になります。 さらに、*範囲-最大値*は、k の範囲の*最小値* + から*k*\**範囲*の範囲で指定する必要があります。

たとえば、*範囲の最小値*が0、範囲の*最大値*が10、*範囲の増分*値が2の場合、許容される値は、0、2、4、6、8、および10になるようになります。

許容される電源設定の値を値の一覧として最もよく記述できる場合は、各値が値固有のカスタムデータ型を持つことができる場合は、 **ValueRange**ディレクティブではなく**値**ディレクティブを使用します。

<a href="" id="range-minimum-value"></a>*範囲-最小値*  
許容される最小電源設定を指定する[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)型の値。

<a href="" id="range-maximum-value"></a>*範囲-最大値*  
許容される電源設定の最大値を指定する[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)型の値。 最大値は、最小値以上にする必要があります。0より大きい整数*k*の場合は、最小値以上 + *\*k 範囲のインクリメント*と等しくする必要があります。

<a href="" id="range-increment-"></a>*範囲-増分*   
0より大きい[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)型の値です。 この値は、*範囲の最小値*と*最大値の範囲*で指定される包括範囲内の連続する値の差を指定します。

<a href="" id="range-unit-label-"></a>*範囲-単位-ラベル*   
電源設定の値を説明する、省略可能な文字列。 文字列は、*設定名*と共に、入力するデータの種類をユーザーに通知します。

たとえば、文字列を使用して、"minutes" や "%" (パーセントを表す) などの値の単位を指定できます。

<a href="" id="default"></a>**標準**  
**Addpowersetting**セクションに含める必要がある**既定**のディレクティブは6つあります。 **既定**のディレクティブは、AC 電源状態に適用される3つのシステム定義の電源設定個性の1つ、および DC 電源状態に適用される3つのシステム定義電源設定個性の既定値を指定します。

既定値が有効で正確であることが非常に重要です。 ユーザーが電源設定を手動で設定していない場合は、**既定**のディレクティブで指定されている既定値が使用されます。

<a href="" id="power-scheme-personality-guid"></a>*電源設定-パーソナリティ-GUID*  
次の Guid のいずれかで、既定値が適用される電源設定を指定します。

| パーソナリティ      | GUID                                   |
|------------------|----------------------------------------|
| 省電力      | {A1841308-3541-4FAB-BC81-F71556F20B4A} |
| 高パフォーマンス | {8C5E7FDA-E8BF-4A96-9A85-A6E23A8C635C} |
| Balanced         | {381B4222-F61K 4-1F0-9685FF5BB260DF2E} |

 

これらの Guid は、 *Wdm*で定義されています。

<a href="" id="ac-dc-index"></a>*AC/DC-インデックス*  
*Ac/dc-index*が0の場合、設定は ac 電源状態に適用され、 *ac/dc-index*が1の場合は、設定が DC 電源状態に適用されます。 0または1以外の値は無効です。

<a href="" id="default-setting-index-"></a>*既定値-インデックス*   
**Value**ディレクティブを使用して許可された値を指定した場合、*既定の設定-インデックス*は**値**ディレクティブの*値インデックスエントリ*の値になります。 **ValueRange**ディレクティブを使用して許可値を指定した場合、このエントリは適用されません。

<a href="" id="default-setting-value-"></a>*既定値-値*   
**ValueRange**ディレクティブを使用して許可される値を指定する場合、 **ValueRange**ディレクティブで指定されている許可値の1つとして、*既定*値が使用されます。 **Value**ディレクティブを使用して許可される値を指定する場合、このエントリは適用されません。

<a name="remarks"></a>解説
-------

*追加のパワー設定セクション*名は、inf ファイル内で一意である必要がありますが、同じ inf ファイル内の複数の**addpowersetting**ディレクティブで参照できます。 各セクション名は、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」で説明されている一般的な規則に従う必要があります。

デバイスをアンインストールした後、電源マネージャーによってデバイスの電源ポリシーが自動的に削除されることはありません。 電源設定、値、および既定値のインストールまたは削除は、 *Powrprof*で定義されているシステム指定の電源設定ルーチンを使用して、共同インストーラーによって実行できます。 これらの電源管理ルーチンの詳細については、Microsoft Windows SDK のドキュメントに記載されている電源管理のリファレンスを参照してください。

また、 *Powercfg*コマンドラインツールを使用して、電源設定を変更することもできます。 *Powercfg*の詳細については、Microsoft ヘルプとサポートセンターを参照してください。

システム定義の**nt**、 **ntx86**、. **ntia64**、. **ntamd64**、. **ntarm**、および**ntarm64**の各拡張機能の使用方法の詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の INF ファイルの作成](creating-inf-files-for-multiple-platforms-and-operating-systems.md)」を参照してください。

### <a name="specifying-an-addpowersetting-string-entry-value"></a>AddPowerSetting 文字列エントリ値の指定

[REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)型の*値データ*のエントリを除き、 **addpowersetting**ディレクティブで指定される他のすべての文字列エントリ値は、二重引用符 ("*引用符で*囲まれた文字列") で囲まれた文字列として、または inf ファイルの inf 文字列セクションで定義されている%*strkey*% トークン、または言語に依存しないレジストリ値として

言語に依存しないレジストリ値は、Windows の多言語ユーザーインターフェイス (MUI) をサポートするために使用され、次のように指定されています。

```inf
"@file-path,-resourceID[;comment]"
```

言語に依存しないレジストリ値を指定するエントリは、次のとおりです。

<a href="" id="file-path"></a>*ファイルパス*  
リソースを格納しているファイルの完全修飾パス。

<a href="" id="resourceid"></a>*resourceID*  
対応するリソースのリソース ID。 文字列の場合、 *resourceID*は文字列を参照します。 アイコンの場合、 *resourceID*はアイコンを参照します。

<a href="" id="comment"></a>*関する*  
デバッグを支援したり、設定に関する追加のコメントを提供したりするために使用できる省略可能な値。 文字列リソースの場合、電源マネージャーは、指定されたリソース文字列とコメント文字列を結合または表示しません。

言語に依存しないレジストリ値を指定する方法の詳細については、「[シェルとレジストリ文字列のレンダリング](https://go.microsoft.com/fwlink/p/?linkid=70407)」を参照してください。

<a name="examples"></a>例
--------

次の2つの例では、LCD の明るさを制御する電源設定を定義します。 最初の例では、 **Value**ディレクティブを使用して、最小、中、および LCD の明るさの最大値を定義する方法を示します。

```inf
// Within a DDinstall or ClassInstall23 section
AddPowerSetting=LCDDim
...

[LCDDim]
SubGroup = {7516B95F-F776-4464-8C53-06167F40CC99}
Setting = {381B4222-F694-41F0-9685-FF5BB260DF2E}, "LCD Brightness", "Controls the brightness of the LCD display"

Value = 0, "Low", "Minimum Brightness", %FLG_ADDREG_TYPE_DWORD%, 0x50
Value = 1, "Medium", "Medium Brightness", %FLG_ADDREG_TYPE_DWORD%, 0x75
Value = 2, "High", "Maximum Brightness", %FLG_ADDREG_TYPE_DWORD%, 0x100

Default = %GUID_MAX_POWER_SAVINGS%, %AC%, 0
Default = %GUID_MAX_POWER_SAVINGS%, %DC%, 0
Default = %GUID_TYPICAL_POWER_SAVINGS%, %AC%, 2
Default = %GUID_TYPICAL_POWER_SAVINGS%, %DC%, 1
Default = %GUID_MIN_POWER_SAVINGS%, %AC%, 2
Default = %GUID_MIN_POWER_SAVINGS%, %DC%, 2
...

[Strings]
GUID_MAX_POWER_SAVINGS = {a1841308-3541-4fab-bc81-f71556f20b4a}
GUID_TYPICAL_POWER_SAVINGS = {381b4222-f694-41f0-9685-ff5bb260df2e}
GUID_MIN_POWER_SAVINGS = {8c5e7fda-e8bf-4a96-9a85-a6e23a8c635c}
AC = 0
DC = 1
FLG_ADDREG_TYPE_DWORD = 0x00010001
```

2番目の例では、 **ValueRange**ディレクティブを使用して、許容される LCD 輝度値の範囲を定義しています。これは、許可されている値の間に1% のインクリメントを使用して、0% ~ 100% に変化します。

```inf
// Within a DDinstall or a ClassInstall23 section
AddPowerSetting=LCDDimRange
...

[LCDDimRange]
SubGroup = {7516B95F-F776-4464-8C53-06167F40CC99}
Setting = {381B4222-F694-41F0-9685-FF5BB260DF2E}, "LCD Brightness", "Controls the brightness of the LCD display"
ValueRange = 0, 100, 1, "%"
Default = %GUID_MAX_POWER_SAVINGS%, %AC%, 50
Default = %GUID_MAX_POWER_SAVINGS%, %DC%, 50
Default = %GUID_TYPICAL_POWER_SAVINGS%, %AC%, 95
Default = %GUID_TYPICAL_POWER_SAVINGS%, %DC%, 50
Default = %GUID_MIN_POWER_SAVINGS%, %AC%, 100
Default = %GUID_MIN_POWER_SAVINGS%, %DC%, 100

[Strings]
GUID_MAX_POWER_SAVINGS = {a1841308-3541-4fab-bc81-f71556f20b4a}
GUID_TYPICAL_POWER_SAVINGS = {381b4222-f694-41f0-9685-ff5bb260df2e}
GUID_MIN_POWER_SAVINGS = {8c5e7fda-e8bf-4a96-9a85-a6e23a8c635c}
AC = 0
DC = 1
```

## <a name="see-also"></a>関連項目


[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。CoInstallers**](inf-ddinstall-coinstallers-section.md)

[***DDInstall *。ハードウェア**](inf-ddinstall-hw-section.md)

[***DDInstall *。インターフェイス**](inf-ddinstall-interfaces-section.md)

[***DDInstall *。サーヴィス**](inf-ddinstall-services-section.md)

 

 






