---
title: 数 0x62driver_verifier_detected_violation (C4) のメモリ リークのデバッグ
description: Driver Verifier は、最初のプール割り当てのすべてを解放せず、ドライバーをアンロードするときに数 0x62 のパラメーター 1 の値を持つ 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION のバグの確認を生成します。
ms.assetid: CDBE9A18-4126-4AD7-8E53-6D75DCA8B022
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01151f9b50e7e8a10e8f4e8a88a16c233bb10243
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532790"
---
# <a name="debugging-memory-leaks---driververifierdetectedviolation-c4-0x62"></a>ドライバーのメモリ リークのデバッグ\_VERIFIER\_検出\_違反 (C4)。数 0 x 62


[Driver Verifier](driver-verifier.md)生成[ **0xC4 のバグ チェック。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187)が最初に、ドライバーをアンロードするときに数 0x62 のパラメーター 1 の値には、割り当てられたプールのすべてを解放します。 未解放のメモリの割り当て (メモリ リークとも呼ばれます) は、短くしたオペレーティング システムのパフォーマンスの一般的な原因です。 これらはシステム プールのフラグメントあり、最終的にシステムのクラッシュの原因します。

カーネル デバッガーが実行されているテスト コンピューターに接続されている必要がある[Driver Verifier](driver-verifier.md)、Driver Verifier は、デバッガーを Windows 区切り、違反が検出され、エラーの簡単な説明が表示されます。

## <a name="debugging-memory-leaks-at-driver-unload"></a>> ドライバーのアンロードにリーク メモリのデバッグ


