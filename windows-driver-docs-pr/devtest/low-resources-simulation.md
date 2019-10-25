---
title: 低リソースのシミュレーション
description: 低リソースのシミュレーション
ms.assetid: 2710fa23-26cd-493b-abb4-3a0969a98eb1
keywords:
- 低リソースシミュレーションオプション WDK ドライバー検証ツール
- '低メモリチェック: WDK ドライバー検証ツール'
- 不十分なメモリチェック (WDK ドライバー検証ツール)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da811f69a57f0cdacd5e615eb43630f23bdd1379
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840129"
---
# <a name="low-resources-simulation"></a>低リソースのシミュレーション

## <span id="ddk_low_resources_simulation_tools"></span><span id="DDK_LOW_RESOURCES_SIMULATION_TOOLS"></span>

低リソースシミュレーションオプション (Windows 8.1 でランダム化された*低リソースシミュレーション*と呼ばれる) がアクティブになっている場合、ドライバーの検証ツールは、ドライバーのメモリ割り当てのランダムなインスタンスを、メモリが不足しています。 これにより、ドライバーが低メモリおよびその他の低リソース状態に適切に応答するかどうかがテストされます。

低リソースシミュレーションテストは、 [**Exallocatepoolwithxxx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)、 [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)、 [**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)[**など、いくつかの異なる関数の呼び出しによって要求された割り当てに失敗します。MmMapLockedPagesSpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache)および[**Mmmapiospace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace)。

Windows Vista 以降、低リソースのシミュレーションテストでは、 [**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)、 [**IoAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)、 [**ioallocateworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)、 [**ioallocateerrorlogentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateerrorlogentry)、 [**MmAllocateContiguousMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemory)[**にもエラーが挿入されます。MmAllocateContiguousMemorySpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycache)、 [**MmAllocatePagesForMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdl)、および[**MmAllocatePagesForMdlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdlex)。 さらに、Windows Vista 以降では、リソース不足のシミュレーションが有効になっている場合、 [**KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)または[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)を呼び出すと、警告可能*なパラメーターを* **TRUE**に設定すると、\_状態が返されることがあります。特権のないプロセスのコンテキストで実行されている場合。 これにより、特権のない同じアプリケーション内の別のスレッドから発生する可能性のあるスレッドアラートがシミュレートされます。

低リソースシミュレーションテストでは、次の GDI 関数にもエラーが挿入されます: [**EngAllocMem**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engallocmem)、 [**EngAllocUserMem**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engallocusermem)、 [**EngCreateBitmap**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatebitmap)、 [**EngCreateDeviceSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatedevicesurface)、 [**EngCreateDeviceBitmap**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatedevicebitmap)、 [**EngCreatePalette**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatepalette)、 [**EngCreateClip**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreateclip)、 [**EngCreatePath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatepath)、 [**EngCreateWnd**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatewnd)、 [**EngCreateDriverObj**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatedriverobj)、 [**brushobj\_Pvallocrbrush**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_pvallocrbrush)、 [**CLIPOBJ\_ppogetpath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-clipobj_ppogetpath)。

Windows 7 以降のバージョンの Windows オペレーティングシステムでは、低リソースシミュレーションオプションは、次のカーネル Api を使用して割り当てられたメモリをサポートしています。

-   [**IoAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)

-   [**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)および i/o 要求パケット (IRP) データ構造を割り当てることができる他のルーチン

-   [**RtlAnsiStringToUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlansistringtounicodestring)およびその他のランタイムライブラリ (RTL) 文字列ルーチン

-   [**IoSetCompletionRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)

Windows 8.1 以降、低リソースシミュレーションオプションは、MmAllocateNodePagesForMdlEx の呼び出しによって要求された割り当てにも失敗します。 また、一部の関数では、ドライバーの検証ツールによって、割り当てられたメモリにランダムなパターンが挿入されるようになりました。 ただし、関数が初期化されていないメモリを返す場合のみです。 次のような関数があります。

-   [**MmAllocatePagesForMdlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdlex)
-   MmAllocateNodePagesForMdlEx
-   [**MmAllocateContiguousMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemory)
-   [**MmAllocateContiguousMemorySpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycache)
-   [**MmAllocateContiguousMemorySpecifyCacheNode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycachenode)
-   [**MmAllocateContiguousNodeMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousnodememory)
-   [**MmAllocateNonCachedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmallocatenoncachedmemory)

### <a name="span-idcustom_settings_for_low_resources_simulationspanspan-idcustom_settings_for_low_resources_simulationspancustom-settings-for-low-resources-simulation"></a><span id="custom_settings_for_low_resources_simulation"></span><span id="CUSTOM_SETTINGS_FOR_LOW_RESOURCES_SIMULATION"></span>低リソースシミュレーションのカスタム設定

Windows Vista 以降のバージョンの Windows では、次のカスタム設定を指定できます。

-   特定の割り当てが失敗する**確率**。 既定値は6% です。

-   影響を受ける**アプリケーション**。 この設定は、指定されたアプリケーションに対して、挿入に失敗した割り当てを制限します。 既定では、すべての割り当てが影響を受けます。

-   影響を受けた**プールタグ**。 この設定は、挿入されたエラーを、指定したプールタグを持つ割り当てに限定します。 既定では、すべての割り当てが影響を受けます。

-   割り当てが失敗するまでの**遅延**(分)。 この遅延により、障害が挿入される前にシステムを起動して安定させることができます。 既定値は8分です。

Windows Vista より前のオペレーティングシステムでは、これらの設定をカスタマイズすることはできません。 オペレーティングシステムでは、既定値が使用されます。

### <a name="span-idlow_resources_simulation_without_rebootingspanspan-idlow_resources_simulation_without_rebootingspanlow-resources-simulation-without-rebooting"></a><span id="low_resources_simulation_without_rebooting"></span><span id="LOW_RESOURCES_SIMULATION_WITHOUT_REBOOTING"></span>再起動せずに低リソースのシミュレーションを行う

Windows 2000 以降のバージョンの Windows では、 **/volatile**パラメーターを使用してコンピューターを再起動しなくても、リソース不足のシミュレーションを有効にすることができます。 設定は直ちに有効になりますが、コンピューターをシャットダウンまたは再起動した場合は失われます。

また、 **/volatile**パラメーターを省略して、リソース不足のシミュレーション設定をレジストリに格納することもできます。 これらの設定は、コンピューターを再起動した場合にのみ有効になりますが、変更するまで有効なままです。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブにする

ドライバー検証ツールマネージャーまたは Verifier コマンドラインを使用して、1つまたは複数のドライバーの低リソースシミュレーションオプションをアクティブにすることができます。 詳細については、「[ドライバーの検証オプションの選択](selecting-driver-verifier-options.md)」を参照してください。

-   **コマンドラインで**

    コマンドラインでは、低リソースシミュレーションオプションは**ビット 2 (0x4)** で表されます。 低リソースシミュレーションをアクティブにするには、フラグ値0x4 を使用するか、フラグ値に0x4 を追加します。 次に、例を示します。

    ```
    verifier /flags 0x4 /driver MyDriver.sys
    ```

    オプションは、次回の起動時にアクティブになります。

    Windows Vista 以降のバージョンの Windows では、 */fault*パラメーターまたは**0x4**のフラグ値を使用して、低リソースシミュレーションをアクティブにすることができます。 リソース不足のシミュレーションの設定を変更するには、 **/障害**を使用する必要があります。 次に、例を示します。

    ```
    verifier /faults /driver MyDriver.sys
    ```

    Windows 2000 以降のバージョンの Windows では、 **/volatile**パラメーターをコマンドに追加することで、コンピューターを再起動せずに、低リソースシミュレーションのアクティブ化と非アクティブ化を行うこともできます。 次に、例を示します。

    ```
    verifier /volatile /flags 0x4 /adddriver MyDriver.sys
    ```

    この設定は直ちに有効になりますが、コンピューターをシャットダウンまたは再起動すると失われます。 詳細については、「 [Volatile 設定の使用](using-volatile-settings.md)」を参照してください。

    Windows Vista では、 **/fault**パラメーターを使用して、 **/volatile**パラメーターを使用して低リソースシミュレーションを表すことで、再起動しなくても有効な設定を表すことができます。 設定の変更が表示されます。 次に、例を示します。

    ```
    0>  verifier /volatile /faults /adddriver MyDriver.sys
    New Low Resources Simulation options:

    - Use default fault injection probability.
    - Allocations using any pool tag can be failed.
    - Simulate low resources conditions in any application.

    The new settings are in effect until you restart this computer
    or change them again.
    ```

