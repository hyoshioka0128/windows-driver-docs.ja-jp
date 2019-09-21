---
title: Windows カーネルのマクロ
description: Windows カーネルのマクロ
ms.assetid: 91366400-3307-4F13-A839-50BA85B7F73E
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7acea88bbee2cd0b39680f536fc207d14faec3fe
ms.sourcegitcommit: ee1fc949d1ae5eb14df4530758f767702a886e36
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2019
ms.locfileid: "71164789"
---
# <a name="windows-kernel-macros"></a>Windows カーネルのマクロ


次の一覧には、Windows カーネルマクロが含まれています。


## <a name="address_and_size_to_span_pages"></a>**ADDRESS_AND_SIZE_TO_SPAN_PAGES**

定義されている:Wdm

**ADDRESS_AND_SIZE_TO_SPAN_PAGES**マクロは、仮想アドレスによって定義された仮想範囲にまたがるページ数と、転送要求のサイズ (バイト単位) を返します。

_Va [入力]_

**PVOID**

範囲のベースである仮想アドレスへのポインター。

_サイズ [入力]_

**ULONG**

転送要求のサイズ (バイト単位) を指定します。

**戻り値**

**ULONG**

**ADDRESS_AND_SIZE_TO_SPAN_PAGES**は、 _Va_で始まる仮想範囲によってスパンされたページ数を返します。

DMA 転送を行うドライバーは、転送要求を一連のデバイス DMA 操作に分割する必要があるかどうかを判断するために**ADDRESS_AND_SIZE_TO_SPAN_PAGES**を呼び出します。

ドライバーは、システム定義の定数 PAGE_SIZE を使用して、転送されるバイト数が現在のプラットフォームの仮想メモリページサイズよりも小さいかどうかを判断できます。

**ADDRESS_AND_SIZE_TO_SPAN_PAGES**の呼び出し元は、任意の IRQL で実行できます。 呼び出し元は、指定されたパラメーターがメモリオーバーフローを発生させないようにする必要があります。

Windows 2000 以降で使用できます。


## <a name="byte_offset"></a>**BYTE_OFFSET**

定義されている:Wdm

**BYTE_OFFSET**マクロは仮想アドレスを受け取り、ページ内のそのアドレスのバイトオフセットを返します。

_Va [入力]_

**PVOID**

仮想アドレスへのポインター。

**戻り値**

**ULONG**

**BYTE_OFFSET**は、仮想アドレスのオフセット部分を返します。

Windows 2000 以降で使用できます。

IRQL任意のレベル


## <a name="bytes_to_pages"></a>**BYTES_TO_PAGES**

定義されている:Wdm

**BYTES_TO_PAGES**マクロは、転送要求のサイズ (バイト単位) を取得し、バイトを格納するために必要なページ数を計算します。

_サイズ [入力]_

**ULONG**

転送要求のサイズ (バイト単位) を指定します。

**戻り値**

**ULONG**

**BYTES_TO_PAGES**は、指定されたバイト数を格納するために必要なページ数を返します。

システム定義定数 PAGE_SIZE を使用すると、転送用に指定された長さのバイト数が、現在のプラットフォームの仮想メモリページサイズよりも小さいかどうかを判断できます。

Windows 2000 以降で使用できます。

IRQL任意のレベル


## <a name="containing_record"></a>**CONTAINING_RECORD**

定義されている:Ntdef. h

**CONTAINING_RECORD**マクロは、構造体の型と、それを含む構造体内のフィールドのアドレスを指定して、構造体のインスタンスのベースアドレスを返します。

_アドレス [入力]_

**PCHAR**

Type 型の構造体のインスタンス内のフィールドへのポインター _。_

_型 [in]_

**TYPE**

返されるベースアドレスを持つ構造体の型の名前。

_フィールド [in]_

**PCHAR**

_アドレス_によって示され _、型の_構造体に含まれるフィールドの名前。

**戻り値**

**PCHAR**

_フィールド_を含む構造体のベースのアドレスを返します。

呼び出し元がこのような構造体内のフィールドへのポインターを持っている場合に、型がわかっている構造体のベースアドレスを決定するために呼び出されます。 このマクロは、既知の型の構造内の他のフィールドにシンボリックアクセスする場合に便利です。

Windows 2000 以降で使用できます。

IRQL任意のレベル


## <a name="ioskipcurrentirpstacklocation"></a>**Ioskipon Entiの場所**

定義されている:Wdm

IO_STACK_LOCATIONは、システムの[**IO_STACK_LOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)配列ポインターを変更します。これにより、現在のドライバーが次に低いドライバーを呼び出すと、そのドライバーは、現在のドライバーを受信しました。

_Irp [in, out]_

**PIRP**

IRP へのポインター。

**戻り値**

**無効化**

ドライバーが次の下位のドライバーに IRP を送信すると、ドライバーは [_IoCompletion_](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) ルーチンを提供しない場合 **IoSkipCurrentIrpStackLocation** を呼び出すことができます (これは、ドライバーの [**IO_STACK_LOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location) 構造に格納されているアドレスです)。 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)を呼び出す前に**Ioskip entilocation**を呼び出すと、ドライバーが受信したものと同じ**IO_STACK_LOCATION**が次の下位のドライバーに渡されます。

IRP に対して_Iocompletion_ルーチンを提供する場合、ドライバーは**Ioskipの場所**ではなく[**iocopy"enti"** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)を呼び出す必要があります。 正しく記述されていないドライバーによって**Ioskipに**よって処理が失敗し、完了ルーチンが設定された場合、このドライバーは、その下のドライバーによって設定された完了ルーチンを上書きする可能性があります。

