---
title: Windows カーネルのマクロ
description: Windows カーネルのマクロ
ms.assetid: 91366400-3307-4F13-A839-50BA85B7F73E
ms.localizationpriority: High
ms.date: 10/17/2018
ms.openlocfilehash: 3b242a3fa79a07ae3c5a0332ef54ac287ebf79ac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827845"
---
# <a name="windows-kernel-macros"></a>Windows カーネルのマクロ


次の一覧は、Windows カーネルのマクロです。


## <a name="address_and_size_to_span_pages"></a>**ADDRESS_AND_SIZE_TO_SPAN_PAGES**

定義されている場所: Wdm.h

**ADDRESS_AND_SIZE_TO_SPAN_PAGES** は、仮想アドレスによって定義された仮想範囲にまたがるページ数と、転送要求のサイズ (バイト単位) を返すマクロです。

_Va [in]_

**PVOID**

範囲のベースである仮想アドレスへのポインター。

_Size [in]_

**ULONG**

転送要求のサイズをバイト単位で指定します。

**戻り値**

**ULONG**

**ADDRESS_AND_SIZE_TO_SPAN_PAGES** からは、_Va_ から始まる仮想範囲にまたがるページ数が返されます。

DMA 転送を行うドライバーにより **ADDRESS_AND_SIZE_TO_SPAN_PAGES** が呼び出され、転送要求を一連のデバイス DMA 操作に分割する必要があるかどうかが判断されます。

ドライバーでは、システム定義定数 PAGE_SIZE を使用して、転送されるバイト数が現在のプラットフォームの仮想メモリ ページ サイズよりも小さいかどうかを判断できます。

**ADDRESS_AND_SIZE_TO_SPAN_PAGES** の呼び出し元は、どの IRQL で実行されていてもかまいません。 呼び出し元は、指定したパラメーターによってメモリ オーバーフローが確実に発生しないようにする必要があります。

Windows 2000 以降で使用できます。


## <a name="byte_offset"></a>**BYTE_OFFSET**

定義されている場所: Wdm.h

**BYTE_OFFSET** は、仮想アドレスを受け取り、ページ内のそのアドレスのバイト オフセットを返すマクロです。

_Va [in]_

**PVOID**

仮想アドレスへのポインター。

**戻り値**

**ULONG**

**BYTE_OFFSET** からは、仮想アドレスのオフセット部分が返されます。

Windows 2000 以降で使用できます。

IRQL: 任意のレベル


## <a name="bytes_to_pages"></a>**BYTES_TO_PAGES**

定義されている場所: Wdm.h

**BYTES_TO_PAGES** は、転送要求のサイズ (バイト単位) を受け取り、そのバイト数を格納するために必要なページ数を計算するマクロです。

_Size [in]_

**ULONG**

転送要求のサイズをバイト単位で指定します。

**戻り値**

**ULONG**

**BYTES_TO_PAGES** からは、指定したバイト数を格納するために必要なページ数が返されます。

システム定義定数 PAGE_SIZE を使用すると、転送する対象として指定したバイト単位の長さが、現在のプラットフォームの仮想メモリ ページ サイズよりも小さいかどうかを判断できます。

Windows 2000 以降で使用できます。

IRQL: 任意のレベル


## <a name="containing_record"></a>**CONTAINING_RECORD**

定義されている場所: Ntdef. h

**CONTAINING_RECORD** マクロでは、構造体の型と、構造体に含まれるフィールドのアドレスを指定すると、構造体のインスタンスのベース アドレスが返されます。

_Address [in]_

**PCHAR**

型が _Type_ である構造体のインスタンス内のフィールドへのポインター。

_Type [in]_

**TYPE**

返されるベース アドレスを持つ構造体の型の名前。

_Field [in]_

**PCHAR**

型が _Type_ である構造体に含まれている、_Address_ によって示されたフィールドの名前。

**戻り値**

**PCHAR**

_Field_ を含む構造体のベース アドレスが返されます。

呼び出し元がこうした構造体のフィールドへのポインターを把握している場合に、型がわかっている構造体のベース アドレスを判別するために呼び出されます。 このマクロは、既知の型を持つ構造体の他のフィールドへのシンボリック アクセスに便利です。

Windows 2000 以降で使用できます。

IRQL: 任意のレベル


## <a name="ioskipcurrentirpstacklocation"></a>**IoSkipCurrentIrpStackLocation**

定義されている場所: Wdm.h

\n**IoSkipCurrentIrpStackLocation** は、システムの [**IO_STACK_LOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location) 配列ポインターを変更することにより、現在のドライバーにより次に下位のドライバーが呼び出されたときに、そのドライバーが、現在のドライバーが受け取ったのと同じ **IO_STACK_LOCATION** 構造体を受け取るようにするマクロです。

_Irp [in, out]_

**PIRP**

IRP へのポインター。

**戻り値**

**VOID**

ドライバーで次に下位のドライバーに IRP を送信するとき、[_IoCompletion_](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) ルーチン (そのアドレスがドライバーの [**IO_STACK_LOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location) 構造体に格納されている) を指定しない場合は、ドライバーで **IoSkipCurrentIrpStackLocation** を呼び出すことができます。 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) を呼び出す前に **IoSkipCurrentIrpStackLocation** を呼び出すと、次に下位のドライバーは、ドライバーが受け取ったのと同じ **IO_STACK_LOCATION** を受け取ります。

IRP に _IoCompletion_ ルーチンを指定する場合、ドライバーで **IoSkipCurrentIrpStackLocation** ではなく、[**IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) を呼び出す必要があります。 正しく記述されていないドライバーで、誤って **IoSkipCurrentIrpStackLocation** を呼び出してから完了ルーチンを設定すると、そのドライバーよりも下位のドライバーによって設定された完了ルーチンが上書きされることがあります。

