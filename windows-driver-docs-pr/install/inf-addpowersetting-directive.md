---
title: INF AddPowerSetting ディレクティブ
description: AddPowerSetting ディレクティブを変更するか電源設定の情報の作成に使用される 1 つまたは複数のセクションを参照します。
ms.assetid: 0231ba90-5de4-4f5a-83bb-0f73be4b23ae
keywords:
- INF AddPowerSetting ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF AddPowerSetting Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7285dcf05973b87c886ce0a9db0a90d65f0d421
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537826"
---
# <a name="inf-addpowersetting-directive"></a>INF AddPowerSetting ディレクティブ


**AddPowerSetting**ディレクティブが変更または電源設定の情報の作成に使用される 1 つまたは複数のセクションを参照します。 各*追加設定 power セクション*電源設定、電源設定、電源設定のフレンドリ名と電源設定の説明に使用できる値を定義します。 *追加設定 power セクション*も各電源スキーム パーソナリティの既定値を指定します。 電源設定と電源スキーム個性の詳細については、[管理デバイスのパフォーマンス状態](https://msdn.microsoft.com/library/windows/hardware/ff554353)を参照してください。

```ini
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

一般に、*追加設定 power セクション*次のディレクティブが含まれます。

-   A**サブグループ**ディレクティブ。
-   A**設定**ディレクティブ
-   2 つ以上の一覧**値**ディレクティブまたは**ValueRange**ディレクティブ。
-   一連の 6 つ**既定**ディレクティブ。

*追加設定 power セクション*は次の 2 つの可能な形式のいずれか。

-   一覧を使用して、許可されている電源設定の値が最適な 2 つ以上の離散値のセットとして定義されていることができる場合、**値**ディレクティブを次のように、許可されている値を指定します。

    ```ini
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

-   場合は許可されている電源設定の値が指定した範囲内の負以外の整数値のインクリメントのシーケンスとして最適なは、1 つを使用して、 **ValueRange**ディレクティブを次のように、許可されている値を指定します。

    ```ini
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


**注**  を除き、*値データ*エントリ、文字列値を指定するすべて、次のエントリで指定できます文字列で説明されている方法のいずれか[AddPowerSetting を指定します。エントリの値を文字列](#specifying-an-addpowersetting-string-entry-value)します。

 

<a href="" id="subgroup"></a>**サブグループ**  
サブグループには、論理的に関連する電源設定がグループ化します。

システム定義のサブグループを指定する、**サブグループ**ディレクティブを指定のみ、*サブグループ guid*エントリ。 システム定義のサブグループが GUID_ 定数によって表される*Xxx*_SUBGROUP とで定義されている、NO_SUBGROUP_GUID *Wdm.h*します。

たとえば、GUID_VIDEO_SUBGROUP は電源スキームのパーソナリティのビデオの電源設定を含んだサブグループを表します。 NO_SUBGROUP_GUID 定数は、すべてのサブグループに論理的に属していない設定のコレクションを表します。 場合、**サブグループ**ディレクティブが含まれていない、設定は既定では、コレクションに追加のサブグループに論理的に属していない設定します。

新しいサブグループを定義するには、**サブグループ**ディレクティブし、次の必要なエントリを指定:*サブグループ guid*、*サブグループ名*、 *サブグループ説明*、および*サブグループ アイコン。* 新しいサブグループの GUID は一意である必要があり、その他のエントリをできるだけわかりやすいものにする必要があります。

<a href="" id="subgroup-guid"></a>*サブグループの guid*  
必要なエントリは、サブグループを識別する GUID を提供します。 このエントリの形式が **{**<em>XXXXXXXX XXXX XXXX XXXXXXXXXXXX</em>**}**"X"は 16 進数です。

たとえば、定数 GUID_VIDEO_SUBGROUP のシステム定義の値は、{7516B95F-F776-4464-8C53-06167F40CC99}。 この GUID は、電源スキームのパーソナリティのビデオの電源設定を含んだサブグループを表します。

<a href="" id="subgroup-name"></a>*subgroup-name*  
電源設定のサブグループの名前を指定する文字列。 サブグループがシステム定義のサブグループである場合は、このエントリを指定しない必要があります。 サブグループが新しい場合は、このエントリが必要です。

<a href="" id="subgroup-description"></a>*サブグループの説明*  
電源サブグループをユーザーに説明する文字列。 サブグループがシステム定義のサブグループである場合は、このエントリを指定しない必要があります。 サブグループが新しい場合は、このエントリが必要です。

<a href="" id="subgroup-icon"></a>*subgroup-icon*  
アイコン リソースへの参照。 サブグループがシステム定義のサブグループである場合は、このエントリを指定しない必要があります。 サブグループが新しい場合は、このエントリが必要です。

アイコン リソースは、言語に依存しないレジストリ値として指定する必要があります。 言語に依存しないレジストリ値を指定する方法については、[AddPowerSetting 文字列エントリの値を指定する](#specifying-an-addpowersetting-string-entry-value)を参照してください。

<a href="" id="setting"></a>**設定**  
**設定**ディレクティブは、設定を指定します。 すべてのセクションではその他のエントリが適用されます。 1 つ**設定**ディレクティブが電源設定の追加のセクションで必要なのみ 1 つできます**設定**電源設定の追加のセクションではディレクティブ。 INF ファイルには、1 つ以上の設定が定義されている場合、追加電源設定 セクションで、独自の各設定を定義する必要があります。

関連付けられているエントリを次に、**設定**ディレクティブ。

<a href="" id="setting-guid"></a>*設定 guid*  
電源設定を表す GUID を指定する必要なエントリです。 このエントリの形式が **{**<em>XXXXXXXX XXXX XXXX XXXXXXXXXXXX</em>**}**"X"は 16 進数です。

たとえば、次は、カスタム GUID 値: {BFC0D9E9-549C-483D-AD2A-3D90C98A8B03}。

<a href="" id="setting-name"></a>*設定名*  
電源設定のフレンドリ名を含む文字列を指定する省略可能なエントリです。 **電源オプション**コントロール パネルの ユーザーにわかりやすい名前が表示されます。

<a href="" id="setting-description"></a>*設定の説明*  
電源設定と設定がシステムの能力とパフォーマンスに与える影響をユーザーに説明する文字列を指定する省略可能なエントリです。

<a href="" id="setting-icon"></a>*setting-icon*  
アイコン リソースへの参照は、省略可能なエントリです。 言語に依存しないレジストリ値では、アイコン リソースを指定してください。

言語に依存しない-レジストリ値を指定する方法については、[AddPowerSetting 文字列エントリの値を指定する](#specifying-an-addpowersetting-string-entry-value)を参照してください。

<a href="" id="value"></a>**値**  
A**値**ディレクティブは、電源設定の許容値を定義します。 **値**ディレクティブを使用する場合、2 つ以上の値のセットとしては、値が適切に定義されたそれぞれの値が値に固有のカスタム データ型を持つことができます。 このような状況で、追加の電源の設定-セクションを 2 つ以上含める必要があります**値**ディレクティブ。 ユーザーがこれらの値のいずれかを選択できる**電源オプション**電源設定を構成するコントロール パネルの します。

許可されている電源設定の値が最適な正の整数の範囲内のインクリメントのセットとして記述されていることができる場合に、使用して、 **ValueRange**ディレクティブの代わりに、**値**許可されているを指定するディレクティブ電源設定の値。

<a href="" id="value-index"></a>*value インデックス*  
大きいまたは 0 以上であるし、対応する値の設定の参照に使用される、一意のインデックス値を指定する必要なエントリです。 **電源オプション**コントロール パネルの 電源設定を値に、対応するインデックスの値の順序でのユーザーから最も低い最高が表示されます。

<a href="" id="value-name"></a>*値の名前*  
設定の対応する値のフレンドリ名を提供する文字列を提供する必要なエントリです。 **電源オプション**コントロール パネルの ユーザーの電源設定の値のフレンドリ名が表示されます。

<a href="" id="value-description"></a>*値の説明*  
電源設定の値と設定値がシステムの能力とパフォーマンスに与える影響をユーザーに説明する文字列を提供する省略可能なエントリです。

<a href="" id="value-flags"></a>*値フラグ*  
次の表に示されているように、対応する値のデータ エントリのデータ型を指定する必要なエントリです。

| フラグの値 | データの種類   |
|------------|-------------|
| 0x00000001 | [REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types) |
| 0x00010001 | [REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)  |
| 0x00000000 | [REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)     |

 

<a href="" id="value-data"></a>*値データ*  
対応する指定されたデータ型に対応する設定の値のデータを提供する必要なエントリ、される形式依存*値フラグ*次のように、エントリ。

-   A [REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)値は、0 x 表記では、ペアの 16 進数 0 x 表記なしのコンマ区切りのリストを使用して、16 進数形式で指定することができます。

    たとえば、次のエントリは同等です。0xFEDCBA9876543210 とペアになっているの 16 進数字の次のコンマ区切り一覧。FE、DC、BA、98、76、54、32、10。

-   A [REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types) (表記を使用して 0 x) の 16 進形式で、またはの値を指定できます 10 進形式。
-   A [REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)のみ二重引用符で囲まれた文字列として値を表現できます ("*引用符で囲まれた文字列*") または % として*strkey*INFで定義されている%トークン[**文字列**](inf-strings-section.md) INF ファイルのセクション。

**注**  ローカライズすることはできませんがあるため、文字列値を使用しないでください。 代わりに、型の値を使用して、 [REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)または[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)します。

 

<a href="" id="valuerange"></a>**ValueRange**  
使用して、 **ValueRange**ディレクティブが許可されている電源設定の値が最適な場合は、指定した範囲内の正の整数値のインクリメントのシーケンスとして定義します。 電源マネージャーを検証する、ユーザーが選択した設定**電源オプション**はコントロール パネルの 使用できる値のいずれか。 許可されている値のセットが決定されます値、および範囲内で許可されている値のインクリメントで値を許容される最小、最大が使用できます。 値が許可されるは、次を満たす場合。

```ini
range-minimum-value + k*range-increment
```

場所*範囲の最小値*より大きいまたは 0 以上では、 *k*と*範囲インクリメント*小さいが、1つと、値に等しいかより大きい*範囲と最大値*します。 さらに、*範囲と最大値*必要があります*範囲の最小値* + *k*\**範囲インクリメント*のいくつかの k。

たとえば、*範囲の最小値*を 0 に等しい、*範囲と最大値*10 に等しくないと*増分値の範囲*2 に等しいか、使用できる値は次のように。0、2、4、6、8、および 10。

許可されている電源設定の値を場所の各値は、値に固有のカスタム データ型には、値のリストとして記述できます最適な場合は、使用、**値**ディレクティブの代わりに、 **ValueRange**ディレクティブ。

<a href="" id="range-minimum-value"></a>*範囲の最小値*  
型の値[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)最小の許可されている電源設定を指定します。

<a href="" id="range-maximum-value"></a>*範囲値の最大値*  
型の値[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)最大許可されている電源設定の値を指定します。 最大値の最小値以上にする必要があり、範囲の最小値と等しい必要があります + *k\*範囲インクリメント*、いくつかの整数の*k*が 0 より大きくなります。

<a href="" id="range-increment-"></a>*増分値の範囲*   
型の値[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)が 0 より大きいをします。 この値によって指定される範囲内の連続する値の差を指定する*範囲の最小値*と*範囲と最大値*します。

<a href="" id="range-unit-label-"></a>*range-unit-label*   
電源設定の値を記述する省略可能な文字列。 文字列、と共に*設定名*、入力データの種類のユーザーに通知されます。

たとえば、"minutes"または「%」(パーセントを表す) などの値の単位を指定する文字列を使用できます。

<a href="" id="default"></a>**既定値**  
6 つを使用する必要がある**既定**ディレクティブに含める必要がありますが、 **AddPowerSetting**セクション。 A**既定**ディレクティブが AC 電源の状態に適用される 3 つのシステム定義の電源スキーム個性と DC 電源の状態に適用される 3 つのシステム定義の電源スキームの性格のいずれかの既定値を指定します。

既定値が有効であり、正確なをすることが非常に重要です。 電源マネージャーで指定されている既定値を使用して、ユーザーが電源設定を手動で設定されていない場合、**既定**ディレクティブ。

<a href="" id="power-scheme-personality-guid"></a>*電源スキーム パーソナリティ GUID*  
次の Guid は、既定値が適用される電源設定の識別の 1 つ。

| 性格      | GUID                                   |
|------------------|----------------------------------------|
| [省電力]      | {A1841308-3541-4FAB-BC81-F71556F20B4A} |
| 高パフォーマンス | {8C5E7FDA-E8BF-4A96-9A85-A6E23A8C635C} |
| 分散         | {381B4222-F694-41F0-9685-FF5BB260DF2E} |

 

これらの Guid が定義されている*Wdm.h*します。

<a href="" id="ac-dc-index"></a>*AC/DC のインデックス*  
場合*AC/DC インデックス*が 0 の場合、設定、AC 電源の状態に適用される場合*AC/DC インデックス*は 1 です。 DC 電源の状態に設定が適用されます。 0 または 1 以外の値が無効です。

<a href="" id="default-setting-index-"></a>*既定のインデックス設定*   
場合、**値**ディレクティブを使用して、許可されている値を指定する*既定のインデックス設定*の値である、 *value インデックス エントリ*の**値**ディレクティブ。 場合、 **ValueRange**ディレクティブを使用して、許可されている値を指定する、このエントリは適用されません。

<a href="" id="default-setting-value-"></a>*既定の設定値*   
場合、 **ValueRange**ディレクティブを使用して、許可されている値を指定する*既定の設定値*で指定されている許可値の 1 つは、 **ValueRange**ディレクティブ。 場合、**値**ディレクティブを使用して、許可されている値を指定する、このエントリは適用されません。

<a name="remarks"></a>注釈
-------

*追加設定 power セクション*、INF ファイルで名前が一意である必要がありますが、1 つ以上で参照できる**AddPowerSetting**同じ INF ファイルでディレクティブ。 各セクション名が記載されている一般的な規則に従う必要があります[INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)します。

電源マネージャーはデバイスの電源ポリシーがデバイスのアンインストール後に自動的に削除していません。 定義されているシステム提供の電源設定のルーチンを共同インストーラーによって電源設定、値、および既定のインストールまたは削除を実行できる*Powrprof.h*します。 これらの電源管理ルーチンの詳細については、Microsoft Windows sdk に付属しているクライアント管理のリファレンスを参照してください。

さらに、 *Powercfg.exe*電源設定を変更するコマンド ライン ツールを使用できます。 について*Powercfg.exe*、Microsoft ヘルプとサポート センターを参照してください。

詳細については、システム定義を使用する方法についての **.nt**、 **.ntx86**、 **.ntia64**、 **.ntamd64**、 **.ntarm**、および **.ntarm64** 、拡張機能を参照してください[INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](creating-inf-files-for-multiple-platforms-and-operating-systems.md)します。

### <a name="specifying-an-addpowersetting-string-entry-value"></a>AddPowerSetting 文字列エントリの値を指定します。

除く*値データ*の種類のエントリ[REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)、すべての他の文字列エントリの値が用意されています、 **AddPowerSetting**ディレクティブは、文字列として表現できます二重引用符で囲む ("*引用符で囲まれた文字列*")、% として*strkey*% トークン文字列のセクションでは、INF ファイル、または言語に依存しないレジストリの値として INF で定義されています。

言語に依存しないレジストリの値は、Windows Multilingual User Interface (MUI) をサポートするために使用し、次のように指定されます。

```ini
"@file-path,-resourceID[;comment]"
```

言語に依存しないレジストリ値を指定したエントリは次のとおりです。

<a href="" id="file-path"></a>*ファイル パス*  
リソースを含むファイルの完全修飾パス。

<a href="" id="resourceid"></a>*ResourceID*  
対応するリソースのリソース ID。 文字列の場合、 *resourceID*文字列を参照します。 場合は、アイコン、 *resourceID*アイコンを参照します。

<a href="" id="comment"></a>*コメント*  
デバッグを支援する、または、設定に関するその他のコメントを提供するために使用できる省略可能な値。 場合は、文字列リソースを電源マネージャー結合またはしませんコメント文字列は、文字列が指定されたリソースを表示します。

言語に依存しないレジストリ値を指定する方法の詳細については、[シェルのレンダリングとレジストリの文字列](https://go.microsoft.com/fwlink/p/?linkid=70407)を参照してください。

<a name="examples"></a>例
--------

次の 2 つの例では、LCD の明るさを制御する電源設定を定義します。 最初の例は、使用する方法を示します、**値**ディレクティブを少なくとも、中規模、および最大 LCD の明るさの値を定義します。

```ini
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

2 番目の例は、使用する方法を示します、 **ValueRange**ディレクティブを異なる 0% から 100% で、許可されている値の間で 1% がインクリメントされたは許可されている LCD の明るさの値の範囲を定義します。

```ini
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

[***DDInstall *。共同インストーラー**](inf-ddinstall-coinstallers-section.md)

[***DDInstall *。ハードウェア**](inf-ddinstall-hw-section.md)

[***DDInstall *。インターフェイス**](inf-ddinstall-interfaces-section.md)

[***DDInstall *。サービス**](inf-ddinstall-services-section.md)

 

 






