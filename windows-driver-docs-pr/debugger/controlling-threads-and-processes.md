---
title: スレッドとプロセスの制御
description: スレッドとプロセスの制御
ms.assetid: 6182ca34-ee5e-47e9-82fe-29266397e3a8
keywords:
- デバッガーエンジン API、スレッドとプロセス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a928327db59c9fcf45d1a90913060865b049ba1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837818"
---
# <a name="controlling-threads-and-processes"></a>スレッドとプロセスの制御


## <span id="ddk_threads_and_processes_dbx"></span><span id="DDK_THREADS_AND_PROCESSES_DBX"></span>


デバッガーエンジンでのスレッドとプロセスの概要については、「[スレッドとプロセス](threads-and-processes.md)」を参照してください。

イベントが発生すると、イベントスレッドとイベントプロセスは、イベントが発生したスレッドとプロセス (オペレーティングシステムまたは仮想) に設定されます。 これらは、それぞれ[**Geteventthread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-geteventthread)と[**geteventthread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-geteventprocess)を使用して見つけることができます。

### <a name="span-idimplicit_threads_and_processesspanspan-idimplicit_threads_and_processesspanimplicit-threads-and-processes"></a><span id="implicit_threads_and_processes"></span><span id="IMPLICIT_THREADS_AND_PROCESSES"></span>暗黙のスレッドとプロセス

カーネルモードのデバッグでは、デバッガーエンジンは*暗黙的なプロセス*を使用して、仮想から物理アドレスへの変換を実行するときに使用する仮想アドレス空間を決定します。たとえば、 [**virtualtophysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-virtualtophysical)や[**readvirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readvirtual)などです。 イベントが発生すると、暗黙のプロセスが現在のプロセスに設定されます。

暗黙のプロセスは、 [**SetImplicitProcessDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-setimplicitprocessdataoffset)を使用して変更できます。 暗黙的なプロセスを特定するには、 [**GetImplicitProcessDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getimplicitprocessdataoffset)を使用します。