ドライバーで IRP を保留した場合は、IRP を次に下位のドライバーに渡す前に **IoSkipCurrentIrpStackLocation** を呼び出さないでください。 保留した IRP に対してドライバーで **IoSkipCurrentIrpStackLocation** を呼び出してから、それを次に下位のドライバーに渡した場合、次のドライバーに対して I/O スタックの場所を表す **Control** メンバーに、SL_PENDING_RETURNED フラグが設定されたままになります。 そのスタックの場所は次のドライバーが所有しており、変更される可能性があるため、保留中のフラグがクリアされる可能性があります。 このような状況が発生すると、オペレーティング システムによってバグ チェックが発行されたり、IRP の処理が完了しなくなったりすることがあります。

代わりに、IRP を保留にしたドライバーで **IoCallDriver** を呼び出す前に **IoCopyCurrentIrpStackLocationToNext** を呼び出し、次に下位のドライバーに対して新しいスタックの場所を設定する必要があります。

ドライバーで **IoSkipCurrentIrpStackLocation** を呼び出す場合は、そのドライバーに関連して下位のドライバーやシステムの動作が意図せず影響を受けるような方法で **IO_STACK_LOCATION** 構造体を変更しないように注意してください。 例としては、**IO_STACK_LOCATION** 構造体の **Parameters** 共用体を変更することや、[**IoMarkIrpPending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) を呼び出すことがあります。

Windows 2000 以降で使用できます。

IRQL: 任意のレベル


## <a name="keinitializecallbackrecord"></a>**KeInitializeCallbackRecord**

定義されている場所: Wdm.h

**KeInitializeCallbackRecord** は、[**KBUGCHECK_CALLBACK_RECORD**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess) 構造体または [**KBUGCHECK_REASON_CALLBACK_RECORD**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess) 構造体を初期化するマクロです。

_CallbackRecord [in]_

**PKBUGCHECK_CALLBACK_RECORD**

**KBUGCHECK_CALLBACK_RECORD** 構造体または **KBUGCHECK_REASON_CALLBACK_RECORD** 構造体へのポインター。 その構造体は、非ページ プールなどの常駐メモリに存在する必要があります。

**戻り値**

**VOID**

Windows 2000 以降のバージョンの Windows で使用できます。

IRQL: 任意のレベル


## <a name="mm_bad_pointer"></a>**MM_BAD_POINTER**

定義されている場所: Wdm.h

ドライバーで **MM_BAD_POINTER** マクロを無効なポインター値として使用して、初期化されていない、または無効になったポインター変数に割り当てることができます。 この無効なポインター変数が指すメモリ位置にアクセスしようとすると、バグ チェックが発生します。

多くのハードウェア プラットフォームでは、アドレス 0 (多くの場合、名前付き定数 **NULL** として表される) は無効なアドレスですが、ドライバー開発者はアドレス 0 がすべてのプラットフォームで汎用的に無効であると想定することはできません。 初期化されていない、または無効なポインター変数をアドレス 0 に設定した場合、これらのポインターによる不適切なアクセスが常に検出されるとは限りません。

これに対し、**MM_BAD_POINTER** 値は、ドライバーが実行されるすべてのプラットフォームで無効なアドレスであることが保証されます。

アドレス 0 が無効なアドレスであるプラットフォームでは、IRQL < DISPATCH_LEVEL でアドレス 0 にアクセスするドライバーによって、`try/except` ステートメントで誤ってキャッチされる可能性がある例外 (アクセス違反) が発生することがあります。 このため、無効なアクセスがドライバーの例外処理コードによってマスクされ、デバッグ中に検出されない可能性があります。 ただし、**MM_BAD_POINTER** アドレスへのアクセスによって必ずバグ チェックが行われます。これは、例外ハンドラーによってマスクされることはありません。

次のコード例は、`ptr` という名前のポインター変数に **MM_BAD_POINTER** 値を割り当てる方法を示しています。 `unsigned char` へのポインターとなる PUCHAR 型は、Ntdef.h ヘッダー ファイルに定義されています。

`PUCHAR ptr = (PUCHAR)MM_BAD_POINTER; // Now _ptr is guaranteed to fault._`

`ptr` が **MM_BAD_POINTER** に設定された後、`ptr` が指すメモリ位置にアクセスしようとすると、バグ チェックが行われます。

実際には、**MM_BAD_POINTER** は無効なアドレスのページ全体のベース アドレスです。 したがって、**MM_BAD_POINTER** から (**MM_BAD_POINTER** + **PAGE_SIZE** - 1) までの範囲にあるアドレスにアクセスすると、バグ チェックが発生します。

Windows 8.1 以降では、**MM_BAD_POINTER** マクロは、Wdm.h ヘッダー ファイルに定義されています。 ただし、このマクロ定義を使用するドライバー コードでは、Windows Vista 以降の以前のバージョンの Windows で実行できます。

Windows Vista 以降では、[**MmBadPointer**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm64bitphysicaladdress) グローバル変数は、無効なアドレスであることが保証されているポインター値へのポインターとして使用できます。 ただし、Windows 8.1 以降では、**MmBadPointer** の使用は非推奨とされており、代わりに **MM_BAD_POINTER** マクロを使用するようにドライバーを更新する必要があります。

Windows 8.1 以降で使用できます。 Windows Vista 以降では、以前のバージョンの Windows と互換性があります。


## <a name="mmgetmdlbytecount"></a>**MmGetMdlByteCount**

定義されている場所: Wdm.h

**MmGetMdlByteCount** は、指定した MDL によって記述したバッファーの長さをバイト単位で返すマクロです。

_Mdl [in]_

**PMDL**

物理メモリ内の仮想メモリ バッファーのレイアウトを記述した [**MDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl) 構造体へのポインター。 詳細については、「[MDL の使用](using-mdls.md)」を参照してください。

**戻り値**

**ULONG**

## <a name="mmgetmdlbytecount-returns-the-length-in-bytes-of-the-buffer-described-by-_mdl_"></a>**MmGetMdlByteCount** からは、_Mdl_ によって記述したバッファーの長さがバイト単位で返されます。

