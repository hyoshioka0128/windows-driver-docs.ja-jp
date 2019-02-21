---
title: 低リソース シミュレーション
description: 低リソース シミュレーション
ms.assetid: 2710fa23-26cd-493b-abb4-3a0969a98eb1
keywords:
- 低リソース シミュレーション オプション WDK Driver Verifier
- メモリ不足は、WDK の Driver Verifier を確認します。
- メモリ不足は、WDK の Driver Verifier を確認します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe03c5ca66904d7232fe3ca078610f0dfdea4d68
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539280"
---
# <a name="low-resources-simulation"></a>低リソース シミュレーション


## <span id="ddk_low_resources_simulation_tools"></span><span id="DDK_LOW_RESOURCES_SIMULATION_TOOLS"></span>


場合低リソース シミュレーション オプション (と呼ばれる*低リソース シミュレーションをランダム化*Windows 8.1 で) がアクティブな場合は、Driver Verifier にエラーが発生、ドライバーのメモリの割り当てのランダムなインスタンスで、ドライバーが実行されている場合に発生する可能性があります、十分なメモリを備えたコンピューター。 これは、メモリ不足とその他のリソース不足状態に適切に対応するドライバーの機能をテストします。

低リソース シミュレーション テストの失敗など、いくつかの異なる機能への呼び出しによって要求された割り当て[ **ExAllocatePoolWithXXX**](https://msdn.microsoft.com/library/windows/hardware/ff544520)、 [ **MmGetSystemAddressForMdlSafe**](https://msdn.microsoft.com/library/windows/hardware/ff554559)、 [ **MmProbeAndLockPages**](https://msdn.microsoft.com/library/windows/hardware/ff554664)、 [ **MmMapLockedPagesSpecifyCache** ](https://msdn.microsoft.com/library/windows/hardware/ff554629)、および[ **MmMapIoSpace**](https://msdn.microsoft.com/library/windows/hardware/ff554618)します。

Windows Vista 以降、低リソース シミュレーション テストも挿入エラーに[ **IoAllocateIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548257)、 [ **IoAllocateMdl**](https://msdn.microsoft.com/library/windows/hardware/ff548263)、[ **IoAllocateWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff548276)、 [ **IoAllocateErrorLogEntry**](https://msdn.microsoft.com/library/windows/hardware/ff548245)、 [ **MmAllocateContiguousMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554460)、 [ **MmAllocateContiguousMemorySpecifyCache**](https://msdn.microsoft.com/library/windows/hardware/ff554464)、 [ **MmAllocatePagesForMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff554482)、および[ **MmAllocatePagesForMdlEx**](https://msdn.microsoft.com/library/windows/hardware/ff554489)します。 さらへの呼び出し以降、Windows Vista では低リソース シミュレーションが有効にすると、 [ **KeWaitForMultipleObjects** ](https://msdn.microsoft.com/library/windows/hardware/ff553324)または[ **kewaitforsingleobject の 1**](https://msdn.microsoft.com/library/windows/hardware/ff553350)で、 *Alertable*パラメーターに設定**TRUE**状態を返すことができます\_特権のないプロセスのコンテキストで実行するときに通知します。 これは、同じ特権のないアプリケーションで別のスレッドから可能なスレッドのアラートをシミュレートします。

低リソース シミュレーション テストでは、次の GDI 関数にエラーも挿入します。[**EngAllocMem**](https://msdn.microsoft.com/library/windows/hardware/ff564176)、 [ **EngAllocUserMem**](https://msdn.microsoft.com/library/windows/hardware/ff564178)、 [ **EngCreateBitmap**](https://msdn.microsoft.com/library/windows/hardware/ff564199)、 [ **EngCreateDeviceSurface**](https://msdn.microsoft.com/library/windows/hardware/ff564206)、 [ **EngCreateDeviceBitmap**](https://msdn.microsoft.com/library/windows/hardware/ff564204)、 [ **EngCreatePalette** ](https://msdn.microsoft.com/library/windows/hardware/ff564212)、 [ **EngCreateClip**](https://msdn.microsoft.com/library/windows/hardware/ff564202)、 [ **EngCreatePath**](https://msdn.microsoft.com/library/windows/hardware/ff564755)、 [ **EngCreateWnd**](https://msdn.microsoft.com/library/windows/hardware/ff564769)、 [ **EngCreateDriverObj**](https://msdn.microsoft.com/library/windows/hardware/ff564207)、 [ **BRUSHOBJ\_pvAllocRbrush**](https://msdn.microsoft.com/library/windows/hardware/ff538263)、および[**CLIPOBJ\_ppoGetPath**](https://msdn.microsoft.com/library/windows/hardware/ff539423)します。

Windows 7 および Windows オペレーティング システムの以降のバージョンでは、低リソース シミュレーション オプションは、次のカーネル Api を使用して割り当てられたメモリをサポートしています。

-   [**IoAllocateMdl**](https://msdn.microsoft.com/library/windows/hardware/ff548263)

-   [**IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257)と I/O を割り当てることができるその他のルーチン要求パケット (IRP) データ構造体

-   [**RtlAnsiStringToUnicodeString** ](https://msdn.microsoft.com/library/windows/hardware/ff561729)およびその他のランタイム ライブラリ (RTL) の文字列ルーチン

-   [**IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)

Windows 8.1 以降、低リソース シミュレーション オプションはまた、MmAllocateNodePagesForMdlEx への呼び出しによって要求された割り当てを失敗します。 さらに、一部の関数では、Driver Verifier 収まっていることをパターンがランダムに割り当てられたメモリ。 ただし、関数が返す状況のみが初期化されていないメモリ。 これらの関数は次のとおりです。

-   [**MmAllocatePagesForMdlEx**](https://msdn.microsoft.com/library/windows/hardware/ff554489)
-   MmAllocateNodePagesForMdlEx
-   [**MmAllocateContiguousMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554460)
-   [**MmAllocateContiguousMemorySpecifyCache**](https://msdn.microsoft.com/library/windows/hardware/ff554464)
-   [**MmAllocateContiguousMemorySpecifyCacheNode**](https://msdn.microsoft.com/library/windows/hardware/ff554469)
-   [**MmAllocateContiguousNodeMemory**](https://msdn.microsoft.com/library/windows/hardware/jj602795)
-   [**MmAllocateNonCachedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554479)

### <a name="span-idcustomsettingsforlowresourcessimulationspanspan-idcustomsettingsforlowresourcessimulationspancustom-settings-for-low-resources-simulation"></a><span id="custom_settings_for_low_resources_simulation"></span><span id="CUSTOM_SETTINGS_FOR_LOW_RESOURCES_SIMULATION"></span>低リソース シミュレーション用のカスタム設定

Windows Vista と Windows の以降のバージョンでは、次のカスタム設定を指定できます。

-   **確率**を特定の割り当ては失敗します。 既定では 6% です。

-   **アプリケーション**影響を受けます。 挿入された、この設定の制限では、指定したアプリケーションへの割り当てが失敗しました。 既定では、すべての割り当てを受けます。

-   **プール タグ**影響を受けます。 この設定は、指定されたプール タグの割り当てに挿入されたエラーを制限します。 既定では、すべての割り当てを受けます。

-   **遅延**(分単位) を前に、割り当てが失敗しました。 この遅延により、システムを起動し、エラーを挿入する前に安定した状態にします。 既定では 8 分です。

Windows Vista より前のオペレーティング システムでは、これらの設定をカスタマイズすることはできません。 オペレーティング システムには、既定値が使用されます。

### <a name="span-idlowresourcessimulationwithoutrebootingspanspan-idlowresourcessimulationwithoutrebootingspanlow-resources-simulation-without-rebooting"></a><span id="low_resources_simulation_without_rebooting"></span><span id="LOW_RESOURCES_SIMULATION_WITHOUT_REBOOTING"></span>再起動しなくても、低リソース シミュレーション

使用して、コンピューターを再起動しなくても Windows 2000 以降のバージョンの Windows での低リソース シミュレーションをアクティブ化することができます、 **/volatile**パラメーター。 設定が、すぐに有効が、シャット ダウンまたは再起動すると失われます。

省略することで、レジストリの低リソース シミュレーションの設定を格納することも、 **/volatile**パラメーター。 これらの設定は、それらを変更するまで、有効なまま、コンピューターを再起動する場合のみ有効です。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。

ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して、1 つまたは複数のドライバーの低リソース シミュレーション オプションをアクティブ化することができます。 詳細については、次を参照してください。[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。

-   **コマンドラインで**

    によって表される低リソース シミュレーション オプション、コマンド行で**ビット 2 (0x4)** します。 低リソース シミュレーションをアクティブ化するには、0x4 のフラグ値を使用または 0x4 をフラグ値に追加します。 次に、例を示します。

    ```
    verifier /flags 0x4 /driver MyDriver.sys
    ```

    オプションは、[次へ] の起動後にアクティブになります。

    Windows Vista と Windows の以降のバージョンで使用することができます、*フォールト/* パラメーターまたはのフラグ値**0x4**低リソース シミュレーションをアクティブ化します。 低リソース シミュレーションの設定を変更するを使用する必要があります**フォールト/** します。 次に、例を示します。

    ```
    verifier /faults /driver MyDriver.sys
    ```

    Windows 2000 と Windows の以降のバージョンでもアクティブ化し、低リソース シミュレーションを追加することで、コンピューターを再起動しなくても非アクティブ化することができます、 **/volatile**パラメーターをコマンド。 次に、例を示します。

    ```
    verifier /volatile /flags 0x4 /adddriver MyDriver.sys
    ```

    この設定は、すぐに有効は、シャット ダウンするか、コンピューターを再起動すると失われます。 詳細については、次を参照してください。[揮発性の設定を使用する](using-volatile-settings.md)します。

    Windows vista では、使用することができます、**フォールト/** パラメーターを表すと低リソース シミュレーション、 **/volatile**を再起動しなくても有効な制限が設定を表すパラメーター。 設定の変更が表示されます。 次に、例を示します。

    ```
    0>  verifier /volatile /faults /adddriver MyDriver.sys
    New Low Resources Simulation options:

    - Use default fault injection probability.
    - Allocations using any pool tag can be failed.
    - Simulate low resources conditions in any application.

    The new settings are in effect until you restart this computer
    or change them again.
    ```

-   **ドライバー検証マネージャーを使用します。**
    1.  ドライバー検証マネージャーを起動します。 型**Verifier**コマンド プロンプト ウィンドウでします。
    2.  選択 **(コード開発者) 用のカスタム設定を作成する**、順にクリックします**次**します。
    3.  選択**完全な一覧から個々 の設定を選択します。** します。
    4.  選択**低リソース シミュレーション**します。

### <a name="span-idcustomizingthesettingswindowsvistaandlaterspanspan-idcustomizingthesettingswindowsvistaandlaterspancustomizing-the-settings-windows-vista-and-later"></a><span id="customizing_the_settings__windows_vista_and_later_"></span><span id="CUSTOMIZING_THE_SETTINGS__WINDOWS_VISTA_AND_LATER_"></span>設定のカスタマイズ (Windows Vista 以降)

以降 Windows Vista では、遅延、確率、アプリケーションなどの既定の設定を変更して、プール タグ低リソース シミュレーション オプションのプロパティ。 ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して、これらの設定を変更することができます。 詳細については、次を参照してください。[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。

コマンドラインで、これらの設定の構文はとおりです。

**verifier** \[**/volatile**\] **/faults**\[*Probability*|*PoolTags*|*Applications*|*DelayMins*\]\[**/driver**|*DriverList*\]

**注**カスタム設定パラメーターが表示される順序で表示する必要があります。 値を省略した場合は、その場所を保持するために引用符を入力します。



**サブパラ メーター**

- **/faults**

  Driver Verifier の低リソース シミュレーション オプションを有効にします。 (/Flags 0x4 はカスタム設定のサブパラ メーターを使用できません)。

- *確率*

  Driver Verifier の特定の割り当てが失敗する確率を指定します。 10,000 件の Driver Verifier の割り当てが失敗する可能性の数を表現するには、(10 進数または 16 進数形式)、数値を入力します。 既定値は 600 では、600/10000、または 6% を意味します。

- *PoolTags*

  Driver Verifier を指定したプール タグの割り当てに失敗できる割り当てを制限します。 ワイルドカード文字を使用することができます (* *\\* * *) を複数のプール タグを表します。 複数のプール タグを一覧表示するには、空白で、タグを区切ります。 既定では、すべての割り当てが失敗することができます。

- *アプリケーション*

  Driver Verifier は、指定したプログラムの割り当てに失敗できる割り当てを制限します。 実行可能ファイルの名前を入力します。 プログラムの一覧を表示するには、プログラムを区切るスペースを含む名前を付けます。 既定では、すべての割り当てが失敗することができます。

- *DelayMins*

  起動後の分の間 Driver Verifier が意図的に失敗しない割り当て数を指定します。 この遅延により、ドライバーがロードされ、システム テストの前に安定化が開始されます。 (10 進数または 16 進数形式) で数値を入力します。 既定値は、8 (分です)。

たとえば、次のコマンドは 10% の確率で低リソース シミュレーションを有効 (1000/10000) と、プール タグ、Tag1 と Fred、および、アプリケーションでは、Notepad.exe 5 分の遅延が発生します。

```
verifier /faults 1000 "Tag1 Fred" Notepad.exe 5
```

次のコマンドは、10 分間に遅延を拡張する点を除いては既定値で低リソース シミュレーションを有効します。

```
verifier /faults "" "" "" 0xa
```

**ドライバー検証マネージャーを使用します。**

1.  ドライバー検証マネージャーを起動します。 型**Verifier**コマンド プロンプト ウィンドウでします。
2.  選択 **(コード開発者) 用のカスタム設定を作成する**、順にクリックします**次**します。

3.  選択**完全な一覧から個々 の設定を選択します。** します。

4.  選択**低リソース シミュレーション**、 をクリックし、 **次へ。**

5.  遅延、確率、アプリケーション、設定を変更して、プール タグとして必要なプロパティ。

### <a name="span-idviewingtheresultsspanspan-idviewingtheresultsspanviewing-the-results"></a><span id="viewing_the_results"></span><span id="VIEWING_THE_RESULTS"></span>結果を表示します。

Driver Verifier リソース割り当てがドライバーの検証ツールを表示することによって意図的に失敗した回数を監視する*フォールト挿入*グローバル カウンター。 このカウンターは、Driver Verifier は、最後の起動後意図的に失敗したリソース割り当ての合計数を表示します。

このカウンターを表示するには、Driver Verifier のログ ファイルに (**/ログ**)、コマンドラインで (**クエリ/**) またはドライバー検証マネージャー。 Windows 2000 でグローバル カウンターを表示するには、選択、**グローバル カウンター**タブ。以降のバージョンの Windows では、次のように選択します。**現在検証済みのドライバーに関する情報を表示**タスク、およびキーを押します**次**2 回です。 詳細については、次を参照してください。[グローバル カウンターの監視](monitoring-global-counters.md)します。

使用して、意図的に失敗した割り当ての数と (確率を計算) する割り当ての合計数を表示することも、 **! verifier**デバッガー拡張機能。 次の例のサンプルを示しています、 **! verifier**出力します。

この例で**ランダム低リソース API エラーを挿入**低リソース シミュレーションが有効になっていることを示します。 **リソース割り当て故意に失敗しました**意図的に失敗した割り当ての数を表すと**プールの割り当ての試行**割り当ての合計数を表します。

```
!verifier

Verify Level 5 ... enabled options are:
        Special pool
        Inject random low-resource API failures

Summary of All Verifier Statistics

RaiseIrqls                             0x2c671f
AcquireSpinLocks                       0xca1a02
Synch Executions                       0x10a623
Trims                                  0x0

Pool Allocations Attempted             0x862e0e
Pool Allocations Succeeded             0x8626e3
Pool Allocations Succeeded SpecialPool 0x768060
Pool Allocations With NO TAG           0x0
Pool Allocations Failed                0x34f
Resource Allocations Failed Deliberately   0x3f5
```

Driver Verifier で最も最近失敗した割り当てのスタック トレースを表示する使用 **! verifier 4**カーネル デバッガーにします。

次の例からの出力のサンプルを示しています。 **! verifier 4**します。 既定では、 **! verifier 4**最近失敗した割り当ての 4 つのほとんどからスタック トレースを表示し、使用することがその*数量*パラメーターを表示するスタック トレースの数を増やします。 たとえば、! verifier 0x80 128 最近失敗した割り当てを表示します。

この例では、Verifier がインターセプトし、ドライバーの呼び出しに置き換えられますことに注意してください**exallocatepoolwithtag に**します。 ドライバーは、メモリを割り当てようとするときに発生し、割り当て関数が返すはないことを検証する前にポインターを使用してのドライバー クラッシュの最も一般的な原因の 1 つ**NULL**します。

```
kd> !verifier 4
Resource fault injection history:
Tracker @ 8354A000 (# entries: 80, size: 80, depth: 8)

Entry @ 8354B258 (index 75)

    Thread: C2638220

    816760CB nt!VerifierExAllocatePoolWithTag+0x49
    A4720443 win32k!bDeleteAllFlEntry+0x15d
    A4720AB0 win32k!GreEnableEUDC+0x70
    A47218FA win32k!CleanUpEUDC+0x37
    A473998E win32k!GdiMultiUserFontCleanup+0x5
    815AEACC nt!MiDereferenceSession+0x74
    8146D3B4 nt!MmCleanProcessAddressSpace+0x112
    815DF739 nt!PspExitThread+0x603

Entry @ 8354B230 (index 74)

    Thread: 8436D770

    816760CB nt!VerifierExAllocatePoolWithTag+0x49
    A462141C win32k!Win32AllocPool+0x13
    A4725F94 win32k!StubGdiAlloc+0x10
```

低リソース シミュレーション テストの経験では、ほとんどのドライバー クラッシュが最近失敗した割り当てを原因となったことが表示されます。 上記の例では、クラッシュがパスの**win32k!GreEnableEUDC**します。 クラッシュの原因を特定する割り当てのパスでコードを調べます。

について **! verifier**を参照してください、*ツールを Windows のデバッグ*ドキュメント。

コマンドラインでレジストリの設定を表示する、 **/querysettings**オプション。 次に、例を示します。

```
C:\>verifier /querysettings
Special pool: Disabled
Pool tracking: Disabled
Force IRQL checking: Disabled
I/O verification: Disabled
Enhanced I/O verification: Disabled
Deadlock detection: Disabled
DMA checking: Disabled
Security checks: Disabled
Force pending I/O requests: Disabled
Low resources simulation: Enabled
IRP Logging: Disabled
Miscellaneous checks: Disabled
Disk integrity checking: Disabled

Low Resources Simulation options:

- Fault injection probability: 1/10000.
- Fail only allocations using pool tags: Tag1 Tag2.
- Simulate low resources conditions only in applications: test1.exe test2.exe.
- Boot time delay: 2 minutes.

Verified drivers:

blah.sys
```









