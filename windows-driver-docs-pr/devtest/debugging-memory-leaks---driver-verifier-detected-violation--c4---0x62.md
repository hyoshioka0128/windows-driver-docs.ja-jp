---
title: メモリリークのデバッグ-DRIVER_VERIFIER_DETECTED_VIOLATION (C4) 0x62
description: ドライバーの検証ツールは、最初にプールの割り当てをすべて解放せずにドライバーがアンロードされたときに、パラメーター1の値が0x62 のバグチェック 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION を生成します。
ms.assetid: CDBE9A18-4126-4AD7-8E53-6D75DCA8B022
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6147ff25f22b1be366924c7e121172e9f5aba495
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839570"
---
# <a name="debugging-memory-leaks---driver_verifier_detected_violation-c4-0x62"></a>メモリリークのデバッグ-DRIVER\_VERIFIER\_検出された\_違反 (C4): 0x62


ドライバーの[検証ツール](driver-verifier.md)によって[**バグチェック0xc4 が生成されます。ドライバー\_Verifier\_検出された\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)は、最初にプール割り当てをすべて解放せずにドライバーがアンロードされたときに、パラメーター1の値が0x62 になりました。 解放さのメモリ割り当て (メモリリークとも呼ばれます) は、オペレーティングシステムのパフォーマンスを低下させる一般的な原因です。 システムプールをフラグメント化し、最終的にシステムクラッシュを引き起こす可能性があります。

[ドライバー検証ツール](driver-verifier.md)を実行しているテストコンピューターにカーネルデバッガーを接続している場合、ドライバーの検証ツールによって違反が検出されると、Windows はデバッガーにブレークし、エラーの簡単な説明を表示します。

## <a name="debugging-memory-leaks-at-driver-unload"></a>ドライバーのアンロード時のメモリリークのデバッグ >