**MmGetMdlByteCount** の呼び出し元は、どの IRQL で実行されていてもかまいません。 通常、呼び出し元は IRQL < = DISPATCH_LEVEL で実行されます。

Windows 2000 以降で使用できます。

IRQL: 任意のレベル


## <a name="mmgetmdlbyteoffset"></a>**MmGetMdlByteOffset**

定義されている場所: Wdm.h

**MmGetMdlByteOffset** は、指定した MDL によって記述したバッファーの最初のページ内のバイト オフセットを返すマクロです。

_Mdl [in]_

**PMDL**

MDL へのポインター。

**戻り値**

**ULONG**

## <a name="mmgetmdlbyteoffset-returns-the-offset-in-bytes"></a>**MmGetMdlByteOffset** からは、バイト単位のオフセットが返されます。

**MmGetMdlByteOffset** の呼び出し元は、どの IRQL で実行されていてもかまいません。 通常、呼び出し元は IRQL < = DISPATCH_LEVEL で実行されます。

Windows 2000 以降のバージョンの Windows で使用できます。

IRQL: 任意のレベル


## <a name="mmgetmdlpfnarray"></a>**MmGetMdlPfnArray**

定義されている場所: Wdm.h

**MmGetMdlPfnArray** は、メモリ記述子リスト (MDL) に関連付けられている物理ページ番号の配列の先頭へのポインターを返すマクロです。

_Mdl [in]_

**PMDL**

MDL へのポインター。

**戻り値**

**PPFN_NUMBER**

MDL に関連付けられている物理ページ番号の配列の先頭へのポインター。 配列内のエントリの数は **ADDRESS_AND_SIZE_TO_SPAN_PAGES**(**MmGetMdlVirtualAddress**(_Mdl_)、**MmGetMdlByteCount**(_Mdl_)) です。 各配列要素は PFN_NUMBER 型の整数値であり、Wdm.h に次のように定義されています。

`cpp typedef ULONG PFN_NUMBER, *PPFN_NUMBER;`

**注意**: 配列の内容を変更すると、診断が難しい軽度なシステムの問題が発生する可能性があります。 この配列の内容を読み取ったり、変更したりしないことをお勧めします。

ページング可能なメモリの場合、配列の内容は [**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages) でロックされているバッファーに対してのみ有効です。 非ページ プールの場合、配列の内容は [**MmBuildMdlForNonPagedPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool)、[**MmAllocatePagesForMdlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdlex)、[**MmAllocatePagesForMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdl) のいずれかで更新された MDL に対してのみ有効です。

MDL の詳細については、「[MDL の使用](using-mdls.md)」を参照してください。

Windows 2000 以降で使用できます。

IRQL: 任意のレベル


## <a name="mmgetmdlvirtualaddress"></a>**MmGetMdlVirtualAddress**

定義されている場所: Wdm.h

**MmGetMdlVirtualAddress** は、MDL によって記述したバッファーのベース仮想アドレスを返すマクロです。

_Mdl [in]_

**PMDL**

初期仮想アドレスを返すバッファーを記述した MDL へのポインター。

**戻り値**

**PVOID**

## <a name="mmgetmdlvirtualaddress-returns-the-starting-virtual-address-of-the-mdl"></a>**MmGetMdlVirtualAddress** からは、MDL の開始仮想アドレスが返されます。

**MmGetMdlVirtualAddress** から返される仮想アドレスは、現在のスレッド コンテキストで必ずしも有効ではありません。 下位レベルのドライバーでは、返された仮想アドレスを使用してメモリにアクセスすること、特にユーザー メモリ領域にアクセスすることは、しないでください。

返されるアドレスは、MDL の物理アドレス エントリのインデックスとして使用され、[**MapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer) に入力できます。

**MmGetMdlVirtualAddress** の呼び出し元は、どの IRQL で実行されていてもかまいません。 通常、呼び出し元は IRQL = DISPATCH_LEVEL で実行されます (このルーチンは、**MapTransfer** への _CurrentVa_ パラメーターを取得するために通常呼び出されるため)。

Windows 2000 以降のバージョンの Windows で使用できます。

IRQL: 任意のレベル


## <a name="mmgetsystemaddressformdlsafe"></a>**MmGetSystemAddressForMdlSafe**

定義されている場所: Wdm.h

**MmGetSystemAddressForMdlSafe** は、指定した MDL で記述するバッファーの非ページ システム領域の仮想アドレスを返すマクロです。

_Mdl [in]_

**PMDL**

対応するベース仮想アドレスをマップする対象のバッファーへのポインター。

_Priority [in]_

## <a name="mm_page_priority"></a>**Mm_PAGE_PRIORITY**

使用可能な PTE が少ない状況での成功の重要度を示す **MM_PAGE_PRIORITY** 値を指定します。 **LowPagePriority**、**NormalPagePriority**、**HighPagePriority** のいずれかの優先度の値を指定します。 Windows 8 以降では、指定した優先度の値と **MdlMappingNoWrite** または **MdlMappingNoExecute** フラグとの、ビットごとの OR 演算を行うことができます。

*   **LowPagePriority** は、システムのリソースがかなり少ない場合にマッピング要求が失敗する可能性があることを示します。 このような状況の例としては、ドライバーでマッピング エラーを処理できる、重要でないネットワーク接続が挙げられます。

*   **NormalPagePriority** は、システムのリソースが非常に少ない場合にマッピング要求が失敗する可能性があることを示します。 このような状況の例としては、重要でないローカル ファイル システム要求が挙げられます。

*   **HighPagePriority** は、システムのリソースが完全に不足していない限り、マッピング要求が失敗してはならないことを示します。 このような状況の例として、ドライバー内のページング ファイル パスが挙げられます。

*   **MdlMappingNoWrite** は、マップされた物理ページが書き込み不可 (読み取り専用) メモリとして構成されることを示します。 Windows 8 以降では、このフラグ ビットと **MM_PAGE_PRIORITY** 値とのビットごとの OR 演算によって、書き込みを無効にするメモリを指定できます。

