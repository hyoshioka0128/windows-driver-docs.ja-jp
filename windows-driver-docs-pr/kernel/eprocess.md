---
title: Windows カーネル不透明構造体
description: Windows カーネル不透明構造体
ms.assetid: 4053d82e-78ae-4945-ad5b-44ba41229a5d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ba5d30b1a937505bd2d8dc8e27e15c56690e3c9f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838709"
---
# <a name="windows-kernel-opaque-structures"></a>Windows カーネル不透明構造体


次の表に、Windows カーネル不透明な構造を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>非透過構造体</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>EPROCESS</strong></td>
<td><p><strong>Eprocess</strong>構造体は、プロセスのプロセスオブジェクトとして機能する不透明な構造体です。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psgetprocesscreatetimequadpart" data-raw-source="[&lt;strong&gt;PsGetProcessCreateTimeQuadPart&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psgetprocesscreatetimequadpart)"><strong>PsGetProcessCreateTimeQuadPart</strong></a>などの一部のルーチンでは、 <strong>eprocess</strong>を使用して操作対象のプロセスを識別します。 ドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer#psgetcurrentprocess" data-raw-source="[&lt;strong&gt;PsGetCurrentProcess&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer#psgetcurrentprocess)"><strong>Psgetcurrentprocess</strong></a>ルーチンを使用して、現在のプロセスのプロセスオブジェクトへのポインターを取得し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)"><strong>Obreferenceobjectbyhandle</strong></a>ルーチンを使用して、指定されたに関連付けられているプロセスオブジェクトへのポインターを取得できます。扱え. <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm64bitphysicaladdress" data-raw-source="[&lt;strong&gt;PsInitialSystemProcess&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm64bitphysicaladdress)"><strong>Psinitialsystemprocess</strong></a>グローバル変数は、システムプロセスのプロセスオブジェクトを指します。</p>
<p>Process オブジェクトはオブジェクトマネージャーオブジェクトであることに注意してください。 ドライバーは、オブジェクトの参照カウントを維持するために、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)"><strong>Obreferenceobject</strong></a>や<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject" data-raw-source="[&lt;strong&gt;ObDereferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)"><strong>ObDereferenceObject</strong></a>などのオブジェクトマネージャールーチンを使用する必要があります。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
<tr class="even">
<td><strong>ETHREAD</strong></td>
<td><p><strong>Ethread</strong>構造体は、スレッドのスレッドオブジェクトとして機能する不透明な構造体です。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-psissystemthread" data-raw-source="[&lt;strong&gt;PsIsSystemThread&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-psissystemthread)"><strong>PsIsSystemThread</strong></a>などの一部のルーチンでは、 <strong>ethread</strong>を使用して操作対象のスレッドを識別します。 ドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psgetcurrentthread" data-raw-source="[&lt;strong&gt;PsGetCurrentThread&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psgetcurrentthread)"><strong>Psgetcurrentthread</strong></a>ルーチンを使用して、現在のスレッドのスレッドオブジェクトへのポインターを取得します。また、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)"><strong>Obreferenceobjectbyhandle</strong></a>ルーチンを使用して、指定したに関連付けられているスレッドオブジェクトへのポインターを取得できます。扱え.</p>
<p>スレッドオブジェクトはオブジェクトマネージャーオブジェクトであることに注意してください。 ドライバーは、オブジェクトの参照カウントを維持するために、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)"><strong>Obreferenceobject</strong></a>や<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject" data-raw-source="[&lt;strong&gt;ObDereferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)"><strong>ObDereferenceObject</strong></a>などのオブジェクトマネージャールーチンを使用する必要があります。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
<tr class="odd">
<td><strong>EX_RUNDOWN_REF</strong></td>
<td><p><strong>EX_RUNDOWN_REF</strong>構造体は、関連付けられた共有オブジェクトの実行時の保護の状態に関する情報を含む、不透明なシステム構造です。</p>
<pre class="syntax"><code>typedef struct _EX_RUNDOWN_REF {
  
  ...  // opaque
  
} EX_RUNDOWN_REF, *PEX_RUNDOWN_REF;</code></pre>
<p>実行時の保護ルーチンはすべて、最初のパラメーターとして<strong>EX_RUNDOWN_REF</strong>構造体へのポインターを取得します。 これらのルーチンは、このページの下部に表示されています。</p>
<p>詳細については、「実行時の<a href="run-down-protection.md" data-raw-source="[Run-Down Protection](run-down-protection.md)">保護</a>」を参照してください。</p>
<p>ヘッダー: Wdm. h. 「Wdm」を含めます。</p></td>
</tr>
<tr class="even">
<td><strong>EX_TIMER</strong></td>
<td><p><strong>EX_TIMER</strong>構造体は、 <strong>EX_TIMER</strong> TIMER オブジェクトを表すためにオペレーティングシステムによって使用される非透過構造体です。</p>
<pre class="syntax"><code>typedef struct _EX_TIMER *PEX_TIMER;</code></pre>
<p>この構造体のすべてのメンバーは、ドライバーに対して非透過的です。</p>
<p>次の<strong>例の<em>Xxx</em>タイマー</strong>ルーチンでは、入力パラメーターとしてシステムによって割り当てられた<strong>EX_TIMER</strong>構造体へのポインターが必要です。</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimer" data-raw-source="[&lt;strong&gt;ExSetTimer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimer)"><strong>ExSetTimer</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-excanceltimer" data-raw-source="[&lt;strong&gt;ExCancelTimer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-excanceltimer)"><strong>ExCancelTimer</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletetimer" data-raw-source="[&lt;strong&gt;ExDeleteTimer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletetimer)"><strong>ExDeleteTimer</strong></a></li>
</ul>
<p><strong>EX_TIMER</strong>ベースのタイマーオブジェクトは、オペレーティングシステムによって作成されます。 このようなタイマーオブジェクトを取得するために、ドライバーは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatetimer" data-raw-source="[&lt;strong&gt;ExAllocateTimer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatetimer)"><strong>Exallocatetimer</strong></a>ルーチンを呼び出します。 このオブジェクトが不要になった場合、ドライバーは<strong>Exdeletetimer</strong>を呼び出してオブジェクトを削除します。</p>
<p>詳細については、「 <a href="exxxxtimer-routines-and-ex-timer-objects.md" data-raw-source="[Ex&lt;em&gt;Xxx&lt;/em&gt;Timer Routines and EX_TIMER Objects](exxxxtimer-routines-and-ex-timer-objects.md)">Ex<em>Xxx</em>Timer ルーチン」および「EX_TIMER Objects</a>」を参照してください。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
<tr class="odd">
<td><strong>FAST_MUTEX</strong></td>
<td><p><strong>FAST_MUTEX</strong>構造体は、高速ミューテックスを表す不透明なデータ構造体です。</p>
<p><strong>FAST_MUTEX</strong>構造体は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializefastmutex" data-raw-source="[&lt;strong&gt;ExInitializeFastMutex&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializefastmutex)"><strong>Exinitializefastmutex</strong></a>ルーチンによって初期化されます。</p>
<p>高速ミューテックスの詳細については、「<a href="fast-mutexes-and-guarded-mutexes.md" data-raw-source="[Fast Mutexes and Guarded Mutexes](fast-mutexes-and-guarded-mutexes.md)">高速ミューテックスと保護</a>されたミューテックス」を参照してください。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
<tr class="even">
<td><strong>IO_CSQ</strong></td>
<td><p><strong>IO_CSQ</strong>構造体は、ドライバーのキャンセルセーフな IRP キュールーチンを指定するために使用される非透過構造体です。 この構造体のメンバーを直接設定しないでください。 この構造体を初期化するには、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinitialize" data-raw-source="[&lt;strong&gt;IoCsqInitialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinitialize)"><strong>IoCsqInitialize</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinitializeex" data-raw-source="[&lt;strong&gt;IoCsqInitializeEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinitializeex)"><strong>IoCsqInitializeEx</strong></a>を使用します。</p>
<p>キャンセルセーフな IRP キューの使用方法の概要については、「<a href="cancel-safe-irp-queues.md" data-raw-source="[Cancel-Safe IRP Queues](cancel-safe-irp-queues.md)">キャンセルセーフな Irp キュー</a>」を参照してください。</p>
<p>Microsoft Windows XP 以降のバージョンの Windows オペレーティングシステムで使用できます。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
<tr class="odd">
<td><strong>IO_CSQ_IRP_CONTEXT</strong></td>
<td><p><strong>IO_CSQ_IRP_CONTEXT</strong>構造体は、ドライバーのキャンセルセーフな irp キュー内の IRP の irp コンテキストを指定するために使用される非透過データ構造体です。 これは、キュー内の特定の Irp を識別するために、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirp" data-raw-source="[&lt;strong&gt;IoCsqInsertIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirp)"><strong>IoCsqInsertIrp</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirpex" data-raw-source="[&lt;strong&gt;IoCsqInsertIrpEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirpex)"><strong>IoCsqInsertIrpEx</strong></a>、および<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremoveirp" data-raw-source="[&lt;strong&gt;IoCsqRemoveIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremoveirp)"><strong>IoCsqRemoveIrp</strong></a>ルーチンによってキーとして使用されます。</p>
<p>キャンセルセーフな IRP キューの使用方法の概要については、「<a href="cancel-safe-irp-queues.md" data-raw-source="[Cancel-Safe IRP Queues](cancel-safe-irp-queues.md)">キャンセルセーフな Irp キュー</a>」を参照してください。</p>
<p>Microsoft Windows XP 以降のバージョンの Windows オペレーティングシステムで使用できます。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
<tr class="even">
<td><strong>IO_WORKITEM</strong></td>
<td><p><strong>IO_WORKITEM</strong>構造体は、システムワーカースレッドの作業項目を記述する不透明な構造体です。</p>
<p>ドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem" data-raw-source="[&lt;strong&gt;IoAllocateWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)"><strong>Ioallocateworkitem</strong></a>を呼び出すことによって、作業項目を割り当てることができます。 または、ドライバーが独自のバッファーを割り当て、そのバッファーを作業項目として初期化する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeworkitem" data-raw-source="[&lt;strong&gt;IoInitializeWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeworkitem)"><strong>Ioinitializeworkitem</strong></a>を呼び出すこともできます。</p>
<p><strong>Ioallocateworkitem</strong>によって割り当てられた作業項目は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeworkitem" data-raw-source="[&lt;strong&gt;IoFreeWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeworkitem)"><strong>IoFreeWorkItem</strong></a>によって解放される必要があります。 <strong>Ioinitializeworkitem</strong>によって初期化されるメモリは、解放する前に、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iouninitializeworkitem" data-raw-source="[&lt;strong&gt;IoUninitializeWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iouninitializeworkitem)"><strong>iouninitializeworkitem</strong></a>で初期化されていない必要があります。</p>
<p>作業項目の詳細については、「<a href="system-worker-threads.md" data-raw-source="[System Worker Threads](system-worker-threads.md)">システムワーカースレッド</a>」を参照してください。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
<tr class="odd">
<td><strong>KBUGCHECK_CALLBACK_RECORD</strong></td>
<td><p><strong>KBUGCHECK_CALLBACK_RECORD</strong>構造体は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckcallback" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckcallback)"><strong>KeRegisterBugCheckCallback</strong></a>ルーチンと<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckcallback" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckcallback)"><strong>KeDeregisterBugCheckCallback</strong></a>ルーチンによって使用される非透過構造体です。</p>
<p><strong>KBUGCHECK_CALLBACK_RECORD</strong>構造体は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback)"><strong>KeRegisterBugCheckReasonCallback</strong></a>ルーチンと<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback)"><strong>KeDeregisterBugCheckReasonCallback</strong></a>ルーチンによるブックキーピングに使用されます。</p>
<p>構造体は、非ページプールなどの常駐メモリに割り当てる必要があります。 使用する前に、 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;KeInitializeCallbackRecord&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"><strong>Keinitializer Ecallbackrecord</strong></a>ルーチンを使用して構造体を初期化します。</p>
<p>ヘッダー: Ntddk。 インクルード: Ntddk。</p></td>
</tr>
<tr class="even">
<td><strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong></td>
<td><p><strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong>構造体は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback)"><strong>KeRegisterBugCheckReasonCallback</strong></a>ルーチンと<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback)"><strong>KeDeregisterBugCheckReasonCallback</strong></a>ルーチンによって使用される非透過構造体です。</p>
<p><strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong>構造体は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback)"><strong>KeRegisterBugCheckReasonCallback</strong></a>ルーチンと<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback)"><strong>KeDeregisterBugCheckReasonCallback</strong></a>ルーチンによるブックキーピングに使用されます。</p>
<p>構造体は、非ページプールなどの常駐メモリに割り当てる必要があります。 使用する前に、 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;KeInitializeCallbackRecord&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"><strong>Keinitializer Ecallbackrecord</strong></a>ルーチンを使用して構造体を初期化します。</p>
<p>Microsoft Windows XP Service Pack 1 (SP1)、Windows Server 2003、およびそれ以降のバージョンの Windows オペレーティングシステムで使用できます。</p>
<p>ヘッダー: Ntddk。 インクルード: Ntddk。</p></td>
</tr>
<tr class="odd">
<td><strong>KDPC</strong></td>
<td><p><strong>Kdpc</strong>構造体は、DPC オブジェクトを表す不透明な構造体です。 この構造体のメンバーを直接設定しないでください。 「 <a href="dpc-objects-and-dpcs.md" data-raw-source="[DPC Objects and DPCs](dpc-objects-and-dpcs.md)">Dpc オブジェクトと dpc」を</a>参照してください。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
<tr class="even">
<td><strong>KFLOATING_SAVE</strong></td>
<td><p><strong>KFLOATING_SAVE</strong>構造体は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesavefloatingpointstate" data-raw-source="[&lt;strong&gt;KeSaveFloatingPointState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesavefloatingpointstate)"><strong>Kesaveflo pointstate</strong></a>ルーチンによって保存された浮動小数点の状態を記述する不透明な構造体です。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestorefloatingpointstate" data-raw-source="[&lt;strong&gt;KeRestoreFloatingPointState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestorefloatingpointstate)"><strong>Kerestoreflo/Pointstate</strong></a>を使用して、浮動小数点の状態を復元します。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
<tr class="odd">
<td><strong>KGUARDED_MUTEX</strong></td>
<td><p><strong>KGUARDED_MUTEX</strong>構造体は、保護されたミューテックスを表す不透明な構造体です。</p>
<p><strong>KeInitializeGuardedMutex</strong>を使用して、 <strong>KGUARDED_MUTEX</strong>構造体を保護されたミューテックスとして初期化します。</p>
<p>保護されたミューテックスは、非ページプールから割り当てる必要があります。</p>
<p>保護されたミューテックスの詳細については、「<a href="fast-mutexes-and-guarded-mutexes.md" data-raw-source="[Fast Mutexes and Guarded Mutexes](fast-mutexes-and-guarded-mutexes.md)">高速ミューテックスと保護</a>されたミューテックス」を参照してください。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
<tr class="even">
<td><strong>KINTERRUPT</strong></td>
<td><p><strong>Kinterrupt</strong>構造体は、システムへの割り込みを表す不透明な構造体です。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex" data-raw-source="[&lt;strong&gt;IoConnectInterruptEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)"><strong>IoConnectInterruptEx</strong></a>は、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine" data-raw-source="[&lt;em&gt;InterruptService&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)"><em>InterruptService</em></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kmessage_service_routine" data-raw-source="[&lt;em&gt;InterruptMessageService&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kmessage_service_routine)"><em>InterruptMessageService</em></a>ルーチンを登録するときに、割り込みの<strong>kinterrupt</strong>構造体へのポインターを提供します。 ドライバーは、割り込みの割り込みスピンロックを取得または解放するときに、このポインターを使用します。 ドライバーは、 <em>InterruptService</em>ルーチンの登録を解除するときにもこのポインターを使用します。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
<tr class="odd">
<td><strong>KLOCK_QUEUE_HANDLE</strong></td>
<td><p><strong>KLOCK_QUEUE_HANDLE</strong>構造体は、キューに置かれたスピンロックを記述する不透明な構造体です。 ドライバーは<strong>KLOCK_QUEUE_HANDLE</strong>構造体を割り当て、それを<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLock&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))"><strong>KeAcquireInStackQueuedSpinLock</strong></a>と<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLockAtDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))"><strong>KeAcquireInStackQueuedSpinLockAtDpcLevel</strong></a>に渡して、キューに置かれたスピンロックを取得します。 これらのルーチンは、キューに置かれたスピンロックを表す構造体を初期化します。 スピンロックを解除すると、ドライバーは構造体を<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)"><strong>KeReleaseInStackQueuedSpinLock</strong></a>および<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLockFromDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)"><strong>KeReleaseInStackQueuedSpinLockFromDpcLevel</strong></a>に渡します。</p>
<p>詳細については、「キューに置かれた<a href="queued-spin-locks.md" data-raw-source="[Queued Spin Locks](queued-spin-locks.md)">スピンロック</a>」を参照してください。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
<tr class="even">
<td><strong>KTIMER</strong></td>
<td><p><strong>Ktimer</strong>構造体は、タイマーオブジェクトを表す不透明な構造体です。 この構造体のメンバーを直接設定しないでください。 詳細については、「 <a href="timer-objects-and-dpcs.md" data-raw-source="[Timer Objects and DPCs](timer-objects-and-dpcs.md)">Timer オブジェクトと dpc</a>」を参照してください。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
<tr class="odd">
<td><strong>LOOKASIDE_LIST_EX</strong></td>
<td><p><strong>LOOKASIDE_LIST_EX</strong>構造体は、ルックアサイドリストを記述します。</p>
<pre class="syntax"><code>typedef struct _LOOKASIDE_LIST_EX {
  ...  // opaque
} LOOKASIDE_LIST_EX, *PLOOKASIDE_LIST_EX;</code></pre>
<p>ルックアサイドリストは、ドライバーがローカルで管理できる固定サイズバッファーのプールで、システム割り当てルーチンへの呼び出しの回数を減らし、パフォーマンスを向上させるために使用します。 バッファーは一様なサイズで、ルックアサイドリストにエントリとして格納されます。</p>
<p>ドライバーは、 <strong>LOOKASIDE_LIST_EX</strong>構造体を不透明として処理する必要があります。 構造体のメンバーにアクセスするか、これらのメンバーの場所に依存するドライバーは、移植性が維持され、他のドライバーと相互運用可能であるとは限りません。</p>
<p>次の「関連項目」セクションには、この構造を使用するルーチンの一覧が含まれています。</p>
<p>ルックアサイドリストの詳細については、「<a href="using-lookaside-lists.md" data-raw-source="[Using Lookaside Lists](using-lookaside-lists.md)">ルックアサイドリストの使用</a>」を参照してください。</p>
<p>64ビットプラットフォームでは、この構造体は16バイトでアラインされている必要があります。</p>
<p>Windows Vista 以降でサポートされています。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
<tr class="even">
<td><strong>NPAGED_LOOKASIDE_LIST</strong></td>
<td><p><strong>NPAGED_LOOKASIDE_LIST</strong>構造体は、非ページプールから割り当てられた固定サイズバッファーのルックアサイドリストを記述する不透明な構造体です。 システムによって新しいエントリが作成され、必要に応じてリスト上の未使用のエントリが破棄されます。 固定サイズのバッファーでは、ルックアサイドリストを使用する方がメモリを直接割り当てるよりも短時間で済みます。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializenpagedlookasidelist" data-raw-source="[&lt;strong&gt;ExInitializeNPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializenpagedlookasidelist)"><strong>ExInitializeNPagedLookasideList</strong></a>を使用して、ルックアサイドリストを初期化します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefromnpagedlookasidelist" data-raw-source="[&lt;strong&gt;ExAllocateFromNPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefromnpagedlookasidelist)"><strong>ExAllocateFromNPagedLookasideList</strong></a>を使用してリストからバッファーを割り当て、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetonpagedlookasidelist" data-raw-source="[&lt;strong&gt;ExFreeToNPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetonpagedlookasidelist)"><strong>ExFreeToNPagedLookasideList</strong></a>を使用してリストにバッファーを返します。</p>
<p>ドライバーは、アンロードする前に作成したすべてのルックアサイドリストを明示的に解放する必要があります。 それ以外の場合は、プログラミング上の重大なエラーになります。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletenpagedlookasidelist" data-raw-source="[&lt;strong&gt;ExDeleteNPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletenpagedlookasidelist)"><strong>ExDeleteNPagedLookasideList</strong></a>を使用して、一覧を解放します。</p>
<p>ドライバーは、ページプールのルックアサイドリストを使用することもできます。 Windows 2000 以降では、 <strong>PAGED_LOOKASIDE_LIST</strong>構造体は、ページングされたバッファーを含むルックアサイドリストを記述します。 Windows Vista 以降では、 <strong>LOOKASIDE_LIST_EX</strong>構造体は、ページングされていないバッファーまたは非ページバッファーを含むルックアサイドリストを記述できます。 詳細については、「<a href="using-lookaside-lists.md" data-raw-source="[Using Lookaside Lists](using-lookaside-lists.md)">ルックアサイドリストの使用</a>」を参照してください。</p>
<p>64ビットプラットフォームでは、この構造体は16バイトでアラインされている必要があります。</p>
<p>Windows 2000 以降でサポートされています。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
<tr class="odd">
<td><strong>OBJECT_TYPE</strong></td>
<td><p><strong>OBJECT_TYPE</strong>は、ハンドルのオブジェクトの種類を指定する不透明な構造体です。 詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)"><strong>Obreferenceobjectbyhandle</strong></a>」を参照してください。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
<tr class="even">
<td><strong>PAGED_LOOKASIDE_LIST</strong></td>
<td><p><strong>PAGED_LOOKASIDE_LIST</strong>構造体は、ページプールから割り当てられた固定サイズバッファーのルックアサイドリストを記述する不透明な構造体です。 システムによって新しいエントリが作成され、必要に応じてリスト上の未使用のエントリが破棄されます。 固定サイズのバッファーでは、ルックアサイドリストを使用する方がメモリを直接割り当てるよりも短時間で済みます。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializepagedlookasidelist" data-raw-source="[&lt;strong&gt;ExInitializePagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializepagedlookasidelist)"><strong>ExInitializePagedLookasideList</strong></a>を使用して、ルックアサイドリストを初期化します。 リストにバッファーを返すには、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefrompagedlookasidelist" data-raw-source="[&lt;strong&gt;ExAllocateFromPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefrompagedlookasidelist)"><strong>Exallocatefrompagedlook</strong></a> the list を使用します。また、リストにバッファーを返すには、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetopagedlookasidelist" data-raw-source="[&lt;strong&gt;ExFreeToPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetopagedlookasidelist)"><strong>exfreetopagedlook のリスト</strong></a>からバッファーを割り当てます。</p>
<p>ドライバーは、アンロードする前に作成したすべてのルックアサイドリストを明示的に解放する必要があります。 それ以外の場合は、プログラミング上の重大なエラーになります。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletepagedlookasidelist" data-raw-source="[&lt;strong&gt;ExDeletePagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletepagedlookasidelist)"><strong>ExDeletePagedLookasideList</strong></a>を使用して、一覧を解放します。</p>
<p>ドライバーは、非ページプールのルックアサイドリストを使用することもできます。 Windows 2000 以降では、 <strong>NPAGED_LOOKASIDE_LIST</strong>構造体は、非ページバッファーを含むルックアサイドリストを記述します。 Windows Vista 以降では、 <strong>LOOKASIDE_LIST_EX</strong>構造体は、ページングされていないバッファーまたは非ページバッファーを含むルックアサイドリストを記述できます。 詳細については、「<a href="using-lookaside-lists.md" data-raw-source="[Using Lookaside Lists](using-lookaside-lists.md)">ルックアサイドリストの使用</a>」を参照してください。</p>
<p>64ビットプラットフォームでは、この構造体は16バイトでアラインされている必要があります。</p>
<p>Windows 2000 以降でサポートされています。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
<tr class="odd">
<td><strong>RTL_BITMAP</strong></td>
<td><p><strong>RTL_BITMAP</strong>構造体は、ビットマップを記述する不透明な構造体です。</p>
<pre class="syntax"><code>typedef struct _RTL_BITMAP {
  // opaque
} RTL_BITMAP, *PRTL_BITMAP;</code></pre>
<p>この構造体のメンバーに直接アクセスしないでください。 メンバーの場所に依存しているか、メンバーの値に直接アクセスするドライバーは、将来のバージョンの Windows オペレーティングシステムとの互換性が維持されていない可能性があります。</p>
<p><strong>RTL_BITMAP</strong>構造体は、任意の長さの汎用的な1次元ビットマップのヘッダーとして機能します。 ドライバーは、このようなビットマップを経済的な方法で使用して、一連の再利用可能な項目を追跡できます。 たとえば、ファイルシステムでは、ビットマップを使用して、ハードディスク上のファイルデータを保持するために既に割り当てられているクラスターやセクターを追跡できます。</p>
<p><strong>RTL_BITMAP</strong>構造体を使用する<strong>Rtl<em>Xxx</em></strong> ルーチンの一覧については、次の「関連項目」も参照してください。 これらの<strong>Rtl<em>Xxx</em></strong> ルーチンの呼び出し元は、 <strong>RTL_BITMAP</strong>構造体と、ビットマップを含むバッファーのストレージを割り当てる必要があります。 このバッファーは、メモリ内の4バイトの境界で開始する必要があり、長さが4バイトの倍数である必要があります。 ビットマップは、バッファーの先頭から開始しますが、割り当てられたバッファーに格納される任意の数のビットを含めることができます。</p>
<p><strong>RTL_BITMAP</strong>構造体を<strong>RTL<em>Xxx</em></strong> ルーチンのパラメーターとして指定する前に、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlinitializebitmap" data-raw-source="[&lt;strong&gt;RtlInitializeBitMap&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlinitializebitmap)"><strong>RtlInitializeBitMap</strong></a>ルーチンを呼び出して構造体を初期化します。 このルーチンへの入力パラメーターは、ビットマップを格納しているバッファーへのポインターと、ビットマップのサイズ (ビット単位) です。 <strong>RtlInitializeBitMap</strong>は、このバッファーの内容を変更しません。</p>
<p>呼び出し元がページングされたメモリ内の<strong>RTL_BITMAP</strong>構造体とビットマップのストレージを割り当てる場合、この構造体へのポインターを<strong>RTL<em>Xxx</em></strong> ルーチンへのパラメーターとして渡すと、呼び出し元は IRQL &lt;= APC_LEVEL で実行されている必要があります。詳細については、「関連項目」を参照してください。 呼び出し元が、非ページ化されたメモリから (または、ロックされているページメモリから) ストレージを割り当てる場合、 <strong>Rtl<em>Xxx</em></strong> ルーチンを呼び出すと、呼び出し元は任意の IRQL で実行できます。</p>
<p>Windows 2000 以降のバージョンの Windows でサポートされています。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
<tr class="even">
<td><strong>RTL_RUN_ONCE</strong></td>
<td><p><strong>RTL_RUN_ONCE</strong>構造体は、ワンタイム初期化の情報を格納する不透明な構造体です。</p>
<p>ドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlrunonceinitialize" data-raw-source="[&lt;strong&gt;RtlRunOnceInitialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlrunonceinitialize)"><strong>RtlRunOnceInitialize</strong></a>ルーチンを呼び出して、他の<strong>Rtlrunonce<em>Xxx</em></strong> ルーチンに渡す前に、この構造体を初期化する必要があります。</p>
<p>Windows Vista 以降のバージョンの Windows オペレーティングシステムでのみ使用できます。</p>
<p>ヘッダー: Ntddk。 インクルード: Ntddk。</p></td>
</tr>
<tr class="odd">
<td><strong>SECURITY_SUBJECT_CONTEXT</strong></td>
<td><p><strong>SECURITY_SUBJECT_CONTEXT</strong>構造体は、特定の操作が行われているセキュリティコンテキストを表す不透明な構造体です。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
<tr class="even">
<td><strong>SLIST_HEADER</strong></td>
<td><p><strong>SLIST_HEADER</strong>構造体は、シーケンスされた単一のシングルリンクリストのヘッダーとして機能する不透明な構造体です。 詳細については、「<a href="singly-and-doubly-linked-lists.md" data-raw-source="[Singly and Doubly Linked Lists](singly-and-doubly-linked-lists.md)">単一およびダブルリンクリスト</a>」を参照してください。</p>
<p>64ビットプラットフォームでは、 <strong>SLIST_HEADER</strong>構造体が16バイトでアラインされている必要があります。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
<tr class="odd">
<td><strong>XSTATE_SAVE</strong></td>
<td><p><strong>XSTATE_SAVE</strong>構造体は、カーネルモードドライバーによって保存および復元される拡張プロセッサの状態情報を記述する不透明な構造体です。</p>
<pre class="syntax"><code>typedef struct _XSTATE_SAVE {
  ...  // opaque
} XSTATE_SAVE, *PXSTATE_SAVE;</code></pre>
<p>すべてのメンバーは不透明です。</p>
<p>この構造体は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate" data-raw-source="[&lt;strong&gt;KeSaveExtendedProcessorState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate)"><strong>KeSaveExtendedProcessorState</strong></a>および<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestoreextendedprocessorstate" data-raw-source="[&lt;strong&gt;KeRestoreExtendedProcessorState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestoreextendedprocessorstate)"><strong>Kerestoreextendedprocessorstate</strong></a>ルーチンによって使用されます。</p>
<p>Windows 7 以降のバージョンの Windows オペレーティングシステムでサポートされています。</p>
<p>ヘッダー: Wdm. h. インクルード: Ntifs、Ntddk、および。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[**BugCheckDumpIoCallback**](https://msdn.microsoft.com/library/windows/hardware/ff540677)  
[**BugCheckSecondaryDumpDataCallback**](https://msdn.microsoft.com/library/windows/hardware/ff540679)  
[**ExAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))  
[**ExAcquireFastMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544340(v=vs.85))  
[**Exallocatefromlook Stex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefromlookasidelistex)  
[**ExAllocateFromNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefromnpagedlookasidelist)  
[**Exallocatefrompagedlook のリスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefrompagedlookasidelist)  
[**ExAllocateTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatetimer)  
[**ExDeletePagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletepagedlookasidelist)  
[**Exfreetopagedlook のリスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetopagedlookasidelist)  
[**ExInitializePagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializepagedlookasidelist)  
[**ExCancelTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-excanceltimer)  
[**Exdeletelook Asiststex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletelookasidelistex)  
[**ExDeleteNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletenpagedlookasidelist)  
[**ExDeleteTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletetimer)  
[**Exflushstasiアス Stex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exflushlookasidelistex)  
[**Exfreetolook Asifrostex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetolookasidelistex)  
[**ExFreeToNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetonpagedlookasidelist)  
[**Exststokasiアス Stex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializelookasidelistex)  
[**ExInitializeNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializenpagedlookasidelist)  
[**ExInitializeSListHead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-initializeslisthead)  
[**ExInterlockedFlushSList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinterlockedflushslist)  
[**ExInterlockedPopEntrySList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinterlockedpopentryslist)  
[**ExInterlockedPushEntrySList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinterlockedpushentryslist)  
[**ExQueryDepthSList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exquerydepthslist)  
[**ExReleaseFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545549(v=vs.85))  
[**ExReleaseFastMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545567(v=vs.85))  
[**ExSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimer)  
[**ExTryToAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545647(v=vs.85))  
[*ExTimerCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ext_callback)  
[**IoAllocateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)  
[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)  
[**IoCsqInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinitialize)  
[**IoCsqInitializeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinitializeex)  
[**IoCsqInsertIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirp)  
[**IoCsqInsertIrpEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirpex)  
[**IoCsqRemoveIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremoveirp)  
[**IoDisconnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterruptex)  
[**IoFreeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeworkitem)  
[**IoInitializeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeworkitem)  
[**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc)  
[**IoUninitializeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iouninitializeworkitem)  
[**KeAcquireGuardedMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551892(v=vs.85))  
[**KeAcquireGuardedMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551894(v=vs.85))  
[**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))  
[**KeAcquireInStackQueuedSpinLockAtDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))  
[**KeAcquireInterruptSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551914(v=vs.85))  
[**KeCancelTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kecanceltimer)  
[**Ke初期化 Ecallbackrecord**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)  
[**KeInitializeGuardedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeguardedmutex)  
[**KeInitializeTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimer)  
[**KeInitializeTimerEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimerex)  
[**KeReadStateTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereadstatetimer)  
[**KeRestoreExtendedProcessorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestoreextendedprocessorstate)  
[**KeSaveExtendedProcessorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate)  
[**KeSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer)  
[**KeSetTimerEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimerex)  
[**KeDeregisterBugCheckCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckcallback)  
[**KeDeregisterBugCheckReasonCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback)  
[**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)  
[**KeRegisterBugCheckCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckcallback)  
[**KeRegisterBugCheckReasonCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback)  
[**KeReleaseGuardedMutexUnsafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseguardedmutexunsafe)  
[**KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)  
[**KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)  
[**KeReleaseInterruptSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinterruptspinlock)  
[**Kerestoreflo/Pointstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestorefloatingpointstate)  
[**Kesaveflo/Pointstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesavefloatingpointstate)  
[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)  
[*ルック Asiアス Stallocateex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-allocate_function_ex)  
[*ルック Asiフリー Ex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-free_function_ex)  
[**ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)  
[**PsGetCurrentProcess**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer#psgetcurrentprocess)  
[**PsGetProcessCreateTimeQuadPart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psgetprocesscreatetimequadpart)  
[**PsInitialSystemProcess**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm64bitphysicaladdress)  
[**PsIsSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-psissystemthread)  
[**RtlRunOnceBeginInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlrunoncebegininitialize)  
[**RtlRunOnceComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlrunoncecomplete)  
[**RtlRunOnceExecuteOnce**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlrunonceexecuteonce)  
[**RtlRunOnceInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlrunonceinitialize)  
[*RunOnceInitialization*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-rtl_run_once_init_fn)  
[実行時の保護](run-down-protection.md)  
[**SeAccessCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seaccesscheck)  
[**Se割り当てのセキュリティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seassignsecurity)  
[**Se割り当て Securityex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seassignsecurityex)  



