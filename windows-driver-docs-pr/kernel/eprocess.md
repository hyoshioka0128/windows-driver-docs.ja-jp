---
title: Windows カーネルの不透明な構造体
description: Windows カーネルの不透明な構造体
ms.assetid: 4053d82e-78ae-4945-ad5b-44ba41229a5d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9b22a03616aa0b43a2d46979510f19787c23d50a
ms.sourcegitcommit: 69e7e3a70c491feb4b7cee258f710585843168c0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2019
ms.locfileid: "59480335"
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
<p>一部のルーチンなど<a href="https://msdn.microsoft.com/library/windows/hardware/ff559939" data-raw-source="[&lt;strong&gt;PsGetProcessCreateTimeQuadPart&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559939)"> <strong>PsGetProcessCreateTimeQuadPart</strong></a>を使用して、 <strong>」プロセス</strong>で動作するプロセスを特定します。 ドライバーを使用できる、 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer#psgetcurrentprocess" data-raw-source="[&lt;strong&gt;PsGetCurrentProcess&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer#psgetcurrentprocess)"> <strong>PsGetCurrentProcess</strong> </a>プロセスへのポインターを取得するルーチンが、現在のプロセス オブジェクトし、を使用できます、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff558679" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558679)"> <strong>ObReferenceObjectByHandle</strong></a>ルーチンを指定したハンドルに関連付けられているプロセス オブジェクトへのポインターを取得します。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559943" data-raw-source="[&lt;strong&gt;PsInitialSystemProcess&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559943)"> <strong>PsInitialSystemProcess</strong> </a>グローバル変数は、システム プロセスのプロセス オブジェクトを指します。</p>
<p>プロセス オブジェクトはオブジェクトの Manager オブジェクトであることに注意してください。 ドライバーはなどオブジェクト マネージャー ルーチンを使用する必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff558678" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558678)"> <strong>ObReferenceObject</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff557724" data-raw-source="[&lt;strong&gt;ObDereferenceObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557724)"> <strong>ObDereferenceObject</strong> </a>オブジェクトを維持するには参照カウントします。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="even">
<td><strong>ETHREAD</strong></td>
<td><p><strong>ETHREAD</strong>構造体は、スレッドのスレッド オブジェクトとして機能するための非透過構造体。</p>
<p>一部のルーチンなど<a href="https://msdn.microsoft.com/library/windows/hardware/ff559945" data-raw-source="[&lt;strong&gt;PsIsSystemThread&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559945)"> <strong>PsIsSystemThread</strong></a>を使用して、 <strong>ETHREAD</strong>を操作するスレッドを識別するためにします。 ドライバーを使用できる、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559936" data-raw-source="[&lt;strong&gt;PsGetCurrentThread&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559936)"> <strong>PsGetCurrentThread</strong> </a>スレッドへのポインターを取得するルーチンが、現在のスレッド オブジェクトし、を使用できます、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff558679" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558679)"> <strong>ObReferenceObjectByHandle</strong></a>ルーチンを指定したハンドルに関連付けられているスレッド オブジェクトへのポインターを取得します。</p>
<p>スレッド オブジェクトはオブジェクトの Manager オブジェクトであることに注意してください。 ドライバーはなどオブジェクト マネージャー ルーチンを使用する必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff558678" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558678)"> <strong>ObReferenceObject</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff557724" data-raw-source="[&lt;strong&gt;ObDereferenceObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557724)"> <strong>ObDereferenceObject</strong> </a>オブジェクトを維持するには参照カウントします。</p>
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
<li><a href="https://msdn.microsoft.com/library/windows/hardware/dn265188" data-raw-source="[&lt;strong&gt;ExSetTimer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265188)"><strong>ExSetTimer</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/dn265180" data-raw-source="[&lt;strong&gt;ExCancelTimer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265180)"><strong>ExCancelTimer</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/dn265181" data-raw-source="[&lt;strong&gt;ExDeleteTimer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265181)"><strong>ExDeleteTimer</strong></a></li>
</ul>
<p><strong>EX_TIMER</strong>-ベースのタイマー オブジェクトは、オペレーティング システムによって作成されます。 タイマー オブジェクトをドライバーの呼び出しのようなを取得する、 <a href="https://msdn.microsoft.com/library/windows/hardware/dn265179" data-raw-source="[&lt;strong&gt;ExAllocateTimer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265179)"> <strong>ExAllocateTimer</strong> </a>ルーチン。 呼び出すことによって、オブジェクトを削除するため、ドライバーはこのオブジェクトが不要<strong>ExDeleteTimer</strong>します。</p>
<p>詳細については、次を参照してください。 <a href="exxxxtimer-routines-and-ex-timer-objects.md" data-raw-source="[Ex&lt;em&gt;Xxx&lt;/em&gt;Timer Routines and EX_TIMER Objects](exxxxtimer-routines-and-ex-timer-objects.md)">Ex<em>Xxx</em>タイマー ルーチンと EX_TIMER オブジェクト</a>します。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="odd">
<td><strong>FAST_MUTEX</strong></td>
<td><p>A <strong>FAST_MUTEX</strong>構造が高速なミュー テックスを表す非透過データ構造体。</p>
<p>A <strong>FAST_MUTEX</strong>で構造体が初期化される、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff545293" data-raw-source="[&lt;strong&gt;ExInitializeFastMutex&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545293)"> <strong>ExInitializeFastMutex</strong> </a>ルーチン。</p>
<p>高速なミュー テックスの詳細については、次を参照してください。<a href="fast-mutexes-and-guarded-mutexes.md" data-raw-source="[Fast Mutexes and Guarded Mutexes](fast-mutexes-and-guarded-mutexes.md)">高速なミュー テックスと保護されたミュー テックス</a>します。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="even">
<td><strong>IO_CSQ</strong></td>
<td><p><strong>IO_CSQ</strong>構造体は、非透過構造体がドライバーのキャンセルの安全な IRP キュー ルーチンを指定するために使用します。 この構造体のメンバーを直接設定しないでください。 使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff549054" data-raw-source="[&lt;strong&gt;IoCsqInitialize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549054)"> <strong>IoCsqInitialize</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff549060" data-raw-source="[&lt;strong&gt;IoCsqInitializeEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549060)"> <strong>IoCsqInitializeEx</strong> </a>この構造体を初期化します。</p>
<p>キャンセルの安全な IRP のキューを使用する方法の概要については、次を参照してください。<a href="cancel-safe-irp-queues.md" data-raw-source="[Cancel-Safe IRP Queues](cancel-safe-irp-queues.md)">キャンセル セーフ IRP キュー</a>します。</p>
<p>Microsoft Windows XP および Windows オペレーティング システムの以降のバージョンで使用できます。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="odd">
<td><strong>IO_CSQ_IRP_CONTEXT</strong></td>
<td><p><strong>IO_CSQ_IRP_CONTEXT</strong>構造体は、非透過的なデータ構造をドライバーのキャンセルの安全な IRP のキューに IRP の IRP コンテキストを指定するために使用します。 キーとして使用されて、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff549066" data-raw-source="[&lt;strong&gt;IoCsqInsertIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549066)"> <strong>IoCsqInsertIrp</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff549067" data-raw-source="[&lt;strong&gt;IoCsqInsertIrpEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549067)"> <strong>IoCsqInsertIrpEx</strong></a>、および<a href="https://msdn.microsoft.com/library/windows/hardware/ff549070" data-raw-source="[&lt;strong&gt;IoCsqRemoveIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549070)"> <strong>IoCsqRemoveIrp</strong> </a>ルーチンは、キュー内の特定の Irp を識別するためにします。</p>
<p>キャンセルの安全な IRP のキューを使用する方法の概要については、次を参照してください。<a href="cancel-safe-irp-queues.md" data-raw-source="[Cancel-Safe IRP Queues](cancel-safe-irp-queues.md)">キャンセル セーフ IRP キュー</a>します。</p>
<p>Microsoft Windows XP および Windows オペレーティング システムの以降のバージョンで使用できます。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="even">
<td><strong>IO_WORKITEM</strong></td>
<td><p><strong>IO_WORKITEM</strong>構造は、システムのワーカー スレッドの作業項目を記述するための非透過構造体。</p>
<p>ドライバーは、呼び出すことによって、作業項目を割り当てることができます<a href="https://msdn.microsoft.com/library/windows/hardware/ff548276" data-raw-source="[&lt;strong&gt;IoAllocateWorkItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548276)"> <strong>IoAllocateWorkItem</strong></a>します。 または、ドライバーが、独自のバッファーを割り当てることができますを呼び出して<a href="https://msdn.microsoft.com/library/windows/hardware/ff549349" data-raw-source="[&lt;strong&gt;IoInitializeWorkItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549349)"> <strong>IoInitializeWorkItem</strong> </a>を作業項目としては、そのバッファーを初期化します。</p>
<p>任意の作業項目が割り当てられる<strong>IoAllocateWorkItem</strong>によって解放する必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff549133" data-raw-source="[&lt;strong&gt;IoFreeWorkItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549133)"> <strong>IoFreeWorkItem</strong></a>します。 初期化されているメモリ<strong>IoInitializeWorkItem</strong>で初期化する必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff550392" data-raw-source="[&lt;strong&gt;IoUninitializeWorkItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550392)"> <strong>IoUninitializeWorkItem</strong> </a>解放できる前にします。</p>
<p>作業項目の詳細については、次を参照してください。<a href="system-worker-threads.md" data-raw-source="[System Worker Threads](system-worker-threads.md)">システム ワーカー スレッド</a>します。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="odd">
<td><strong>KBUGCHECK_CALLBACK_RECORD</strong></td>
<td><p><strong>KBUGCHECK_CALLBACK_RECORD</strong>構造体は、非透過構造体で使用される、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff553105" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553105)"> <strong>KeRegisterBugCheckCallback</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff551992" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551992)"> <strong>KeDeregisterBugCheckCallback</strong> </a>ルーチン。</p>
<p><strong>KBUGCHECK_CALLBACK_RECORD</strong> 、ブックキーピングの構造が使用される、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff553110" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckReasonCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553110)"> <strong>KeRegisterBugCheckReasonCallback</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff552003" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckReasonCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552003)"> <strong>KeDeregisterBugCheckReasonCallback</strong> </a>ルーチン。</p>
<p>構造は、非ページ プールなど、メモリに割り当てる必要があります。 使用して、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff552109" data-raw-source="[&lt;strong&gt;KeInitializeCallbackRecord&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552109)"> <strong>KeInitializeCallbackRecord</strong> </a>ルーチンを使用する前に、構造体を初期化します。</p>
<p>ヘッダー:Ntddk.h します。 次のとおりNtddk.h します。</p></td>
</tr>
<tr class="even">
<td><strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong></td>
<td><p><strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong>構造体は、非透過構造体で使用される、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff553110" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckReasonCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553110)"> <strong>KeRegisterBugCheckReasonCallback</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff552003" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckReasonCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552003)"> <strong>KeDeregisterBugCheckReasonCallback</strong> </a>ルーチン。</p>
<p><strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong> 、ブックキーピングの構造が使用される、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff553110" data-raw-source="[&lt;strong&gt;KeRegisterBugCheckReasonCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553110)"> <strong>KeRegisterBugCheckReasonCallback</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff552003" data-raw-source="[&lt;strong&gt;KeDeregisterBugCheckReasonCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552003)"> <strong>KeDeregisterBugCheckReasonCallback</strong> </a>ルーチン。</p>
<p>構造は、非ページ プールなど、メモリに割り当てる必要があります。 使用して、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff552109" data-raw-source="[&lt;strong&gt;KeInitializeCallbackRecord&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552109)"> <strong>KeInitializeCallbackRecord</strong> </a>ルーチンを使用する前に、構造体を初期化します。</p>
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
<td><p><strong>KFLOATING_SAVE</strong>構造体は、不透明な浮動小数点を表す構造体の状態を<a href="https://msdn.microsoft.com/library/windows/hardware/ff553243" data-raw-source="[&lt;strong&gt;KeSaveFloatingPointState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553243)"> <strong>KeSaveFloatingPointState</strong> </a>ルーチンを保存します。</p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff553185" data-raw-source="[&lt;strong&gt;KeRestoreFloatingPointState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553185)"> <strong>KeRestoreFloatingPointState</strong> </a>浮動小数点状態を復元します。</p>
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
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548378" data-raw-source="[&lt;strong&gt;IoConnectInterruptEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548378)"><strong>IoConnectInterruptEx</strong> </a>へのポインター、 <strong>KINTERRUPT</strong>ドライバーの登録時に、割り込みの構造、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff547958" data-raw-source="[&lt;em&gt;InterruptService&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547958)"> <em>InterruptService</em> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff547940" data-raw-source="[&lt;em&gt;InterruptMessageService&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547940)"> <em>InterruptMessageService</em> </a>ルーチン。 ドライバーでは、このポインターを取得または割り込みの割り込みスピン ロックを解放するときに使用します。 ドライバーは、登録を解除するときにもこのポインターを使用する<em>InterruptService</em>ルーチン。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="odd">
<td><strong>KLOCK_QUEUE_HANDLE</strong></td>
<td><p><strong>KLOCK_QUEUE_HANDLE</strong>構造体は、非透過構造体をキューに置かれたスピン ロックについて説明します。 ドライバーを割り当てます、 <strong>KLOCK_QUEUE_HANDLE</strong>構造体、およびそれを<a href="https://msdn.microsoft.com/library/windows/hardware/ff551899" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551899)"> <strong>KeAcquireInStackQueuedSpinLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff551908" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLockAtDpcLevel&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551908)"> <strong>KeAcquireInStackQueuedSpinLockAtDpcLevel</strong> </a>キューに置かれたスピン ロックを取得します。 これらのルーチンでは、キューに置かれたスピン ロックを表す構造体を初期化します。 ドライバーは、構造体を渡します<a href="https://msdn.microsoft.com/library/windows/hardware/ff553130" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553130)"> <strong>KeReleaseInStackQueuedSpinLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff553137" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLockFromDpcLevel&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553137)"> <strong>KeReleaseInStackQueuedSpinLockFromDpcLevel</strong> </a>ときに、スピン ロックを解放します。</p>
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
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545301" data-raw-source="[&lt;strong&gt;ExInitializeNPagedLookasideList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545301)"> <strong>ExInitializeNPagedLookasideList</strong> </a>ルック アサイド リストを初期化します。 使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff544388" data-raw-source="[&lt;strong&gt;ExAllocateFromNPagedLookasideList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544388)"> <strong>ExAllocateFromNPagedLookasideList</strong> </a>リストから、バッファーを割り当て、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff544601" data-raw-source="[&lt;strong&gt;ExFreeToNPagedLookasideList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544601)"> <strong>ExFreeToNPagedLookasideList</strong> </a>を返す、一覧にバッファー。</p>
<p>ドライバーでは、アンロードの前に作成する任意のルック アサイド リストを常に明示的に解放する必要があります。 それ以外の場合に実行する場合は、重大なプログラミング エラーになります。 使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff544566" data-raw-source="[&lt;strong&gt;ExDeleteNPagedLookasideList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544566)"> <strong>ExDeleteNPagedLookasideList</strong> </a>リストを解放します。</p>
<p>ドライバーのページ プール ルック アサイド リストにも使用できます。 Windows 2000 以降、 <strong>PAGED_LOOKASIDE_LIST</strong>構造体には、ページ バッファを含むルック アサイド リストがについて説明します。 以降、Windows Vista では、 <strong>LOOKASIDE_LIST_EX</strong>構造体は、非ページや段組のバッファーを含むルック アサイド リストを記述できます。 詳細については、次を参照してください。<a href="using-lookaside-lists.md" data-raw-source="[Using Lookaside Lists](using-lookaside-lists.md)">ルック アサイド リストを使用した</a>します。</p>
<p>64 ビットのプラットフォームでは、16 バイトでアラインがこの構造体にあります。</p>
<p>Windows 2000 以降をサポートします。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="odd">
<td><strong>OBJECT_TYPE</strong></td>
<td><p><strong>OBJECT_TYPE</strong>はハンドルのオブジェクトの種類を指定するための非透過構造体。 詳細については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff558679" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558679)"> <strong>ObReferenceObjectByHandle</strong></a>します。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="even">
<td><strong>PAGED_LOOKASIDE_LIST</strong></td>
<td><p><strong>PAGED_LOOKASIDE_LIST</strong>構造は、ページ プールから割り当てられる固定サイズ バッファーのルック アサイド リストを記述するための非透過構造体。 システムでは、新しいエントリを作成し、必要に応じて、一覧に含まれる未使用エントリを破棄します。 固定サイズ バッファー、ルック アサイド リストを使用しては直接メモリの割り当てよりも高速です。</p>
<p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545309" data-raw-source="[&lt;strong&gt;ExInitializePagedLookasideList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545309)"> <strong>ExInitializePagedLookasideList</strong> </a>ルック アサイド リストを初期化します。 使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff544393" data-raw-source="[&lt;strong&gt;ExAllocateFromPagedLookasideList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544393)"> <strong>ExAllocateFromPagedLookasideList</strong> </a>リストから、バッファーを割り当て、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff544605" data-raw-source="[&lt;strong&gt;ExFreeToPagedLookasideList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544605)"> <strong>ExFreeToPagedLookasideList</strong> </a>を返す、一覧にバッファー。</p>
<p>ドライバーでは、アンロードの前に作成する任意のルック アサイド リストを常に明示的に解放する必要があります。 それ以外の場合に実行する場合は、重大なプログラミング エラーになります。 使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff544570" data-raw-source="[&lt;strong&gt;ExDeletePagedLookasideList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544570)"> <strong>ExDeletePagedLookasideList</strong> </a>リストを解放します。</p>
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
<p>指定する前に、 <strong>RTL_BITMAP</strong>へのパラメーターとして構造体、 <strong>Rtl<em>Xxx</em></strong> ルーチンを呼び出し、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff561925" data-raw-source="[&lt;strong&gt;RtlInitializeBitMap&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561925)"> <strong>RtlInitializeBitMap</strong></a>ルーチンを構造体を初期化します。 このルーチンへの入力パラメーターは、ビットマップとビットマップのビット単位のサイズを格納しているバッファーへのポインターです。 <strong>RtlInitializeBitMap</strong>このバッファーの内容は変更されません。</p>
<p>呼び出し元のストレージを割り当てる場合、 <strong>RTL_BITMAP</strong> IRQL で呼び出し元を実行する必要があります構造とページングされたメモリにビットマップの場合は、 &lt;のいずれかのパラメーターとしてこの構造体へのポインターを渡すときに、APC_LEVELを=<strong>Rtl<em>Xxx</em></strong>  「参照」セクションに記載されているルーチン。 呼び出すときに、呼び出し元を任意の IRQL で実行できる場合は、呼び出し元は、非ページ メモリから (または同等に、ロックされているページ メモリから)、記憶域を割り当て、 <strong>Rtl<em>Xxx</em></strong> ルーチン。</p>
<p>Windows 2000 以降のバージョンの Windows でサポートされています。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
<tr class="even">
<td><strong>RTL_RUN_ONCE</strong></td>
<td><p><strong>RTL_RUN_ONCE</strong>構造は、one-time initialization の情報を格納するための非透過構造体。</p>
<p>ドライバーは、呼び出すことによってこの構造体を初期化する必要があります、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff562767" data-raw-source="[&lt;strong&gt;RtlRunOnceInitialize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562767)"> <strong>RtlRunOnceInitialize</strong> </a>他に渡す前に日常的な<strong>RtlRunOnce<em>Xxx</em></strong> ルーチン。</p>
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
<p>この構造が使用者、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff553238" data-raw-source="[&lt;strong&gt;KeSaveExtendedProcessorState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553238)"> <strong>KeSaveExtendedProcessorState</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff553182" data-raw-source="[&lt;strong&gt;KeRestoreExtendedProcessorState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553182)"> <strong>KeRestoreExtendedProcessorState</strong> </a>ルーチン。</p>
<p>Windows 7 および Windows オペレーティング システムの以降のバージョンでサポートされています。</p>
<p>ヘッダー:Wdm.h します。 次のとおりWdm.h、Ntddk.h、Ntifs.h します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[**BugCheckDumpIoCallback**](https://msdn.microsoft.com/library/windows/hardware/ff540677)  
[**BugCheckSecondaryDumpDataCallback**](https://msdn.microsoft.com/library/windows/hardware/ff540679)  
[**ExAcquireFastMutex**](https://msdn.microsoft.com/library/windows/hardware/ff544337)  
[**ExAcquireFastMutexUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff544340)  
[**ExAllocateFromLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff544381)  
[**ExAllocateFromNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544388)  
[**ExAllocateFromPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544393)  
[**ExAllocateTimer**](https://msdn.microsoft.com/library/windows/hardware/dn265179)  
[**ExDeletePagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544570)  
[**ExFreeToPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544605)  
[**ExInitializePagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545309)  
[**ExCancelTimer**](https://msdn.microsoft.com/library/windows/hardware/dn265180)  
[**ExDeleteLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff544563)  
[**ExDeleteNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544566)  
[**ExDeleteTimer**](https://msdn.microsoft.com/library/windows/hardware/dn265181)  
[**ExFlushLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff544587)  
[**ExFreeToLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff544597)  
[**ExFreeToNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544601)  
[**ExInitializeLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff545298)  
[**ExInitializeNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545301)  
[**ExInitializeSListHead**](https://msdn.microsoft.com/library/windows/hardware/ff545321)  
[**ExInterlockedFlushSList**](https://msdn.microsoft.com/library/windows/hardware/ff545379)  
[**ExInterlockedPopEntrySList**](https://msdn.microsoft.com/library/windows/hardware/ff545414)  
[**ExInterlockedPushEntrySList**](https://msdn.microsoft.com/library/windows/hardware/ff545422)  
[**ExQueryDepthSList**](https://msdn.microsoft.com/library/windows/hardware/ff545502)  
[**ExReleaseFastMutex**](https://msdn.microsoft.com/library/windows/hardware/ff545549)  
[**ExReleaseFastMutexUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff545567)  
[**ExSetTimer**](https://msdn.microsoft.com/library/windows/hardware/dn265188)  
[**ExTryToAcquireFastMutex**](https://msdn.microsoft.com/library/windows/hardware/ff545647)  
[*ExTimerCallback*](https://msdn.microsoft.com/library/windows/hardware/dn265190)  
[**IoAllocateWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff548276)  
[**IoConnectInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff548378)  
[**IoCsqInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff549054)  
[**IoCsqInitializeEx**](https://msdn.microsoft.com/library/windows/hardware/ff549060)  
[**IoCsqInsertIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549066)  
[**IoCsqInsertIrpEx**](https://msdn.microsoft.com/library/windows/hardware/ff549067)  
[**IoCsqRemoveIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549070)  
[**IoDisconnectInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff549093)  
[**IoFreeWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549133)  
[**IoInitializeWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549349)  
[**IoRequestDpc**](https://msdn.microsoft.com/library/windows/hardware/ff549657)  
[**IoUninitializeWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff550392)  
[**KeAcquireGuardedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff551892)  
[**KeAcquireGuardedMutexUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff551894)  
[**KeAcquireInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551899)  
[**KeAcquireInStackQueuedSpinLockAtDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff551908)  
[**KeAcquireInterruptSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551914)  
[**KeCancelTimer**](https://msdn.microsoft.com/library/windows/hardware/ff551970)  
[**KeInitializeCallbackRecord**](https://msdn.microsoft.com/library/windows/hardware/ff552109)  
[**KeInitializeGuardedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff552144)  
[**KeInitializeTimer**](https://msdn.microsoft.com/library/windows/hardware/ff552168)  
[**KeInitializeTimerEx**](https://msdn.microsoft.com/library/windows/hardware/ff552173)  
[**KeReadStateTimer**](https://msdn.microsoft.com/library/windows/hardware/ff553099)  
[**KeRestoreExtendedProcessorState**](https://msdn.microsoft.com/library/windows/hardware/ff553182)  
[**KeSaveExtendedProcessorState**](https://msdn.microsoft.com/library/windows/hardware/ff553238)  
[**KeSetTimer**](https://msdn.microsoft.com/library/windows/hardware/ff553286)  
[**KeSetTimerEx**](https://msdn.microsoft.com/library/windows/hardware/ff553292)  
[**KeDeregisterBugCheckCallback**](https://msdn.microsoft.com/library/windows/hardware/ff551992)  
[**KeDeregisterBugCheckReasonCallback**](https://msdn.microsoft.com/library/windows/hardware/ff552003)  
[**KeInsertQueueDpc**](https://msdn.microsoft.com/library/windows/hardware/ff552185)  
[**KeRegisterBugCheckCallback**](https://msdn.microsoft.com/library/windows/hardware/ff553105)  
[**KeRegisterBugCheckReasonCallback**](https://msdn.microsoft.com/library/windows/hardware/ff553110)  
[**KeReleaseGuardedMutexUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff553125)  
[**KeReleaseInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553130)  
[**KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553137)  
[**KeReleaseInterruptSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553139)  
[**KeRestoreFloatingPointState**](https://msdn.microsoft.com/library/windows/hardware/ff553185)  
[**KeSaveFloatingPointState**](https://msdn.microsoft.com/library/windows/hardware/ff553243)  
[**KeSynchronizeExecution**](https://msdn.microsoft.com/library/windows/hardware/ff553302)  
[*LookasideListAllocateEx*](https://msdn.microsoft.com/library/windows/hardware/ff554322)  
[*LookasideListFreeEx*](https://msdn.microsoft.com/library/windows/hardware/ff554324)  
[**ObReferenceObjectByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff558679)  
[**PsGetCurrentProcess**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer#psgetcurrentprocess)  
[**PsGetProcessCreateTimeQuadPart**](https://msdn.microsoft.com/library/windows/hardware/ff559939)  
[**PsInitialSystemProcess**](https://msdn.microsoft.com/library/windows/hardware/ff559943)  
[**PsIsSystemThread**](https://msdn.microsoft.com/library/windows/hardware/ff559945)  
[**RtlRunOnceBeginInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff562759)  
[**RtlRunOnceComplete**](https://msdn.microsoft.com/library/windows/hardware/ff562763)  
[**RtlRunOnceExecuteOnce**](https://msdn.microsoft.com/library/windows/hardware/ff562765)  
[**RtlRunOnceInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff562767)  
[*RunOnceInitialization*](https://msdn.microsoft.com/library/windows/hardware/ff563635)  
[ランダウン防止](run-down-protection.md)  
[**SeAccessCheck**](https://msdn.microsoft.com/library/windows/hardware/ff563674)  
[**SeAssignSecurity**](https://msdn.microsoft.com/library/windows/hardware/ff563676)  
[**SeAssignSecurityEx**](https://msdn.microsoft.com/library/windows/hardware/ff563679)  