*   **MdlMappingNoExecute** は、マップされた物理ページを実行不可メモリとして構成することを示します。 Windows 8 以降では、このフラグ ビットと **MM_PAGE_PRIORITY** 値とのビットごとの OR 演算によって、命令の実行を無効にするメモリを指定できます。 ベスト プラクティスとして、Windows 8 以降のバージョンの Windows 用に記述されたドライバーでは、実行可能メモリが明示的に必要な場合を除き、常に実行不可メモリを指定する必要があります。

*   **戻り値**

    **PVOID**

    **MmGetSystemAddressForMdlSafe** は、指定した MDL で記述する物理ページをマップする基本システム領域の仮想アドレスを返すマクロです。 ページがまだシステム アドレス空間にマップされておらず、ページをマップしようとして失敗した場合は、**NULL** が返されます。

指定した MDL によって記述した物理ページがシステム アドレス空間にまだマップされていない場合、それらのページがこのルーチンによってシステム アドレス空間にマップされます。

プログラム I/O (PIO) デバイスのドライバーでは、ユーザー モード バッファー (**Irp->MdlAddress** にある MDL によって記述されており、ユーザー モードの仮想アドレス範囲に既にマップされている) をシステム アドレス空間の範囲にマップするために、このルーチンが呼び出されます。

このルーチンに入る時点で、指定した MDL にはロックダウンされた物理ページが記述されている必要があります。 ロックダウンされた MDL は、[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)、[**MmBuildMdlForNonPagedPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool)、[**IoBuildPartialMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl)、[**MmAllocatePagesForMdlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdlex) のいずれかのルーチンを使用して作成できます。

**MmGetSystemAddressForMdlSafe** によって返されたシステム アドレス空間マッピングが不要になった場合、マッピングを解放する必要があります。 マッピングを解放するために必要な手順は、MDL が作成された方法によって異なります。 次の 4 つのケースが考えられます。

*   MDL が **MmProbeAndLockPages** ルーチンの呼び出しによって作成された場合、システム アドレス空間マッピングを明示的に解放する必要はありません。 代わりに、[**MmUnlockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages) ルーチンによってマッピング (割り当てられている場合) が解放されます。

*   MDL が **MmBuildMdlForNonPagedPool** ルーチンの呼び出しによって作成された場合、**MmGetSystemAddressForMdlSafe** で既存のシステム アドレス空間マッピングが再利用され、新しいシステム アドレス空間マッピングは作成されません。 この場合、クリーンアップは必要ありません (つまり、ロックを解除したり、マップを解除したりする必要はありません)。

*   MDL が **IoBuildPartialMdl** ルーチンの呼び出しによって作成された場合、ドライバーによって [**MmPrepareMdlForReuse**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) ルーチンまたは [**IoFreeMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreemdl) ルーチンが呼び出だれ、システム アドレス空間マッピングが解放される必要があります。

*   MDL が **MmAllocatePagesForMdlEx** ルーチンの呼び出しによって作成された場合、ドライバーで **MmUnmapLockedPages** ルーチンを呼び出して、システム アドレス空間マッピングを解放する必要があります。 **MmGetSystemAddressForMdlSafe** が 1 つの MDL に対して複数回呼び出された場合、後続の **MmGetSystemAddressForMdlSafe** 呼び出しでは、単に最初の呼び出しで作成されたマッピングだけが返されます。 このマッピングを解放するには、**MmUnmapLockedPages** を 1 回呼び出すだけで十分です。

Windows 7 以降および Windows Server 2008 R2 以降では、**MmAllocatePagesForMdlEx** によって作成された MDL に対して **MmUnmapLockedPages** を明示的に呼び出す必要はありません。 代わりに、[**MmFreePagesFromMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreepagesfrommdl) ルーチンを呼び出すと、システム アドレス空間マッピング (割り当てられている場合) が解放されます。

新しいシステム アドレス空間マッピングを作成するために、**MmGetSystemAddressForMdlSafe** では、_CacheType_ パラメーターを **MmCached** に設定して、**MmMapLockedPagesSpecifyCache** が呼び出されます。 **MmCached** 以外のキャッシュの種類を必要とするドライバーでは、**MmGetSystemAddressForMdlSafe** を呼び出すのではなく、**MmMapLockedPagesSpecifyCache** を直接呼び出す必要があります。 _CacheType_ パラメーターの詳細については、[**MmMapLockedPagesSpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache)に関するページを参照してください。

**MmMapLockedPagesSpecifyCache** の呼び出しでは、指定したキャッシュの種類は、MDL によって記述したページにキャッシュの種類がまだ関連付けられていない場合に限って使用されます。 ただし、ほぼすべての場合において、ページには既に関連付けられたキャッシュの種類があり、このキャッシュの種類が新しいマッピングに使用されます。 このルールの例外は、ページが **MmAllocatePagesForMdl** によって割り当てられた場合です。この場合、ページの元のキャッシュの種類に関係なく、キャッシュの種類が **MmCached** に設定されます。

一度に 1 つのスレッドだけが、特定の MDL に対して **MmGetSystemAddressForMdlSafe** を安全に呼び出すことができます。このルーチンは、呼び出し元のスレッドが MDL を所有していると想定しているためです。 ただし、同じスレッドからすべての呼び出しを行うか、呼び出しを明示的に同期する (複数のスレッドからの呼び出しの場合) ことによって、同じ MDL に対して **MmGetSystemAddressForMdlSafe** を複数回呼び出すことができます。

ドライバーで要求を小さい要求に分割する必要がある場合、ドライバーで追加の MDL を割り当てることができます。または、ドライバーで **IoBuildPartialMdl** ルーチンを使用できます。

返されるベース アドレスのオフセットは、MDL 内の仮想アドレスのオフセットと同じです。

Windows 98 で **MmGetSystemAddressForMdlSafe** はサポートされていません。 代わりに [**MmGetSystemAddressForMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmgetsystemaddressformdl) を使用してください。