-   **ドライバー検証マネージャーの使用**
    1.  ドライバー検証マネージャーを起動します。 コマンドプロンプトウィンドウで「 **Verifier** 」と入力します。
    2.  [**カスタム設定の作成] (コード開発者向け)** を選択し、 **[次へ]** をクリックします。
    3.  [**完全な一覧から個々の設定を選択]** を選択します。
    4.  **[低リソースシミュレーション]** を選択します。

### <a name="span-idcustomizing_the_settings__windows_vista_and_later_spanspan-idcustomizing_the_settings__windows_vista_and_later_spancustomizing-the-settings-windows-vista-and-later"></a><span id="customizing_the_settings__windows_vista_and_later_"></span><span id="CUSTOMIZING_THE_SETTINGS__WINDOWS_VISTA_AND_LATER_"></span>設定のカスタマイズ (Windows Vista 以降)

Windows Vista 以降では、低リソースシミュレーションオプションの遅延、確率、アプリケーション、およびプールタグのプロパティの既定の設定を変更できます。 これらの設定を変更するには、ドライバー検証マネージャーまたは Verifier コマンドラインを使用します。 詳細については、「[ドライバーの検証オプションの選択](selecting-driver-verifier-options.md)」を参照してください。

コマンドラインでは、これらの設定の構文は次のようになります。

**verifier** \[ **/volatile**\] **/障害**\[*確率*|*pooltags*|*アプリケーション*|*delaymins*\]\[ **/driver**|*Driverlist*\]

**メモ** カスタム設定のパラメーターは、表示されている順序で表示される必要があります。 値を省略する場合は、その位置を保持する引用符を入力します。



**サブパラメーター**

- **/障害**

  ドライバー検証ツールの低リソースシミュレーションオプションを有効にします。 (/Flags 0x4 をカスタム設定のサブパラメーターと共に使用することはできません)。

- *確率*

  ドライバーの検証ツールが特定の割り当てに失敗する確率を指定します。 1万での確率を表す数値 (10 進数または16進数形式) を入力します。この値を指定すると、ドライバー検証ツールが割り当てに失敗します。 既定値600は、600/10000 または6% を意味します。

- *PoolTags*

  指定されたプールタグを使用して、ドライバーの検証で失敗する可能性がある割り当てを制限します。 ワイルドカード文字 ( **\*** ) を使用して、複数のプールタグを表すことができます。 複数のプールタグを一覧表示するには、タグをスペースで区切ります。 既定では、すべての割り当てが失敗する可能性があります。

- *プログラム*

  指定したプログラムのドライバーの割り当てに失敗する可能性がある割り当てを制限します。 実行可能ファイルの名前を入力します。 プログラムを一覧表示するには、プログラム名をスペースで区切ります。 既定では、すべての割り当てが失敗する可能性があります。

- *DelayMins*

  ドライバー検証ツールが意図的に割り当てを失敗させない、起動後の時間 (分単位) を指定します。 この遅延により、ドライバーが読み込まれ、テストが開始される前にシステムが安定化されます。 数値 (10 進数または16進数形式) を入力します。 既定値は 8 (分) です。