ドライバーが IRP を保留にしている場合、ドライバーは、IRP を次の下位のドライバーに渡す前に、 **Ioskipfinalentifinallocation**を呼び出さないでください。 ドライバーが、次の下位のドライバーに渡す前に、保留中の IRP で**IoskipSL_PENDING_RETURNED**を呼び出すと、次のドライバーの i/o スタックの場所の**コントロール**メンバーに、このフラグが設定されたままになります。 次のドライバーがそのスタックの場所を所有しており、変更される可能性があるため、保留中のフラグがクリアされる可能性があります。 このような状況が発生すると、オペレーティングシステムがバグチェックを発行したり、IRP の処理が完了しないことがあります。

代わりに、IRP を保留にしたドライバーは、 **IocopyIoCallDriver**を呼び出す前に、次に低いドライバー用に新しいスタックの場所を設定する必要があります。

ドライバーが**IoskipIO_STACK_LOCATION Entilocation**を呼び出す場合は、そのドライバーに関して、下位のドライバーやシステムの動作に意図しない影響を与える可能性のある方法で、構造体を変更しないように注意してください。 例としては、 **IO_STACK_LOCATION**構造体の**パラメーター**共用体を変更したり、 [**iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)を呼び出したりすることができます。

Windows 2000 以降で使用できます。

IRQL任意のレベル


## <a name="keinitializecallbackrecord"></a>**Ke初期化 Ecallbackrecord**

定義されている:Wdm

**KeInitializeCallbackRecord** マクロは [**KBUGCHECK_CALLBACK_RECORD**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess) または [**KBUGCHECK_REASON_CALLBACK_RECORD**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess) 構造体を初期化します。

_[入力]_

**PKBUGCHECK_CALLBACK_RECORD**

**KBUGCHECK_CALLBACK_RECORD**または**KBUGCHECK_REASON_CALLBACK_RECORD**構造体へのポインター。 構造体は、非ページプールなどの常駐メモリ内に存在する必要があります。

**戻り値**

**無効化**

Windows 2000 以降のバージョンの Windows で使用できます。

IRQL任意のレベル


## <a name="mm_bad_pointer"></a>**MM_BAD_POINTER**

定義されている:Wdm

ドライバーは、 **MM_BAD_POINTER**マクロを無効なポインター値として使用して、初期化されていない、または無効になっているポインター変数に割り当てることができます。 この無効なポインター変数が指すメモリ位置にアクセスしようとすると、バグチェックが発生します。

多くのハードウェアプラットフォームでは、アドレス 0 (名前付き定数**NULL**としてよく表されます) は無効なアドレスですが、ドライバー開発者は、アドレス0がすべてのプラットフォームで汎用的に無効であると想定しないでください。 初期化されていない、または無効なポインター変数をアドレス0に設定すると、これらのポインターによる不適切なアクセスが検出されるとは限らない場合があります。

これに対し、値**MM_BAD_POINTER**は、ドライバーを実行するすべてのプラットフォームで無効なアドレスであることが保証されます。

アドレス0が無効なアドレスであるプラットフォームでは、IRQL < DISPATCH_LEVEL でアドレス0にアクセスするドライバーにより、 `try/except`ステートメントで誤ってキャッチされる例外 (アクセス違反) が発生します。 このため、ドライバーの例外処理コードによって無効なアクセスがマスクされ、デバッグ中に検出されない可能性があります。 ただし、 **MM_BAD_POINTER**アドレスへのアクセスによってバグチェックが確実に行われることは保証されていますが、これは例外ハンドラーによってマスクされることはありません。

次のコード例は、という名前`ptr`のポインター変数に値**MM_BAD_POINTER**を割り当てる方法を示しています。 Ntdef .h ヘッダーファイルは、へ`unsigned char`のポインターとなる puchar 型を定義します。

`PUCHAR ptr = (PUCHAR)MM_BAD_POINTER; // Now _ptr is guaranteed to fault._`

が MM_BAD_POINTER に設定されると、が指す`ptr`メモリ位置にアクセスしようとすると、バグチェックが発生します。 `ptr`

実際、 **MM_BAD_POINTER**は、無効なアドレスのページ全体のベースアドレスです。 そのため、範囲**MM_BAD_POINTER** (**MM_BAD_POINTER** + **PAGE_SIZE** -1) のアドレスにアクセスすると、バグチェックが発生します。

Windows 8.1 以降では、 **MM_BAD_POINTER**マクロは、Wdm ヘッダーファイルで定義されています。 ただし、このマクロ定義を使用するドライバーコードは、Windows Vista 以降の以前のバージョンの Windows で実行できます。

Windows Vista 以降では、 [**Mmbadpointer**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm64bitphysicaladdress)グローバル変数は、無効なアドレスであることが保証されるポインター値へのポインターとして使用できます。 ただし Windows 8.1 以降では、 **Mmbadpointer**の使用は非推奨とされます。代わりに、 **MM_BAD_POINTER**マクロを使用するようにドライバーを更新する必要があります。

Windows 8.1 \ から使用できます。 Windows Vista 以降では、以前のバージョンの Windows と互換性があります。


## <a name="mmgetmdlbytecount"></a>**MmGetMdlByteCount**

定義されている:Wdm

**MmGetMdlByteCount**マクロは、指定された MDL によって記述されるバッファーの長さをバイト単位で返します。

_Mdl [in]_

**PMDL**

物理メモリ内の仮想メモリバッファーのレイアウトを記述する[**MDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_mdl)構造体へのポインター。 詳細については、「 [MDLs の使用](using-mdls.md)」を参照してください。

**戻り値**

**ULONG**

## <a name="mmgetmdlbytecount-returns-the-length-in-bytes-of-the-buffer-described-by-_mdl_"></a>**MmGetMdlByteCount**は、 _Mdl_によって記述されるバッファーの長さをバイト単位で返します。

**MmGetMdlByteCount**の呼び出し元は、任意の IRQL で実行できます。 通常、呼び出し元は IRQL < = DISPATCH_LEVEL で実行されます。