このマクロでは [**MmMapLockedPagesSpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache) を呼び出すので、このマクロを使用するには、NtosKrnl.lib へのリンクが必要になることがあります。

Windows 2000 以降で使用できます。

IRQL <= DISPATCH_LEVEL


## <a name="mminitializemdl"></a>**MmInitializeMdl**

定義されている場所: Wdm.h

**MmInitializeMdl** は、MDL のヘッダーを初期化するマクロです。

_MemoryDescriptorList [in]_

**PMDL**

MDL として初期化するバッファーへのポインター。 詳細については、以下のセクションを参照してください。

_BaseVa [in]_

**PVOID**

バッファーのベース仮想アドレスへのポインター。

_Length [in]_

**SIZE_T**

MDL によって記述されるバッファーの長さをバイト単位で指定します。 このルーチンでは、MAXULONG バイトの最大バッファー長がサポートされています。

**戻り値**

**VOID**

_MemoryDescriptorList_ が示すバッファーは、非ページ メモリに割り当てられている必要があります。 このバッファーのサイズ (バイト単位) は、少なくとも **sizeof**(MDL) + **sizeof**(PFN_NUMBER) * **ADDRESS_AND_SIZE_TO_SPAN_PAGES**(_BaseVa_, _Length_) である必要があります。

Windows 2000 以降のバージョンの Windows で使用できます。

IRQL <= DISPATCH_LEVEL


## <a name="mmpreparemdlforreuse"></a>**MmPrepareMdlForReuse**

定義されている場所: Wdm.h

**MmPrepareMdlForReuse** は、部分的な MDL に関連付けられているリソースを解放して、MDL を再利用できるようにするマクロです。

_Mdl [in]_

**PMDL**

再利用できるように準備する部分的な MDL へのポインター。

**戻り値**

**VOID**

このマクロは、[**IoBuildPartialMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl) ルーチンの呼び出しで _TargetMdl_ パラメーターとして同じ割り当て済み MDL を繰り返し使用するドライバーで使用します。 **MmPrepareMdlForReuse** の呼び出しで、指定した部分的な MDL に、システム アドレス空間に対するマッピングが関連付けられている場合、**MmPrepareMdlForReuse** によってマッピングが解放され、MDL を再利用できるようになります。

**MmPrepareMdlForReuse** では、**IoBuildPartialMdl**によって作成された部分的な MDL のみが受け入れられます。 **MmPrepareMdlForReuse** に、システム アドレス空間にマップされているが **IoBuildPartialMdl** によって作成されていない MDL が渡された場合、**MmPrepareMdlForReuse** によってマッピングは解放されず、チェック ビルドではアサーションが失敗します。

部分的な MDL の詳細については、「[MDL の使用](using-mdls.md)」を参照してください。

Windows 2000 以降のバージョンの Windows で使用できます。

IRQL <= DISPATCH_LEVEL


## <a name="page_align"></a>**PAGE_ALIGN**

定義されている場所: Wdm.h

**PAGE_ALIGN** は、指定した仮想アドレスに対して、ページ境界に配置された仮想アドレスを返すマクロです。

_Va [in]_

**PVOID**

仮想アドレスへのポインター。

**戻り値**

**PVOID**

## <a name="page_align-returns-a-pointer-to-the-page-aligned-virtual-address"></a>**PAGE_ALIGN** からは、ページ境界に配置された仮想アドレスへのポインターが返されます。

Windows 2000 以降で使用できます。

IRQL: 任意のレベル


## <a name="paged_code"></a>**PAGED_CODE**

定義されている場所: Wdm.h

**PAGED_CODE** は、呼び出し元のスレッドが、ページングを許可するのに十分な下位の IRQL で実行されていることを確認するマクロです。

**戻り値**

**VOID**

IRQL > APC_LEVEL の場合、**PAGED_CODE** マクロによってシステムで ASSERT が実行されます。

このマクロの呼び出しは、ページング可能なコードを含むか、ページング可能なコードにアクセスするすべてのドライバー ルーチンの先頭で行う必要があります。

**PAGED_CODE** マクロでは、ドライバー コードでこのマクロを実行した時点でのみ、IRQL がチェックされます。 それ以降にコードで IRQL を引き上げた場合、この変更はマクロで検出されません。 ドライバー開発者は、[静的ドライバー検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)と[ドライバーの検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)を使用して、ドライバー ルーチンの実行中に IRQL が不適切に引き上げられたときにそれを検出する必要があります。

**PAGED_CODE** マクロは、チェック ビルドでのみ動作します。

Windows 2000 以降で使用できます。


## <a name="paged_code_locked"></a>**PAGED_CODE_LOCKED**

定義されている場所: Wdm.h

**PAGED_CODE_LOCKED** は、現在実行中のコード セクションがページング可能であり、実行前にメモリにロックされている必要があることを表明するマクロです。

**戻り値**

**VOID**

ページング可能なコードは、所定の位置にロックされていない限り、特定の制限 (IRQL < = APC_LEVEL など) に従っている必要があります。 正常に動作するために所定の位置にロックされている必要があるページング可能なルーチンは、**PAGED_CODE_LOCKED** の呼び出しから開始する必要があります。

コード セクションを所定の位置にロックする方法の詳細については、「[ページング可能なコードまたはデータのロック](locking-pageable-code-or-data.md)」を参照してください。


## <a name="posetdevicebusy"></a>**PoSetDeviceBusy**

定義されている場所: Wdm.h

**PoSetDeviceBusy** は、_IdlePointer_ に関連付けられているデバイスがビジー状態であることを[電源マネージャー](power-manager.md)に通知するマクロです。

_IdlePointer [in, out]_

**PULONG**

[**PoRegisterDeviceForIdleDetection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poregisterdeviceforidledetection) によって以前に返された、**NULL** でないアイドル ポインターを指定します。 **PoRegisterDeviceForIdleDetection** から **NULL** ポインターが返される場合があることに注意してください。 **PoSetDeviceBusy** の呼び出し元は、ポインターを **PoSetDeviceBusy** に渡す前に、そのポインターが **NULL** でないことを確認する必要があります。