-   [使用してバグ チェックに関する情報を表示するために分析。](#use-analyze-to-display-information-about-the-bug-check)
-   [使用して、! verifier 3 の拡張機能コマンド プールの割り当てについて](#use-the-verifier-3-extension-command-to-find-out-about-the-pool-allocations)
-   [シンボルがある場合、ソース ファイルで、メモリの割り当てが発生した場所を見つけることができます。](#if-you-have-symbols-you-can-locate-where-in-the-source-files-the-memory-allocations-occurred)
-   [メモリ割り当てのログを調べます](#examine-the-log-for-memory-allocations)
-   [修正のメモリ リークします。](#fixing-memory-leaks)

### <a name="use-analyze-to-display-information-about-the-bug-check"></a>使用してバグ チェックに関する情報を表示するために分析。

デバッガーの制御をした後に発生するすべてのバグ チェックと同様、最適な最初の手順が実行するが、 [ **! 分析-v** ](https://msdn.microsoft.com/library/windows/hardware/ff562112)コマンド。

```
kd> !analyze -v
Connected to Windows 8 9600 x86 compatible target
Loading Kernel Symbols
.................................................................................
Loading User Symbols
.......................
Loading unloaded module list
........
*******************************************************************************
*                                                                             *
*                        Bugcheck Analysis                                    *
*                                                                             *
*******************************************************************************

DRIVER_VERIFIER_DETECTED_VIOLATION (c4)
A device driver attempting to corrupt the system has been caught.  This is
because the driver was specified in the registry as being suspect (by the
administrator) and the kernel has enabled substantial checking of this driver.
If the driver attempts to corrupt the system, bugchecks 0xC4, 0xC1 and 0xA will
be among the most commonly seen crashes.
Arguments:
Arg1: 00000062, A driver has forgotten to free its pool allocations prior to unloading.
Arg2: 9707712c, name of the driver having the issue.
Arg3: 9c1faf70, verifier internal structure with driver information.
Arg4: 00000003, total # of (paged+nonpaged) allocations that weren't freed.
    Type !verifier 3 drivername.sys for info on the allocations
    that were leaked that caused the bugcheck.
```

A [**チェック 0xC4 のバグします。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187)数 0x62 の値が次のように説明されているパラメーターの 1 (Arg1)。

ドライバー\_VERIFIER\_検出\_違反 (C4) Arg1 Arg2 Arg3 Arg4 原因 Driver Verifier フラグ数 0x62 ドライバー名を設定します。
解放されず、ページおよび非ページの両方のプールを含む割り当ての予約の合計数。
アンロード最初に割り当てられたプールを解放せずに、ドライバーを作成しています。 Windows 8.1 では、このバグ チェック場合にも発生、ドライバーが最初にすべての作業項目を解放せずにアンロード ([**IO\_WORKITEM**](https://msdn.microsoft.com/library/windows/hardware/ff550679)) で、割り当てが[ **IoAllocateWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff548276)します。 このパラメーターでのバグ チェックにのみ発生するときに、[プール追跡](pool-tracking.md)オプションがアクティブです。
指定[プール追跡](pool-tracking.md)(**verifier/flags 0x8**)。 標準のフラグでプールの追跡オプションが有効になっている (**verifier/standard** )。
 

### <a name="use-the-verifier-3-extension-command-to-find-out-about-the-pool-allocations"></a>使用して、! verifier 3 の拡張機能コマンド プールの割り当てについて

この特定のバグ チェック パラメーター 4 (Arg4) で提供される情報は、最も重要です。 Arg4 解放されなかった割り当ての数を示します。 出力、 [ **! 分析**](https://msdn.microsoft.com/library/windows/hardware/ff562112)コマンドでも、 [ **! verifier** ](https://msdn.microsoft.com/library/windows/hardware/ff565591)デバッガーの拡張機能コマンドで使用できる内容を表示するにはそれらの割り当ては次のとおりでした。 完全な出力 **! verifier 3 MyDriver.sys**コマンドが次の例で示すようにします。

```
kd> !verifier 3 Mydriver.sys

Verify Flags Level 0x000209bb

  STANDARD FLAGS:
    [X] (0x00000000) Automatic Checks
    [X] (0x00000001) Special pool
    [X] (0x00000002) Force IRQL checking
    [X] (0x00000008) Pool tracking
    [X] (0x00000010) I/O verification
    [X] (0x00000020) Deadlock detection
    [X] (0x00000080) DMA checking
    [X] (0x00000100) Security checks
    [X] (0x00000800) Miscellaneous checks
    [X] (0x00020000) DDI compliance checking

  ADDITIONAL FLAGS:
    [ ] (0x00000004) Randomized low resources simulation
    [ ] (0x00000200) Force pending I/O requests
    [ ] (0x00000400) IRP logging
    [ ] (0x00002000) Invariant MDL checking for stack
    [ ] (0x00004000) Invariant MDL checking for driver
    [ ] (0x00008000) Power framework delay fuzzing
    [ ] (0x00040000) Systematic low resources simulation
    [ ] (0x00080000) DDI compliance checking (additional)
    [ ] (0x00200000) NDIS/WIFI verification
    [ ] (0x00800000) Kernel synchronization delay fuzzing
    [ ] (0x01000000) VM switch verification

    [X] Indicates flag is enabled


Summary of All Verifier Statistics

  RaiseIrqls           0x0
  AcquireSpinLocks     0x0
  Synch Executions     0x0
  Trims                0x0

  Pool Allocations Attempted             0x2db1a
  Pool Allocations Succeeded             0x2db1a
  Pool Allocations Succeeded SpecialPool 0x2db1a
  Pool Allocations With NO TAG           0x0
  Pool Allocations Failed                0x0

  Current paged pool allocations         0x0 for 00000000 bytes
  Peak paged pool allocations            0x0 for 00000000 bytes
  Current nonpaged pool allocations      0x3 for 00001058 bytes
  Peak nonpaged pool allocations         0x13 for 0004A4A0 bytes

## Driver Verification List


  MODULE: 0x84226b28 MyDriver.sys (Loaded)

    Pool Allocation Statistics: ( NonPagedPool / PagedPool )

      Current Pool Allocations: ( 0x00000003 / 0x00000000 )
      Current Pool Bytes:       ( 0x00001058 / 0x00000000 )
      Peak Pool Allocations:    ( 0x00000013 / 0x00000000 )
      Peak Pool Bytes:          ( 0x0004A4A0 / 0x00000000 )
      Contiguous Memory Bytes:       0x00000000
      Peak Contiguous Memory Bytes:  0x00000000

    Pool Allocations:

      Address     Length      Tag   Caller    
      ----------  ----------  ----  ----------
      0x982a8fe0  0x00000020  VMdl  0x9a3bf6ac  MyDriver!DeviceControlDispatch
      0x8645a000  0x00001008  mdrv  0x9a3bf687  MyDriver!DeviceControlDispatch
      0x9a836fd0  0x00000030  Vfwi  0x9a3bf6ed  MyDriver!GetNecessaryObjects
```

例では、ドライバー、MyDriver.sys は 2 つのメモリ割り当てと正しく解放されていない 1 つの I/O 作業項目にします。 各一覧では、割り当ての要求が行われたドライバー コードの現在の割り当て、サイズ、使用すると、プール タグおよびアドレスのアドレスが表示されます。 ドライバーの問題は、シンボルが読み込まれている場合は、呼び出し元のアドレスの横にある関数の名前も示します。

表示、タグの (0x8645a000 アドレスの割り当て) の 1 つだけが、ドライバー自体によって提供されました (**mdrv**)。 タグ**VMdl** Driver Verifier によって検証されているドライバーの呼び出しを行うたびに使用されます[ **IoAllocateMdl**](https://msdn.microsoft.com/library/windows/hardware/ff548263)します。 同様に、タグ**Vfwi**は、ドライバーがドライバーの検証ツールによって検証されているように要求します。 項目を使用して作業を割り当てるときに使用[ **IoAllocateWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff548276)します。

### <a name="if-you-have-symbols-you-can-locate-where-in-the-source-files-the-memory-allocations-occurred"></a>シンボルがある場合、ソース ファイルで、メモリの割り当てが発生した場所を見つけることができます。

これらのシンボルには、行番号情報が含まれている場合、ドライバーのシンボルが読み込まれて、ときに使用できます、 **ln** *CallerAddress*呼び出しが行われた行を表示するコマンド。 この出力では、割り当てを行った関数のオフセットも表示されます。

```
kd> ln 0x9a3bf6ac  
d:\coding\wdmdrivers\mydriver\handleioctl.c(50)+0x15
(9a3bf660)   MyDriver!DeviceControlDispatch+0x4c   |  (9a3bf6d0)   MyDriver!DeviceControlDispatch

kd> ln 0x9a3bf687  
d:\coding\wdmdrivers\mydriver\handleioctl.c(38)+0x12
(9a3bf660)   MyDriver!DeviceControlDispatch+0x27   |  (9a3bf6d0)   MyDriver!DeviceControlDispatch

kd> ln 0x9a3bf6ed  
d:\coding\wdmdrivers\mydriver\handleioctl.c(72)+0xa
(9a3bf6d0)   MyDriver!GetNecessaryObjects+0x1d   |  (9a3bf71c)   MyDriver!GetNecessaryObjects
```

### <a name="examine-the-log-for-memory-allocations"></a>メモリ割り当てのログを調べます

Driver Verifier は、プールの追跡が有効にすると、カーネル領域で行われたすべてのメモリ割り当ての循環ログも保持します。 既定では、最新の 65,536 (0x10000) の割り当ては保持されます。 新しい割り当てが行われると、ログの最も古い割り当ては上書きされます。 割り当てが、クラッシュ前に最近行われた場合より具体的には、スレッドのアドレスと、カーネル スタックのフレーム上の図に、割り当て時に割り当てに関する追加情報を取得することがあります。

このログは、コマンドを使用してアクセスできる **! verifier 0x80** *AddressOfPoolAllocation*します。 これにはすべて、割り当ての一覧し、ログでこの特定のアドレスを解放に注意してください。 をキャンセルまたは履歴ログの表示を停止するには、キーボード ショートカットを使用します。**Ctrl キーを押しながら Break** windbg と**Ctrl + C** KD とします。

```
kd> !verifier 0x80 0x982a8fe0

Log of recent kernel pool Allocate and Free operations:

There are up to 0x10000 entries in the log.

Parsing 0x00010000 log entries, searching for address 0x982a8fe0.

# 

Pool block 982a8fe0, Size 00000020, Thread 9c158bc0
81b250cd nt!IovAllocateMdl+0x3d
8060e41d VerifierExt!IoAllocateMdl_internal_wrapper+0x35
81b29388 nt!VerifierIoAllocateMdl+0x22
9a3bf6ac MyDriver!DeviceControlDispatch+0x4c
9a3bf611 MyDriver!NonPNPIRPDispatch0x51
9a3bf05a MyDriver!AllIRPDispatch+0x1a
80611710 VerifierExt!xdv_IRP_MJ_DEVICE_CONTROL_wrapper+0xd0
81b3b635 nt!ViGenericDispatchHandler+0x2d
81b3b784 nt!ViGenericDeviceControl+0x18
81b24b4d nt!IovCallDriver+0x2cc
81703772 nt!IofCallDriver+0x62
8191165e nt!IopSynchronousServiceTail+0x16e
81915518 nt!IopXxxControlFile+0x3e8

kd> !verifier 0x80 0x8645a000

Log of recent kernel pool Allocate and Free operations:

There are up to 0x10000 entries in the log.

Parsing 0x00010000 log entries, searching for address 0x8645a000.

# 

Pool block 8645a000, Size 00001000, Thread 9c158bc0
8060ee4f VerifierExt!ExAllocatePoolWithTagPriority_internal_wrapper+0x5b
81b2619e nt!VerifierExAllocatePoolWithTag+0x24
9a3bf687 MyDriver!DeviceControlDispatch+0x27
9a3bf611 MyDriver!NonPNPIRPDispatch0x51
9a3bf05a MyDriver!AllIRPDispatch+0x1a
80611710 VerifierExt!xdv_IRP_MJ_DEVICE_CONTROL_wrapper+0xd0
81b3b635 nt!ViGenericDispatchHandler+0x2d
81b3b784 nt!ViGenericDeviceControl+0x18
81b24b4d nt!IovCallDriver+0x2cc
81703772 nt!IofCallDriver+0x62
8191165e nt!IopSynchronousServiceTail+0x16e
81915518 nt!IopXxxControlFile+0x3e8
81914516 nt!NtDeviceIoControlFile+0x2a

kd> !verifier 0x80 0x9a836fd0  

Log of recent kernel pool Allocate and Free operations:

There are up to 0x10000 entries in the log.

Parsing 0x00010000 log entries, searching for address 0x9a836fd0.

# 

Pool block 9a836fd0, Size 00000030, Thread 88758740
8151713d nt!IovAllocateWorkItem+0x1b
84a133d9 VerifierExt!IoAllocateWorkItem_internal_wrapper+0x29
8151b3a7 nt!VerifierIoAllocateWorkItem+0x16
9a3bf6ed MyDriver!GetNecessaryObjects+0x1d
9a3bf620 MyDriver!NonPNPIRPDispatch0x51
9a3bf05a MyDriver!AllIRPDispatch+0x1a
84a16710 VerifierExt!xdv_IRP_MJ_DEVICE_CONTROL_wrapper+0xd0
8152d635 nt!ViGenericDispatchHandler+0x2d
8152d784 nt!ViGenericDeviceControl+0x18
81516b4d nt!IovCallDriver+0x2cc
810f5772 nt!IofCallDriver+0x62
8130365e nt!IopSynchronousServiceTail+0x16e
81307518 nt!IopXxxControlFile+0x3e8
```

### <a name="fixing-memory-leaks"></a>修正のメモリ リークします。

このドライバーの検証ツールのバグ チェックは、ドライバーがカーネル メモリ リークが発生するを防ぐために設計されています。 各ケースでは、適切な修正は、割り当てられたオブジェクトが解放されません既存のコード パスを特定しが正しく解放していることを確認するです。

[Static Driver Verifier](static-driver-verifier.md)は Windows ドライバーのソース コードをスキャンし、さまざまなコード パスの実行をシミュレートすることで考えられる問題を報告するツールです。 Static Driver Verifier は、このような問題を識別するための優れた開発時ユーティリティです。

など、ドライバーの検証ツールが含まれていない、シナリオ、使用できるその他の手法を参照してください。[カーネル モード メモリ リークを検出](https://msdn.microsoft.com/library/windows/hardware/ff545403)します。

## <a name="related-topics"></a>関連トピック


[カーネル モード メモリ リークを検出](https://msdn.microsoft.com/library/windows/hardware/ff545403)

[Static Driver Verifier](static-driver-verifier.md)

[Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)

[バグ チェック時にドライバー検証機能を処理が有効になっています。](https://msdn.microsoft.com/library/windows/hardware/hh450984)

 

 