Windows 2000 以降で使用できます。

IRQL任意のレベル


## <a name="mmgetmdlbyteoffset"></a>**MmGetMdlByteOffset**

定義されている:Wdm

**Mmgetmdlbyteoffset**マクロは、指定された MDL によって記述されるバッファーの最初のページ内のバイトオフセットを返します。

_Mdl [in]_

**PMDL**

MDL へのポインター。

**戻り値**

**ULONG**

## <a name="mmgetmdlbyteoffset-returns-the-offset-in-bytes"></a>**Mmgetmdlbyteoffset**は、バイト単位のオフセットを返します。

**Mmgetmdlbyteoffset**の呼び出し元は、任意の IRQL で実行できます。 通常、呼び出し元は IRQL < = DISPATCH_LEVEL で実行されます。

Windows 2000 以降のバージョンの Windows で使用できます。

IRQL任意のレベル


## <a name="mmgetmdlpfnarray"></a>**MmGetMdlPfnArray**

定義されている:Wdm

**MmGetMdlPfnArray**マクロは、メモリ記述子リスト (MDL) に関連付けられている物理ページ番号の配列の先頭へのポインターを返します。

_Mdl [in]_

**PMDL**

MDL へのポインター。

**戻り値**

**PPFN_NUMBER**

MDL に関連付けられている物理ページ番号の配列の先頭へのポインター。 配列内のエントリの数は**ADDRESS_AND_SIZE_TO_SPAN_PAGES**(**mmgetmdlvirtualaddress**(_mdl_), **MmGetMdlByteCount**(_mdl_)) です。 各配列要素は、次のように定義されている PFN_NUMBER 型の整数値です。次のようにします。

`cpp typedef ULONG PFN_NUMBER, *PPFN_NUMBER;`

**メモ**配列の内容を変更すると、診断が困難なシステムの問題が発生する可能性があります。 この配列の内容を読み取ったり、変更したりしないことをお勧めします。

ページング可能なメモリの場合、配列の内容は、 [**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)でロックされているバッファーに対してのみ有効です。 非ページプールの場合、配列の内容は、 [**MmBuildMdlForNonPagedPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmbuildmdlfornonpagedpool)、 [**MmAllocatePagesForMdlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatepagesformdlex)、または[**MmAllocatePagesForMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatepagesformdl)で更新された MDL に対してのみ有効です。

MDLs の詳細については、「 [MDLs の使用](using-mdls.md)」を参照してください。

Windows 2000 以降で使用できます。

IRQL任意のレベル


## <a name="mmgetmdlvirtualaddress"></a>**MmGetMdlVirtualAddress**

定義されている:Wdm

**Mmgetmdlvirtualaddress**マクロは、MDL によって記述されるバッファーのベース仮想アドレスを返します。

_Mdl [in]_

**PMDL**

初期仮想アドレスを返すバッファーを記述する MDL へのポインター。

**戻り値**

**PVOID**

## <a name="mmgetmdlvirtualaddress-returns-the-starting-virtual-address-of-the-mdl"></a>**Mmgetmdlvirtualaddress**は、MDL の開始仮想アドレスを返します。

**Mmgetmdlvirtualaddress**は、現在のスレッドコンテキストで必ずしも有効ではない仮想アドレスを返します。 下位レベルのドライバーでは、返された仮想アドレスを使用してメモリにアクセスしたり、特にユーザーメモリ領域にアクセスしたりしないでください。

返されたアドレスは、MDL の物理アドレスエントリのインデックスとして使用され、 [**Maptransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pmap_transfer)に入力できます。

**Mmgetmdlvirtualaddress**の呼び出し元は、任意の IRQL で実行できます。 通常、呼び出し元は IRQL = DISPATCH_LEVEL で実行されています。このルーチンは通常、 **Maptransfer**の_currentva_パラメーターを取得するために呼び出されるためです。

Windows 2000 以降のバージョンの Windows で使用できます。

IRQL任意のレベル


## <a name="mmgetsystemaddressformdlsafe"></a>**MmGetSystemAddressForMdlSafe**

定義されている:Wdm

**MmGetSystemAddressForMdlSafe**マクロは、指定された MDL が記述するバッファーの非ページシステム領域の仮想アドレスを返します。

_Mdl [in]_

**PMDL**

対応するベース仮想アドレスをマップするバッファーへのポインター。

_優先順位 [入力]_

## <a name="mm_page_priority"></a>**Mm_PAGE_PRIORITY**

使用可能な PTE の状態が低い場合に成功の重要度を示す**MM_PAGE_PRIORITY**値を指定します。 優先度の値として**Lowpagepriority**、 **normalpagepriority**、または**highpagepriority**を指定します。 Windows 8 以降では、指定された優先順位値は**Mdlmappingnowrite**または**Mdlmappingnowrite**フラグとビットごとの論理積を持つことができます。

*   **Lowpagepriority**は、システムのリソースが非常に少ない場合にマッピング要求が失敗する可能性があることを示します。 このような状況の例としては、ドライバーがマッピングエラーを処理できる、重要でないネットワーク接続が挙げられます。

*   **Normalpagepriority**は、システムのリソースが不足している場合にマッピング要求が失敗する可能性があることを示します。 このような状況の例としては、重要でないローカルファイルシステムの要求が挙げられます。

*   **Highpagepriority**は、システムで完全にリソースが不足していない限り、マッピング要求が失敗しないようにする必要があることを示します。 このような状況の例として、ドライバーのページングファイルパスが挙げられます。

*   **Mdlmappingnowrite**は、マップされた物理ページが書き込み不可 (読み取り専用) メモリとして構成されることを示します。 Windows 8 以降では、このフラグビットを**MM_PAGE_PRIORITY**値とビットごとの or 演算を実行して、書き込みが無効になるメモリを指定できます。