**戻り値**

**VOID**

**注意**: [**PoSetDeviceBusyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetdevicebusyex) は、**PoSetDeviceBusy** マクロを直接置き換えるルーチンです。 Windows Vista Service Pack 1 (SP1) 以降のバージョンの Windows 用の新しいドライバー コードを作成する場合は、**PoSetDeviceBusy** ではなく、**PoSetDeviceBusyEx** を呼び出します。

ドライバーでは、**PoSetDeviceBusy** を **PoRegisterDeviceForIdleDetection** と共に使用して、デバイスのシステム アイドル検出を有効にします。 アイドル検出の対象として登録されたデバイスがアイドル状態になると、電源マネージャーによって [**IRP_MN_SET_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) 要求が送信されて、デバイスが要求されたスリープ状態になります。

**PoSetDeviceBusy** によって、デバイスがビジー状態であることが報告され、電源マネージャーがアイドル状態のカウントダウンを再開できるようになります。 デバイスの電源が入っていない場合は、**PoSetDeviceBusy** によって状態が変更されることはありません。 つまり、それによってシステムが電源オン要求を送信することはありません。

ドライバーでは、すべての I/O 要求で **PoSetDeviceBusy** を呼び出す必要があります。

Windows 2000 以降で使用できます。

IRQL: 任意のレベル


## <a name="psgetcurrentprocess"></a>**PsGetCurrentProcess**

定義されている場所: Ntddk.h

現在のスレッドのプロセスへのポインターが返されます。

**戻り値**

不透明なプロセス オブジェクトへのポインター。



Windows 2000 以降で使用できます。

IRQL: 任意のレベル


## <a name="read_register_buffer_ulong64"></a>**READ_REGISTER_BUFFER_ULONG64**

定義されている場所: Wdm.h

**READ_REGISTER_BUFFER_ULONG64** は、指定したレジスタ アドレスから多数の ULONG64 値をバッファーに読み込むマクロです。

_Register [in]_

**PULONG64**

レジスタへのポインター。これは、メモリ空間内のマップされた範囲である必要があります。

_Buffer [out]_

**PULONG64**

ULONG64 値の配列が読み込まれるバッファーへのポインター。

_Count [in]_

**ULONG**

バッファーに読み込む ULONG64 値の数を指定します。

**戻り値**

**VOID**

_Buffer_ バッファーのサイズは、少なくとも指定した数の ULONG64 値を格納できる大きさである必要があります。

**READ_REGISTER_BUFFER_ULONG64** マクロの呼び出し元は、どの IRQL で実行されていてもかまいません (_Buffer_ バッファーが常駐で、_Register_ のレジスタが常駐のマップされたデバイス メモリと想定した場合)。

64 ビット バージョンの Windows でのみ使用できます。

IRQL: 任意のレベル


## <a name="read_register_ulong64"></a>**READ_REGISTER_ULONG64**

定義されている場所: Wdm.h

**READ_REGISTER_ULONG64** は、指定したレジスタ アドレスから ULONG64 値を読み取るマクロです。

_volatile *Register [in]_

**ULONG64**

レジスタ アドレスへのポインター。これは、メモリ空間内のマップされた範囲である必要があります。

**戻り値**

**ULONG64**

**READ_REGISTER_ULONG64** からは、指定したレジスタ アドレスから読み取られた ULONG64 値が返されます。

**READ_REGISTER_ULONG64** マクロの呼び出し元は、どの IRQL で実行されていてもかまいません (_Register_ のアドレスが常駐のマップされたデバイス メモリであると想定した場合)。

64 ビット バージョンの Windows でのみ使用できます。

IRQL: 任意のレベル


## <a name="round_to_pages"></a>**ROUND_TO_PAGES**

定義されている場所: Wdm.h

**ROUND_TO_PAGES** は、バイト単位のサイズを受け取って次の完全なページに切り上げるマクロです。

_Size [in]_

**ULONG_PTR**

ページの倍数に切り上げるサイズをバイト単位で指定します。

**戻り値**

**ULONG_PTR**

**ROUND_TO_PAGES** からは、現在のプラットフォームでの仮想メモリ ページ サイズの倍数に切り上げられた入力サイズが返されます。

**ROUND_TO_PAGES** の呼び出し元は、どの IRQL で実行されていてもかまいません。 呼び出し元は、指定したパラメーターによってメモリ オーバーフローが確実に発生しないようにする必要があります。

IRQL: 任意のレベル


## <a name="rtlequalluid"></a>**RtlEqualLuid**

定義されている場所: Wdm.h

**戻り値**

Windows 2000 以降で使用できます。

IRQL: 任意のレベル


## <a name="rtlinitemptyansistring"></a>**RtlInitEmptyAnsiString**

定義されている場所: Wdm.h

**RtlInitEmptyAnsiString** は、空のカウントされた ANSI 文字列を初期化するマクロです。

_DestinationString [out]_

**PANSI_STRING**

初期化する [**ANSI_STRING**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_string) 構造体へのポインター。

_Buffer [in]_

**PCHAR**

WCHAR 文字列を格納するために使用される、呼び出し元によって割り当てられたバッファーへのポインター。

_BufferSize [in]_

**USHORT**

_Buffer_ が指すバッファーの長さ (バイト単位)。

**戻り値**

**VOID**

_DestinationString_ パラメーターが指す構造体のメンバーは、次のように初期化されます。

*   **Length**。 ゼロ。

*   **MaximumLength**。 _BufferSize_。

*   **Buffer**。 _SourceString_。

空ではないカウントされた Unicode 文字列を初期化するには、[**RtlInitAnsiString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlinitansistring) を呼び出します。

Microsoft Windows XP 以降のバージョンの Windows で使用できます。

IRQL: 任意のレベル


