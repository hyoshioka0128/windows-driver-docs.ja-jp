---
title: INF ファイルのセクションではモニター
description: INF ファイルのセクションではモニター
ms.assetid: f5208b6a-00b0-446e-82f7-eb26082ed9a5
keywords:
- 表示されるセクションでは Windows 2000 の WDK INF ファイルを監視します。
- Windows 2000 の WDK の INF ファイルを表示します。
- ライター定義 INF セクション WDK Windows 2000 の表示します。
- DDInstall セクション WDK Windows 2000 の表示
- モデルのセクション WDK Windows 2000 の表示
- SourceDisksFiles WDK Windows 2000 セクションを表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be80268e6a106f6e9118d3d1274137288d6c8c10
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550848"
---
# <a name="monitor-inf-file-sections"></a>INF ファイルのセクションではモニター


## <span id="ddk_monitor_inf_file_sections_gg"></span><span id="DDK_MONITOR_INF_FILE_SECTIONS_GG"></span>


モニターは、INF ファイルを使用して NT ベースのオペレーティング システムにインストールする必要があります。 INF ファイル、サンプルの監視を提供する Windows Driver Kit (WDK) *monsamp.inf*モニターの INF ファイルを生成するテンプレートとして使用する必要があります。 使用することはできません、 *geninf.exe*で説明されているツール[グラフィックス INF ファイルの作成](creating-graphics-inf-files.md)モニター INF を生成します。