*   **Mdlmappingnoexecute**は、マップされた物理ページを実行不可メモリとして構成することを示します。 Windows 8 以降では、このフラグビットを**MM_PAGE_PRIORITY**値とビットごとに or 処理して、命令の実行が無効になるメモリを指定することができます。 ベストプラクティスとして、Windows 8 以降のバージョンの Windows 用に記述されたドライバーでは、実行可能メモリが明示的に必要な場合を除き、常に実行なしのメモリを指定する必要があります。

*   **戻り値**

    **PVOID**

    **MmGetSystemAddressForMdlSafe**は、指定された MDL が記述する物理ページをマップする基本システム領域の仮想アドレスを返します。 ページがシステムアドレス空間にマップされていないためにマップしようとして失敗した場合は、 **NULL**が返されます。

このルーチンは、指定された MDL によって記述される物理ページがシステムアドレス空間にまだマップされていない場合、システムアドレス空間にマップします。

プログラムされた i/o (PIO) デバイスのドライバーは、このルーチンを呼び出してユーザーモードのバッファーをマップします。これは、の **>** MDL によって記述され、ユーザーモードの仮想アドレスの範囲に既にマップされている、システムアドレス空間の範囲に割り当てられています。

このルーチンへの入力時に、指定された MDL はロックダウンされている物理ページを記述する必要があります。 ロックダウンされた MDL は、 [**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)、 [**MmBuildMdlForNonPagedPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmbuildmdlfornonpagedpool)、 [**iobuildpartialmdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildpartialmdl)、または[**MmAllocatePagesForMdlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatepagesformdlex)ルーチンを使用して作成できます。

**MmGetSystemAddressForMdlSafe**によって返されるシステムアドレス空間のマッピングが不要になった場合は、解放する必要があります。 マッピングを解放するために必要な手順は、MDL の構築方法によって異なります。 次の4つのケースが考えられます。

*   **MmProbeAndLockPages**ルーチンの呼び出しによって MDL を構築した場合、システムアドレス空間のマッピングを明示的に解放する必要はありません。 代わりに、 [**MmUnlockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunlockpages)ルーチンを呼び出すと、割り当てられている場合はマッピングが解放されます。

*   **MmBuildMdlForNonPagedPool**ルーチンの呼び出しによって MDL が構築された場合、 **MmGetSystemAddressForMdlSafe**は新しいシステムアドレス空間マッピングを作成するのではなく、既存のシステムアドレス空間マッピングを再利用します。 この場合、クリーンアップは必要ありません (つまり、ロックを解除したり、マップを解除したりする必要はありません)。

*   MDL が**Iobuildpartialmdl**ルーチンの呼び出しによって構築されている場合、ドライバーは[**Mmpreparemdlforreuse 利用**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)ルーチンを呼び出すか、または[**iofreemdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreemdl)ルーチンを呼び出して、システムアドレス空間のマッピングを解放する必要があります。

*   **MmAllocatePagesForMdlEx**ルーチンの呼び出しによって MDL がビルドされた場合、ドライバーは**MmUnmapLockedPages**ルーチンを呼び出して、システムアドレス空間のマッピングを解放する必要があります。 **MmGetSystemAddressForMdlSafe**が1つの MDL に対して複数回呼び出された場合、後続の**MmGetSystemAddressForMdlSafe**呼び出しでは、最初の呼び出しで作成されたマッピングが返されます。 このマッピングを解放するには、 **MmUnmapLockedPages**を1回呼び出すだけで十分です。

Windows 7 と Windows Server 2008 R2 以降では、 **MmAllocatePagesForMdlEx**によって作成された MDL の**MmUnmapLockedPages**を明示的に呼び出す必要はありません。 代わりに、 [**Mmfreepagesfrommdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmfreepagesfrommdl)ルーチンを呼び出すと、システムアドレス空間マッピングが割り当てられている場合は解放されます。

新しいシステムアドレス空間マッピングを作成するために、 **MmGetSystemAddressForMdlSafe**は_Cachetype_パラメーターを**Mmcached**に設定して**MmMapLockedPagesSpecifyCache**を呼び出します。 **Mmcached**以外のキャッシュの種類を必要とするドライバーは、 **MmGetSystemAddressForMdlSafe**を呼び出す代わりに、 **MmMapLockedPagesSpecifyCache**を直接呼び出す必要があります。 _Cachetype_パラメーターの詳細については、「 [**MmMapLockedPagesSpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmaplockedpagesspecifycache)」を参照してください。

**MmMapLockedPagesSpecifyCache**の呼び出しでは、指定されたキャッシュの種類は、MDL によって記述されたページにキャッシュの種類がまだ関連付けられていない場合にのみ使用されます。 ただし、ほとんどの場合、ページには既に関連付けられたキャッシュの種類があり、このキャッシュの種類は新しいマッピングによって使用されます。 このルールの例外は、 **MmAllocatePagesForMdl**によって割り当てられたページです。これにより、ページの元のキャッシュの種類に関係なく、キャッシュの種類が**mmcached**に設定されます。

このルーチンは、呼び出し元のスレッドが MDL を所有していると想定しているため、一度に1つのスレッドだけが特定の MDL の**MmGetSystemAddressForMdlSafe**を安全に呼び出すことができます。 ただし、同じスレッドからすべての呼び出しを行うか、複数のスレッドからの呼び出しの場合は、呼び出しを明示的に同期することによって、同じ MDL に対して**MmGetSystemAddressForMdlSafe**を複数回呼び出すことができます。

ドライバーが要求を小さい要求に分割する必要がある場合、ドライバーは追加の MDLs を割り当てることができます。また、ドライバーは**Iobuildpartialmdl**ルーチンを使用できます。

返されるベースアドレスのオフセットは、MDL 内の仮想アドレスと同じです。

