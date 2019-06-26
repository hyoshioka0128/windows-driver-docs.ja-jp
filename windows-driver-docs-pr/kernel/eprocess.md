---
title: Windows カーネルの不透明な構造体
description: Windows カーネルの不透明な構造体
ms.assetid: 4053d82e-78ae-4945-ad5b-44ba41229a5d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0babcca7994c19d37d40e0e30a06dd3bf6bb92c2
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393777"
---
# <a name="windows-kernel-opaque-structures"></a>Windows カーネルの不透明な構造体


次の表には、Windows カーネルの非透過構造体が含まれています。

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
<td><strong>」プロセス</strong></td>
<td><p><strong>」プロセス</strong>構造体は、プロセスのプロセス オブジェクトとして機能するための非透過構造体。</p>
<p>一部のルーチンなど<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psgetprocesscreatetimequadpart" data-raw-source="[&lt;strong&gt;PsGetProcessCreateTimeQuadPart&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psgetprocesscreatetimequadpart)"> <strong>PsGetProcessCreateTimeQuadPart</strong></a>を使用して、 <strong>」プロセス</strong>で動作するプロセスを特定します。 ドライバーを使用できる、 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer#psgetcurrentprocess" data-raw-source="[&lt;strong&gt;PsGetCurrentProcess&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer#psgetcurrentprocess)"> <strong>PsGetCurrentProcess</strong> </a>プロセスへのポインターを取得するルーチンが、現在のプロセス オブジェクトし、を使用できます、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)"> <strong>ObReferenceObjectByHandle</strong></a>ルーチンを指定したハンドルに関連付けられているプロセス オブジェクトへのポインターを取得します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm64bitphysicaladdress" data-raw-source="[&lt;strong&gt;PsInitialSystemProcess&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm64bitphysicaladdress)"> <strong>PsInitialSystemProcess</strong> </a>グローバル変数は、システム プロセスのプロセス オブジェクトを指します。</p>
<p>プロセス オブジェクトはオブジェクトの Manager オブジェクトであることに注意してください。 ドライバーはなどオブジェクト マネージャー ルーチンを使用する必要があります<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject)"> <strong>ObReferenceObject</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject" data-raw-source="[&lt;strong&gt;ObDereferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)"> <strong>ObDereferenceObject</strong> </a>オブジェクトを維持するには参照カウントします。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="even">
<td><strong>ETHREAD</strong></td>
<td><p><strong>ETHREAD</strong>構造体は、スレッドのスレッド オブジェクトとして機能するための非透過構造体。</p>
<p>一部のルーチンなど<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-psissystemthread" data-raw-source="[&lt;strong&gt;PsIsSystemThread&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-psissystemthread)"> <strong>PsIsSystemThread</strong></a>を使用して、 <strong>ETHREAD</strong>を操作するスレッドを識別するためにします。 ドライバーを使用できる、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psgetcurrentthread" data-raw-source="[&lt;strong&gt;PsGetCurrentThread&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psgetcurrentthread)"> <strong>PsGetCurrentThread</strong> </a>スレッドへのポインターを取得するルーチンが、現在のスレッド オブジェクトし、を使用できます、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)"> <strong>ObReferenceObjectByHandle</strong></a>ルーチンを指定したハンドルに関連付けられているスレッド オブジェクトへのポインターを取得します。</p>
<p>スレッド オブジェクトはオブジェクトの Manager オブジェクトであることに注意してください。 ドライバーはなどオブジェクト マネージャー ルーチンを使用する必要があります<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject)"> <strong>ObReferenceObject</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject" data-raw-source="[&lt;strong&gt;ObDereferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)"> <strong>ObDereferenceObject</strong> </a>オブジェクトを維持するには参照カウントします。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="odd">
<td><strong>EX_RUNDOWN_REF</strong></td>
<td><p><strong>EX_RUNDOWN_REF</strong>構造体が関連付けられている共有オブジェクトの run-down 保護の状態に関する情報が含まれる非透過システム構造体。</p>
<pre class="syntax"><code>typedef struct _EX_RUNDOWN_REF {
  
  ...  // opaque
  
} EX_RUNDOWN_REF, *PEX_RUNDOWN_REF;</code></pre>
<p>すべて run-down 保護ルーチンへのポインターの取得、 <strong>EX_RUNDOWN_REF</strong>最初のパラメーターとして構造体。 これらのルーチンは、このページの下部に一覧表示されます。</p>
<p>詳細については、次を参照してください。<a href="run-down-protection.md" data-raw-source="[Run-Down Protection](run-down-protection.md)">紹介保護</a>します。</p>
<p>ヘッダー:Wdm.h します。 Wdm.h が含まれます。</p></td>
</tr>
<tr class="even">
<td><strong>EX_TIMER</strong></td>
<td><p><strong>EX_TIMER</strong>構造体が表すオペレーティング システムで使用される非透過構造、 <strong>EX_TIMER</strong>タイマー オブジェクト。</p>
<pre class="syntax"><code>typedef struct _EX_TIMER *PEX_TIMER;</code></pre>
<p>この構造体のすべてのメンバーは、ドライバーに対して非透過的です。</p>
<p>次<strong>Ex<em>Xxx</em>タイマー</strong>ルーチンがシステムによって割り当てられたへのポインターを必要と<strong>EX_TIMER</strong>入力パラメーターとして構造体。</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exsettimer" data-raw-source="[&lt;strong&gt;ExSetTimer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exsettimer)"><strong>ExSetTimer</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-excanceltimer" data-raw-source="[&lt;strong&gt;ExCancelTimer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-excanceltimer)"><strong>ExCancelTimer</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletetimer" data-raw-source="[&lt;strong&gt;ExDeleteTimer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletetimer)"><strong>ExDeleteTimer</strong></a></li>
</ul>
<p><strong>EX_TIMER</strong>-ベースのタイマー オブジェクトは、オペレーティング システムによって作成されます。 タイマー オブジェクトをドライバーの呼び出しのようなを取得する、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatetimer" data-raw-source="[&lt;strong&gt;ExAllocateTimer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatetimer)"> <strong>ExAllocateTimer</strong> </a>ルーチン。 呼び出すことによって、オブジェクトを削除するため、ドライバーはこのオブジェクトが不要<strong>ExDeleteTimer</strong>します。</p>
<p>詳細については、次を参照してください。 <a href="exxxxtimer-routines-and-ex-timer-objects.md" data-raw-source="[Ex&lt;em&gt;Xxx&lt;/em&gt;Timer Routines and EX_TIMER Objects](exxxxtimer-routines-and-ex-timer-objects.md)">Ex<em>Xxx</em>タイマー ルーチンと EX_TIMER オブジェクト</a>します。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="odd">
<td><strong>FAST_MUTEX</strong></td>
<td><p>A <strong>FAST_MUTEX</strong>構造が高速なミュー テックスを表す非透過データ構造体。</p>
<p>A <strong>FAST_MUTEX</strong>で構造体が初期化される、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializefastmutex" data-raw-source="[&lt;strong&gt;ExInitializeFastMutex&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializefastmutex)"> <strong>ExInitializeFastMutex</strong> </a>ルーチン。</p>
<p>高速なミュー テックスの詳細については、次を参照してください。<a href="fast-mutexes-and-guarded-mutexes.md" data-raw-source="[Fast Mutexes and Guarded Mutexes](fast-mutexes-and-guarded-mutexes.md)">高速なミュー テックスと保護されたミュー テックス</a>します。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="even">
<td><strong>IO_CSQ</strong></td>
<td><p><strong>IO_CSQ</strong>構造体は、非透過構造体がドライバーのキャンセルの安全な IRP キュー ルーチンを指定するために使用します。 この構造体のメンバーを直接設定しないでください。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinitialize" data-raw-source="[&lt;strong&gt;IoCsqInitialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinitialize)"> <strong>IoCsqInitialize</strong> </a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinitializeex" data-raw-source="[&lt;strong&gt;IoCsqInitializeEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinitializeex)"> <strong>IoCsqInitializeEx</strong> </a>この構造体を初期化します。</p>
<p>キャンセルの安全な IRP のキューを使用する方法の概要については、次を参照してください。<a href="cancel-safe-irp-queues.md" data-raw-source="[Cancel-Safe IRP Queues](cancel-safe-irp-queues.md)">キャンセル セーフ IRP キュー</a>します。</p>
<p>Microsoft Windows XP および Windows オペレーティング システムの以降のバージョンで使用できます。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="odd">
<td><strong>IO_CSQ_IRP_CONTEXT</strong></td>
<td><p><strong>IO_CSQ_IRP_CONTEXT</strong>構造体は、非透過的なデータ構造をドライバーのキャンセルの安全な IRP のキューに IRP の IRP コンテキストを指定するために使用します。 キーとして使用されて、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirp" data-raw-source="[&lt;strong&gt;IoCsqInsertIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirp)"> <strong>IoCsqInsertIrp</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirpex" data-raw-source="[&lt;strong&gt;IoCsqInsertIrpEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirpex)"> <strong>IoCsqInsertIrpEx</strong></a>、および<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqremoveirp" data-raw-source="[&lt;strong&gt;IoCsqRemoveIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqremoveirp)"> <strong>IoCsqRemoveIrp</strong> </a>ルーチンは、キュー内の特定の Irp を識別するためにします。</p>
<p>キャンセルの安全な IRP のキューを使用する方法の概要については、次を参照してください。<a href="cancel-safe-irp-queues.md" data-raw-source="[Cancel-Safe IRP Queues](cancel-safe-irp-queues.md)">キャンセル セーフ IRP キュー</a>します。</p>
<p>Microsoft Windows XP および Windows オペレーティング システムの以降のバージョンで使用できます。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="even">
<td><strong>IO_WORKITEM</strong></td>
<td><p><strong>IO_WORKITEM</strong>構造は、システムのワーカー スレッドの作業項目を記述するための非透過構造体。</p>
<p>ドライバーは、呼び出すことによって、作業項目を割り当てることができます<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateworkitem" data-raw-source="[&lt;strong&gt;IoAllocateWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateworkitem)"> <strong>IoAllocateWorkItem</strong></a>します。 または、ドライバーが、独自のバッファーを割り当てることができますを呼び出して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinitializeworkitem" data-raw-source="[&lt;strong&gt;IoInitializeWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinitializeworkitem)"> <strong>IoInitializeWorkItem</strong> </a>を作業項目としては、そのバッファーを初期化します。</p>
<p>任意の作業項目が割り当てられる<strong>IoAllocateWorkItem</strong>によって解放する必要があります<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeworkitem" data-raw-source="[&lt;strong&gt;IoFreeWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeworkitem)"> <strong>IoFreeWorkItem</strong></a>します。 初期化されているメモリ<strong>IoInitializeWorkItem</strong>で初期化する必要があります<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iouninitializeworkitem" data-raw-source="[&lt;strong&gt;IoUninitializeWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iouninitializeworkitem)"> <strong>IoUninitializeWorkItem</strong> </a>解放できる前にします。</p>
<p>作業項目の詳細については、次を参照してください。<a href="system-worker-threads.md" data-raw-source="[System Worker Threads](system-worker-threads.md)">システム ワーカー スレッド</a>します。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="odd">
<td><strong>KBUGCHECK_CALLBACK_RECORD</strong></td>
<td><p><strong>KBUGCHECK_CALLBACK_RECORD</strong>構造体は、非透過構造体で使用される、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckcallback" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckcallback)"> <strong>KeRegisterBugCheckCallback</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckcallback" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckcallback)"> <strong>KeDeregisterBugCheckCallback</strong> </a>ルーチン。</p>
<p><strong>KBUGCHECK_CALLBACK_RECORD</strong> 、ブックキーピングの構造が使用される、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback)"> <strong>KeRegisterBugCheckReasonCallback</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback)"> <strong>KeDeregisterBugCheckReasonCallback</strong> </a>ルーチン。</p>
<p>構造は、非ページ プールなど、メモリに割り当てる必要があります。 使用して、 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;KeInitializeCallbackRecord&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"> <strong>KeInitializeCallbackRecord</strong> </a>ルーチンを使用する前に、構造体を初期化します。</p>
<p>ヘッダー:Ntddk.h します。 次のとおりNtddk.h します。</p></td>
</tr>
<tr class="even">
<td><strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong></td>
<td><p><strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong>構造体は、非透過構造体で使用される、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback)"> <strong>KeRegisterBugCheckReasonCallback</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback)"> <strong>KeDeregisterBugCheckReasonCallback</strong> </a>ルーチン。</p>
<p><strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong> 、ブックキーピングの構造が使用される、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback)"> <strong>KeRegisterBugCheckReasonCallback</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckReasonCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback)"> <strong>KeDeregisterBugCheckReasonCallback</strong> </a>ルーチン。</p>
<p>構造は、非ページ プールなど、メモリに割り当てる必要があります。 使用して、 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;KeInitializeCallbackRecord&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"> <strong>KeInitializeCallbackRecord</strong> </a>ルーチンを使用する前に、構造体を初期化します。</p>
<p>Microsoft Windows XP Service Pack 1 (SP1)、Windows Server 2003、および以降のバージョンの Windows オペレーティング システムで使用できます。</p>
<p>ヘッダー:Ntddk.h します。 次のとおりNtddk.h します。</p></td>
</tr>
<tr class="odd">
<td><strong>KDPC</strong></td>
<td><p><strong>KDPC</strong>構造体は、DPC オブジェクトを表す非透過構造体。 この構造体のメンバーを直接設定しないでください。 参照してください<a href="dpc-objects-and-dpcs.md" data-raw-source="[DPC Objects and DPCs](dpc-objects-and-dpcs.md)">DPC オブジェクトと Dpc</a>します。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="even">
<td><strong>KFLOATING_SAVE</strong></td>
<td><p><strong>KFLOATING_SAVE</strong>構造体は、不透明な浮動小数点を表す構造体の状態を<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesavefloatingpointstate" data-raw-source="[&lt;strong&gt;KeSaveFloatingPointState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesavefloatingpointstate)"> <strong>KeSaveFloatingPointState</strong> </a>ルーチンを保存します。</p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kerestorefloatingpointstate" data-raw-source="[&lt;strong&gt;KeRestoreFloatingPointState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kerestorefloatingpointstate)"> <strong>KeRestoreFloatingPointState</strong> </a>浮動小数点状態を復元します。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="odd">
<td><strong>KGUARDED_MUTEX</strong></td>
<td><p><strong>KGUARDED_MUTEX</strong>構造体は、保護されたミュー テックスを表す非透過構造体。</p>
<p>使用<strong>KeInitializeGuardedMutex</strong>初期化するために、 <strong>KGUARDED_MUTEX</strong>として保護されたミュー テックス構造体。</p>
<p>保護されたミュー テックスは、非ページ プールから割り当てる必要があります。</p>
<p>保護されたミュー テックスの詳細については、次を参照してください。<a href="fast-mutexes-and-guarded-mutexes.md" data-raw-source="[Fast Mutexes and Guarded Mutexes](fast-mutexes-and-guarded-mutexes.md)">ミュー テックスを高速と保護されたミュー テックス</a>します。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="even">
<td><strong>KINTERRUPT</strong></td>
<td><p>A <strong>KINTERRUPT</strong>構造体は、システムの割り込みを表す非透過構造。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex" data-raw-source="[&lt;strong&gt;IoConnectInterruptEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex)"><strong>IoConnectInterruptEx</strong> </a>へのポインター、 <strong>KINTERRUPT</strong>ドライバーの登録時に、割り込みの構造、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kservice_routine" data-raw-source="[&lt;em&gt;InterruptService&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kservice_routine)"> <em>InterruptService</em> </a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kmessage_service_routine" data-raw-source="[&lt;em&gt;InterruptMessageService&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kmessage_service_routine)"> <em>InterruptMessageService</em> </a>ルーチン。 ドライバーでは、このポインターを取得または割り込みの割り込みスピン ロックを解放するときに使用します。 ドライバーは、登録を解除するときにもこのポインターを使用する<em>InterruptService</em>ルーチン。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="odd">
<td><strong>KLOCK_QUEUE_HANDLE</strong></td>
<td><p><strong>KLOCK_QUEUE_HANDLE</strong>構造体は、非透過構造体をキューに置かれたスピン ロックについて説明します。 ドライバーを割り当てます、 <strong>KLOCK_QUEUE_HANDLE</strong>構造体、およびそれを<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLock&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))"> <strong>KeAcquireInStackQueuedSpinLock</strong> </a>と<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLockAtDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))"> <strong>KeAcquireInStackQueuedSpinLockAtDpcLevel</strong> </a>キューに置かれたスピン ロックを取得します。 これらのルーチンでは、キューに置かれたスピン ロックを表す構造体を初期化します。 ドライバーは、構造体を渡します<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock)"> <strong>KeReleaseInStackQueuedSpinLock</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLockFromDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)"> <strong>KeReleaseInStackQueuedSpinLockFromDpcLevel</strong> </a>ときに、スピン ロックを解放します。</p>
<p>詳細については、次を参照してください。<a href="queued-spin-locks.md" data-raw-source="[Queued Spin Locks](queued-spin-locks.md)">スピン ロックをキューに置かれた</a>します。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="even">
<td><strong>KTIMER</strong></td>
<td><p><strong>KTIMER</strong>構造体は、タイマー オブジェクトを表す非透過構造体。 この構造体のメンバーを直接設定しないでください。 詳細については、次を参照してください。<a href="timer-objects-and-dpcs.md" data-raw-source="[Timer Objects and DPCs](timer-objects-and-dpcs.md)">タイマー オブジェクトと Dpc</a>します。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="odd">
<td><strong>LOOKASIDE_LIST_EX</strong></td>
<td><p><strong>LOOKASIDE_LIST_EX</strong>構造体にルック アサイド リストがについて説明します。</p>
<pre class="syntax"><code>typedef struct _LOOKASIDE_LIST_EX {
  ...  // opaque
} LOOKASIDE_LIST_EX, *PLOOKASIDE_LIST_EX;</code></pre>
<p>ルック アサイド リストのシステム割り当てルーチンと、これによって、呼び出しの数を減らす、ドライバーがローカルで管理できる固定サイズ バッファー プールは、パフォーマンスが向上します。 バッファーが均一のサイズ、ルック アサイド リストのエントリとして格納されます。</p>
<p>ドライバーを扱う必要があります、 <strong>LOOKASIDE_LIST_EX</strong>不透明として構造体します。 ドライバーまたは構造体のメンバーへのアクセスに、これらのメンバーの場所にある依存関係があることには、移植性とその他のドライバーと相互運用されない可能性があります。</p>
<p>次の「参照」セクションにには、この構造を使用するルーチン一覧が含まれていますいます。</p>
<p>ルック アサイド リストの詳細については、次を参照してください。<a href="using-lookaside-lists.md" data-raw-source="[Using Lookaside Lists](using-lookaside-lists.md)">ルック アサイド リストを使用した</a>します。</p>
<p>64 ビットのプラットフォームでは、16 バイトでアラインがこの構造体にあります。</p>
<p>Windows Vista 以降でサポートされています。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="even">
<td><strong>NPAGED_LOOKASIDE_LIST</strong></td>
<td><p><strong>NPAGED_LOOKASIDE_LIST</strong>構造は、非ページ プールから割り当てられる固定サイズ バッファーのルック アサイド リストを記述するための非透過構造体。 システムでは、新しいエントリを作成し、必要に応じて、一覧に含まれる未使用エントリを破棄します。 固定サイズ バッファー、ルック アサイド リストを使用しては直接メモリの割り当てよりも高速です。</p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializenpagedlookasidelist" data-raw-source="[&lt;strong&gt;ExInitializeNPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializenpagedlookasidelist)"> <strong>ExInitializeNPagedLookasideList</strong> </a>ルック アサイド リストを初期化します。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatefromnpagedlookasidelist" data-raw-source="[&lt;strong&gt;ExAllocateFromNPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatefromnpagedlookasidelist)"> <strong>ExAllocateFromNPagedLookasideList</strong> </a>リストから、バッファーを割り当て、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreetonpagedlookasidelist" data-raw-source="[&lt;strong&gt;ExFreeToNPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreetonpagedlookasidelist)"> <strong>ExFreeToNPagedLookasideList</strong> </a>を返す、一覧にバッファー。</p>
<p>ドライバーでは、アンロードの前に作成する任意のルック アサイド リストを常に明示的に解放する必要があります。 それ以外の場合に実行する場合は、重大なプログラミング エラーになります。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletenpagedlookasidelist" data-raw-source="[&lt;strong&gt;ExDeleteNPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletenpagedlookasidelist)"> <strong>ExDeleteNPagedLookasideList</strong> </a>リストを解放します。</p>
<p>ドライバーのページ プール ルック アサイド リストにも使用できます。 Windows 2000 以降、 <strong>PAGED_LOOKASIDE_LIST</strong>構造体には、ページ バッファを含むルック アサイド リストがについて説明します。 以降、Windows Vista では、 <strong>LOOKASIDE_LIST_EX</strong>構造体は、非ページや段組のバッファーを含むルック アサイド リストを記述できます。 詳細については、次を参照してください。<a href="using-lookaside-lists.md" data-raw-source="[Using Lookaside Lists](using-lookaside-lists.md)">ルック アサイド リストを使用した</a>します。</p>
<p>64 ビットのプラットフォームでは、16 バイトでアラインがこの構造体にあります。</p>
<p>Windows 2000 以降をサポートします。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="odd">
<td><strong>OBJECT_TYPE</strong></td>
<td><p><strong>OBJECT_TYPE</strong>はハンドルのオブジェクトの種類を指定するための非透過構造体。 詳細については、次を参照してください。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)"> <strong>ObReferenceObjectByHandle</strong></a>します。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="even">
<td><strong>PAGED_LOOKASIDE_LIST</strong></td>
<td><p><strong>PAGED_LOOKASIDE_LIST</strong>構造は、ページ プールから割り当てられる固定サイズ バッファーのルック アサイド リストを記述するための非透過構造体。 システムでは、新しいエントリを作成し、必要に応じて、一覧に含まれる未使用エントリを破棄します。 固定サイズ バッファー、ルック アサイド リストを使用しては直接メモリの割り当てよりも高速です。</p>
<p>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializepagedlookasidelist" data-raw-source="[&lt;strong&gt;ExInitializePagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializepagedlookasidelist)"> <strong>ExInitializePagedLookasideList</strong> </a>ルック アサイド リストを初期化します。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatefrompagedlookasidelist" data-raw-source="[&lt;strong&gt;ExAllocateFromPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatefrompagedlookasidelist)"> <strong>ExAllocateFromPagedLookasideList</strong> </a>リストから、バッファーを割り当て、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreetopagedlookasidelist" data-raw-source="[&lt;strong&gt;ExFreeToPagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreetopagedlookasidelist)"> <strong>ExFreeToPagedLookasideList</strong> </a>を返す、一覧にバッファー。</p>
<p>ドライバーでは、アンロードの前に作成する任意のルック アサイド リストを常に明示的に解放する必要があります。 それ以外の場合に実行する場合は、重大なプログラミング エラーになります。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletepagedlookasidelist" data-raw-source="[&lt;strong&gt;ExDeletePagedLookasideList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletepagedlookasidelist)"> <strong>ExDeletePagedLookasideList</strong> </a>リストを解放します。</p>
<p>ドライバーの非ページ プール ルック アサイド リストにも使用できます。 Windows 2000 以降、 <strong>NPAGED_LOOKASIDE_LIST</strong>構造体には、非ページのバッファーを含むルック アサイド リストがについて説明します。 以降、Windows Vista では、 <strong>LOOKASIDE_LIST_EX</strong>構造体は、非ページや段組のバッファーを含むルック アサイド リストを記述できます。 詳細については、次を参照してください。<a href="using-lookaside-lists.md" data-raw-source="[Using Lookaside Lists](using-lookaside-lists.md)">ルック アサイド リストを使用した</a>します。</p>
<p>64 ビットのプラットフォームでは、16 バイトでアラインがこの構造体にあります。</p>
<p>Windows 2000 以降をサポートします。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="odd">
<td><strong>RTL_BITMAP</strong></td>
<td><p><strong>RTL_BITMAP</strong>構造はビットマップを記述するための非透過構造体。</p>
<pre class="syntax"><code>typedef struct _RTL_BITMAP {
  // opaque
} RTL_BITMAP, *PRTL_BITMAP;</code></pre>
<p>この構造体のメンバーに直接アクセスしない操作を行います。 メンバーの場所への依存関係や、メンバーの値にアクセス直接残る可能性がありますいない Windows オペレーティング システムの将来のバージョンと互換性があるドライバー。</p>
<p><strong>RTL_BITMAP</strong>構造体は、任意の長さの汎用的な 1 次元のビットマップのヘッダーとして機能します。 ドライバーは、一連の再利用可能な項目を追跡する経済的な方法として、このようなビットマップを使用できます。 たとえば、ファイル システムは、ビットマップを使用して、どのクラスターを追跡するためとハード ディスク上のセクターがファイル データを保持するために既に割り当てられています。</p>
<p>一覧については、 <strong>Rtl<em>Xxx</em></strong> ルーチンを使用する<strong>RTL_BITMAP</strong>構造体は、次の「参照」セクションを参照してください。 これらの呼び出し元<strong>Rtl<em>Xxx</em></strong> ルーチンのストレージを割り当て、 <strong>RTL_BITMAP</strong>構造体であり、ビットマップを含んでいるバッファー。 このバッファーはメモリ内の 4 バイト境界で開始する必要があり、長さは 4 バイトの倍数である必要があります。 ビットマップは、バッファーの先頭から始まりますが、割り当てられたバッファーに収まるビットの任意の数を含めることができます。</p>
<p>指定する前に、 <strong>RTL_BITMAP</strong>へのパラメーターとして構造体、 <strong>Rtl<em>Xxx</em></strong> ルーチンを呼び出し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlinitializebitmap" data-raw-source="[&lt;strong&gt;RtlInitializeBitMap&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlinitializebitmap)"> <strong>RtlInitializeBitMap</strong></a>ルーチンを構造体を初期化します。 このルーチンへの入力パラメーターは、ビットマップとビットマップのビット単位のサイズを格納しているバッファーへのポインターです。 <strong>RtlInitializeBitMap</strong>このバッファーの内容は変更されません。</p>
<p>呼び出し元のストレージを割り当てる場合、 <strong>RTL_BITMAP</strong> IRQL で呼び出し元を実行する必要があります構造とページングされたメモリにビットマップの場合は、 &lt;のいずれかのパラメーターとしてこの構造体へのポインターを渡すときに、APC_LEVELを=<strong>Rtl<em>Xxx</em></strong>  「参照」セクションに記載されているルーチン。 呼び出すときに、呼び出し元を任意の IRQL で実行できる場合は、呼び出し元は、非ページ メモリから (または同等に、ロックされているページ メモリから)、記憶域を割り当て、 <strong>Rtl<em>Xxx</em></strong> ルーチン。</p>
<p>Windows 2000 以降のバージョンの Windows でサポートされています。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="even">
<td><strong>RTL_RUN_ONCE</strong></td>
<td><p><strong>RTL_RUN_ONCE</strong>構造は、one-time initialization の情報を格納するための非透過構造体。</p>
<p>ドライバーは、呼び出すことによってこの構造体を初期化する必要があります、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlrunonceinitialize" data-raw-source="[&lt;strong&gt;RtlRunOnceInitialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlrunonceinitialize)"> <strong>RtlRunOnceInitialize</strong> </a>他に渡す前に日常的な<strong>RtlRunOnce<em>Xxx</em></strong> ルーチン。</p>
<p>Windows Vista および Windows オペレーティング システムの以降のバージョンでのみ使用できます。</p>
<p>ヘッダー:Ntddk.h します。 次のとおりNtddk.h します。</p></td>
</tr>
<tr class="odd">
<td><strong>SECURITY_SUBJECT_CONTEXT</strong></td>
<td><p><strong>SECURITY_SUBJECT_CONTEXT</strong>構造体は、特定の操作が行われるセキュリティ コンテキストを表す非透過構造体。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="even">
<td><strong>SLIST_HEADER</strong></td>
<td><p><strong>SLIST_HEADER</strong>構造は、シーケンス処理されたシングル リンク リストのヘッダーとして機能するための非透過構造体。 詳細については、次を参照してください。<a href="singly-and-doubly-linked-lists.md" data-raw-source="[Singly and Doubly Linked Lists](singly-and-doubly-linked-lists.md)">リンクされたリストの片方向と双方向</a>します。</p>
<p>64 ビットのプラットフォームで<strong>SLIST_HEADER</strong>構造体は 16 バイトでアラインである必要があります。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="odd">
<td><strong>XSTATE_SAVE</strong></td>
<td><p><strong>XSTATE_SAVE</strong>構造体は、カーネル モード ドライバーの保存および復元する拡張プロセッサの状態情報を記述するための非透過構造体。</p>
<pre class="syntax"><code>typedef struct _XSTATE_SAVE {
  ...  // opaque
} XSTATE_SAVE, *PXSTATE_SAVE;</code></pre>
<p>すべてのメンバーは、不透明です。</p>
<p>この構造が使用者、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesaveextendedprocessorstate" data-raw-source="[&lt;strong&gt;KeSaveExtendedProcessorState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesaveextendedprocessorstate)"> <strong>KeSaveExtendedProcessorState</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kerestoreextendedprocessorstate" data-raw-source="[&lt;strong&gt;KeRestoreExtendedProcessorState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kerestoreextendedprocessorstate)"> <strong>KeRestoreExtendedProcessorState</strong> </a>ルーチン。</p>
<p>Windows 7 および Windows オペレーティング システムの以降のバージョンでサポートされています。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[**BugCheckDumpIoCallback**](https://msdn.microsoft.com/library/windows/hardware/ff540677)  
[**BugCheckSecondaryDumpDataCallback**](https://msdn.microsoft.com/library/windows/hardware/ff540679)  
[**ExAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))  
[**ExAcquireFastMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544340(v=vs.85))  
[**ExAllocateFromLookasideListEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatefromlookasidelistex)  
[**ExAllocateFromNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatefromnpagedlookasidelist)  
[**ExAllocateFromPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatefrompagedlookasidelist)  
[**ExAllocateTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatetimer)  
[**ExDeletePagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletepagedlookasidelist)  
[**ExFreeToPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreetopagedlookasidelist)  
[**ExInitializePagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializepagedlookasidelist)  
[**ExCancelTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-excanceltimer)  
[**ExDeleteLookasideListEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletelookasidelistex)  
[**ExDeleteNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletenpagedlookasidelist)  
[**ExDeleteTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletetimer)  
[**ExFlushLookasideListEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exflushlookasidelistex)  
[**ExFreeToLookasideListEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreetolookasidelistex)  
[**ExFreeToNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreetonpagedlookasidelist)  
[**ExInitializeLookasideListEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializelookasidelistex)  
[**ExInitializeNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializenpagedlookasidelist)  
[**ExInitializeSListHead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-initializeslisthead)  
[**ExInterlockedFlushSList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinterlockedflushslist)  
[**ExInterlockedPopEntrySList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinterlockedpopentryslist)  
[**ExInterlockedPushEntrySList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinterlockedpushentryslist)  
[**ExQueryDepthSList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exquerydepthslist)  
[**ExReleaseFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545549(v=vs.85))  
[**ExReleaseFastMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545567(v=vs.85))  
[**ExSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exsettimer)  
[**ExTryToAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545647(v=vs.85))  
[*ExTimerCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ext_callback)  
[**IoAllocateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateworkitem)  
[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex)  
[**IoCsqInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinitialize)  
[**IoCsqInitializeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinitializeex)  
[**IoCsqInsertIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirp)  
[**IoCsqInsertIrpEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirpex)  
[**IoCsqRemoveIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqremoveirp)  
[**IoDisconnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodisconnectinterruptex)  
[**IoFreeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeworkitem)  
[**IoInitializeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinitializeworkitem)  
[**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iorequestdpc)  
[**IoUninitializeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iouninitializeworkitem)  
[**KeAcquireGuardedMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551892(v=vs.85))  
[**KeAcquireGuardedMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551894(v=vs.85))  
[**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))  
[**KeAcquireInStackQueuedSpinLockAtDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))  
[**KeAcquireInterruptSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551914(v=vs.85))  
[**KeCancelTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kecanceltimer)  
[**KeInitializeCallbackRecord**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)  
[**KeInitializeGuardedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializeguardedmutex)  
[**KeInitializeTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializetimer)  
[**KeInitializeTimerEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializetimerex)  
[**KeReadStateTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereadstatetimer)  
[**KeRestoreExtendedProcessorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kerestoreextendedprocessorstate)  
[**KeSaveExtendedProcessorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesaveextendedprocessorstate)  
[**KeSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesettimer)  
[**KeSetTimerEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesettimerex)  
[**KeDeregisterBugCheckCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckcallback)  
[**KeDeregisterBugCheckReasonCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback)  
[**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertqueuedpc)  
[**KeRegisterBugCheckCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckcallback)  
[**KeRegisterBugCheckReasonCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback)  
[**KeReleaseGuardedMutexUnsafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseguardedmutexunsafe)  
[**KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock)  
[**KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)  
[**KeReleaseInterruptSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinterruptspinlock)  
[**KeRestoreFloatingPointState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kerestorefloatingpointstate)  
[**KeSaveFloatingPointState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesavefloatingpointstate)  
[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)  
[*LookasideListAllocateEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-allocate_function_ex)  
[*LookasideListFreeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-free_function_ex)  
[**ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)  
[**PsGetCurrentProcess**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer#psgetcurrentprocess)  
[**PsGetProcessCreateTimeQuadPart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psgetprocesscreatetimequadpart)  
[**PsInitialSystemProcess**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm64bitphysicaladdress)  
[**PsIsSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-psissystemthread)  
[**RtlRunOnceBeginInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlrunoncebegininitialize)  
[**RtlRunOnceComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlrunoncecomplete)  
[**RtlRunOnceExecuteOnce**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlrunonceexecuteonce)  
[**RtlRunOnceInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlrunonceinitialize)  
[*RunOnceInitialization*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-rtl_run_once_init_fn)  
[Run-Down 保護](run-down-protection.md)  
[**SeAccessCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-seaccesscheck)  
[**SeAssignSecurity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-seassignsecurity)  
[**SeAssignSecurityEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-seassignsecurityex)  