たとえば、次のコマンドは、確率が10% の低リソースシミュレーションを有効にします (1000/10000)。プールタグ、Tag1 と Fred、およびアプリケーション Notepad.exe に5分の遅延があります。

```
verifier /faults 1000 "Tag1 Fred" Notepad.exe 5
```

次のコマンドを実行すると、既定値を使用して低リソースシミュレーションが有効になります。ただし、遅延が10分に延長される点が異なります。

```
verifier /faults "" "" "" 0xa
```

**ドライバー検証マネージャーの使用**

1.  ドライバー検証マネージャーを起動します。 コマンドプロンプトウィンドウで「 **Verifier** 」と入力します。
2.  [**カスタム設定の作成] (コード開発者向け)** を選択し、 **[次へ]** をクリックします。

3.  [**完全な一覧から個々の設定を選択]** を選択します。

4.  **低リソースシミュレーション** を選択し、次へ をクリックし**ます。**

5.  遅延、確率、アプリケーション、およびプールタグのプロパティの設定を必要に応じて変更します。

### <a name="span-idviewing_the_resultsspanspan-idviewing_the_resultsspanviewing-the-results"></a><span id="viewing_the_results"></span><span id="VIEWING_THE_RESULTS"></span>結果の表示

ドライバー検証ツールによって意図的にリソース割り当てに失敗した回数を監視するには、ドライバー検証*エラーの挿入*されたグローバルカウンターを表示します。 このカウンターは、ドライバーの検証ツールが前回の起動から故意に失敗したリソース割り当ての合計数を表示します。

このカウンターは、ドライバー検証ログファイル ( **/log**)、コマンドライン ( **/query**)、またはドライバー検証マネージャーで表示できます。 Windows 2000 でグローバルカウンターを表示するには、 **[グローバルカウンター]** タブを選択します。新しいバージョンの Windows では、 **[現在検証されているドライバータスクに関する情報を表示する]** を選択し、 **[次へ]** を2回押します。 詳細については、「[グローバルカウンターの監視](monitoring-global-counters.md)」を参照してください。

また、 **! verifier**デバッガー拡張機能を使用して、意図的に失敗した割り当ての数と割り当ての合計数 (確率を計算する場合) を表示することもできます。 次の例は、 **! verifier**出力のサンプルを示しています。

この例では、**ランダムな低リソースの API エラーを挿入**すると、リソース不足のシミュレーションが有効になっていることが示されます。 **リソース割り当て**が意図的に失敗した割り当ての数と、試行された**プールの割り当て**が割り当ての合計数を表しています。

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

ドライバーの検証ツールによって最近失敗した割り当てのスタックトレースを表示するには、カーネルデバッガーで **! verifier 4**を使用します。

次の例は、 **! verifier 4**からの出力のサンプルを示しています。 既定では、 **! verifier 4**は最近失敗した4つの割り当てのスタックトレースを表示しますが、 *Quantity*パラメーターを使用すると、表示されるスタックトレースの数を増やすことができます。 たとえば、! verifier 0x80 は、最後に失敗した割り当ての128を表示します。

この例では、検証ツールによって、ドライバーの**Exallocatepoolwithtag**への呼び出しが傍受され、置き換えられていることに注意してください。 ドライバーのクラッシュの最も一般的な原因の1つは、ドライバーがメモリを割り当てようとしたときに、割り当て関数が返すポインターを使用して**NULL**でないことを確認したときです。

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

低リソースのシミュレーションテストでは、最近失敗した割り当てが原因で、ほとんどのドライバーのクラッシュが発生していることがわかりました。 上記の例では、クラッシュは win32k のパスにありました **。GreEnableEUDC**。 割り当てのパスのコードを調べて、クラッシュの原因を見つけます。

**! Verifier**の詳細については、 *Windows 用デバッグツール*のドキュメントを参照してください。

コマンドラインでレジストリの設定を表示するには、 **/querysettings**オプションを使用します。 次に、例を示します。

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