Windows 98 では、 **MmGetSystemAddressForMdlSafe**はサポートされていません。 代わりに[**MmGetSystemAddressForMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmgetsystemaddressformdl)を使用してください。

このマクロは[**MmMapLockedPagesSpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmaplockedpagesspecifycache)を呼び出すため、これを使用するには、ntoskrnl.exe へのリンクが必要になることがあります。

Windows 2000 以降で使用できます。

IRQL < = DISPATCH_LEVEL


## <a name="mminitializemdl"></a>**MmInitializeMdl**

定義されている:Wdm

**MmInitializeMdl**マクロは、MDL のヘッダーを初期化します。

_Memory記述子の一覧 [in]_

**PMDL**

MDL として初期化するバッファーへのポインター。 詳細については、次のセクションを参照してください。

_BaseVa [in]_

**PVOID**

バッファーのベース仮想アドレスへのポインター。

_長さ [入力]_

**SIZE_T**

MDL によって記述されるバッファーの長さをバイト単位で指定します。 このルーチンは、MAXULONG バイトの最大バッファー長をサポートしています。

**戻り値**

**無効化**

_Memory記述子のリスト_が指すバッファーは、ページングされていないメモリに割り当てられている必要があります。 このバッファーのサイズ (バイト単位) は、少なくとも**sizeof**(MDL) + **sizeof**(PFN_NUMBER) * **ADDRESS_AND_SIZE_TO_SPAN_PAGES**(_baseva_, _Length_) である必要があります。

Windows 2000 以降のバージョンの Windows で使用できます。

IRQL < = DISPATCH_LEVEL


## <a name="mmpreparemdlforreuse"></a>**MmPrepareMdlForReuse 利用**

定義されている:Wdm

**Mmare Mdlfor再利用**マクロは、部分的な mdl に関連付けられているリソースを解放して、mdl を再利用できるようにします。

_Mdl [in]_

**PMDL**

再利用のために準備される部分的な MDL へのポインター。

**戻り値**

**無効化**

このマクロは、 [**Iobuildpartialmdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildpartialmdl)ルーチンの呼び出しで、 _targetmdl_パラメーターに割り当てられた同じ MDL を繰り返し使用するドライバーによって使用されます。 **Mmpreparemdlforreuse 利用**の呼び出しで、指定された部分的な mdl がシステムアドレス空間に関連付けられているマッピングを持っている場合、 **Mmpreparemdlforreuse 利用**によってマッピングが解放され、MDL を再利用できるようになります。

**Mmare Mdlfor再利用**では、 **Iobuildpartialmdl**によって構築された一部の mdls のみが受け入れられます。 **Mmpreparemdlforreuse 利用**がシステムアドレス空間にマップされているが、 **Iobuildpartialmdl**によって構築されていない MDL を受信した場合、 **Mm/mdlfor再利用**によってマッピングが解放されず、チェックされたビルドでアサーションが失敗します。

部分 MDLs の詳細については、「 [MDLs の使用](using-mdls.md)」を参照してください。

Windows 2000 以降のバージョンの Windows で使用できます。

IRQL < = DISPATCH_LEVEL


## <a name="page_align"></a>**PAGE_ALIGN**

定義されている:Wdm

**PAGE_ALIGN**マクロは、指定された仮想アドレスに対してページを固定した仮想アドレスを返します。

_Va [入力]_

**PVOID**

仮想アドレスへのポインター。

**戻り値**

**PVOID**

## <a name="page_align-returns-a-pointer-to-the-page-aligned-virtual-address"></a>**PAGE_ALIGN**は、ページを固定した仮想アドレスへのポインターを返します。

Windows 2000 以降で使用できます。

IRQL任意のレベル


## <a name="paged_code"></a>**PAGED_CODE**

定義されている:Wdm

**PAGED_CODE**マクロは、呼び出し元のスレッドが、ページングを許可するのに十分な数の IRQL で実行されていることを確認します。

**戻り値**

**無効化**

IRQL > APC_LEVEL の場合、 **PAGED_CODE**マクロによってシステムがアサートされます。

このマクロの呼び出しは、ページング可能なコードを含むか、ページング可能なコードにアクセスするすべてのドライバールーチンの先頭で行う必要があります。

**PAGED_CODE**マクロは、ドライバーコードがマクロを実行するポイントでのみ、IRQL をチェックします。 その後、コードによって IRQL が発生した場合、マクロはこの変更を検出しません。 ドライバー開発者は、ドライバールーチンの実行中に IRQL が不適切に発生したことを検出するために、[静的ドライバー検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)と[ドライバー検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)を使用する必要があります。

**PAGED_CODE**マクロは、チェックされたビルドでのみ機能します。

Windows 2000 以降で使用できます。


## <a name="paged_code_locked"></a>**PAGED_CODE_LOCKED**

定義されている:Wdm

**PAGED_CODE_LOCKED**マクロは、現在実行中のコードセクションがページング可能であり、実行される前にメモリにロックされている必要があることをアサートします。

**戻り値**

**無効化**

ページング可能なコードは、ロックされていない限り、特定の制限 (IRQL < = APC_LEVEL など) に従う必要があります。 正常に動作するために適切にロックする必要があるページング可能なルーチンは、 **PAGED_CODE_LOCKED**の呼び出しから開始する必要があります。

コードセクションを適切にロックする方法の詳細については、「ページング可能な[コードまたはデータのロック](locking-pageable-code-or-data.md)」を参照してください。


## <a name="posetdevicebusy"></a>**PoSetDeviceBusy**

定義されている:Wdm

**Posetdevicebusy**マクロは、 _IdlePointer_に関連付けられているデバイスがビジー状態であることを[電源マネージャー](power-manager.md)に通知します。

_IdlePointer [in, out]_

**このように**

