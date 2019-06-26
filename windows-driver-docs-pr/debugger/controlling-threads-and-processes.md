---
title: スレッドとプロセスの制御
description: スレッドとプロセスの制御
ms.assetid: 6182ca34-ee5e-47e9-82fe-29266397e3a8
keywords:
- エンジン API、スレッドおよびプロセスをデバッガーします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea72fa364f2336d7d6fad2403af3643608ab5c3c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366997"
---
# <a name="controlling-threads-and-processes"></a>スレッドとプロセスの制御


## <span id="ddk_threads_and_processes_dbx"></span><span id="DDK_THREADS_AND_PROCESSES_DBX"></span>


スレッドと、デバッガーのエンジン プロセスの概要については、次を参照してください。[スレッドとプロセス](threads-and-processes.md)します。

イベントの発生時にイベント スレッドとプロセスのイベントは、スレッドとプロセスに設定されます (オペレーティング システムまたは仮想) で、イベントが発生しました。 使用して検出できます[ **GetEventThread** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-geteventthread)と[ **GetEventProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-geteventprocess)、それぞれします。

### <a name="span-idimplicitthreadsandprocessesspanspan-idimplicitthreadsandprocessesspanimplicit-threads-and-processes"></a><span id="implicit_threads_and_processes"></span><span id="IMPLICIT_THREADS_AND_PROCESSES"></span>暗黙的なスレッドとプロセス

カーネル モードでを使用して、デバッガー エンジンのデバッグは、*暗黙的なプロセス*メソッドへの物理アドレス変換 - たとえば、仮想を実行するときに使用するには、どの仮想アドレス空間を決定する[ **VirtualToPhysical** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-virtualtophysical)と[ **ReadVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-readvirtual)します。 イベントの発生時に、暗黙的なプロセスは、現在のプロセスに設定されます。

使用して、暗黙的なプロセスを変更することがあります[ **SetImplicitProcessDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-setimplicitprocessdataoffset)します。 暗黙的なプロセスの使用方法の決定に[ **GetImplicitProcessDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getimplicitprocessdataoffset)します。