## <a name="rtlinitemptyunicodestring"></a>**RtlInitEmptyUnicodeString**

定義されている場所: Wdm.h

**RtlInitEmptyUnicodeString** は、空のカウントされた Unicode 文字列を初期化するマクロです。

_DestinationString [out]_

**PUNICODE_STRING**

初期化する [**UNICODE_STRING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string) 構造体へのポインター。

_Buffer [in]_

**PWCHAR**

WCHAR 文字列を格納するために使用される、呼び出し元によって割り当てられたバッファーへのポインター。

_BufferSize [in]_

**USHORT**

_Buffer_ が指すバッファーの長さ (バイト単位)。

**戻り値**

**VOID**

_DestinationString_ パラメーターが指す構造体のメンバーは、次のように初期化されます。

*   **Length**。 ゼロ。

*   **MaximumLength**。 _BufferSize_。

*   **Buffer**。 _SourceString_。

空ではないカウントされた Unicode 文字列を初期化するには、[**RtlInitUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlinitunicodestring) を呼び出します。

Windows XP 以降で使用できます。

IRQL: 任意のレベル


## <a name="rtliszeroluid"></a>**RtlIsZeroLuid**

定義されている場所: Ntddk.h

**RtlIsZeroLuid** は、指定した LUID が 0 の LUID であるかどうかを判断するマクロです。

_L1 [in]_

**PLUID**

確認する [**LUID**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_luid) を指定します。

**戻り値**

**BOOLEAN**

_L1_ が 0 の場合は、**RtlIsZeroLuid** から **TRUE** が返されます。それ以外の場合は **FALSE** が返されます。

IRQL: 任意のレベル


## <a name="rtlretrieveulong"></a>**RtlRetrieveUlong**

定義されている場所: Wdm.h

**RtlRetrieveUlong** は、アラインメント エラーを回避しながらソース アドレスから ULONG 値を取得するマクロです。 宛先アドレスは、アラインされていると想定されます。

_DestinationAddress [out]_

**PULONG**

ULONG 値を格納する、ULONG でアラインされた場所へのポインター。

_SourceAddress [in]_

**PULONG**

ULONG 値の取得元である場所へのポインター。

**戻り値**

**VOID**

指定したアドレスが非ページ プールにある場合、**RtlRetrieveUlong** の呼び出し元はどの IRQL で実行されていてもかまいません。 それ以外の場合、呼び出し元は IRQL < = APC_LEVEL で実行されている必要があります。

Windows 2000 以降のバージョンの Windows で使用できます。


## <a name="rtlretrieveushort"></a>**RtlRetrieveUshort**

定義されている場所: Wdm.h

**RtlRetrieveUshort** は、アラインメント エラーを回避しながらソース アドレスから USHORT 値を取得するマクロです。

_DestinationAddress [out]_

**PUSHORT**

値を格納する、USHORT でアラインされた場所へのポインター。

_SourceAddress [in]_

**PUSHORT**

値の取得元である場所へのポインター。

**戻り値**

**VOID**

指定したアドレスが非ページ プールにある場合、**RtlRetrieveUshort** の呼び出し元はどの IRQL で実行されていてもかまいません。 それ以外の場合、呼び出し元は IRQL < = APC_LEVEL で実行されている必要があります。

Windows 2000 以降のバージョンの Windows で使用できます。

IRQL: 任意のレベル


## <a name="rtlstoreulong"></a>**RtlStoreUlong**

定義されている場所: Wdm.h

**RtlStoreUlong** は、アラインメント エラーを回避しながら特定のアドレスに ULONG 値を格納するマクロです。

_Address [out]_

**PULONG**

指定した ULONG 値を格納する場所へのポインター。

_Value [in]_

**ULONG**

格納する対象の ULONG 値を指定します。

**戻り値**

**VOID**

_Address_ が非ページ プールを指している場合、呼び出し元はどの IRQL で実行されていてもかまいません。 それ以外の場合、呼び出し元は IRQL < = APC_LEVEL で実行されている必要があります。

Windows 2000 以降のバージョンの Windows で使用できます。

IRQL: 任意のレベル


## <a name="rtlstoreulonglong"></a>**RtlStoreUlonglong**

定義されている場所: Wdm.h

**RtlStoreUlonglong** は、メモリ アラインメント エラーを回避しながら、指定したメモリ アドレスに指定した ULONGLONG 値を格納するマクロです。

_Address [out]_

**PULONGLONG**

指定した ULONGLONG 値を格納する場所へのポインター。

_Value [in]_

**ULONGLONG**

格納する対象の ULONGLONG 値。

**戻り値**

**VOID**

**RtlStoreUlonglong** を使用すると、メモリ アラインメント エラーが回避されます。 _Address_ に指定したアドレスが ULONGLONG のストレージ要件に適合していない場合、**RtlStoreUlonglong** では、メモリ位置 (PUCHAR)_Address_ から始まる _Value_ のバイト数が格納されます。

_Address_ が非ページ プールを指している場合、**RtlStoreUlonglong** は、どの IRQL でも実行されます。それ以外の場合は、IRQL < = APC_LEVEL で実行される必要があります。

Windows 2000 以降で使用できます。

IRQL: 任意のレベル


## <a name="rtlstoreulongptr"></a>**RtlStoreUlongPtr**

定義されている場所: Wdm.h

**RtlStoreUlongPtr** は、メモリ アラインメント エラーを回避しながら、指定した ULONG_PTR 値を指定したメモリ位置に格納するマクロです。

_Address [out]_

**PULONG_PTR**

ULONG_PTR 値を格納する場所へのポインター。

_Value [in]_

**ULONG_PTR**

格納する対象の ULONG_PTR 値を指定します。

**戻り値**

**VOID**

**RtlStoreUlongPtr** を使用すると、メモリ アラインメント エラーが回避されます。 _Address_ の値が ULONG_PTR のストレージ要件に適合していない場合、**RtlStoreUlongPtr** では、メモリ位置 (PUCHAR)_Address_ から始まる _Value_ のバイト数が格納されます。