以前に[**PoRegisterDeviceForIdleDetection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-poregisterdeviceforidledetection)によって返された**NULL**以外のアイドルポインターを指定します。 **PoRegisterDeviceForIdleDetection**は**NULL**ポインターを返す場合があることに注意してください。 **Posetdevicebusy**の呼び出し元は、ポインターが**NULL**でないことを確認してから**posetdevicebusy**に渡す必要があります。

**戻り値**

**無効化**

**メモ**[**PoSetDeviceBusyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-posetdevicebusyex)ルーチンは、 **Posetdevicebusy**マクロを直接置換したものです。 Windows Vista Service Pack 1 (SP1) 以降のバージョンの Windows 用の新しいドライバーコードを作成する場合は、 **Posetdevicebusy**ではなく**PoSetDeviceBusyEx**を呼び出します。

ドライバーは、 **Posetdevicebusy**と**PoRegisterDeviceForIdleDetection**を使用して、デバイスのシステムアイドル検出を有効にします。 アイドル検出用に登録されているデバイスがアイドル状態になると、電源マネージャーは[**IRP_MN_SET_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)要求を送信して、要求されたスリープ状態にデバイスを配置します。

**Posetdevicebusy**は、デバイスがビジー状態であることを報告し、電源マネージャーがアイドル状態のカウントダウンを再開できるようにします。 デバイスの電源が入っていない場合、 **Posetdevicebusy**はその状態を変更しません。 つまり、システムが電源オン要求を送信することはありません。

ドライバーは、すべての i/o 要求で**Posetdevicebusy**を呼び出す必要があります。

Windows 2000 以降で使用できます。

IRQL任意のレベル


## <a name="psgetcurrentprocess"></a>**PsGetCurrentProcess**

定義されている:Ntddk

現在のスレッドのプロセスへのポインターを返します。

**戻り値**

不透明なプロセスオブジェクトへのポインター。



Windows 2000 以降で使用できます。

IRQL任意のレベル


## <a name="read_register_buffer_ulong64"></a>**READ_REGISTER_BUFFER_ULONG64**

定義されている:Wdm

**READ_REGISTER_BUFFER_ULONG64**マクロは、指定されたレジスタアドレスから多数の ULONG64 値をバッファーに読み込みます。

_レジスタ [in]_

**PULONG64**

レジスタへのポインター。これは、メモリ空間内のマップされた範囲である必要があります。

_Buffer [out]_

**PULONG64**

ULONG64 値の配列が読み込まれるバッファーへのポインター。

_カウント [入力]_

**ULONG**

バッファーに読み込む ULONG64 値の数を指定します。

**戻り値**

**無効化**

_バッファー_バッファーのサイズは、少なくとも指定した数の ULONG64 値を格納するのに十分な大きさである必要があります。

**READ_REGISTER_BUFFER_ULONG64**マクロの呼び出し元は、_バッファー_バッファーが常駐し、_レジスタ_レジスタが常駐し、マップされたデバイスメモリであることを前提として、任意の IRQL で実行できます。

64ビットバージョンの Windows でのみ使用できます。

IRQL任意のレベル


## <a name="read_register_ulong64"></a>**READ_REGISTER_ULONG64**

定義されている:Wdm

**READ_REGISTER_ULONG64**マクロは、指定されたレジスタアドレスから ULONG64 値を読み取ります。

_volatile * レジスタ [in]_

**ULONG64**

レジスタアドレスへのポインター。これは、メモリ空間内のマップされた範囲である必要があります。

**戻り値**

**ULONG64**

**READ_REGISTER_ULONG64**は、指定されたレジスタアドレスから読み取られた ULONG64 値を返します。

**READ_REGISTER_ULONG64**マクロの呼び出し元は、_レジスタ_アドレスが常駐、マップされたデバイスメモリであることを前提として、任意の IRQL で実行できます。

64ビットバージョンの Windows でのみ使用できます。

IRQL任意のレベル


## <a name="round_to_pages"></a>**ROUND_TO_PAGES**

定義されている:Wdm

**ROUND_TO_PAGES**マクロはバイト単位のサイズを取得し、次の完全なページに切り上げます。

_サイズ [入力]_

**ULONG_PTR**

複数のページに切り上げたサイズをバイト単位で指定します。

**戻り値**

**ULONG_PTR**

**ROUND_TO_PAGES**は、現在のプラットフォームの仮想メモリページサイズの倍数に切り上げられた入力サイズを返します。

**ROUND_TO_PAGES**の呼び出し元は、任意の IRQL で実行できます。 呼び出し元は、指定されたパラメーターがメモリオーバーフローを発生させることができないようにする必要があります。

IRQL任意のレベル


## <a name="rtlequalluid"></a>**RtlEqualLuid**

定義されている:Wdm

**戻り値**

Windows 2000 以降で使用できます。

IRQL任意のレベル


## <a name="rtlinitemptyansistring"></a>**RtlInitEmptyAnsiString**

定義されている:Wdm

**RtlInitEmptyAnsiString**マクロは、空のカウントされた ANSI 文字列を初期化します。

_DestinationString [out]_

**PANSI_STRING**

初期化される[**ANSI_STRING**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_string)構造体へのポインター。

_バッファー [入力]_

**PCHAR**

WCHAR 文字列を格納するために使用される、呼び出し元に割り当てられたバッファーへのポインター。

_BufferSize [in]_

**USHORT**

_バッファー_が指すバッファーの長さ (バイト単位)。

**戻り値**

**無効化**

_Destinationstring_パラメーターが指す構造体のメンバーは、次のように初期化されます。

*   **長さ**。 回.

*   **Maximumlength**。 _BufferSize_。

*   **バッファー**。 _Sourcestring_。

空でないカウントされた Unicode 文字列を初期化するには、 [**RtlInitAnsiString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlinitansistring)を呼び出します。

Microsoft Windows XP 以降のバージョンの Windows で使用できます。