このトピックの残りの部分のコメントのセクションの一部を*monsamp.inf*モニター INF ライターに特定の関心のあります。 INF ファイルの概要については、[INF ファイルのセクションとディレクティブ](https://msdn.microsoft.com/library/windows/hardware/ff547433)を参照してください。

Extended Display Identification Data (EDID) のモニターを上書きするのに、INF ファイルを使用することもできます。 参照してください[オーバーライド、INF でモニター EDIDs](overriding-monitor-edids.md)します。

### <a name="span-idsourcedisksfilessectionspanspan-idsourcedisksfilessectionspanspan-idsourcedisksfilessectionspansourcedisksfiles-section"></a><span id="SourceDisksFiles_Section"></span><span id="sourcedisksfiles_section"></span><span id="SOURCEDISKSFILES_SECTION"></span>SourceDisksFiles セクション

インストールの監視中にコピーする必要がありますファイルを配置する必要があります、 **\[SourceDisksFiles\]** セクション。 次の例を識別します。*icm*配布ディスク 1 上にあるファイル。

```inf
[SourceDisksFiles]
profile1.icm=1
```

詳細については、[ **INF SourceDisksFiles セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547472)を参照してください。 参照してください[プロファイルを監視する](monitor-profiles.md)色の管理とプロファイルの詳細についてはします。

### <a name="span-idmodelssectionspanspan-idmodelssectionspanspan-idmodelssectionspanmodels-section"></a><span id="Models_Section"></span><span id="models_section"></span><span id="MODELS_SECTION"></span>モデルのセクション

指定された製造元でサポートされている各モデルに関する情報を格納する、*モデル*セクション。 次の例では、ACME によって製造された 2 つのモデルを識別します。

```inf
[ACME]
%ACME-1234%=ACME-1234.Install, Monitor\MON12AB
%ACME-5678%=ACME-5678.Install, Monitor\MON34CD
```

各モデルは、1 行で表されます。 各行には、3 つの要素が含まれています。

-   モデルの名前 - たとえば、 **%%acme-1234**は実際のモデル名を表すトークンです (これに含まれる、**文字列**セクション)。

-   後続リンク*DDInstall*セクション - たとえば、 **ACME 1234 します。インストール**以降へのリンクは、  **\[ACME 1234 します。インストール\]** セクション。

-   ハードウェア id - たとえば、式**モニター\\MON12AB**デバイスのようにデバイス クラス (モニター) とデバイスの識別 (MON12AB) を組み合わせた*EDID*.

詳細については、[ **INF モデル セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547456)を参照してください。

### <a name="span-idddinstallsectionspanspan-idddinstallsectionspanspan-idddinstallsectionspanddinstall-section"></a><span id="DDInstall_Section"></span><span id="ddinstall_section"></span><span id="DDINSTALL_SECTION"></span>DDInstall セクション

*DDInstall*でドライバーを指定されたデバイスをインストールするときに実行する操作についての情報を提供します。 このセクションでは各の行または複数のさまざまな INF ライター定義セクションに INF ファイルに後で表示されるリンクを提供します。 次の例は、 *DDInstall* ACME 1234 モデルのセクション。

```inf
[ACME-1234.Install]
DelReg=DEL_CURRENT_REG
AddReg=ACME-1234.AddReg, 1280, DPMS
CopyFiles=ACME-1234.CopyFiles
```

-   [**** ](https://msdn.microsoft.com/library/windows/hardware/ff547374)ディレクティブ--へのリンクを提供する、 **DEL\_現在\_REG**セクションで、削除するレジストリ キーの詳細。

-   [**AddReg** ](https://msdn.microsoft.com/library/windows/hardware/ff546320) --ディレクティブは、3 つのセクションへのリンクを提供します。 レジストリ キーを追加するは詳細に説明します。 これらのセクションは**ACME 1234 します。AddReg**、 **1280**、および**ラインナップ**します。

-   [**CopyFiles** ](https://msdn.microsoft.com/library/windows/hardware/ff546346)ディレクティブ--へのリンクを提供する、 **ACME 1234 します。CopyFiles**セクションで、配布のディスクまたはディスクからコピーされるファイルを指定します。

詳細については、[ **INF DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)を参照してください。

### <a name="span-idinfwriter-definedsectionsspanspan-idinfwriter-definedsectionsspanspan-idinfwriter-definedsectionsspaninf-writer-defined-sections"></a><span id="INF_Writer-Defined_Sections"></span><span id="inf_writer-defined_sections"></span><span id="INF_WRITER-DEFINED_SECTIONS"></span>ライター定義のセクションでは INF

INF ファイル内で一意である場合、INF ライター定義のセクションでは、任意の名前ことができます。 これらのセクションでは、他のセクションでディレクティブによってポイントされてです。 次の箇条書き項目から、INF ライター定義セクションの説明*monsamp.inf*:

-   **DEL\_現在\_REG**セクション--値がインストールされます。 4 つのレジストリ キーを識別します。**モード**、 **MaxResolution**、**ラインナップ**、および**ICMProfile**します。 これらのキーは、後続のセクションで新しい値で適切に更新されます。

    ```inf
    [DEL_CURRENT_REG]
    HKR,MODES
    HKR,,MaxResolution
    HKR,,DPMS
    HKR,,ICMProfile
    ```

-   **1280**セクション - 更新プログラム、 **MaxResolution**レジストリ キーを示す文字列値。

    ```inf
    [1280]
    HKR,,MaxResolution,,"1280, 1024"
    ```

-   **ラインナップ**セクション - 更新プログラム、**ラインナップ**レジストリ キーを 1 (TRUE) にします。 電源管理をサポートしていないモニターでは、次の行を設定する必要があります代わりに、**ラインナップ**キー値を 0 (FALSE)。

    ```inf
    [DPMS]
    HKR,,DPMS,,1
    ```

-   **AddReg**)。 そのため、**モード**EDID または EDID の解釈に問題が存在する場合にのみ、INF のキー値を使用する必要があります。

    各サブキーを**モード**キー、解像度を指定してされる特定のタイミングまたはタイミングの範囲を指定する値を 9 個まで含めることができます。 各サブキーの名前の解決は、幅と高さ--をコンマで区切られた - 2 つの整数値の組み合わせである必要があります。 特定のタイミングがから名前付き**モード 1 の場合**に**Mode9**します。 名前付けは、連続している必要があります。 文字列値では、ダッシュ (-)、最大値の後に続けて、単一の値または範囲が最小値として指定した場合、範囲として指定するパルスを水平および垂直方向の同期の頻度を許可します。 頻度の値は現在のみ無視小数点に続く任意の数字で整数として解釈されます。 文字列を指定する水平および垂直方向の同期信号の極性を許可します。 ただし、これらの極性の値は無視されています。 各文字列の水平方向の同期が最大のパルス値のみが必要です。 たとえば、各サブキーの文字列の角かっこ内の情報が省略可能なを次に示します。

    ```inf
    [{MinHSync}-]{MaxHSync}[,{MinVSync}-{MaxVSynx}] 
    ```

    したがって、垂直同期範囲なし各サブキーの文字列で指定できます。 ただし、一連の垂直同期なしのサブキーの文字列を指定するは推奨されません。

    次のセットの最初の行、 **"モード\\1280,1024"** サブキーに示されている文字列値。 同じ行は、このサブキーの値の名前も識別**モード 1 の場合**します。 最初の文字列の次の番号のペア、**モード 1 の場合**サブキー KHz で水平方向の同期の周波数の範囲を指定します。 この文字列の番号の次の組み合わせでは、Hz で垂直同期の周波数の範囲を指定します。 2 番目の行で、 **PreferredMode**レジストリ キーが付随する文字列内に表示される値に設定します。 推奨される画面モードの (ピクセル単位) および画面のリフレッシュ レートでヘルツ (Hz) で、水平方向と垂直方向の解像度の両方を設定する文字列の値が使用されます。 ある水平方向と垂直方向の解像度の値が必要な**PreferredMode**文字列。 たとえば、次に示しますの場合、 **PreferredMode**文字列、角かっこ内の情報は省略可能です。

    ```inf
    {Width},{Height}[,{Frequency}]
    ```

    そのため、優先モードは、頻度を指定できます。 ただし、頻度を優先モードを指定するは推奨されません。

    3 番目の行セット、 **ICMProfile**文字列値にキー **"profile1.icm"** します。

    ```inf
    [ACME-1234.AddReg]
    HKR,"MODES\1280,1024",Mode1,,"27.0-106.0,55.0-160.0,+,+"
    HKR,,PreferredMode,,"1024,768,70"
    HKR,,ICMProfile,0,"profile1.icm"
    ```

    モニターをお勧め、sRGB の仕様を満たすには、モニターのプロファイルは必要ありません。

