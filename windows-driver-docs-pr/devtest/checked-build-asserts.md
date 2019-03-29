---
title: チェック ビルドの ASSERT
description: チェック ビルドの ASSERT
ms.assetid: f002950d-6af9-42bb-9a1f-186873b09919
keywords:
- チェック ビルド WDK、アサート
- WDK のチェック ビルドをアサートします。
- WDK のエラー チェック ビルド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6834664e7ac21b81a19ccad8b7f6d3ded02b331
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348943"
---
# <a name="checked-build-asserts"></a>チェック ビルドの ASSERT


## <span id="ddk_checked_build_asserts_tools"></span><span id="DDK_CHECKED_BUILD_ASSERTS_TOOLS"></span>


このトピックでは、共通の一覧を含む[ **ASSERT**](https://msdn.microsoft.com/library/windows/hardware/ff542107)のドライバー作成者によって発生します。

ハンドル前述のアサート (とそれに記載されていない) する方法に関するヒントを参照してください[チェック ビルドで問題を示す方法](how-the-checked-build-indicates-a-problem.md)します。

「ルーチンを呼び出す」列に表示されるルーチンは、このエラーを出さずにドライバー開発者およびシステム コンポーネントの呼び出しは最も一般的なルーチンです。 以下に示すルーチンの一部は、文書化されているルーチンのドライバーを呼び出すことです。 他のユーザーは、システム コンポーネントのみを呼び出すことができる内部のルーチンです。 内部的に呼び出された関数で発生可能性があります、ドライバーから他の関数を呼び出すことに注意して呼び出すように有効にする問題の可能性がありますの上記の関数の 1 つ、 **ASSERT**します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルーチンが呼び出されます</th>
<th align="left">ASSERT のテキスト</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548263" data-raw-source="[&lt;strong&gt;IoAllocateMdl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548263)"><strong>IoAllocateMdl</strong></a></p></td>
<td align="left"><p>ASSERT(Length)</p></td>
<td align="left"><p>記述されているユーザー バッファーの長さは 0 です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548300" data-raw-source="[&lt;strong&gt;IoAttachDeviceToDeviceStack&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548300)"><strong>IoAttachDeviceToDeviceStack</strong></a></p></td>
<td align="left"><p>ASSERT( sourceExtension-&gt;AttachedTo == <strong>NULL</strong> )</p></td>
<td align="left"><p>デバイスが (ソース デバイス) にアタッチされるオブジェクトは別のデバイス オブジェクトに既にアタッチされています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a></p></td>
<td align="left"><p>ASSERT( Irp-&gt;Type == IO_TYPE_IRP )</p></td>
<td align="left"><p>PIRP 引数が IRP を指していません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548338" data-raw-source="[&lt;strong&gt;IoCancelIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548338)"><strong>IoCancelIrp</strong></a></p></td>
<td align="left"><p>ASSERT( Irp-&gt;Type == IO_TYPE_IRP )</p></td>
<td align="left"><p>PIRP 引数が IRP を指していません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548343" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548343)"><strong>IoCompleteRequest</strong></a></p></td>
<td align="left"><p>ASSERT( Irp-&gt;Type == IO_TYPE_IRP )</p></td>
<td align="left"><p>PIRP 引数が IRP を指していません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IoCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT( !Irp-&gt;CancelRoutine )</p></td>
<td align="left"><p>IRP に存在するキャンセル ルーチンがあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT( Irp-&gt;IoStatus.Status != STATUS_PENDING )</p></td>
<td align="left"><p>STATUS_PENDING を IRP の完了を試みます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IoCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT( Irp-&gt;IoStatus.Status != 0xffffffff )</p></td>
<td align="left"><p>無効な状態コードでは IRP を完了しようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT( Irp-&gt;Tail.Overlay.AuxiliaryBuffer != <strong>NULL</strong> )</p></td>
<td align="left"><p>Status_reparse を不確実、IO_REPARSE_TAG_MOUNT_POINT、IRP が入力されていると補助バッファーが<strong>NULL</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548397" data-raw-source="[&lt;strong&gt;IoCreateDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548397)"><strong>IoCreateDevice</strong></a></p></td>
<td align="left"><p>アサート ((DriverObject-&gt;フラグ&amp;DRVO_UNLOAD_INVOKED) 0 を = =)</p></td>
<td align="left"><p>デバイス オブジェクトが作成されたらは、作成すると、ドライバーは、アンロード設定されています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549113" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549113)"><strong>IoFreeIrp</strong></a></p></td>
<td align="left"><p>ASSERT( Irp-&gt;Type == IO_TYPE_IRP )</p></td>
<td align="left"><p>PIRP は IRP を指していません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IoFreeIrp</strong></p></td>
<td align="left"><p>ASSERT(IsListEmpty(&amp;(Irp)-&gt;ThreadListEntry))</p></td>
<td align="left"><p>IRP が解放されるスレッドの IRP に表示されるボックスの一覧し、使用中でもそのためです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoFreeIrp</strong></p></td>
<td align="left"><p>ASSERT( Irp-&gt;CurrentLocation &gt;= Irp-&gt;StackCount )</p></td>
<td align="left"><p>IRP が解放されているが、この IRP を処理するすべてのドライバーのまだ終了していません I/O 完了します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549661" data-raw-source="[&lt;strong&gt;IoReuseIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549661)"><strong>IoReuseIrp</strong></a></p></td>
<td align="left"><p>ASSERT(Irp-&gt;CancelRoutine == <strong>NULL</strong>)</p></td>
<td align="left"><p>再利用するように要求された IRP に残っているキャンセル ルーチンがあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoReuseIrp</strong></p></td>
<td align="left"><p>アサート (IsListEmpty (&amp;Irp-&gt;ThreadListEntry))</p></td>
<td align="left"><p>IRP が再利用されるスレッドの IRP に表示されるボックスの一覧し、使用中でもそのためです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549707" data-raw-source="[&lt;strong&gt;IoSetHardErrorOrVerifyDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549707)"><strong>IoSetHardErrorOrVerifyDevice</strong></a></p></td>
<td align="left"><p>ASSERT( Irp-&gt;Tail.Overlay.Thread != <strong>NULL</strong> )</p></td>
<td align="left"><p>すべてのスレッドの IRP の一覧で、IRP が。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IopLoadDriver</strong></p></td>
<td align="left"><p>ASSERT(driverObject-&gt;MajorFunction[i] != <strong>NULL</strong>)</p></td>
<td align="left"><p>ドライバーにディスパッチ エントリ ポイントを設定する<strong>NULL</strong>でその<strong>DriverEntry</strong>ルーチン。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IopCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT( irp-&gt;IoStatus.Status != 0xffffffff)</p></td>
<td align="left"><p>IRP が明らかに無効な状態で完了しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IopCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT(reparseBuffer-&gt;ReparseTag == IO_REPARSE_TAG_MOUNT_POINT)</p></td>
<td align="left"><p>IRP が状態で完了しました status_reparse を不確実と情報を = = IO_REPARSE_TAG_MOUNT_POINT、= = が、ReparseTag を MOUNT_POINT のではありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IopCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT (reparseBuffer -&gt;ReparseDataLength &lt; MAXIMUM_REPARSE_DATA_BUFFER_SIZE)</p></td>
<td align="left"><p>IRP が状態で完了しました = = status_reparse を不確実 and 情報が返される、IO_REPARSE_TAG_MOUNT_POINT、= = タグが長さが無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IopCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT (reparseBuffer -&gt;占有&lt;MAXIMUM_REPARSE_DATA_BUFFER_SIZE)</p></td>
<td align="left"><p>IRP が状態で完了しました = = status_reparse を不確実 and 情報が返される、IO_REPARSE_TAG_MOUNT_POINT、= = タグが長さが無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IopSynchronousServiceTail</strong></p></td>
<td align="left"><p>ASSERT( !Irp-&gt;PendingReturned )</p></td>
<td align="left"><p>IRP が保留中でマークされましたが、ステータスのディスパッチ ルーチンが同期的に返される! STATUS_PENDING を = です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554664" data-raw-source="[&lt;strong&gt;MmProbeAndLockPages&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554664)"><strong>MmProbeAndLockPages</strong></a></p></td>
<td align="left"><p>ASSERT (MemoryDescriptorList-&gt;ByteCount != 0)</p></td>
<td align="left"><p>渡された MDL のバイト数には 0 です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmProbeAndLockPages</strong></p></td>
<td align="left"><p>アサート (((ULONG) MemoryDescriptorList -&gt;ByteOffset &amp; ~(PAGE_SIZE-1)) 0 を = =)</p></td>
<td align="left"><p>MDL の最初のページへのオフセットは&gt;= PAGE_SIZE; MDL の形式が正しくありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmProbeAndLockPages</strong></p></td>
<td align="left"><p>ASSERT (((ULONG_PTR)MemoryDescriptorList-&gt;StartVa &amp; (PAGE_SIZE - 1)) == 0)</p></td>
<td align="left"><p>MDL で開始 VA は、調整されています。 ページではないです。MDL の形式が正しくありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmProbeAndLockPages</strong></p></td>
<td align="left"><p>ASSERT ((MemoryDescriptorList-&gt;MdlFlags &amp; ( MDL_PAGES_LOCKED | MDL_MAPPED_TO_SYSTEM_VA | MDL_SOURCE_IS_NONPAGED_POOL | MDL_PARTIAL | MDL_IO_SPACE)) == 0)</p></td>
<td align="left"><p>MDL は、この関数の呼び出しに対して適切な状態ではありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmProbeAndLockPages</strong></p></td>
<td align="left"><p>ASSERT (NumberOfPagesToLock != 0)</p></td>
<td align="left"><p>MDL では、さまざまなページをロックするには、ゼロ ページについて説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmProbeAndLockPages</strong></p></td>
<td align="left"><p>アサート (<strong>FALSE</strong>)</p></td>
<td align="left"><p>MDL で説明されているバッファー内のページが表示された時間数が異常に高いメモリにロックされています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556381" data-raw-source="[&lt;strong&gt;MmUnlockPages&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556381)"><strong>MmUnlockPages</strong></a></p></td>
<td align="left"><p>アサート ((MemoryDescriptorList-&gt;MdlFlags &amp; MDL_PAGES_LOCKED)! = 0)</p></td>
<td align="left"><p>この MDL で説明されているバッファーを構成するページがロックされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>アサート ((MemoryDescriptorList-&gt;MdlFlags &amp; MDL_SOURCE_IS_NONPAGED_POOL) 0 を = =)</p></td>
<td align="left"><p>MDL は、非ページ プールからバッファーを記述します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>アサート ((MemoryDescriptorList-&gt;MdlFlags &amp; MDL_PARTIAL) 0 を = =)</p></td>
<td align="left"><p>呼び出すことによって構築された MDL <strong>IoBuildPartialMdl</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>ASSERT (MemoryDescriptorList-&gt;ByteCount != 0)</p></td>
<td align="left"><p>MDL では、ゼロ バイト長であるバッファーについて説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>アサート (NumberOfPages! = 0)</p></td>
<td align="left"><p>MDL では、すべてのページは含まれません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>アサート ((SPFN_NUMBER) プロセス -&gt;NumberOfLockedPages &gt;= 0)</p></td>
<td align="left"><p>MDL に関連付けられたプロセスには、ロックされている任意のページはありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>アサート (<em>ページ&lt;MmHighestPhysicalPage =)</p></td>
<td align="left"><p>MDL のページ フレーム ポインターが無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554498" data-raw-source="[&lt;strong&gt;MmBuildMdlForNonPagedPool&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554498)"><strong>MmBuildMdlForNonPagedPool</strong></a></p></td>
<td align="left"><p>ASSERT (MemoryDescriptorList-&gt;ByteCount != 0)</p></td>
<td align="left"><p>MDL で説明されているバッファーは、長さ 0 バイトです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmBuildMdlForNonPagedPool</strong></p></td>
<td align="left"><p>ASSERT ((MemoryDescriptorList-&gt;MdlFlags &amp; (MDL_PAGES_LOCKED | MDL_MAPPED_TO_SYSTEM_VA | MDL_SOURCE_IS_NONPAGED_POOL | MDL_PARTIAL)) == 0)</p></td>
<td align="left"><p>この関数の呼び出しに対して適切な状態でない MDL</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmBuildMdlForNonPagedPool</strong></p></td>
<td align="left"><p>アサート (NumberOfPages! = 0)</p></td>
<td align="left"><p>MDL には、ゼロ ページを使用して、バッファーがについて説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554629" data-raw-source="[&lt;strong&gt;MmMapLockedPagesSpecifyCache&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554629)"><strong>MmMapLockedPagesSpecifyCache</strong></a></p></td>
<td align="left"><p>ASSERT (MemoryDescriptorList-&gt;ByteCount != 0)</p></td>
<td align="left"><p>MDL が長さが 0 です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmMapLockedPagesSpecifyCache</strong></p></td>
<td align="left"><p>アサート ((MemoryDescriptorList-&gt;MdlFlags &amp; MDL_MAPPED_TO_SYSTEM_VA) 0 を = =)</p></td>
<td align="left"><p>この MDL によって記述されたバッファーは、既にカーネル仮想アドレス空間にマップされています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmMapLockedPagesSpecifyCache</strong></p></td>
<td align="left"><p>ASSERT ((MemoryDescriptorList-&gt;MdlFlags &amp; ( MDL_MAPPED_TO_SYSTEM_VA | MDL_SOURCE_IS_NONPAGED_POOL | MDL_PARTIAL_HAS_BEEN_MAPPED)) == 0)</p></td>
<td align="left"><p>MDL は、この関数の呼び出しに対して適切な状態ではありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmMapLockedPagesSpecifyCache</strong></p></td>
<td align="left"><p>ASSERT ((MemoryDescriptorList-&gt;MdlFlags &amp; ( MDL_PAGES_LOCKED | MDL_PARTIAL)) != 0)</p></td>
<td align="left"><p>MDL は、この操作に対して適切な状態ではありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmMapLockedPagesSpecifyCache</strong></p></td>
<td align="left"><p>ASSERT (PointerPte-&gt;u.Hard.Valid == 0)</p></td>
<td align="left"><p>MDL で説明されているバッファーには、メモリに常駐することはないページが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmMapLockedPagesSpecifyCache</strong></p></td>
<td align="left"><p>ASSERT (Pfn2-&gt;u3.e2.ReferenceCount != 0)</p></td>
<td align="left"><p>MDL で説明されているバッファーには、メモリにロックされていないページが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556391" data-raw-source="[&lt;strong&gt;MmUnmapLockedPages&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556391)"><strong>MmUnmapLockedPages</strong></a></p></td>
<td align="left"><p>ASSERT (MemoryDescriptorList-&gt;ByteCount != 0)</p></td>
<td align="left"><p>MDL では、ゼロ バイト長であるバッファーについて説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmUnmapLockedPages</strong></p></td>
<td align="left"><p>アサート (MemoryDescriptorList -&gt;MdlFlags &amp; MDL_MAPPED_TO_SYSTEM_VA)</p></td>
<td align="left"><p>パラメーターはベース アドレスには、カーネルの仮想アドレス空間内のアドレスが指定されましたが、これで、MDL バッファー説明と一致していませんを指定するには、この関数に渡されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmUnmapLockedPages</strong></p></td>
<td align="left"><p>ASSERT (PointerPte-&gt;u.Hard.Valid == 1)</p></td>
<td align="left"><p>MDL で説明されているバッファー内のページがメモリに常駐ではありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmUnmapLockedPages</strong></p></td>
<td align="left"><p>アサート (</em>ページ MI_GET_PAGE_FRAME_FROM_PTE (PointerPte) = =)</p></td>
<td align="left"><p>MDL のページ フレーム ポインターが無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmUnmapLockedPages</strong></p></td>
<td align="left"><p>ASSERT (Pfn3-&gt;u3.e2.ReferenceCount != 0)</p></td>
<td align="left"><p>MDL で説明されているバッファーには、メモリにロックされていないページが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554618" data-raw-source="[&lt;strong&gt;MmMapIoSpace&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554618)"><strong>MmMapIoSpace</strong></a></p></td>
<td align="left"><p>ASSERT (PhysicalAddress.HighPart == 0)</p></td>
<td align="left"><p>物理メモリの 4 gb を超えるいない x86 ベース システムで実行しているが、I/O の領域のアドレスの上位 32 ビットを指定するには、この関数に渡されるパラメーターが 0 以外。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmMapIoSpace</strong></p></td>
<td align="left"><p>ASSERT (NumberOfBytes != 0)</p></td>
<td align="left"><p>マップ対象のバイト数を指定するには、この関数に渡されるパラメーターには 0 です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmMapIoSpace</strong></p></td>
<td align="left"><p>ASSERT (PointerPte-&gt;u.Hard.Valid == 0)</p></td>
<td align="left"><p>アドレスの範囲のページは、I/O 領域ではありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556387" data-raw-source="[&lt;strong&gt;MmUnmapIoSpace&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556387)"><strong>MmUnmapIoSpace</strong></a></p></td>
<td align="left"><p>ASSERT (NumberOfBytes != 0)</p></td>
<td align="left"><p>マップ解除するバイト数を指定するには、この関数に渡されるパラメーターには 0 です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554460" data-raw-source="[&lt;strong&gt;MmAllocateContiguousMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554460)"><strong>MmAllocateContiguousMemory</strong></a></p></td>
<td align="left"><p>ASSERT (NumberOfBytes != 0)</p></td>
<td align="left"><p>割り当てるバイト数を指定するには、この関数に渡されるパラメーターには 0 です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MemorySpecifyCache</strong></p></td>
<td align="left"><p>ASSERT (NumberOfBytes != 0)</p></td>
<td align="left"><p>割り当てるバイト数を指定するには、この関数に渡されるパラメーターには 0 です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554479" data-raw-source="[&lt;strong&gt;MmAllocateNonCachedMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554479)"><strong>MmAllocateNonCachedMemory</strong></a></p></td>
<td align="left"><p>ASSERT (NumberOfBytes != 0)</p></td>
<td align="left"><p>割り当てるバイト数を指定するには、この関数に渡されるパラメーターには 0 です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmFreeNonCachedMemory</strong></p></td>
<td align="left"><p>ASSERT (NumberOfBytes != 0)</p></td>
<td align="left"><p>空きバイト数を指定するには、この関数に渡されるパラメーターには 0 です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmFreeNonCachedMemory</strong></p></td>
<td align="left"><p>ASSERT (PAGE_ALIGN (BaseAddress) == BaseAddress)</p></td>
<td align="left"><p>パラメーターはベース アドレスが有効でないを指定するには、この関数に渡されます。</p></td>
</tr>
</tbody>
</table>

 

 

 