IRQL任意のレベル


## <a name="rtlinitemptyunicodestring"></a>**RtlInitEmptyUnicodeString**

定義されている:Wdm

**RtlInitEmptyUnicodeString**マクロは、空のカウントされた Unicode 文字列を初期化します。

_DestinationString [out]_

**PUNICODE_STRING**

初期化される[**UNICODE_STRING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/ns-wudfwdm-_unicode_string)構造体へのポインター。

_バッファー [入力]_

**PWCHAR**

WCHAR 文字列を格納するために使用される、呼び出し元に割り当てられたバッファーへのポインター。

_BufferSize [in]_

**USHORT**

_バッファー_が指すバッファーの長さ (バイト単位)。

**戻り値**

**無効化**

_Destinationstring_パラメーターが指す構造体のメンバーは、次のように初期化されます。

*   **長さ**。 回.

*   **Maximumlength**。 _BufferSize_。

*   **バッファー**。 _Sourcestring_。

空でないカウントされた Unicode 文字列を初期化するには、 [**RtlInitUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlinitunicodestring)を呼び出します。

Windows XP 以降で使用できます。

IRQL任意のレベル


## <a name="rtliszeroluid"></a>**RtlIsZeroLuid**

定義されている:Ntddk

**RtlIsZeroLuid**マクロは、指定された luid が 0 luid であるかどうかを判断します。

_L1 [in]_

**PLUID**

確認する[**LUID**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_luid)を指定します。

**戻り値**

**演算**

**RtlIsZeroLuid**は、 _L1_が0の場合は**TRUE**を返し、それ以外の場合は**FALSE**を返します。

IRQL任意のレベル


## <a name="rtlretrieveulong"></a>**RtlRetrieveUlong**

定義されている:Wdm

**RtlRetrieveUlong**マクロは、ソースアドレスから ULONG 値を取得し、アラインメントエラーを回避します。 宛先アドレスは、アラインされていると見なされます。

_DestinationAddress [out]_

**このように**

ULONG 値を格納する、ULONG でアラインメントされた場所へのポインター。

_SourceAddress [in]_

**このように**

ULONG 値の取得元の場所へのポインター。

**戻り値**

**無効化**

指定されたアドレスが非ページプールに存在する場合、 **RtlRetrieveUlong**の呼び出し元は任意の IRQL で実行できます。 それ以外の場合、呼び出し元は IRQL < = APC_LEVEL で実行されている必要があります。

Windows 2000 以降のバージョンの Windows で使用できます。


## <a name="rtlretrieveushort"></a>**RtlRetrieveUshort**

定義されている:Wdm

**RtlRetrieveUshort**マクロは、ソースアドレスから USHORT 値を取得し、アラインメントエラーを回避します。

_DestinationAddress [out]_

**PUSHORT**

値を格納する USHORT 位置に配置された位置を指すポインター。

_SourceAddress [in]_

**PUSHORT**

値の取得元の場所へのポインター。

**戻り値**

**無効化**

指定されたアドレスが非ページプールに存在する場合、 **RtlRetrieveUshort**の呼び出し元は任意の IRQL で実行できます。 それ以外の場合、呼び出し元は IRQL < = APC_LEVEL で実行されている必要があります。

Windows 2000 以降のバージョンの Windows で使用できます。

IRQL任意のレベル


## <a name="rtlstoreulong"></a>**RtlStoreUlong**

定義されている:Wdm

**RtlStoreUlong**マクロは、特定のアドレスに ULONG 値を格納し、アラインメントエラーを回避します。

_アドレス [out]_

**このように**

指定された ULONG 値を格納する場所へのポインター。

_値 [入力]_

**ULONG**

格納する ULONG 値を指定します。

**戻り値**

**無効化**

_アドレス_が非ページプールを指している場合、呼び出し元は任意の IRQL で実行できます。 それ以外の場合、呼び出し元は IRQL < = APC_LEVEL で実行されている必要があります。

Windows 2000 以降のバージョンの Windows で使用できます。

IRQL任意のレベル


## <a name="rtlstoreulonglong"></a>**RtlStoreUlonglong**

定義されている:Wdm

**RtlStoreUlonglong**マクロは、指定された ULONGLONG 値を指定されたメモリアドレスに格納し、メモリアラインメントエラーを回避します。

_アドレス [out]_

**PULONGLONG**

指定された ULONGLONG 値を格納する場所へのポインター。

_値 [入力]_

**ULONGLONG**

格納される ULONGLONG 値。

**戻り値**

**無効化**

**RtlStoreUlonglong**は、メモリアラインメントエラーを回避します。 _アドレス_によって指定されたアドレスが ULONGLONG のストレージ要件に適合しない場合、 **RtlStoreUlonglong**はメモリ位置 (puchar)_アドレス_で始まる_値_のバイトを格納します。

**RtlStoreUlonglong**は、_アドレス_が非ページプールを指している場合、任意の IRQL で実行されます。それ以外の場合は、IRQL < = APC_LEVEL で実行する必要があります。

Windows 2000 以降で使用できます。

IRQL任意のレベル


## <a name="rtlstoreulongptr"></a>**RtlStoreUlongPtr**

定義されている:Wdm

**RtlStoreUlongPtr**マクロは、指定された ULONG_PTR 値を指定されたメモリ位置に格納し、メモリアラインメントエラーを回避します。

_アドレス [out]_

**PULONG_PTR**

ULONG_PTR 値を格納する場所へのポインター。

_値 [入力]_

**ULONG_PTR**

格納する ULONG_PTR 値を指定します。

**戻り値**

**無効化**

**RtlStoreUlongPtr**は、メモリアラインメントエラーを回避します。 _Address_の値が ULONG_PTR のストレージ要件に一致しない場合、 **RtlStoreUlongPtr**はメモリ位置 (puchar)_アドレス_で始まる_値_のバイトを格納します。

