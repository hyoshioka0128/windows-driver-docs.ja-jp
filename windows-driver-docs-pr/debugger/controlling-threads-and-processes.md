---
title: スレッドとプロセスを制御します。
description: スレッドとプロセスを制御します。
ms.assetid: 6182ca34-ee5e-47e9-82fe-29266397e3a8
keywords:
- エンジン API、スレッドおよびプロセスをデバッガーします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab447354970c82ed874c4317e10fe5a569d9882d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529420"
---
# <a name="controlling-threads-and-processes"></a>スレッドとプロセスを制御します。


## <span id="ddk_threads_and_processes_dbx"></span><span id="DDK_THREADS_AND_PROCESSES_DBX"></span>


スレッドと、デバッガーのエンジン プロセスの概要については、次を参照してください。[スレッドとプロセス](threads-and-processes.md)します。

イベントの発生時にイベント スレッドとプロセスのイベントは、スレッドとプロセスに設定されます (オペレーティング システムまたは仮想) で、イベントが発生しました。 使用して検出できます[ **GetEventThread** ](https://msdn.microsoft.com/library/windows/hardware/ff546646)と[ **GetEventProcess**](https://msdn.microsoft.com/library/windows/hardware/ff546640)、それぞれします。

### <a name="span-idimplicitthreadsandprocessesspanspan-idimplicitthreadsandprocessesspanimplicit-threads-and-processes"></a><span id="implicit_threads_and_processes"></span><span id="IMPLICIT_THREADS_AND_PROCESSES"></span>暗黙的なスレッドとプロセス

カーネル モードでを使用して、デバッガー エンジンのデバッグは、*暗黙的なプロセス*メソッドへの物理アドレス変換 - たとえば、仮想を実行するときに使用するには、どの仮想アドレス空間を決定する[ **VirtualToPhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff560335)と[ **ReadVirtual**](https://msdn.microsoft.com/library/windows/hardware/ff554359)します。 イベントの発生時に、暗黙的なプロセスは、現在のプロセスに設定されます。

使用して、暗黙的なプロセスを変更することがあります[ **SetImplicitProcessDataOffset**](https://msdn.microsoft.com/library/windows/hardware/ff556713)します。 暗黙的なプロセスの使用方法の決定に[ **GetImplicitProcessDataOffset**](https://msdn.microsoft.com/library/windows/hardware/ff546865)します。

**注**  設定するときに[ブレークポイント](multiprocessor-syntax.md#breakpoints)ライブのカーネルがデバッグ セッション中にデバッガー エンジンは、ターゲットに、ブレークポイントの仮想アドレスを渡すは、ターゲットは、ブレークポイントを設定します。 ターゲットのプロセスのコンテキストのみが使用される、ブレークポイントを処理するときにここでは、暗黙的なプロセスの値には関係ありません。

 

カーネル モードのデバッグでは、デバッガー エンジンの使用、*暗黙的なスレッド*のターゲットの一部を決定する[登録](x86-architecture.md#registers)します。 プロセッサ スタックが含まれます (を参照してください[ **GetStackOffset**](https://msdn.microsoft.com/library/windows/hardware/ff548403))、フレームのオフセット (を参照してください[ **GetFrameOffset**](https://msdn.microsoft.com/library/windows/hardware/ff546806))、および命令オフセット (を参照してください[ **GetInstructionOffset**](https://msdn.microsoft.com/library/windows/hardware/ff546916))。 イベントの発生時に、暗黙的なスレッドは、現在のスレッドに設定されます。

暗黙的なスレッドを使用して変更できる[ **SetImplicitThreadDataOffset**](https://msdn.microsoft.com/library/windows/hardware/ff556716)します。 暗黙的なスレッドを調べるには[ **GetImplicitThreadDataOffset**](https://msdn.microsoft.com/library/windows/hardware/ff546871)します。

すべてのレジスタは、暗黙的なスレッドによって決定されます。 いくつかのレジスタは、暗黙的なスレッドが変更されたときに同じです。

**警告**  暗黙的なプロセスと暗黙的なスレッドは独立しています。 暗黙的なスレッドが暗黙の型のプロセスに属していない場合はし、間違った仮想アドレス空間でユーザーとの暗黙的なスレッドのセッション状態になるために、この情報にアクセスしようはエラーが発生するか、不適切な結果を提供します。 すべての仮想アドレス空間の間でカーネルのメモリ アドレスは定数であるため、カーネル メモリにアクセスするとき、この問題は発生しません。 そのためのカーネルのメモリ内にある暗黙的なスレッドの情報にアクセスできます暗黙的なプロセスに依存しません。

 

### <a name="span-idthreadsspanspan-idthreadsspanthreads"></a><span id="threads"></span><span id="THREADS"></span>スレッド

*エンジンのスレッド ID*デバッガー エンジンによって各オペレーティング システム スレッドと各仮想ターゲット スレッドを識別するために使用します。

ターゲットを停止すると、各スレッドが属するプロセスに対する相対インデックスもあります。 、任意のプロセスのプロセスの最初のスレッドのインデックスは 0、および、最後のスレッドのインデックスはから 1 を引いたプロセス内のスレッドの数。 使用して、現在のプロセスでスレッドの数が見つかります[ **GetNumberThreads**](https://msdn.microsoft.com/library/windows/hardware/ff547992)します。 使用して、現在のターゲットのすべてのプロセス内のスレッドの合計数が見つかります[ **GetTotalNumberThreads**](https://msdn.microsoft.com/library/windows/hardware/ff549356)します。

使用して、インデックスからエンジンのスレッド ID と現在のプロセスの 1 つまたは複数のスレッドのシステム スレッド ID を検出できます[ **GetThreadIdsByIndex**](https://msdn.microsoft.com/library/windows/hardware/ff549339)します。

エンジンは、いくつかの各スレッドに関する情報を保持します。 この情報は、現在のスレッドを照会することがありますに、スレッドのエンジン スレッドの ID を調べることができます。

<span id="system_thread_ID__user-mode_debugging_only_"></span><span id="system_thread_id__user-mode_debugging_only_"></span><span id="SYSTEM_THREAD_ID__USER-MODE_DEBUGGING_ONLY_"></span>システム スレッドの ID (ユーザー モード デバッグの場合のみ)  
使用して、現在のスレッドのシステム スレッド ID が見つかりません[ **GetCurrentThreadSystemId**](https://msdn.microsoft.com/library/windows/hardware/ff546544)します。 システム スレッド id では、対応するエンジン スレッドの ID を使用して検出可能性があります[ **GetThreadIdBySystemId**](https://msdn.microsoft.com/library/windows/hardware/ff549329)します。

<span id="thread_environment_block__TEB_"></span><span id="thread_environment_block__teb_"></span><span id="THREAD_ENVIRONMENT_BLOCK__TEB_"></span>スレッド環境ブロックの終了  
使用して、現在のスレッド TEB のアドレスが見つかりません[ **GetCurrentThreadTeb**](https://msdn.microsoft.com/library/windows/hardware/ff546549)します。 TEB アドレスの指定した場合、対応するエンジンのスレッド ID を使用して検出可能性があります[ **GetThreadIdByTeb**](https://msdn.microsoft.com/library/windows/hardware/ff549336)します。 カーネル モードのデバッグ (仮想) スレッドの TEB 最後のイベントが発生したときに、対応するプロセッサ上で実行されるシステムのスレッドの TEB です。

<span id="data_offset"></span><span id="DATA_OFFSET"></span>データ オフセット  
ユーザー モードのデバッグでは、(システム) スレッドのデータ オフセットは、そのスレッドに対する TEB の場所です。 カーネル モードのデバッグ、データでは、(仮想) スレッドのオフセットは、最後のイベントが発生したときに、対応するプロセッサ上で実行されるシステムのスレッドの KTHREAD 構造です。 使用して、現在のスレッドのデータ オフセットが見つかります[ **GetCurrentThreadDataOffset**](https://msdn.microsoft.com/library/windows/hardware/ff545894)します。 指定されたデータのオフセットの対応するエンジン スレッドの ID を使用して検出可能性があります[ **GetThreadIdByDataOffset**](https://msdn.microsoft.com/library/windows/hardware/ff549302)します。

<span id="system_handle"></span><span id="SYSTEM_HANDLE"></span>システムのハンドル  
使用して、現在のスレッド システム ハンドルが見つかりません[ **GetCurrentThreadHandle**](https://msdn.microsoft.com/library/windows/hardware/ff545904)します。 特定のシステム ハンドル用に対応するエンジンのスレッド ID いる可能性がありますを使用して[ **GetThreadIdByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff549312)します。 カーネル モードのデバッグは、(仮想) プロセスごとに、人為的なハンドルが作成されます。 このハンドルは、デバッガー エンジン API のクエリでのみ使用できます。

### <a name="span-idprocessesspanspan-idprocessesspanprocesses"></a><span id="processes"></span><span id="PROCESSES"></span>プロセス

*エンジンのプロセス ID*デバッガー エンジンによって各オペレーティング システム プロセスとターゲットの各仮想プロセスを識別するために使用します。

ターゲットを停止すると、各プロセスが、ターゲットに対するインデックスにします。 ターゲットの最初のプロセスのインデックスは 0、最後のプロセスのインデックスはから 1 を引いたターゲット内プロセスの数とします。 使用して、現在のターゲット内プロセスの数が見つかります[ **GetNumberProcesses**](https://msdn.microsoft.com/library/windows/hardware/ff547946)します。

使用して、インデックスから現在のターゲットの 1 つまたは複数のスレッドのエンジン プロセスの ID とシステム プロセス ID を検出できる[ **GetProcessIdsByIndex**](https://msdn.microsoft.com/library/windows/hardware/ff548160)します。

エンジンは、いくつかの各プロセスに関する情報を保持します。 この情報は、現在のプロセスを照会することがありますに、プロセスのエンジン プロセスの ID を調べることができます。

<span id="system_process_ID__user-mode_debugging_only_"></span><span id="system_process_id__user-mode_debugging_only_"></span><span id="SYSTEM_PROCESS_ID__USER-MODE_DEBUGGING_ONLY_"></span>システムのプロセス ID (ユーザー モード デバッグの場合のみ)  
使用して、現在のプロセスのシステム プロセス ID が見つかりません[ **GetCurrentProcessSystemId**](https://msdn.microsoft.com/library/windows/hardware/ff545850)します。 システム プロセス id、対応するエンジン プロセスの ID を使用して検出可能性があります[ **GetProcessIdBySystemId**](https://msdn.microsoft.com/library/windows/hardware/ff548155)します。

<span id="process_environment_block__PEB_"></span><span id="process_environment_block__peb_"></span><span id="PROCESS_ENVIRONMENT_BLOCK__PEB_"></span>プロセスの環境ブロック (PEB)  
使用して、現在のプロセス PEB のアドレスが見つかりません[ **GetCurrentProcessPeb**](https://msdn.microsoft.com/library/windows/hardware/ff545839)します。 PEB アドレスの指定した場合、対応するエンジンのプロセス ID を使用して検出可能性があります[ **GetProcessIdByPeb**](https://msdn.microsoft.com/library/windows/hardware/ff548150)します。 カーネル モードのデバッグ、PEB (仮想) のプロセスの最後のイベントが発生したときに実行していたシステム プロセスの PEB です。

<span id="data_offset"></span><span id="DATA_OFFSET"></span>データ オフセット  
ユーザー モードのデバッグでは、(システム) プロセスのデータ オフセットは、そのプロセスの PEB の場所です。 カーネル モードのデバッグでは、(仮想) のプロセスのデータ オフセットは、システム プロセスの最後のイベントが発生したときに実行されていた KPROCESS 構造です。 使用して、現在のプロセスのデータ オフセットが見つかります[ **GetCurrentProcessDataOffset**](https://msdn.microsoft.com/library/windows/hardware/ff545787)します。 指定されたデータのオフセットの対応するエンジン プロセスの ID を使用して検出可能性があります[ **GetProcessIdByDataOffset**](https://msdn.microsoft.com/library/windows/hardware/ff548140)します。

<span id="system_handle"></span><span id="SYSTEM_HANDLE"></span>システムのハンドル  
使用して、現在のプロセスのシステムのハンドルが見つかりません[ **GetCurrentProcessHandle**](https://msdn.microsoft.com/library/windows/hardware/ff545829)します。 特定のシステムのハンドルのエンジン プロセスの ID を対応いる可能性がありますを使用して[ **GetProcessIdByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff548147)します。 カーネル モードのデバッグは、(仮想) のプロセス、人為的なハンドルが作成されます。 このハンドルは、デバッガー エンジンのクエリでのみ使用できます。

### <a name="span-ideventsspanspan-ideventsspanevents"></a><span id="events"></span><span id="EVENTS"></span>イベント

スレッドが作成されるたびに、ライブ ユーザー モードのデバッグまたは終了では、ターゲット、作成スレッドとスレッドの終了では、デバッグ イベントが生成されます。 これらのイベントが発生するへの呼び出し、 [ **IDebugEventCallbacks::CreateThread** ](https://msdn.microsoft.com/library/windows/hardware/ff550713)と[ **IDebugEventCallbacks::ExitThread** ](https://msdn.microsoft.com/library/windows/hardware/ff550730)コールバック メソッド。

プロセスが作成されるたびに、ライブ ユーザー モードのデバッグまたはターゲットの終了では、作成プロセスと終了プロセスのデバッグ イベントが生成されます。 これらのイベントが発生するへの呼び出し、 [ **IDebugEventCallbacks::CreateProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff550697)と[ **IDebugEventCallbacks::ExitProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff550728)コールバック メソッド。

イベントの詳細については、次を参照してください。[監視イベント](monitoring-events.md)します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

スレッドと TEB、KTHREAD、PEB、および KPROCESS 構造体を含め、プロセスの詳細については、次を参照してください。 *Microsoft Windows internals 』* David Solomon、Mark Russinovich。

 

 





