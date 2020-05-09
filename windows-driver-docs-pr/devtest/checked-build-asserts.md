---
title: チェック ビルドの ASSERT
description: チェック ビルドの ASSERT
ms.assetid: f002950d-6af9-42bb-9a1f-186873b09919
keywords:
- チェックされたビルド WDK、アサート
- WDK チェックビルドをアサートします
- WDK チェックされたビルドのエラー
ms.date: 05/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: b60262b4fce41ce1af187d9338284a946722e9a9
ms.sourcegitcommit: 076f9cd83313f6d8ab5688340f05bde7e8fbb8ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82999075"
---
# <a name="checked-build-asserts"></a>チェック ビルドの ASSERT


## <span id="ddk_checked_build_asserts_tools"></span><span id="DDK_CHECKED_BUILD_ASSERTS_TOOLS"></span>


このトピックでは、ドライバーライターによって発生する一般的な[**アサート**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))の一覧を示します。

これらのアサートの処理方法に関するヒント (および一覧にない他のもの) については、「チェックされ[たビルドが問題を示し](how-the-checked-build-indicates-a-problem.md)ている方法」を参照してください。

"ルーチンと呼ばれる" 列に示されているルーチンは、ドライバーの作成者やシステムコンポーネントがこのエラーを内容ために呼び出す最も一般的なルーチンです。 次に示すルーチンには、ドライバーが呼び出すルーチンが記載されています。 他の関数は、システムコンポーネントのみが呼び出すことができる内部ルーチンです。 ドライバーから他の関数を呼び出すと、呼び出された関数が、一覧に示されている関数のいずれかを内部的に呼び出すことがあることに注意してください。これにより、**アサート**を発行する可能性があります。