-   [! Analyze を使用して、バグチェックに関する情報を表示します](#use-analyze-to-display-information-about-the-bug-check)
-   [! Verifier 3 拡張コマンドを使用して、プールの割り当てについて確認します。](#use-the-verifier-3-extension-command-to-find-out-about-the-pool-allocations)
-   [シンボルがある場合は、ソースファイル内でメモリ割り当てが発生した場所を見つけることができます。](#if-you-have-symbols-you-can-locate-where-in-the-source-files-the-memory-allocations-occurred)
-   [メモリ割り当てのログを調べます。](#examine-the-log-for-memory-allocations)
-   [メモリリークの修正](#fixing-memory-leaks)

### <a name="use-analyze-to-display-information-about-the-bug-check"></a>! Analyze を使用して、バグチェックに関する情報を表示します

バグチェックが発生した場合と同様に、デバッガーを制御したら、最初に[ **! analyze-v**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)コマンドを実行します。

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

[**バグチェック 0xC4:** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)パラメーター 1 (Arg1) の値が0x62 で\_違反が検出された場合は、次のように\_\_ます。

DRIVER\_VERIFIER\_検出された\_違反 (C4) Arg1 Arg2 Arg3 Arg4 原因ドライバー検証フラグ0x62 ドライバーの名前。
ページ分割されたプールと非ページプールの両方を含む、解放されなかった割り当ての合計数。
ドライバーは、最初にプール割り当てを解放せずにアンロードされています。 Windows 8.1 では、このバグチェックは、 [**Ioallocateworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)で割り当てられた作業項目 ([**IO\_workitem**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)) を最初に解放せずにドライバーがアンロードされた場合にも発生します。 このパラメーターを使用したバグチェックは、[プール追跡](pool-tracking.md)オプションがアクティブになっている場合にのみ行われます。
[プールの追跡](pool-tracking.md)(**verifier/flags 0x8**) を指定します。 プール追跡オプションは、標準フラグ (**verifier/標準**) で有効になっています。
 

### <a name="use-the-verifier-3-extension-command-to-find-out-about-the-pool-allocations"></a>! Verifier 3 拡張コマンドを使用して、プールの割り当てについて確認します。

この特定のバグチェックでは、パラメーター 4 (Arg4) に記載されている情報が最も重要です。 Arg4 は、解放されなかった割り当ての数を示します。 [ **! Analyze**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)コマンドの出力には、 [ **! verifier**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-verifier)デバッガー拡張コマンドも表示されます。このコマンドを使用すると、これらの割り当てを表示できます。 **! Verifier 3 MyDriver. sys**コマンドの完全な出力を次の例に示します。

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

たとえば、ドライバーの MyDriver .sys には、2つのメモリ割り当てと、適切に解放されていない1つの i/o 作業項目があります。 各一覧には、現在の割り当てのアドレス、サイズ、使用されたプールタグ、および割り当て要求が行われたドライバーコード内のアドレスが表示されます。 対象のドライバーのシンボルが読み込まれると、呼び出し元のアドレスの横にある関数の名前も表示されます。

表示されるタグのうち、ドライバー自体 (**mdrv**) によって指定されたのは1つ (アドレス0x8645a000 の割り当て) のみです。 タグ**Vmdl**は、ドライバーの検証ツールによって検証されるドライバーが[**IoAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)を呼び出すたびに使用されます。 同様に、Driver Verifier によって検証されるドライバーが[**Ioallocateworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)を使用して作業項目の割り当てを要求するたびに、タグ**vfwi**が使用されます。

### <a name="if-you-have-symbols-you-can-locate-where-in-the-source-files-the-memory-allocations-occurred"></a>シンボルがある場合は、ソースファイル内でメモリ割り当てが発生した場所を見つけることができます。

ドライバーのシンボルが読み込まれると、シンボルに行番号情報が含まれている場合は、 **ln** *calleraddress*コマンドを使用して、呼び出しが行われた行を表示できます。 この出力では、割り当てを行った関数内のオフセットも表示されます。

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

### <a name="examine-the-log-for-memory-allocations"></a>メモリ割り当てのログを調べます。

また、ドライバー検証ツールでは、プールの追跡が有効になっている場合に、カーネル領域で行われたすべてのメモリ割り当ての循環ログが保持されます。 既定では、最新の 65536 ("") の割り当ては保持されます。 新しい割り当てが行われると、ログ内の最も古い割り当てが上書きされます。 クラッシュの前に割り当てが最近行われた場合、割り当てに関する追加情報 (特に、割り当て時のカーネルスタックのスレッドアドレスとフレーム) を取得できる可能性があります。

このログには **、コマンドを**使用してアクセスできます。 これにより、すべての割り当てが一覧表示され、この特定のアドレスのログに解放されます。 ログ履歴の表示をキャンセルまたは停止するには、キーボードショートカットの**ctrl + Break**を使用します。 WinDbg では、Ctrl + **C**キーを使用します。

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

### <a name="fixing-memory-leaks"></a>メモリリークの修正

このドライバーの検証ツールのバグチェックは、ドライバーがカーネルメモリをリークしないように設計されています。 どちらの場合も、適切な修正は、割り当てられたオブジェクトが解放されていない既存のコードパスを特定し、それらが適切に解放されるようにすることです。

[静的ドライバー検証](static-driver-verifier.md)ツールは、Windows ドライバーのソースコードをスキャンし、さまざまなコードパスの使用をシミュレートすることによって発生する可能性のある問題を報告するツールです。 静的ドライバー検証ツールは、これらの種類の問題を特定するのに役立つ優れた開発時ユーティリティです。

Driver Verifier が関係しないシナリオなど、使用できるその他の手法については、「[カーネルモードのメモリリークの検出](https://docs.microsoft.com/windows-hardware/drivers/debugger/finding-a-kernel-mode-memory-leak)」を参照してください。

## <a name="related-topics"></a>関連トピック


[カーネルモードのメモリリークの検出](https://docs.microsoft.com/windows-hardware/drivers/debugger/finding-a-kernel-mode-memory-leak)

[静的ドライバー検証ツール](static-driver-verifier.md)

[Windows のデバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)

[ドライバーの検証機能が有効になっている場合のバグチェックの処理](https://docs.microsoft.com/windows-hardware/drivers/debugger/handling-a-bug-check-when-driver-verifier-is-enabled)

 

 