**注**  設定するときに[ブレークポイント](multiprocessor-syntax.md#breakpoints)ライブのカーネルがデバッグ セッション中にデバッガー エンジンは、ターゲットに、ブレークポイントの仮想アドレスを渡すは、ターゲットは、ブレークポイントを設定します。 ターゲットのプロセスのコンテキストのみが使用される、ブレークポイントを処理するときにここでは、暗黙的なプロセスの値には関係ありません。

 

カーネル モードのデバッグでは、デバッガー エンジンの使用、*暗黙的なスレッド*のターゲットの一部を決定する[登録](x86-architecture.md#registers)します。 プロセッサ スタックが含まれます (を参照してください[ **GetStackOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getstackoffset))、フレームのオフセット (を参照してください[ **GetFrameOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getframeoffset))、および命令オフセット (を参照してください[ **GetInstructionOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getinstructionoffset))。 イベントの発生時に、暗黙的なスレッドは、現在のスレッドに設定されます。

暗黙的なスレッドを使用して変更できる[ **SetImplicitThreadDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-setimplicitthreaddataoffset)します。 暗黙的なスレッドを調べるには[ **GetImplicitThreadDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getimplicitthreaddataoffset)します。

すべてのレジスタは、暗黙的なスレッドによって決定されます。 いくつかのレジスタは、暗黙的なスレッドが変更されたときに同じです。

**警告**  暗黙的なプロセスと暗黙的なスレッドは独立しています。 暗黙的なスレッドが暗黙の型のプロセスに属していない場合はし、間違った仮想アドレス空間でユーザーとの暗黙的なスレッドのセッション状態になるために、この情報にアクセスしようはエラーが発生するか、不適切な結果を提供します。 すべての仮想アドレス空間の間でカーネルのメモリ アドレスは定数であるため、カーネル メモリにアクセスするとき、この問題は発生しません。 そのためのカーネルのメモリ内にある暗黙的なスレッドの情報にアクセスできます暗黙的なプロセスに依存しません。

 

### <a name="span-idthreadsspanspan-idthreadsspanthreads"></a><span id="threads"></span><span id="THREADS"></span>スレッド

*エンジンのスレッド ID*デバッガー エンジンによって各オペレーティング システム スレッドと各仮想ターゲット スレッドを識別するために使用します。

ターゲットを停止すると、各スレッドが属するプロセスに対する相対インデックスもあります。 、任意のプロセスのプロセスの最初のスレッドのインデックスは 0、および、最後のスレッドのインデックスはから 1 を引いたプロセス内のスレッドの数。 使用して、現在のプロセスでスレッドの数が見つかります[ **GetNumberThreads**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getnumberthreads)します。 使用して、現在のターゲットのすべてのプロセス内のスレッドの合計数が見つかります[ **GetTotalNumberThreads**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-gettotalnumberthreads)します。

使用して、インデックスからエンジンのスレッド ID と現在のプロセスの 1 つまたは複数のスレッドのシステム スレッド ID を検出できます[ **GetThreadIdsByIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getthreadidsbyindex)します。

エンジンは、いくつかの各スレッドに関する情報を保持します。 この情報は、現在のスレッドを照会することがありますに、スレッドのエンジン スレッドの ID を調べることができます。

<span id="system_thread_ID__user-mode_debugging_only_"></span><span id="system_thread_id__user-mode_debugging_only_"></span><span id="SYSTEM_THREAD_ID__USER-MODE_DEBUGGING_ONLY_"></span>システム スレッドの ID (ユーザー モード デバッグの場合のみ)  
使用して、現在のスレッドのシステム スレッド ID が見つかりません[ **GetCurrentThreadSystemId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentthreadsystemid)します。 システム スレッド id では、対応するエンジン スレッドの ID を使用して検出可能性があります[ **GetThreadIdBySystemId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getthreadidbysystemid)します。

<span id="thread_environment_block__TEB_"></span><span id="thread_environment_block__teb_"></span><span id="THREAD_ENVIRONMENT_BLOCK__TEB_"></span>スレッド環境ブロックの終了  
使用して、現在のスレッド TEB のアドレスが見つかりません[ **GetCurrentThreadTeb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentthreadteb)します。 TEB アドレスの指定した場合、対応するエンジンのスレッド ID を使用して検出可能性があります[ **GetThreadIdByTeb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getthreadidbyteb)します。 カーネル モードのデバッグ (仮想) スレッドの TEB 最後のイベントが発生したときに、対応するプロセッサ上で実行されるシステムのスレッドの TEB です。

<span id="data_offset"></span><span id="DATA_OFFSET"></span>データ オフセット  
ユーザー モードのデバッグでは、(システム) スレッドのデータ オフセットは、そのスレッドに対する TEB の場所です。 カーネル モードのデバッグ、データでは、(仮想) スレッドのオフセットは、最後のイベントが発生したときに、対応するプロセッサ上で実行されるシステムのスレッドの KTHREAD 構造です。 使用して、現在のスレッドのデータ オフセットが見つかります[ **GetCurrentThreadDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentthreaddataoffset)します。 指定されたデータのオフセットの対応するエンジン スレッドの ID を使用して検出可能性があります[ **GetThreadIdByDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getthreadidbydataoffset)します。

<span id="system_handle"></span><span id="SYSTEM_HANDLE"></span>システムのハンドル  
使用して、現在のスレッド システム ハンドルが見つかりません[ **GetCurrentThreadHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentthreadhandle)します。 特定のシステム ハンドル用に対応するエンジンのスレッド ID いる可能性がありますを使用して[ **GetThreadIdByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getthreadidbyhandle)します。 カーネル モードのデバッグは、(仮想) プロセスごとに、人為的なハンドルが作成されます。 このハンドルは、デバッガー エンジン API のクエリでのみ使用できます。

### <a name="span-idprocessesspanspan-idprocessesspanprocesses"></a><span id="processes"></span><span id="PROCESSES"></span>プロセス

*エンジンのプロセス ID*デバッガー エンジンによって各オペレーティング システム プロセスとターゲットの各仮想プロセスを識別するために使用します。

ターゲットを停止すると、各プロセスが、ターゲットに対するインデックスにします。 ターゲットの最初のプロセスのインデックスは 0、最後のプロセスのインデックスはから 1 を引いたターゲット内プロセスの数とします。 使用して、現在のターゲット内プロセスの数が見つかります[ **GetNumberProcesses**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getnumberprocesses)します。

使用して、インデックスから現在のターゲットの 1 つまたは複数のスレッドのエンジン プロセスの ID とシステム プロセス ID を検出できる[ **GetProcessIdsByIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getprocessidsbyindex)します。

エンジンは、いくつかの各プロセスに関する情報を保持します。 この情報は、現在のプロセスを照会することがありますに、プロセスのエンジン プロセスの ID を調べることができます。

<span id="system_process_ID__user-mode_debugging_only_"></span><span id="system_process_id__user-mode_debugging_only_"></span><span id="SYSTEM_PROCESS_ID__USER-MODE_DEBUGGING_ONLY_"></span>システムのプロセス ID (ユーザー モード デバッグの場合のみ)  
使用して、現在のプロセスのシステム プロセス ID が見つかりません[ **GetCurrentProcessSystemId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentprocesssystemid)します。 システム プロセス id、対応するエンジン プロセスの ID を使用して検出可能性があります[ **GetProcessIdBySystemId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getprocessidbysystemid)します。

<span id="process_environment_block__PEB_"></span><span id="process_environment_block__peb_"></span><span id="PROCESS_ENVIRONMENT_BLOCK__PEB_"></span>プロセスの環境ブロック (PEB)  
使用して、現在のプロセス PEB のアドレスが見つかりません[ **GetCurrentProcessPeb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentprocesspeb)します。 PEB アドレスの指定した場合、対応するエンジンのプロセス ID を使用して検出可能性があります[ **GetProcessIdByPeb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getprocessidbypeb)します。 カーネル モードのデバッグ、PEB (仮想) のプロセスの最後のイベントが発生したときに実行していたシステム プロセスの PEB です。

<span id="data_offset"></span><span id="DATA_OFFSET"></span>データ オフセット  
ユーザー モードのデバッグでは、(システム) プロセスのデータ オフセットは、そのプロセスの PEB の場所です。 カーネル モードのデバッグでは、(仮想) のプロセスのデータ オフセットは、システム プロセスの最後のイベントが発生したときに実行されていた KPROCESS 構造です。 使用して、現在のプロセスのデータ オフセットが見つかります[ **GetCurrentProcessDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentprocessdataoffset)します。 指定されたデータのオフセットの対応するエンジン プロセスの ID を使用して検出可能性があります[ **GetProcessIdByDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getprocessidbydataoffset)します。

<span id="system_handle"></span><span id="SYSTEM_HANDLE"></span>システムのハンドル  
使用して、現在のプロセスのシステムのハンドルが見つかりません[ **GetCurrentProcessHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentprocesshandle)します。 特定のシステムのハンドルのエンジン プロセスの ID を対応いる可能性がありますを使用して[ **GetProcessIdByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getprocessidbyhandle)します。 カーネル モードのデバッグは、(仮想) のプロセス、人為的なハンドルが作成されます。 このハンドルは、デバッガー エンジンのクエリでのみ使用できます。

### <a name="span-ideventsspanspan-ideventsspanevents"></a><span id="events"></span><span id="EVENTS"></span>イベント

スレッドが作成されるたびに、ライブ ユーザー モードのデバッグまたは終了では、ターゲット、作成スレッドとスレッドの終了では、デバッグ イベントが生成されます。 これらのイベントが発生するへの呼び出し、 [ **IDebugEventCallbacks::CreateThread** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugeventcallbacks-createthread)と[ **IDebugEventCallbacks::ExitThread** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugeventcallbacks-exitthread)コールバック メソッド。

プロセスが作成されるたびに、ライブ ユーザー モードのデバッグまたはターゲットの終了では、作成プロセスと終了プロセスのデバッグ イベントが生成されます。 これらのイベントが発生するへの呼び出し、 [ **IDebugEventCallbacks::CreateProcess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugeventcallbacks-createprocess)と[ **IDebugEventCallbacks::ExitProcess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugeventcallbacks-exitprocess)コールバック メソッド。

イベントの詳細については、次を参照してください。[監視イベント](monitoring-events.md)します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

スレッドと TEB、KTHREAD、PEB、および KPROCESS 構造体を含め、プロセスの詳細については、次を参照してください。 *Microsoft Windows internals 』* David Solomon、Mark Russinovich。

 

 