> [!NOTE]
> チェックを行ったビルドは、Windows 10 バージョン1803より前の古いバージョンの Windows で使用できました。
> Driver Verifier や GFlags などのツールを使用して、新しいバージョンの Windows でドライバーコードを確認します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルーチンが呼び出されました</th>
<th align="left">アサートテキスト</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl" data-raw-source="[&lt;strong&gt;IoAllocateMdl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)"><strong>IoAllocateMdl</strong></a></p></td>
<td align="left"><p>ASSERT (長さ)</p></td>
<td align="left"><p>説明されているユーザーバッファーの長さが0です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack" data-raw-source="[&lt;strong&gt;IoAttachDeviceToDeviceStack&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)"><strong>IoAttachDeviceToDeviceStack</strong></a></p></td>
<td align="left"><p>ASSERT (sourceExtension-&gt;Attachedto = <strong>NULL</strong> )</p></td>
<td align="left"><p>アタッチされているデバイスオブジェクト (ソースデバイス) は、既に別のデバイスオブジェクトにアタッチされています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a></p></td>
<td align="left"><p>ASSERT (Irp&gt;型 = = IO_TYPE_IRP)</p></td>
<td align="left"><p>PIRP 引数が IRP を指していません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp" data-raw-source="[&lt;strong&gt;IoCancelIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)"><strong>IoCancelIrp</strong></a></p></td>
<td align="left"><p>ASSERT (Irp&gt;型 = = IO_TYPE_IRP)</p></td>
<td align="left"><p>PIRP 引数が IRP を指していません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a></p></td>
<td align="left"><p>ASSERT (Irp&gt;型 = = IO_TYPE_IRP)</p></td>
<td align="left"><p>PIRP 引数が IRP を指していません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IoCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT (!Irp-&gt;cancelroutine)</p></td>
<td align="left"><p>IRP にキャンセルルーチンが存在します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT (Irp-&gt;iostatus. status! = STATUS_PENDING)</p></td>
<td align="left"><p>STATUS_PENDING で IRP を完了しようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IoCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT (Irp-&gt;iostatus. status! = 0xffffffff)</p></td>
<td align="left"><p>無効なステータスコードを使用して IRP を完了しようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT (Irp&gt;AuxiliaryBuffer! = <strong>NULL</strong> )</p></td>
<td align="left"><p>IRP が STATUS_REPARSE、IO_REPARSE_TAG_MOUNT_POINT を使用して完了しており、補助バッファーが<strong>NULL</strong>です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice" data-raw-source="[&lt;strong&gt;IoCreateDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)"><strong>IoCreateDevice</strong></a></p></td>
<td align="left"><p>ASSERT ((DriverObject-&gt;Flags & DRVO_UNLOAD_INVOKED) = = 0)</p></td>
<td align="left"><p>デバイスオブジェクトが作成されましたが、それを作成するドライバーは、アンロード用にマークされています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)"><strong>IoFreeIrp</strong></a></p></td>
<td align="left"><p>ASSERT (Irp&gt;型 = = IO_TYPE_IRP)</p></td>
<td align="left"><p>PIRP が IRP を指していません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IoFreeIrp</strong></p></td>
<td align="left"><p>ASSERT (IsListEmpty (& (Irp)-&gt;ThreadListEntry))</p></td>
<td align="left"><p>解放される IRP はまだスレッドの IRP リストにあるため、引き続き使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoFreeIrp</strong></p></td>
<td align="left"><p>ASSERT (Irp-&gt;currentlocation &gt;= irp-&gt;stackcount)</p></td>
<td align="left"><p>IRP は解放されていますが、この IRP を処理したすべてのドライバーの i/o 完了がまだ完了していません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp" data-raw-source="[&lt;strong&gt;IoReuseIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp)"><strong>IoReuseIrp</strong></a></p></td>
<td align="left"><p>ASSERT (Irp-&gt;cancelroutine = = <strong>NULL</strong>)</p></td>
<td align="left"><p>再利用するように要求されたキャンセルルーチンが IRP に残っています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoReuseIrp</strong></p></td>
<td align="left"><p>ASSERT (IsListEmpty (&&gt;ThreadListEntry))</p></td>
<td align="left"><p>再利用される IRP は、まだスレッドの IRP リストにあるため、引き続き使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iosetharderrororverifydevice" data-raw-source="[&lt;strong&gt;IoSetHardErrorOrVerifyDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iosetharderrororverifydevice)"><strong>IoSetHardErrorOrVerifyDevice</strong></a></p></td>
<td align="left"><p>ASSERT (Irp&gt;. オーバーレイ. Thread! = <strong>NULL</strong> )</p></td>
<td align="left"><p>IRP は、どのスレッドの IRP リストにもありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Ioの追加</strong></p></td>
<td align="left"><p>ASSERT (driverObject-&gt;MajorFunction [i]! = <strong>NULL</strong>)</p></td>
<td align="left"><p>ドライバーは、その<strong>driverentry</strong>ルーチンでディスパッチエントリポイントを<strong>NULL</strong>に設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IopCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT (irp-&gt;iostatus. status! = 0xffffffff)</p></td>
<td align="left"><p>IRP は、明らかに無効な状態で完了しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IopCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT (reparseBuffer-&gt;ReparseTag = = IO_REPARSE_TAG_MOUNT_POINT)</p></td>
<td align="left"><p>IRP は、Status = = STATUS_REPARSE および Information = = IO_REPARSE_TAG_MOUNT_POINT で完了しましたが、ReparseTag は MOUNT_POINT ではありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IopCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT (reparseBuffer-&gt;ReparseDataLength &lt; MAXIMUM_REPARSE_DATA_BUFFER_SIZE)</p></td>
<td align="left"><p>IRP は Status = = STATUS_REPARSE および Information = = IO_REPARSE_TAG_MOUNT_POINT で完了しましたが、返されたタグの長さが無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IopCompleteRequest</strong></p></td>
<td align="left"><p>ASSERT (reparseBuffer&gt; &lt; MAXIMUM_REPARSE_DATA_BUFFER_SIZE)</p></td>
<td align="left"><p>IRP は Status = = STATUS_REPARSE および Information = = IO_REPARSE_TAG_MOUNT_POINT で完了しましたが、返されたタグの長さが無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IopSynchronousServiceTail</strong></p></td>
<td align="left"><p>ASSERT (!Irp-&gt;pendingreturned 返しました)</p></td>
<td align="left"><p>IRP は pending に設定されましたが、同期されたディスパッチルーチンが status! = STATUS_PENDING で返されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages" data-raw-source="[&lt;strong&gt;MmProbeAndLockPages&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)"><strong>MmProbeAndLockPages</strong></a></p></td>
<td align="left"><p>ASSERT (MemoryByteCount&gt;! = 0)</p></td>
<td align="left"><p>渡された MDL のバイト数が0です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmProbeAndLockPages</strong></p></td>
<td align="left"><p>ASSERT (((ULONG) Memory記述子 List-&gt;byteoffset & ~ (PAGE_SIZE-1)) = = 0)</p></td>
<td align="left"><p>MDL の最初のページへのオフセットは&gt;= PAGE_SIZE;MDL の形式が正しくありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmProbeAndLockPages</strong></p></td>
<td align="left"><p>ASSERT (((ULONG_PTR) Memory記述子 List-&gt;startva & (PAGE_SIZE-1)) = = 0)</p></td>
<td align="left"><p>MDL の開始 VA がページに揃っていません。MDL の形式が正しくありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmProbeAndLockPages</strong></p></td>
<td align="left"><p>ASSERT ((Memory記述子 List-&gt;mdlflags & (MDL_PAGES_LOCKED |MDL_MAPPED_TO_SYSTEM_VA |MDL_SOURCE_IS_NONPAGED_POOL |MDL_PARTIAL |MDL_IO_SPACE)) = = 0)</p></td>
<td align="left"><p>この関数呼び出しでは、MDL が適切な状態ではありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmProbeAndLockPages</strong></p></td>
<td align="left"><p>ASSERT (NumberOfPagesToLock! = 0)</p></td>
<td align="left"><p>MDL は、ロックするページがゼロのページの範囲を記述します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmProbeAndLockPages</strong></p></td>
<td align="left"><p>ASSERT (<strong>FALSE</strong>)</p></td>
<td align="left"><p>MDL によって記述されたバッファー内のページが、異常に頻繁にメモリにロックされています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages" data-raw-source="[&lt;strong&gt;MmUnlockPages&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages)"><strong>MmUnlockPages</strong></a></p></td>
<td align="left"><p>ASSERT ((Memory記述子 List-&gt;mdlflags & MDL_PAGES_LOCKED)! = 0)</p></td>
<td align="left"><p>この MDL によって記述されたバッファーを構成するページはロックされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>ASSERT ((Memory記述子 List-&gt;mdlflags & MDL_SOURCE_IS_NONPAGED_POOL) = = 0)</p></td>
<td align="left"><p>MDL は、非ページプールからのバッファーを記述します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>ASSERT ((Memory記述子 List-&gt;mdlflags & MDL_PARTIAL) = = 0)</p></td>
<td align="left"><p>MDL は、 <strong>Iobuildpartialmdl</strong>を呼び出すことによって構築されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>ASSERT (MemoryByteCount&gt;! = 0)</p></td>
<td align="left"><p>MDL では、長さが0バイトのバッファーが記述されています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>ASSERT (NumberOfPages! = 0)</p></td>
<td align="left"><p>MDL にページが含まれていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>ASSERT ((SPFN_NUMBER)&gt;NumberOfLockedPages &gt;= 0)</p></td>
<td align="left"><p>MDL に関連付けられているプロセスにページがロックされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmUnlockPages</strong></p></td>
<td align="left"><p>ASSERT (<em>Page &lt;= MmHighestPhysicalPage)</p></td>
<td align="left"><p>MDL のページフレームポインターが無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool" data-raw-source="[&lt;strong&gt;MmBuildMdlForNonPagedPool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool)"><strong>MmBuildMdlForNonPagedPool</strong></a></p></td>
<td align="left"><p>ASSERT (MemoryByteCount&gt;! = 0)</p></td>
<td align="left"><p>MDL によって記述されるバッファーの長さは0バイトです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmBuildMdlForNonPagedPool</strong></p></td>
<td align="left"><p>ASSERT ((Memory記述子 List-&gt;mdlflags & (MDL_PAGES_LOCKED |MDL_MAPPED_TO_SYSTEM_VA |MDL_SOURCE_IS_NONPAGED_POOL |MDL_PARTIAL)) = = 0)</p></td>
<td align="left"><p>MDL はこの関数呼び出しに対して適切な状態ではありません</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmBuildMdlForNonPagedPool</strong></p></td>
<td align="left"><p>ASSERT (NumberOfPages! = 0)</p></td>
<td align="left"><p>MDL は、ページがゼロのバッファーを記述します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache" data-raw-source="[&lt;strong&gt;MmMapLockedPagesSpecifyCache&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache)"><strong>MmMapLockedPagesSpecifyCache</strong></a></p></td>
<td align="left"><p>ASSERT (MemoryByteCount&gt;! = 0)</p></td>
<td align="left"><p>MDL の長さが0です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmMapLockedPagesSpecifyCache</strong></p></td>
<td align="left"><p>ASSERT ((Memory記述子 List-&gt;mdlflags & MDL_MAPPED_TO_SYSTEM_VA) = = 0)</p></td>
<td align="left"><p>この MDL によって記述されたバッファーは、既にカーネル仮想アドレス空間にマップされています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmMapLockedPagesSpecifyCache</strong></p></td>
<td align="left"><p>ASSERT ((Memory記述子 List-&gt;mdlflags & (MDL_MAPPED_TO_SYSTEM_VA |MDL_SOURCE_IS_NONPAGED_POOL |MDL_PARTIAL_HAS_BEEN_MAPPED)) = = 0)</p></td>
<td align="left"><p>MDL は、この関数呼び出しに対して適切な状態ではありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmMapLockedPagesSpecifyCache</strong></p></td>
<td align="left"><p>ASSERT ((Memory記述子 List-&gt;mdlflags & (MDL_PAGES_LOCKED |MDL_PARTIAL))! = 0)</p></td>
<td align="left"><p>MDL は、この操作に対して適切な状態ではありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmMapLockedPagesSpecifyCache</strong></p></td>
<td align="left"><p>ASSERT (Pte-&gt;u. Hard. Valid = = 0)</p></td>
<td align="left"><p>MDL によって記述されたバッファーに、メモリに存在しないページが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmMapLockedPagesSpecifyCache</strong></p></td>
<td align="left"><p>ASSERT (Pfn2-&gt;u3! = 0)</p></td>
<td align="left"><p>MDL によって記述されたバッファーに、メモリ内でロックされていないページが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmaplockedpages" data-raw-source="[&lt;strong&gt;MmUnmapLockedPages&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmaplockedpages)"><strong>MmUnmapLockedPages</strong></a></p></td>
<td align="left"><p>ASSERT (MemoryByteCount&gt;! = 0)</p></td>
<td align="left"><p>MDL では、長さが0バイトのバッファーが記述されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmUnmapLockedPages</strong></p></td>
<td align="left"><p>ASSERT (Memory記述子 List-&gt;mdlflags & MDL_MAPPED_TO_SYSTEM_VA)</p></td>
<td align="left"><p>カーネル仮想アドレス空間内のアドレスを指定したベースアドレスを指定するために、この関数に渡されるパラメーター。ただし、これは、MDL 内のバッファーの説明には一致しません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmUnmapLockedPages</strong></p></td>
<td align="left"><p>ASSERT (Pte-&gt;u. Hard. Valid = = 1)</p></td>
<td align="left"><p>MDL によって記述されたバッファー内のページがメモリに存在しません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmUnmapLockedPages</strong></p></td>
<td align="left"><p>ASSERT (</em>Page = = MI_GET_PAGE_FRAME_FROM_PTE (ポインタ PTE))</p></td>
<td align="left"><p>MDL のページフレームポインターが無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmUnmapLockedPages</strong></p></td>
<td align="left"><p>ASSERT (Pfn3-&gt;u3! = 0)</p></td>
<td align="left"><p>MDL によって記述されたバッファーに、メモリ内でロックされていないページが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace" data-raw-source="[&lt;strong&gt;MmMapIoSpace&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace)"><strong>MmMapIoSpace</strong></a></p></td>
<td align="left"><p>ASSERT (PhysicalAddress = = 0)</p></td>
<td align="left"><p>これは、4 GB を超える物理メモリを持つ x86 ベースのシステムで実行されていますが、この関数に渡されたパラメーターを使用して、i/o スペースアドレスの上位32ビットが0以外であることを指定しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmMapIoSpace</strong></p></td>
<td align="left"><p>ASSERT (NumberOfBytes! = 0)</p></td>
<td align="left"><p>マップするバイト数を指定するためにこの関数に渡されるパラメーターが0です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmMapIoSpace</strong></p></td>
<td align="left"><p>ASSERT (Pte-&gt;u. Hard. Valid = = 0)</p></td>
<td align="left"><p>アドレス rage のページが i/o 領域にありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace" data-raw-source="[&lt;strong&gt;MmUnmapIoSpace&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace)"><strong>MmUnmapIoSpace</strong></a></p></td>
<td align="left"><p>ASSERT (NumberOfBytes! = 0)</p></td>
<td align="left"><p>マップ解除するバイト数を指定するためにこの関数に渡されたパラメーターが0です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemory" data-raw-source="[&lt;strong&gt;MmAllocateContiguousMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemory)"><strong>MmAllocateContiguousMemory</strong></a></p></td>
<td align="left"><p>ASSERT (NumberOfBytes! = 0)</p></td>
<td align="left"><p>割り当てるバイト数を指定するためにこの関数に渡されたパラメーターが0です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Memoryのキャッシュ</strong></p></td>
<td align="left"><p>ASSERT (NumberOfBytes! = 0)</p></td>
<td align="left"><p>割り当てるバイト数を指定するためにこの関数に渡されたパラメーターが0です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmallocatenoncachedmemory" data-raw-source="[&lt;strong&gt;MmAllocateNonCachedMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmallocatenoncachedmemory)"><strong>MmAllocateNonCachedMemory</strong></a></p></td>
<td align="left"><p>ASSERT (NumberOfBytes! = 0)</p></td>
<td align="left"><p>割り当てるバイト数を指定するためにこの関数に渡されたパラメーターが0です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MmFreeNonCachedMemory</strong></p></td>
<td align="left"><p>ASSERT (NumberOfBytes! = 0)</p></td>
<td align="left"><p>解放するバイト数を指定するためにこの関数に渡されたパラメーターが0です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MmFreeNonCachedMemory</strong></p></td>
<td align="left"><p>ASSERT (PAGE_ALIGN (BaseAddress) = = BaseAddress)</p></td>
<td align="left"><p>ベースアドレスを指定するためにこの関数に渡されたパラメーターが無効です。</p></td>
</tr>
</tbody>
</table>

 

 

 