**注**   ライブカーネルデバッグセッション中に[ブレークポイント](multiprocessor-syntax.md#breakpoints)を設定すると、デバッガーエンジンによってブレークポイントの仮想アドレスがターゲットに渡され、ターゲットによってブレークポイントが設定されます。 この場合、ブレークポイントを処理するときに、ターゲットのプロセスコンテキストのみが使用されます。暗黙のプロセスの値は無関係です。

 

カーネルモードのデバッグでは、デバッガーエンジンは暗黙的な*スレッド*を使用して、ターゲットの[レジスタ](x86-architecture.md#registers)の一部を決定します。 これには、プロセッサスタック ( [**Getstackoffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getstackoffset)を参照)、フレームオフセット (「 [**getフレームオフセット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getframeoffset)」を参照)、および命令オフセット (「 [**GetInstructionOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getinstructionoffset)」を参照) が含まれます。 イベントが発生すると、暗黙的なスレッドが現在のスレッドに設定されます。

暗黙的なスレッドは[**SetImplicitThreadDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-setimplicitthreaddataoffset)を使用して変更できます。 暗黙的なスレッドを特定するには、 [**GetImplicitThreadDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getimplicitthreaddataoffset)を使用します。

すべてのレジスタが暗黙的なスレッドによって決定されるわけではありません。 一部のレジスタは、暗黙的なスレッドが変更されても同じままです。

**警告**   暗黙のプロセスと暗黙のスレッドは独立しています。 暗黙のスレッドが暗黙的なプロセスに属していない場合、暗黙的なスレッドのユーザーとセッションの状態は間違った仮想アドレス空間になり、この情報にアクセスしようとするとエラーが発生するか、正しくない結果が返されます。 カーネルメモリアドレスはすべての仮想アドレス空間で一定であるため、カーネルメモリにアクセスしても、この問題は発生しません。 したがって、カーネルメモリに存在する暗黙のスレッドに関する情報は、暗黙的なプロセスとは無関係にアクセスされる可能性があります。

 

### <a name="span-idthreadsspanspan-idthreadsspanthreads"></a><span id="threads"></span><span id="THREADS"></span>レッド

*エンジンスレッド ID*は、各オペレーティングシステムスレッドとターゲットの各仮想スレッドを識別するために、デバッガーエンジンによって使用されます。

ターゲットが停止されている間、各スレッドには、それが属するプロセスを基準としたインデックスもあります。 どのプロセスでも、プロセス内の最初のスレッドのインデックスは0になり、最後のスレッドのインデックスはプロセス内のスレッドの数から1を引いたものになります。 現在のプロセス内のスレッドの数は、 [**Getnumber スレッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getnumberthreads)を使用して見つけることができます。 現在のターゲットに含まれるすべてのプロセス内のスレッドの合計数は、 [**Gettotalnumber スレッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-gettotalnumberthreads)を使用して見つけることができます。

現在のプロセス内の1つまたは複数のスレッドのエンジンスレッド ID とシステムスレッド ID は、 [**getて、getを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getthreadidsbyindex)使用してインデックスから見つけることができます。

エンジンは、各スレッドに関する情報の一部を保持します。 この情報は、現在のスレッドに対してクエリを行うことができ、スレッドのエンジンスレッド ID を検索するために使用できます。

<span id="system_thread_ID__user-mode_debugging_only_"></span><span id="system_thread_id__user-mode_debugging_only_"></span><span id="SYSTEM_THREAD_ID__USER-MODE_DEBUGGING_ONLY_"></span>システムスレッド ID (ユーザーモードデバッグのみ)  
現在のスレッドのシステムスレッド ID は、 [**Getcurrentthreadsystemid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentthreadsystemid)を使用して見つけることができます。 システムスレッド ID が指定されている場合は、対応するエンジンスレッド ID[**を使用し**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getthreadidbysystemid)て、対応するエンジンスレッド id を見つけることができます。

<span id="thread_environment_block__TEB_"></span><span id="thread_environment_block__teb_"></span><span id="THREAD_ENVIRONMENT_BLOCK__TEB_"></span>スレッド環境ブロック (TEB)  
現在のスレッドの TEB のアドレスは、 [**GetCurrentThreadTeb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentthreadteb)を使用して見つけることができます。 指定された TEB のアドレスについては、対応するエンジンスレッド ID が、 [**get**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getthreadidbyteb)を使用して検出される場合があります。 カーネルモードのデバッグでは、(仮想) スレッドの TEB は、最後のイベントが発生したときに、対応するプロセッサ上で実行されていたシステムスレッドの TEB です。

<span id="data_offset"></span><span id="DATA_OFFSET"></span>データオフセット  
ユーザーモードのデバッグでは、(システム) スレッドのデータオフセットは、そのスレッドの TEB の場所です。 カーネルモードのデバッグでは、(仮想) スレッドのデータオフセットは、最後のイベントが発生したときに、対応するプロセッサ上で実行されていたシステムスレッドの KTHREAD 構造体になります。 現在のスレッドのデータオフセットは、 [**GetCurrentThreadDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentthreaddataoffset)を使用して見つけることができます。 特定のデータオフセットでは、対応するエンジンスレッド ID が[**GetThreadIdByDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getthreadidbydataoffset)を使用して検出される場合があります。

<span id="system_handle"></span><span id="SYSTEM_HANDLE"></span>システムハンドル  
現在のスレッドのシステムハンドルは、 [**Getcurrentthreadhandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentthreadhandle)を使用して見つけることができます。 システムハンドルが指定されている場合は、対応するエンジンのスレッド ID が、 [**Get3-d**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getthreadidbyhandle)を使用して検出されることがあります。 カーネルモードのデバッグでは、(仮想) プロセスごとに人工ハンドルが作成されます。 このハンドルは、デバッガーエンジンの API クエリでのみ使用できます。

### <a name="span-idprocessesspanspan-idprocessesspanprocesses"></a><span id="processes"></span><span id="PROCESSES"></span>プロセス

*エンジンプロセス ID*は、各オペレーティングシステムプロセスと、ターゲットの各仮想プロセスを識別するために、デバッガーエンジンによって使用されます。

ターゲットが停止されている間、各プロセスにはターゲットを基準としたインデックスがあります。 ターゲット内の最初のプロセスのインデックスは0で、最後のプロセスのインデックスはターゲット内のプロセスの数から1を引いた値です。 現在のターゲットに含まれるプロセスの数は、 [**Getnumber プロセス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getnumberprocesses)を使用して見つけることができます。

現在のターゲット内の1つ以上のスレッドのエンジンプロセス ID とシステムプロセス ID は、 [**Getprocessidsbyindex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getprocessidsbyindex)を使用してインデックスから見つけることができます。

エンジンは、各プロセスに関する情報の一部を保持します。 この情報は、現在のプロセスに対してクエリが実行され、プロセスのエンジンプロセス ID を検索するために使用される場合があります。

<span id="system_process_ID__user-mode_debugging_only_"></span><span id="system_process_id__user-mode_debugging_only_"></span><span id="SYSTEM_PROCESS_ID__USER-MODE_DEBUGGING_ONLY_"></span>システムプロセス ID (ユーザーモードデバッグのみ)  
現在のプロセスのシステムプロセス ID は、 [**Getcurrentprocesssystemid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentprocesssystemid)を使用して見つけることができます。 特定のシステムプロセス ID では、対応するエンジンプロセス ID が[**Getprocessidbysystemid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getprocessidbysystemid)を使用して検出される場合があります。

<span id="process_environment_block__PEB_"></span><span id="process_environment_block__peb_"></span><span id="PROCESS_ENVIRONMENT_BLOCK__PEB_"></span>プロセス環境ブロック (PEB)  
現在のプロセスの PEB のアドレスは、 [**Getcurrentprocesの b**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentprocesspeb)を使用して確認できます。 特定の PEB アドレスについては、 [**Getprocessidbypeb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getprocessidbypeb)を使用して、対応するエンジンプロセス ID を見つけることができます。 カーネルモードのデバッグでは、(仮想) プロセスの PEB は、最後のイベントが発生したときに実行されていたシステムプロセスの PEB です。

<span id="data_offset"></span><span id="DATA_OFFSET"></span>データオフセット  
ユーザーモードのデバッグでは、(システム) プロセスのデータオフセットは、そのプロセスの PEB の場所です。 カーネルモードのデバッグでは、(仮想) プロセスのデータオフセットは、最後のイベントが発生したときに実行されていたシステムプロセスの KPROCESS 構造です。 現在のプロセスのデータオフセットは、 [**GetCurrentProcessDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentprocessdataoffset)を使用して見つけることができます。 特定のデータオフセットでは、対応するエンジンプロセス ID が[**GetProcessIdByDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getprocessidbydataoffset)を使用して検出される場合があります。

<span id="system_handle"></span><span id="SYSTEM_HANDLE"></span>システムハンドル  
現在のプロセスのシステムハンドルは、 [**GetCurrentProcessHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentprocesshandle)を使用して見つけることができます。 特定のシステムハンドルでは、対応するエンジンプロセス ID が[**Getprocessidbyhandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getprocessidbyhandle)を使用して検出される場合があります。 カーネルモードのデバッグでは、(仮想) プロセス用に人工ハンドルが作成されます。 このハンドルは、デバッガーエンジンのクエリでのみ使用できます。

### <a name="span-ideventsspanspan-ideventsspanevents"></a><span id="events"></span><span id="EVENTS"></span>記録

ライブユーザーモードのデバッグでは、スレッドが作成されるかターゲットで終了するたびに、スレッドの作成とスレッドの終了のデバッグイベントが生成されます。 これらのイベントによって、 [**IDebugEventCallbacks:: CreateThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugeventcallbacks-createthread)メソッドと[**IDebugEventCallbacks:: exitthread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugeventcallbacks-exitthread)コールバックメソッドが呼び出されます。

ライブユーザーモードのデバッグでは、プロセスが作成されるかターゲットで終了するたびに、作成プロセスと終了プロセスのデバッグイベントが生成されます。 これらのイベントによって、 [**IDebugEventCallbacks:: CreateProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugeventcallbacks-createprocess)メソッドと[**IDebugEventCallbacks:: ExitProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugeventcallbacks-exitprocess) callback メソッドが呼び出されます。

イベントの詳細については、「[イベントの監視](monitoring-events.md)」を参照してください。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

スレッドとプロセスの詳細 (TEB、KTHREAD、PEB、KTHREAD など) については、「 *Microsoft Windows の内部*」を参照してください。

 

 