_Address_ が非ページ プールを指している場合、**RtlStoreUlongPtr** は、どの IRQL でも実行されます。それ以外の場合は、IRQL < = APC_LEVEL で実行される必要があります。

Windows 2000 以降のバージョンの Windows で使用できます。

IRQL: 任意のレベル


## <a name="rtlstoreushort"></a>**RtlStoreUshort**

定義されている場所: Wdm.h

**RtlStoreUshort** は、アラインメント エラーを回避しながら特定のアドレスに USHORT 値を格納するマクロです。

_Address [out]_

**PUSHORT**

指定した USHORT 値を格納する場所へのポインター。

_Value [in]_

**USHORT**

格納する対象の USHORT 値を指定します。

**戻り値**

**VOID**

_Address_ が非ページ プールを指している場合、呼び出し元はどの IRQL で実行されていてもかまいません。 それ以外の場合、呼び出し元は IRQL < = APC_LEVEL で実行されている必要があります。

Windows 2000 以降のバージョンの Windows で使用できます。

IRQL: 任意のレベル


## <a name="write_register_buffer_ulong64"></a>**WRITE_REGISTER_BUFFER_ULONG64**

定義されている場所: Wdm.h

**WRITE_REGISTER_BUFFER_ULONG64** は、指定したレジスタにバッファーから多数の ULONG64 値を書き込むマクロです。

_Register [in]_

**PULONG64**

レジスタへのポインター。これは、メモリ空間内のマップされた範囲である必要があります。

_Buffer [in]_

**PULONG64**

ULONG64 値の配列が書き込まれるバッファーへのポインター。

_Count [in]_

**ULONG**

レジスタに書き込まれる ULONG64 値の数を指定します。

**戻り値**

**VOID**

_Buffer_ バッファーのサイズは、少なくとも指定した数の ULONG64 値を格納できる大きさである必要があります。

**WRITE_REGISTER_BUFFER_ULONG64** マクロの呼び出し元は、どの IRQL で実行されていてもかまいません (_Buffer_ バッファーが常駐で、_Register_ のレジスタが常駐のマップされたデバイス メモリであると想定した場合)。

64 ビット バージョンの Windows でのみ使用できます。

IRQL: 任意のレベル


## <a name="write_register_ulong64"></a>**WRITE_REGISTER_ULONG64**

定義されている場所: Wdm.h

**WRITE_REGISTER_ULONG64** は、指定したアドレスに ULONG64 値を書き込むマクロです。

_volatile *Register [in]_

**ULONG64**

レジスタへのポインター。これは、メモリ空間内のマップされた範囲である必要があります。

_Value [in]_

**ULONG64**

レジスタに書き込む ULONG64 値を指定します。

**戻り値**

**VOID**

**WRITE_REGISTER_ULONG64** マクロの呼び出し元は、どの IRQL で実行されていてもかまいません (_Register_ のレジスタが常駐のマップされたデバイス メモリであると想定した場合)。

64 ビット バージョンの Windows でのみ使用できます。

IRQL: 任意のレベル


## <a name="zwcurrentprocess"></a>**ZwCurrentProcess**

定義されている場所: Wdm.h

**ZwCurrentProcess** は、現在のプロセスへのハンドルを返すマクロです。

**戻り値**

**HANDLE**

**ZwCurrentProcess** からは、現在のプロセスを表す特別なハンドル値が返されます。

戻り値は真のハンドルではなく、常に現在のプロセスを表す特別な値です。

**NtCurrentProcess** と **ZwCurrentProcess** は、同じ Windows ネイティブ システム サービス ルーチンの 2 つのバージョンです。 Windows カーネルの **NtCurrentProcess** ルーチンからカーネル モード ドライバーに直接アクセスすることはできません。 ただし、カーネル モード ドライバーで **ZwCurrentProcess** を呼び出すことによって、このルーチンに間接的にアクセスできます。

カーネル モード ドライバーからの呼び出しの場合、Windows ネイティブ システム サービス ルーチンの **Nt_Xxx_** バージョンと **Zw_Xxx_** バージョンは、入力パラメーターを処理および解釈する方法で動作が異なることがあります。 **Nt_Xxx_** バージョンと **Zw_Xxx_** バージョンのルーチンの関係の詳細については、「[Nt および Zw バージョンのネイティブ システム サービス ルーチンの使用](using-nt-and-zw-versions-of-the-native-system-services-routines.md)」を参照してください。

サポート対象のすべてのオペレーティング システム。

IRQL: 任意のレベル


## <a name="zwcurrentthread"></a>**ZwCurrentThread**

定義されている場所: Wdm.h

**ZwCurrentThread** は、現在のスレッドへのハンドルを返すマクロです。

**戻り値**

**HANDLE**

**ZwCurrentThread** からは、現在のスレッドを表す特別なハンドル値が返されます。

戻り値は真のハンドルではなく、常に現在のスレッドを表す特別な値です。

**NtCurrentThread** と **ZwCurrentThread** は、同じ Windows ネイティブ システム サービス ルーチンの 2 つのバージョンです。 Windows カーネルの **NtCurrentThread** ルーチンからカーネル モード ドライバーに直接アクセスすることはできません。 ただし、カーネル モード ドライバーで **ZwCurrentThread** ルーチンを呼び出すことによって、このルーチンに間接的にアクセスできます。

カーネル モード ドライバーからの呼び出しの場合、Windows ネイティブ システム サービス ルーチンの **Nt_Xxx_** バージョンと **Zw_Xxx_** バージョンは、入力パラメーターを処理および解釈する方法で動作が異なることがあります。 **Nt_Xxx_** バージョンと **Zw_Xxx_** バージョンのルーチンの関係の詳細については、「[Nt および Zw バージョンのネイティブ システム サービス ルーチンの使用](using-nt-and-zw-versions-of-the-native-system-services-routines.md)」を参照してください。

サポート対象のすべてのオペレーティング システム。

IRQL: 任意のレベル