**RtlStoreUlongPtr**は、_アドレス_が非ページプールを指している場合、任意の IRQL で実行されます。それ以外の場合は、IRQL < = APC_LEVEL で実行する必要があります。

Windows 2000 以降のバージョンの Windows で使用できます。

IRQL任意のレベル


## <a name="rtlstoreushort"></a>**RtlStoreUshort**

定義されている:Wdm

**Rtlstoreushort**マクロは、特定のアドレスに USHORT 値を格納し、アラインメントエラーを回避します。

_アドレス [out]_

**PUSHORT**

指定した USHORT 値を格納する場所へのポインター。

_値 [入力]_

**USHORT**

格納する USHORT 値を指定します。

**戻り値**

**無効化**

_アドレス_が非ページプールを指している場合、呼び出し元は任意の IRQL で実行できます。 それ以外の場合、呼び出し元は IRQL < = APC_LEVEL で実行されている必要があります。

Windows 2000 以降のバージョンの Windows で使用できます。

IRQL任意のレベル


## <a name="write_register_buffer_ulong64"></a>**WRITE_REGISTER_BUFFER_ULONG64**

定義されている:Wdm

**WRITE_REGISTER_BUFFER_ULONG64**マクロは、バッファーから指定されたレジスタに多数の ULONG64 値を書き込みます。

_レジスタ [in]_

**PULONG64**

レジスタへのポインター。これは、メモリ空間内のマップされた範囲である必要があります。

_バッファー [入力]_

**PULONG64**

ULONG64 値の配列が書き込まれるバッファーへのポインター。

_カウント [入力]_

**ULONG**

レジスタに書き込まれる ULONG64 値の数を指定します。

**戻り値**

**無効化**

_バッファー_バッファーのサイズは、少なくとも指定した数の ULONG64 値を格納するのに十分な大きさである必要があります。

**WRITE_REGISTER_BUFFER_ULONG64**マクロの呼び出し元は、_バッファー_バッファーが常駐し、_レジスタ_レジスタが常駐し、マップされたデバイスメモリであることを前提として、任意の IRQL で実行できます。

64ビットバージョンの Windows でのみ使用できます。

IRQL任意のレベル


## <a name="write_register_ulong64"></a>**WRITE_REGISTER_ULONG64**

定義されている:Wdm

**WRITE_REGISTER_ULONG64**マクロは、指定されたアドレスに ULONG64 値を書き込みます。

_volatile * レジスタ [in]_

**ULONG64**

レジスタへのポインター。これは、メモリ空間内のマップされた範囲である必要があります。

_値 [入力]_

**ULONG64**

レジスタに書き込む ULONG64 値を指定します。

**戻り値**

**無効化**

**WRITE_REGISTER_ULONG64**マクロの呼び出し元は、_レジスタ_レジスタが常駐し、マップされたデバイスメモリであると仮定して、任意の IRQL で実行できます。

64ビットバージョンの Windows でのみ使用できます。

IRQL任意のレベル


## <a name="zwcurrentprocess"></a>**ZwCurrentProcess**

定義されている:Wdm

**Zwcurrentprocess**マクロは、現在のプロセスのハンドルを返します。

**戻り値**

**扱え**

**Zwcurrentprocess**は、現在のプロセスを表す特別なハンドル値を返します。

戻り値は真のハンドルではありませんが、常に現在のプロセスを表す特別な値です。

**Ntcurrentprocess**と**zwcurrentprocess**は、同じ Windows ネイティブシステムサービスルーチンの2つのバージョンです。 Windows カーネルの**Ntcurrentprocess**ルーチンは、カーネルモードドライバーに直接アクセスすることはできません。 ただし、カーネルモードドライバーは、 **Zwcurrentprocess**を呼び出すことによって、このルーチンに間接的にアクセスできます。

カーネルモードドライバーからの呼び出しの場合、 **Nt_Xxx_** および**Zw_Xxx_** バージョンの Windows ネイティブシステムサービスルーチンは、入力パラメーターを処理して解釈する方法とは動作が異なります。 ルーチンの**Nt_Xxx_** バージョンと**Zw_Xxx_** バージョンの関係の詳細については、「 [Using Nt And Zw Versions Of the Native System Services ルーチン](using-nt-and-zw-versions-of-the-native-system-services-routines.md)」を参照してください。

サポートされているすべてのオペレーティングシステム。

IRQL任意のレベル


## <a name="zwcurrentthread"></a>**ZwCurrentThread**

定義されている:Wdm

**Zwcurrentthread**マクロは、現在のスレッドへのハンドルを返します。

**戻り値**

**扱え**

**Zwcurrentthread**は、現在のスレッドを表す特別なハンドル値を返します。

戻り値は真のハンドルではありませんが、常に現在のスレッドを表す特別な値です。

**Ntcurrentthread**と**zwcurrentthread**は、同じ Windows ネイティブシステムサービスルーチンの2つのバージョンです。 Windows カーネルの**Ntcurrentthread**ルーチンは、カーネルモードドライバーに直接アクセスすることはできません。 ただし、カーネルモードドライバーは、 **Zwcurrentthread**ルーチンを呼び出すことによって、このルーチンに間接的にアクセスできます。

カーネルモードドライバーからの呼び出しの場合、 **Nt_Xxx_** および**Zw_Xxx_** バージョンの Windows ネイティブシステムサービスルーチンは、入力パラメーターを処理して解釈する方法とは動作が異なります。 ルーチンの**Nt_Xxx_** バージョンと**Zw_Xxx_** バージョンの関係の詳細については、「 [Using Nt And Zw Versions Of the Native System Services ルーチン](using-nt-and-zw-versions-of-the-native-system-services-routines.md)」を参照してください。

サポートされているすべてのオペレーティングシステム。

IRQL任意のレベル










