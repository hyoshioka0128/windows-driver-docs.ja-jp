---
title: Windows カーネル マクロ
description: Windows カーネル マクロ
ms.assetid: 91366400-3307-4F13-A839-50BA85B7F73E
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cc92a84d8af5cf9d5b9752633e34c1ebdbf49dbc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559174"
---
# <a name="windows-kernel-macros"></a>Windows カーネル マクロ


次の一覧には、Windows カーネルのマクロが含まれています。


## <a name="addressandsizetospanpages"></a>**ADDRESS_AND_SIZE_TO_SPAN_PAGES**

定義されています。Wdm.h

**ADDRESS_AND_SIZE_TO_SPAN_PAGES**マクロは、仮想アドレスと転送要求のバイト単位のサイズによって定義されている仮想アドレスの範囲のページの数を返します。

_Va [in]_

**PVOID**

範囲のベースである仮想アドレスへのポインター。

_[In] のサイズ_

**ULONG**

譲渡要求のバイト単位のサイズを指定します。

**戻り値**

**ULONG**

**ADDRESS_AND_SIZE_TO_SPAN_PAGES**で仮想アドレスの範囲の開始により展開されるページの数を返します_Va_します。

呼び出す DMA の転送を行うドライバー **ADDRESS_AND_SIZE_TO_SPAN_PAGES**転送要求をデバイス DMA 操作のシーケンスに分割する必要があるかどうかを判断します。

ドライバーは、システム定義の定数 PAGE_SIZE を使用して、転送されるバイト数が、現在のプラットフォームの仮想メモリのページ サイズより小さいかどうかを判断できます。

呼び出し元**ADDRESS_AND_SIZE_TO_SPAN_PAGES** IRQL で実行されていることができます。 呼び出し元は、指定されたパラメーターには、メモリのオーバーフローが発生しないことを確認する必要があります。

Windows 2000 以降を使用できます。


## <a name="byteoffset"></a>**BYTE_OFFSET**

定義されています。Wdm.h

**BYTE_OFFSET**マクロ仮想アドレスを受け取り、ページ内でそのアドレスのバイト オフセットを返します。

_Va [in]_

**PVOID**

仮想アドレスへのポインター。

**戻り値**

**ULONG**

**BYTE_OFFSET**仮想アドレスのオフセットの部分を返します。

Windows 2000 以降を使用できます。

IRQL:任意のレベル


## <a name="bytestopages"></a>**BYTES_TO_PAGES**

定義されています。Wdm.h

**BYTES_TO_PAGES**マクロ転送要求のバイト単位のサイズを受け取るし、バイトを格納するために必要なページ数を計算します。

_[In] のサイズ_

**ULONG**

譲渡要求のバイト単位のサイズを指定します。

**戻り値**

**ULONG**

**BYTES_TO_PAGES**に指定したバイト数を含めることが必要なページの数を返します。

転送バイト数で指定された長さが現在のプラットフォームの仮想メモリのページ サイズより小さいかどうかを確認するのには、システム定義の定数 PAGE_SIZE を使用できます。

Windows 2000 以降を使用できます。

IRQL:任意のレベル


## <a name="containingrecord"></a>**CONTAINING_RECORD**

定義されています。Ntdef.h

**CONTAINING_RECORD**マクロは、構造体の型とフィールド内に、包含構造体のアドレス指定構造のインスタンスのベース アドレスを返します。

_[In] アドレスします。_

**PCHAR**

型の構造体のインスタンス内のフィールドへのポインター_型_します。

_[In] 入力します。_

**型**

ベース アドレスが返される構造体の型の名前。

_[In] フィールド_

**PCHAR**

によって示されるフィールドの名前_アドレス_は型の構造体に含まれている_型_します。

**戻り値**

**PCHAR**

格納する構造体の基本のアドレスを返して_フィールド_します。

型を持つが、呼び出し元が、このような構造内のフィールドのポインターと呼ばれる構造のベース アドレスを確認するには、呼び出されます。 このマクロは、シンボリック既知の型の構造体の他のフィールドにアクセスするために便利です。

Windows 2000 以降を使用できます。

IRQL:任意のレベル


## <a name="ioskipcurrentirpstacklocation"></a>**IoSkipCurrentIrpStackLocation**

定義されています。Wdm.h

\nThe **IoSkipCurrentIrpStackLocation**マクロの変更、システムの[ **IO_STACK_LOCATION** ](https://msdn.microsoft.com/library/windows/hardware/ff550659)できるように、現在のドライバーが次の下位のドライバーを呼び出すときに、ポインターの配列、そのドライバーが、同じ受信**IO_STACK_LOCATION**現在のドライバーを受信した構造体。

_Irp [で, out]_

**PIRP**

IRP へのポインター。

**戻り値**

**VOID**

ドライバーを呼び出すことができます、ドライバーは IRP を次の下位ドライバーに送信するときに**IoSkipCurrentIrpStackLocation**を提供する予定がない場合、 [ _IoCompletion_ ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチン(ドライバーの内のアドレスが格納されている[ **IO_STACK_LOCATION** ](https://msdn.microsoft.com/library/windows/hardware/ff550659)構造)。 呼び出す場合**IoSkipCurrentIrpStackLocation**呼び出す前に[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)、次の下位のドライバーを受け取る同じ**IO_STACK_LOCATION** 、ドライバーを受信します。

使用する場合、 _IoCompletion_ IRP の日常的なドライバー、呼び出す必要があります[ **IoCopyCurrentIrpStackLocationToNext** ](https://msdn.microsoft.com/library/windows/hardware/ff548387)の代わりに**IoSkipCurrentIrpStackLocation**します。 不完全なドライバーが呼び出し元の間違いを行った場合**IoSkipCurrentIrpStackLocation**完了ルーチンを設定し、このドライバーは、下にあるドライバーによって設定完了ルーチンを上書き可能性があります。

ドライバーを呼び出していない場合、ドライバーは IRP を保留には、 **IoSkipCurrentIrpStackLocation** IRP [次へ] の下のドライバーに渡す前にします。 ドライバーを呼び出す場合**IoSkipCurrentIrpStackLocation**で [次へ] の下のドライバーに渡す前に保留 IRP、SL_PENDING_RETURNED フラグが設定、**コントロール**I/O スタックの場所のメンバー[次へ] のドライバーです。 次のドライバーでは、場所スタックが作成され、変更を所有している、ため、可能性のある保留中フラグをクリアするでした。 オペレーティング システムのバグ チェックがまたはが完了しない IRP の処理を発行するような場合があります。

代わりに、保留 IRP がドライバーを呼び出す必要があります**IoCopyCurrentIrpStackLocationToNext**呼び出し前に次の下位のドライバーの新しいスタックの場所を設定するのには**保留**します。

ドライバーを呼び出す場合**IoSkipCurrentIrpStackLocation**しないように注意を変更することで、 **IO_STACK_LOCATION**下位のドライバーまたはシステムの動作に影響を与える意図しない方法で構造体に関しては、そのドライバー。 例としては、変更、 **IO_STACK_LOCATION**構造体の**パラメーター**共用体、または呼び出し元[ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)します。

Windows 2000 以降を使用できます。

IRQL:任意のレベル


## <a name="keinitializecallbackrecord"></a>**KeInitializeCallbackRecord**

定義されています。Wdm.h

**KeInitializeCallbackRecord**マクロを初期化します、 [ **KBUGCHECK_CALLBACK_RECORD** ](https://msdn.microsoft.com/library/windows/hardware/ff551853)または[ **KBUGCHECK_REASON_CALLBACK_レコード**](https://msdn.microsoft.com/library/windows/hardware/ff551873)構造体。

_[In] CallbackRecord_

**PKBUGCHECK_CALLBACK_RECORD**

いずれかへのポインターを**KBUGCHECK_CALLBACK_RECORD**または**KBUGCHECK_REASON_CALLBACK_RECORD**構造体。 構造体は、非ページ プールなどのメモリでなければなりません。

**戻り値**

**VOID**

Windows 2000 および以降のバージョンの Windows で使用できます。

IRQL:任意のレベル


## <a name="mmbadpointer"></a>**MM_BAD_POINTER**

定義されています。Wdm.h

ドライバーを使用できる、 **MM_BAD_POINTER**が初期化されていないか、無効になったポインター変数に代入するの無効なポインター値としてマクロ。 この無効なポインター変数が指すメモリ位置へのアクセスには、バグ チェックが発生します。

多くのハードウェア プラットフォームでは、アドレス 0 (頻繁に名前付き定数として表される**NULL**)、無効なアドレスですが、ドライバー開発者向けでは、アドレス 0 がユニバーサル無効であるすべてのプラットフォームでは想定しないでください。 変数アドレス 0 が常とは限りません不適切なアクセスこれらのポインターからが検出される初期化されていないか、無効なポインターを設定します。

これに対して、値**MM_BAD_POINTER**ドライバーが実行されているすべてのプラットフォームのアドレスが無効にすることが保証されます。

アクセスするドライバーをどのアドレス 0 は、無効なアドレスのプラットフォームでは、アドレスの IRQL で 0 < DISPATCH_LEVEL によって誤ってキャッチできる例外 (アクセス違反) が発生した、`try/except`ステートメント。 したがって、ドライバーの例外処理コードは、無効なアクセスをマスクし、デバッグ中に検出されているを防ぐこと。 ただしのアクセス、 **MM_BAD_POINTER**アドレス例外ハンドラーによってマスクできませんバグ チェックが発生することが保証されます。

次のコード例は、値を割り当てる方法を示しています。 **MM_BAD_POINTER**というポインター変数に`ptr`します。 Ntdef.h ヘッダー ファイルへのポインターを PUCHAR 型を定義する、`unsigned char`します。

`PUCHAR ptr = (PUCHAR)MM_BAD_POINTER; // Now _ptr is guaranteed to fault._`

後`ptr`に設定されている**MM_BAD_POINTER**、によって示されるメモリ位置へのアクセスに`ptr`バグ チェックが発生します。

実際、 **MM_BAD_POINTER**は無効なアドレスのページ全体のベース アドレスです。 そのため、すべてのアクセス、アドレス範囲内の**MM_BAD_POINTER**に (**MM_BAD_POINTER** + **PAGE_SIZE** - 1) バグ チェックが発生します。

Windows 8.1 では、以降、 **MM_BAD_POINTER** Wdm.h のヘッダー ファイルでマクロが定義されています。 ただし、Windows Vista と共に登場した Windows の以前のバージョンでこのマクロの定義を使用するドライバー コードできます実行。

以降、Windows Vista では、 [ **MmBadPointer** ](https://msdn.microsoft.com/library/windows/hardware/ff554494)グローバル変数は、アドレスが無効にすることが保証されるポインター値へのポインターとして使用します。 ただし、Windows 8.1 での使用を開始**MmBadPointer**は非推奨とし、使用するドライバーを更新する必要があります、 **MM_BAD_POINTER**マクロ代わりにします。

Windows 8.1\ 以降を利用できます。 Windows Vista と共に登場した Windows の以前のバージョンとの互換性 _。


## <a name="mmgetmdlbytecount"></a>**MmGetMdlByteCount**

定義されています。Wdm.h

**MmGetMdlByteCount**マクロは、指定した MDL で説明されているバッファーのバイト単位で長さを返します。

_[In] Mdl_

**PMDL**

ポインター、 [ **MDL** ](https://msdn.microsoft.com/library/windows/hardware/ff554414)物理メモリ内の仮想メモリ バッファーのレイアウトを記述する構造体。 詳細については、次を参照してください。[を使用して MDLs](using-mdls.md)します。

**戻り値**

**ULONG**

## <a name="mmgetmdlbytecount-returns-the-length-in-bytes-of-the-buffer-described-by-mdl"></a>**MmGetMdlByteCount**で説明されているバッファーのバイト単位の長さを返します_Mdl_します。

呼び出し元**MmGetMdlByteCount** IRQL で実行されていることができます。 通常、呼び出し元が IRQL で実行している < = DISPATCH_LEVEL します。

Windows 2000 以降を使用できます。

IRQL:任意のレベル


## <a name="mmgetmdlbyteoffset"></a>**MmGetMdlByteOffset**

定義されています。Wdm.h

**MmGetMdlByteOffset**マクロは、特定の MDL で説明されているバッファーの最初のページ内のバイト オフセットを返します。

_[In] Mdl_

**PMDL**

MDL へのポインター。

**戻り値**

**ULONG**

## <a name="mmgetmdlbyteoffset-returns-the-offset-in-bytes"></a>**MmGetMdlByteOffset**オフセットをバイト単位で返します。

呼び出し元**MmGetMdlByteOffset** IRQL で実行されていることができます。 通常、呼び出し元が IRQL で実行している < = DISPATCH_LEVEL します。

Windows 2000 および以降のバージョンの Windows で使用できます。

IRQL:任意のレベル


## <a name="mmgetmdlpfnarray"></a>**MmGetMdlPfnArray**

定義されています。Wdm.h

**MmGetMdlPfnArray**マクロは、メモリの記述子のリスト (MDL) に関連付けられている物理ページ番号の配列の先頭にポインターを返します。

_[In] Mdl_

**PMDL**

MDL へのポインター。

**戻り値**

**PPFN_NUMBER**

MDL に関連付けられている物理ページ番号の配列の先頭へのポインター。 配列内のエントリの数が**ADDRESS_AND_SIZE_TO_SPAN_PAGES**(**MmGetMdlVirtualAddress**(_Mdl_)、 **MmGetMdlByteCount**(_Mdl_))。 配列の各要素は、型で定義されている、PFN_NUMBER の整数値を示します。次のように Wdm.h:

`cpp typedef ULONG PFN_NUMBER, *PPFN_NUMBER;`

**注**配列の内容を変更すると、診断が困難な微妙なシステム問題が発生することができます。 読み取り使用したり、この配列の内容を変更するはしないをお勧めします。

ページング可能なメモリは、配列の内容はロックされているバッファーでのみ有効です[ **MmProbeAndLockPages**](https://msdn.microsoft.com/library/windows/hardware/ff554664)します。 非ページ プールは、配列の内容は更新 MDL のみ有効です[ **MmBuildMdlForNonPagedPool**](https://msdn.microsoft.com/library/windows/hardware/ff554498)、 [ **MmAllocatePagesForMdlEx**](https://msdn.microsoft.com/library/windows/hardware/ff554489)、または[ **MmAllocatePagesForMdl**](https://msdn.microsoft.com/library/windows/hardware/ff554482)します。

MDLs の詳細については、次を参照してください。[を使用して MDLs](using-mdls.md)します。

Windows 2000 以降を使用できます。

IRQL:任意のレベル


## <a name="mmgetmdlvirtualaddress"></a>**MmGetMdlVirtualAddress**

定義されています。Wdm.h

**MmGetMdlVirtualAddress**マクロが、MDL で説明されているバッファーの基本の仮想アドレスを返します。

_[In] Mdl_

**PMDL**

最初の仮想アドレスを返すバッファーを記述する MDL へのポインター。

**戻り値**

**PVOID**

## <a name="mmgetmdlvirtualaddress-returns-the-starting-virtual-address-of-the-mdl"></a>**MmGetMdlVirtualAddress** MDL の開始仮想アドレスを返します。

**MmGetMdlVirtualAddress**現在のスレッド コンテキストで有効である必要はない仮想アドレスを返します。 下位レベルのドライバーが、返された仮想アドレスを使用して、メモリ、特にメモリ領域をユーザーにアクセスしないようにします。

MDL 内の物理アドレス エントリのインデックスとして使用される、返されたアドレスを入力できる[ **MapTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff554402)します。

呼び出し元**MmGetMdlVirtualAddress** IRQL で実行されていることができます。 IRQL で呼び出し元が実行されている通常は、このルーチンが取得するというよく = DISPATCH_LEVEL、 _CurrentVa_パラメーターを**MapTransfer**します。

Windows 2000 および以降のバージョンの Windows で使用できます。

IRQL:任意のレベル


## <a name="mmgetsystemaddressformdlsafe"></a>**MmGetSystemAddressForMdlSafe**

定義されています。Wdm.h

**MmGetSystemAddressForMdlSafe**マクロは、指定した MDL 説明するバッファーの非ページ システム領域仮想アドレスを返します。

_[In] Mdl_

**PMDL**

対応する基本仮想アドレスにマップするバッファーへのポインター。

_[In] の優先順位_

## <a name="mmpagepriority"></a>**Mm_PAGE_PRIORITY**

指定します、 **MM_PAGE_PRIORITY**低使用可能な PTE 条件下で成功した場合の重要度を示す値。 優先度の値を指定**LowPagePriority**、 **NormalPagePriority**、または**HighPagePriority**します。 Windows 8 以降では、指定した優先順位値はビットごとの論理和。 で、 **MdlMappingNoWrite**または**MdlMappingNoExecute**フラグ。

*   **LowPagePriority**マッピング要求が、システムがリソースに対してかなり少ない場合にフェールオーバーできることを示します。 このような状況の例は、ドライバーがマッピング エラーを処理できる重要でないネットワーク接続です。

*   **NormalPagePriority**マッピング要求が、システムがリソースに非常に低い場合にフェールオーバーできることを示します。 このような状況の例は、重要でないローカル ファイル システム要求です。

*   **HighPagePriority**マッピング要求する必要がありますしない限り、システムがリソース不足が完全に失敗しないことを示します。 このような状況の例では、ドライバーではページング ファイルのパスです。

*   **MdlMappingNoWrite**マップされた物理ページがメモリの非書き込み (読み取り専用) として構成することを示します。 Windows 8 以降、このフラグのビットできるビットごとの論理和。 で、 **MM_PAGE_PRIORITY**書き込みが無効になってメモリを指定する値。

*   **MdlMappingNoExecute**マップされた物理ページ メモリの非実行するように構成されていることを示します。 Windows 8 以降、このフラグのビットできるビットごとの論理和。 で、 **MM_PAGE_PRIORITY**する命令の実行が無効になっているメモリを指定する値。 ベスト プラクティス、Windows 8 および Windows の以降のバージョンのドライバーを指定する必要があります常に非実行メモリ実行可能なメモリが明示的に必要な場合を除き、します。

*   **戻り値**

    **PVOID**

    **MmGetSystemAddressForMdlSafe**指定 MDL が表す物理的なページをマップするシステムの基本領域仮想アドレスを返します。 システム アドレス空間は、失敗した場合、それらをマップしようとすると、ページが既にマップされていない場合**NULL**が返されます。

このルーチンでは、システム アドレス空間にマップされていない場合、システムのアドレス空間に指定された MDL によって記述される物理的なページがマップされます。

プログラミング i/o (PIO) デバイスのドライバーで MDL によって定義された、ユーザー モードのバッファーをマップするには、このルーチンを呼び出す**Irp MdlAddress]-> [** システム アドレスの範囲に、ユーザー モード仮想アドレスの範囲に既にマップされて、領域。

このルーチンの入り口で指定された MDL ロック ダウンされている物理ページを記述します。 使用してロックダウン MDL をビルドすることができます、 [ **MmProbeAndLockPages**](https://msdn.microsoft.com/library/windows/hardware/ff554664)、 [ **MmBuildMdlForNonPagedPool**](https://msdn.microsoft.com/library/windows/hardware/ff554498)、 [ **IoBuildPartialMdl**](https://msdn.microsoft.com/library/windows/hardware/ff548324)、または[ **MmAllocatePagesForMdlEx** ](https://msdn.microsoft.com/library/windows/hardware/ff554489)ルーチン。

によって、システム-アドレス空間マッピングが返されるときに**MmGetSystemAddressForMdlSafe**が不要になった、解放する必要があります。 マッピングを解放するために必要な手順は、MDL がどのように構築されたかによって異なります。 これらは、次の 4 つの可能なケースです。

*   MDL への呼び出しで作成した場合、 **MmProbeAndLockPages** 、日常的な必要はありません、システム アドレス空間のマッピングを明示的に解放します。 代わりへの呼び出し、 [ **MmUnlockPages** ](https://msdn.microsoft.com/library/windows/hardware/ff556381)ルーチンは、割り当てられている場合に、マッピングを解放します。

*   MDL への呼び出しで作成した場合、 **MmBuildMdlForNonPagedPool**ルーチン、 **MmGetSystemAddressForMdlSafe**新規に作成する代わりに既存のシステム アドレス空間のマッピングを再利用されます。 この場合は、クリーンアップは必要ありません (つまり、ロックを解除して、割り当ての解除は必要ありません)。

*   MDL への呼び出しで作成した場合、 **IoBuildPartialMdl** 、日常的なドライバー呼び出す必要がありますか、 [ **MmPrepareMdlForReuse** ](https://msdn.microsoft.com/library/windows/hardware/ff554660)ルーチンまたは[ **IoFreeMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff549126)ルーチンをシステム アドレス空間のマッピングをリリースします。

*   MDL への呼び出しで作成した場合、 **MmAllocatePagesForMdlEx** 、日常的なドライバー呼び出す必要があります、 **MmUnmapLockedPages**ルーチンをシステム アドレス空間のマッピングをリリースします。 場合**MmGetSystemAddressForMdlSafe** MDL、後続の 1 つ以上の時間と呼びます**MmGetSystemAddressForMdlSafe**の呼び出しは単に最初の呼び出しによって作成されたマッピングを返します。 1 回の呼び出しに**MmUnmapLockedPages**このマッピングを解放するだけで十分です。

Windows 7 および Windows Server 2008 R2 以降、必要はありませんを明示的に呼び出す**MmUnmapLockedPages**によって作成された、MDL の**MmAllocatePagesForMdlEx**します。 代わりへの呼び出し、 [ **MmFreePagesFromMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff554521)ルーチンが割り当てられている場合、システム アドレス空間のマッピングを解放します。

新しいシステム アドレス空間マッピングを作成する**MmGetSystemAddressForMdlSafe**呼び出し**MmMapLockedPagesSpecifyCache**で、 _CacheType_パラメーターに設定**MmCached**します。 以外のキャッシュの種類を必要とするドライバー **MmCached**呼び出す必要があります**MmMapLockedPagesSpecifyCache**呼び出す代わりに直接**MmGetSystemAddressForMdlSafe**します。 詳細については、 _CacheType_パラメーターを参照してください[ **MmMapLockedPagesSpecifyCache**](https://msdn.microsoft.com/library/windows/hardware/ff554629)します。

呼び出しで**MmMapLockedPagesSpecifyCache**、MDL によって記述されるページがあるまだないキャッシュの種類が関連付けられている場合にのみ、指定されたキャッシュの種類が使用されます。 ただし、ほぼすべての場合、ページが、関連付けられているキャッシュの種類では、既にあるし、このキャッシュの種類は、新しいマッピングによって使用されます。 このルールの例外は、によって割り当てられているページに**MmAllocatePagesForMdl**、キャッシュの種類に設定**MmCached**ページの元のキャッシュの種類に関係なく。

一度に 1 つのスレッドを安全に呼び出す**MmGetSystemAddressForMdlSafe**特定 MDL のため、このルーチンは、呼び出し元のスレッドが MDL を所有していることを想定しています。 ただし、 **MmGetSystemAddressForMdlSafe**かによって、同じスレッドからのすべての呼び出しを行う同じ MDL の 1 つ以上の時間を呼び出すことができます、または明示的に呼び出しを同期することによって、複数のスレッドからの呼び出しでは場合。

ドライバーを使用して、要求をより小さな要求に分割する必要があります、ドライバーは、追加の MDLs を割り当てることができます、または、ドライバーを使用して、 **IoBuildPartialMdl**ルーチン。

返されるベース アドレスが、MDL 仮想アドレスとして同じオフセット。

Windows 98 はサポートしていません**MmGetSystemAddressForMdlSafe**します。 使用[ **MmGetSystemAddressForMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff554556)代わりにします。

このマクロを呼び出すため[ **MmMapLockedPagesSpecifyCache**](https://msdn.microsoft.com/library/windows/hardware/ff554629)、それを使用して NtosKrnl.lib へのリンクが必要があります。

Windows 2000 以降を使用できます。

IRQL &LT; = DISPATCH_LEVEL


## <a name="mminitializemdl"></a>**MmInitializeMdl**

定義されています。Wdm.h

**MmInitializeMdl**マクロが、MDL のヘッダーを初期化します。

_MemoryDescriptorList [in]_

**PMDL**

MDL として初期化するために、バッファーへのポインター。 詳細については、次のセクションを参照してください。

_BaseVa [in]_

**PVOID**

バッファーの基本の仮想アドレスへのポインター。

_[In] 長_

**SIZE_T**

MDL して説明を取得するバッファーのバイト単位の長さを指定します。 このルーチンには、MAXULONG バイトの最大のバッファー長がサポートしています。

**戻り値**

**VOID**

バッファーを_MemoryDescriptorList_非ページ メモリ内へのポインターを割り当てる必要があります。 このバッファーのバイト単位のサイズは以上である必要があります**sizeof**(MDL) + **sizeof**(PFN_NUMBER)**ADDRESS_AND_SIZE_TO_SPAN_PAGES**(_BaseVa_、_長さ_)。

Windows 2000 および以降のバージョンの Windows で使用できます。

IRQL &LT; = DISPATCH_LEVEL


## <a name="mmpreparemdlforreuse"></a>**MmPrepareMdlForReuse**

定義されています。Wdm.h

**MmPrepareMdlForReuse**マクロが MDL を再利用できるように部分的な MDL に関連付けられているリソースを解放します。

_[In] Mdl_

**PMDL**

再利用するための準備が部分的な MDL へのポインター。

**戻り値**

**VOID**

このマクロは繰り返しの同じ割り当てられた MDL を使用するドライバーを使用、 _TargetMdl_への呼び出しのパラメーター、 [ **IoBuildPartialMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff548324)ルーチン。 呼び出しの場合、 **MmPrepareMdlForReuse**、指定した部分的な MDL は、システム アドレス空間に関連付けられているマッピングを持つ**MmPrepareMdlForReuse** MDL を再利用できるように、マッピングを解放します。

**MmPrepareMdlForReuse**してビルドされる部分的な MDLs のみを受け入れる**IoBuildPartialMdl**します。 場合**MmPrepareMdlForReuse**受信システム アドレス空間にマップされますがビルドされませんでしたが、MDL **IoBuildPartialMdl**、 **MmPrepareMdlForReuse**によって解放されません。マッピングと、チェックのビルドが原因で失敗するアサーション。

部分的な MDLs の詳細については、次を参照してください。[を使用して MDLs](using-mdls.md)します。

Windows 2000 および以降のバージョンの Windows で使用できます。

IRQL &LT; = DISPATCH_LEVEL


## <a name="pagealign"></a>**PAGE_ALIGN**

定義されています。Wdm.h

**PAGE_ALIGN**マクロは、特定の仮想アドレスのページで固定された仮想アドレスを返します。

_Va [in]_

**PVOID**

仮想アドレスへのポインター。

**戻り値**

**PVOID**

## <a name="pagealign-returns-a-pointer-to-the-page-aligned-virtual-address"></a>**PAGE_ALIGN**  ページで固定された仮想アドレスへのポインターを返します。

Windows 2000 以降を使用できます。

IRQL:任意のレベル


## <a name="pagedcode"></a>**PAGED_CODE**

定義されています。Wdm.h

**PAGED_CODE**マクロによりページングを許可するようにできるほど十分に低い IRQL で呼び出し元のスレッドが実行されているようになります。

**戻り値**

**VOID**

場合は、IRQL > APC_LEVEL、 **PAGED_CODE**マクロと、システムはアサートします。

ページング可能なコードが含まれていますか、ページング可能なコードにアクセスするすべてのドライバー ルーチンの先頭には、このマクロに呼び出しを行う必要があります。

**PAGED_CODE**マクロは、ドライバーのコードがマクロを実行するポイントでのみ IRQL を確認します。 その後、コードには、IRQL が発生した場合、マクロには、この変更は検出されません。 ドライバー開発者が使用する必要があります[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)と[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)ドライバー ルーチンの実行中に、IRQL が不適切に発生したときを検出します。

**PAGED_CODE**マクロがチェック ビルドでのみ機能します。

Windows 2000 以降を使用できます。


## <a name="pagedcodelocked"></a>**PAGED_CODE_LOCKED**

定義されています。Wdm.h

**PAGED_CODE_LOCKED**マクロは、現在実行中のコード セクションをページングする必要がありますロックされているメモリにそれを実行する前に、をアサートします。

**戻り値**

**VOID**

ページング可能なコードが特定の制限に従う必要があります (IRQL など < = APC_LEVEL) にロックされていることがない限り、します。 ページング可能なルーチンを正常にロックする必要がありますがへの呼び出しで開始する必要があります**PAGED_CODE_LOCKED**します。

所定の位置にコード セクションのロックの詳細については、次を参照してください。[ページング可能なコードをロックまたはデータ](locking-pageable-code-or-data.md)します。


## <a name="posetdevicebusy"></a>**PoSetDeviceBusy**

定義されています。Wdm.h

**PoSetDeviceBusy**マクロの通知、[電源マネージャー](power-manager.md)デバイスが関連付けられている_IdlePointer_がビジー状態です。

_IdlePointer [で, out]_

**PULONG**

以外を指定**NULL**アイドル状態のポインターによって以前返された[ **PoRegisterDeviceForIdleDetection**](https://msdn.microsoft.com/library/windows/hardware/ff559721)します。 なお**PoRegisterDeviceForIdleDetection**返す可能性があります、 **NULL**ポインター。 呼び出し元**PoSetDeviceBusy**以外、ポインターがあることを確認する必要があります**NULL**に渡す前に**PoSetDeviceBusy**します。

**戻り値**

**VOID**

**注**、 [ **PoSetDeviceBusyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff559759)ルーチンの代わりとして、 **PoSetDeviceBusy**マクロ。 Windows Vista Service Pack 1 (SP1)、以降のバージョンの Windows の新しいドライバーのコードを記述する場合は、呼び出す**PoSetDeviceBusyEx**の代わりに**PoSetDeviceBusy**します。

ドライバーを使用して**PoSetDeviceBusy**と共に**PoRegisterDeviceForIdleDetection**システム、デバイスのアイドル状態の検出を有効にします。 電源マネージャーが送信アイドル状態の検出のために登録されているデバイスがアイドル状態になった場合、 [ **IRP_MN_SET_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)デバイスを要求されたスリープ状態にする要求。

**PoSetDeviceBusy**電源マネージャーがアイドル状態にカウント ダウンを再起動できるように、デバイスがビジー状態であるかを報告します。 場合は、デバイスは、電源が入っていない**PoSetDeviceBusy**その状態は変更されません。 つまり、電源オン要求を送信するシステムは発生しません。

ドライバーを呼び出す必要があります**PoSetDeviceBusy** I/O 要求ごとにします。

Windows 2000 以降を使用できます。

IRQL:任意のレベル


## <a name="psgetcurrentprocess"></a>**PsGetCurrentProcess**

定義されています。Ntddk.h

現在のスレッドのプロセスへのポインターを返します。

**戻り値**

プロセスの不透明なオブジェクトへのポインター。



Windows 2000 以降を使用できます。

IRQL:任意のレベル


## <a name="readregisterbufferulong64"></a>**READ_REGISTER_BUFFER_ULONG64**

定義されています。Wdm.h

**READ_REGISTER_BUFFER_ULONG64**マクロは、バッファーに指定されたレジスタ アドレスから ULONG64 値の数を読み取ります。

_[In] 登録します。_

**PULONG64**

メモリ領域でマップされた範囲である必要があります、レジスタへのポインター。

_バッファー [out]_

**PULONG64**

ULONG64 値の配列に読み取られるバッファーへのポインター。

_[In] カウントします。_

**ULONG**

バッファーに読み取る ULONG64 値の数を指定します。

**戻り値**

**VOID**

サイズ、_バッファー_バッファーは、少なくとも ULONG64 値の指定した数を格納するのに十分な大きさである必要があります。

呼び出し元、 **READ_REGISTER_BUFFER_ULONG64**マクロ実行できる任意の IRQL であると仮定して、_バッファー_バッファーが常駐し、_登録_レジスタは、常駐デバイスのメモリをマップします。

Windows の 64 ビット バージョンでのみ使用できます。

IRQL:任意のレベル


## <a name="readregisterulong64"></a>**READ_REGISTER_ULONG64**

定義されています。Wdm.h

**READ_REGISTER_ULONG64**マクロは、指定されたレジスタ アドレスから ULONG64 値を読み取ります。

_volatile * [in] 登録_

**ULONG64**

メモリ領域でマップされた範囲である必要がありますレジスタ アドレスへのポインター。

**戻り値**

**ULONG64**

**READ_REGISTER_ULONG64**レジスタが指定したアドレスから読み取られる ULONG64 値を返します。

呼び出し元、 **READ_REGISTER_ULONG64**マクロは、任意の IRQL で実行できると仮定すると、_登録_アドレスが常駐する、マップされたデバイスのメモリ。

Windows の 64 ビット バージョンでのみ使用できます。

IRQL:任意のレベル


## <a name="roundtopages"></a>**ROUND_TO_PAGES**

定義されています。Wdm.h

**ROUND_TO_PAGES**マクロ サイズ (バイト単位) を受け取り、次の完全なページまでに四捨五入します。

_[In] のサイズ_

**ULONG_PTR**

ページに切り上げられることをバイト単位でサイズを指定します。 複数。

**戻り値**

**ULONG_PTR**

**ROUND_TO_PAGES**入力サイズが現在のプラットフォームの仮想メモリのページ サイズの倍数に切り上げを返します。

呼び出し元**ROUND_TO_PAGES** IRQL で実行されていることができます。 呼び出し元は、指定したパラメーターは、メモリのオーバーフローで発生することはできませんを確認してください。

IRQL:任意のレベル


## <a name="rtlequalluid"></a>**RtlEqualLuid**

定義されています。Wdm.h

**戻り値**

Windows 2000 以降を使用できます。

IRQL:任意のレベル


## <a name="rtlinitemptyansistring"></a>**RtlInitEmptyAnsiString**

定義されています。Wdm.h

**RtlInitEmptyAnsiString**マクロが空のカウントされた ANSI 文字列を初期化します。

_[Out] DestinationString_

**PANSI_STRING**

ポインター、 [ **ANSI_STRING** ](https://msdn.microsoft.com/library/windows/hardware/ff540605)構造体を初期化します。

_[In] バッファーします。_

**PCHAR**

WCHAR 文字列を含めるために使用する呼び出し元が割り当てたバッファーへのポインター。

_[In] BufferSize_

**USHORT**

バッファーのバイト単位の長さを_バッファー_を指します。

**戻り値**

**VOID**

構造体のメンバーを_DestinationString_パラメーターが指すには次のように初期化されます。

*   **長さ**します。 0 を返します。

*   **MaximumLength**します。 _BufferSize_します。

*   **バッファー**します。 _SourceString_します。

空でないカウント Unicode 文字列を初期化するために呼び出す[ **RtlInitAnsiString**](https://msdn.microsoft.com/library/windows/hardware/ff561918)します。

Microsoft Windows XP および Windows の以降のバージョンで使用できます。

IRQL:任意のレベル


## <a name="rtlinitemptyunicodestring"></a>**RtlInitEmptyUnicodeString**

定義されています。Wdm.h

**RtlInitEmptyUnicodeString**マクロが、空の Unicode 文字列のカウントを初期化します。

_[Out] DestinationString_

**PUNICODE_STRING**

ポインター、 [ **UNICODE_STRING** ](https://msdn.microsoft.com/library/windows/hardware/ff564879)構造体を初期化します。

_[In] バッファーします。_

**PWCHAR**

WCHAR 文字列を含めるために使用する呼び出し元が割り当てたバッファーへのポインター。

_[In] BufferSize_

**USHORT**

バッファーのバイト単位の長さを_バッファー_を指します。

**戻り値**

**VOID**

構造体のメンバーを_DestinationString_パラメーターが指すは次のように初期化されます。

*   **長さ**します。 0 を返します。

*   **MaximumLength**します。 _BufferSize_します。

*   **バッファー**します。 _SourceString_します。

空でないカウント Unicode 文字列を初期化するために呼び出す[ **RtlInitUnicodeString**](https://msdn.microsoft.com/library/windows/hardware/ff561934)します。

Windows xp 以降を使用できます。

IRQL:任意のレベル


## <a name="rtliszeroluid"></a>**RtlIsZeroLuid**

定義されています。Ntddk.h

**RtlIsZeroLuid**マクロの場合、指定の LUID がゼロ LUID であるかどうか。

_[In] L1_

**PLUID**

指定します、 [ **LUID** ](https://msdn.microsoft.com/library/windows/hardware/ff554334)を確認します。

**戻り値**

**ブール値**

**RtlIsZeroLuid**返します**TRUE**場合_L1_は 0 を返します**FALSE**それ以外の場合。

IRQL:任意のレベル


## <a name="rtlretrieveulong"></a>**RtlRetrieveUlong**

定義されています。Wdm.h

**RtlRetrieveUlong**マクロは、配置エラーを回避するには、ソース アドレスから ULONG 値を取得します。 送信先アドレスは、配置すると見なされます。

_DestinationAddress [out]_

**PULONG**

ULONG 値を格納する ULONG で固定された場所へのポインター。

_SourceAddress [in]_

**PULONG**

ULONG 値の取得元の場所へのポインター。

**戻り値**

**VOID**

呼び出し元**RtlRetrieveUlong**特定のアドレスは、非ページ プールの場合は、IRQL で実行できます。 それ以外の場合、呼び出し元は IRQL で実行する必要があります < APC_LEVEL を = です。

Windows 2000 および以降のバージョンの Windows で使用できます。


## <a name="rtlretrieveushort"></a>**RtlRetrieveUshort**

定義されています。Wdm.h

**RtlRetrieveUshort**マクロは、配置エラーを回避するには、ソース アドレスから USHORT の値を取得します。

_DestinationAddress [out]_

**PUSHORT**

USHORT で固定された値を格納する場所へのポインター。

_SourceAddress [in]_

**PUSHORT**

元の値を取得する場所へのポインター。

**戻り値**

**VOID**

呼び出し元**RtlRetrieveUshort**特定のアドレスは、非ページ プールの場合は、IRQL で実行できます。 それ以外の場合、呼び出し元は IRQL で実行する必要があります < APC_LEVEL を = です。

Windows 2000 および以降のバージョンの Windows で使用できます。

IRQL:任意のレベル


## <a name="rtlstoreulong"></a>**RtlStoreUlong**

定義されています。Wdm.h

**RtlStoreUlong**マクロには、特定のアドレスで配置エラーを回避する ULONG 値が格納されます。

_[Out] アドレス_

**PULONG**

指定した ULONG 値を格納する場所へのポインター。

_[In] 値します。_

**ULONG**

格納される ULONG 値を指定します。

**戻り値**

**VOID**

場合、呼び出し元は、IRQL で実行できる_アドレス_非ページ プールにポイントします。 それ以外の場合、呼び出し元は IRQL で実行する必要があります < APC_LEVEL を = です。

Windows 2000 および以降のバージョンの Windows で使用できます。

IRQL:任意のレベル


## <a name="rtlstoreulonglong"></a>**RtlStoreUlonglong**

定義されています。Wdm.h

**RtlStoreUlonglong**マクロは、メモリ配置エラーを回避するには、指定されたメモリ アドレスに指定の ULONGLONG 値を格納します。

_[Out] アドレス_

**PULONGLONG**

指定した ULONGLONG 値を格納する場所へのポインター。

_[In] 値します。_

**ULONGLONG**

格納される ULONGLONG 値。

**戻り値**

**VOID**

**RtlStoreUlonglong**メモリ配置エラーを回避できます。 によってアドレスが指定されている場合_アドレス_を使いの記憶域の要件に固定されていない**RtlStoreUlonglong**のバイト数を格納_値_メモリから始まる場所 (PUCHAR)_アドレス_します。

**RtlStoreUlonglong**場合は、任意の IRQL で実行_アドレス_非ページ プールは; を指す IRQL で実行する必要があります、それ以外の場合、< APC_LEVEL を = です。

Windows 2000 以降を使用できます。

IRQL:任意のレベル


## <a name="rtlstoreulongptr"></a>**RtlStoreUlongPtr**

定義されています。Wdm.h

**RtlStoreUlongPtr**マクロはメモリ配置エラーを回避するには、指定したメモリ位置に指定した ULONG_PTR 値を格納します。

_[Out] アドレス_

**PULONG_PTR**

ULONG_PTR 値を格納する場所へのポインター。

_[In] 値します。_

**ULONG_PTR**

格納される ULONG_PTR 値を指定します。

**戻り値**

**VOID**

**RtlStoreUlongPtr**メモリ配置エラーを回避できます。 場合の値_アドレス_、ULONG_PTR の記憶域の要件に固定されていない**RtlStoreUlongPtr**のバイト数を格納_値_メモリの場所 (先頭PUCHAR)_アドレス_します。

**RtlStoreUlongPtr**場合は、任意の IRQL で実行_アドレス_非ページ プールは; を指す IRQL で実行する必要があります、それ以外の場合 < APC_LEVEL を = です。

Windows 2000 および以降のバージョンの Windows で使用できます。

IRQL:任意のレベル


## <a name="rtlstoreushort"></a>**RtlStoreUshort**

定義されています。Wdm.h

**RtlStoreUshort**マクロには、配置エラーを回避するには、特定のアドレスに USHORT の値が格納されます。

_[Out] アドレス_

**PUSHORT**

指定した USHORT 値を格納する場所へのポインター。

_[In] 値します。_

**USHORT**

格納される USHORT 値を指定します。

**戻り値**

**VOID**

場合、呼び出し元は、IRQL で実行できる_アドレス_非ページ プールにポイントします。 それ以外の場合、呼び出し元は IRQL で実行する必要があります < APC_LEVEL を = です。

Windows 2000 および以降のバージョンの Windows で使用できます。

IRQL:任意のレベル


## <a name="writeregisterbufferulong64"></a>**WRITE_REGISTER_BUFFER_ULONG64**

定義されています。Wdm.h

**WRITE_REGISTER_BUFFER_ULONG64**マクロは、指定した登録バッファーから ULONG64 値の点数を書き込みます。

_[In] 登録します。_

**PULONG64**

メモリ領域でマップされた範囲である必要があります、レジスタへのポインター。

_[In] バッファーします。_

**PULONG64**

ULONG64 値の配列に書き込まれるバッファーへのポインター。

_[In] カウントします。_

**ULONG**

レジスタに書き込まれる ULONG64 値の数を指定します。

**戻り値**

**VOID**

サイズ、_バッファー_バッファーは、少なくとも ULONG64 値の指定した数を格納するのに十分な大きさである必要があります。

呼び出し元、 **WRITE_REGISTER_BUFFER_ULONG64**マクロ実行できる任意の IRQL であると仮定して、_バッファー_バッファーが常駐し、_登録_レジスタは、常駐デバイスのメモリをマップします。

Windows の 64 ビット バージョンでのみ使用できます。

IRQL:任意のレベル


## <a name="writeregisterulong64"></a>**WRITE_REGISTER_ULONG64**

定義されています。Wdm.h

**WRITE_REGISTER_ULONG64**マクロは、指定したアドレスに ULONG64 値を書き込みます。

_volatile * [in] 登録_

**ULONG64**

メモリ領域でマップされた範囲である必要があります、レジスタへのポインター。

_[In] 値します。_

**ULONG64**

レジスタへの書き込みに ULONG64 値を指定します。

**戻り値**

**VOID**

呼び出し元、 **WRITE_REGISTER_ULONG64**マクロは、任意の IRQL で実行できると仮定すると、_登録_レジスタは、デバイスが常駐する、マップされたメモリ。

Windows の 64 ビット バージョンでのみ使用できます。

IRQL:任意のレベル


## <a name="zwcurrentprocess"></a>**ZwCurrentProcess**

定義されています。Wdm.h

**ZwCurrentProcess**マクロの現在のプロセスにハンドルを返します。

**戻り値**

**ハンドル**

**ZwCurrentProcess**現在のプロセスを表す特殊なハンドル値を返します。

返された値が true のハンドルではありませんが、常に現在のプロセスを表す特殊な値。

**NtCurrentProcess**と**ZwCurrentProcess**同じ Windows ネイティブ システム サービス ルーチンの 2 つのバージョンします。 **NtCurrentProcess** Windows カーネルのルーチンがカーネル モード ドライバーに直接アクセスします。 ただし、カーネル モード ドライバー間接的にアクセスできるこのルーチンを呼び出して**ZwCurrentProcess**します。

カーネル モード ドライバーからの呼び出し、 **Nt_Xxx_** と**Zw_Xxx_** のバージョンの Windows のネイティブ システム サービス ルーチンは、処理と、入力パラメーターの解釈で異なった動作できます。 間のリレーションシップの詳細については、 **Nt_Xxx_** と**Zw_Xxx_** 、ルーチンのバージョンを参照してください[を使用して Nt と Zw バージョンのネイティブ システム サービス ルーチン](using-nt-and-zw-versions-of-the-native-system-services-routines.md).

すべてのオペレーティング システムがサポートされています。

IRQL:任意のレベル


## <a name="zwcurrentthread"></a>**ZwCurrentThread**

定義されています。Wdm.h

**ZwCurrentThread**マクロの現在のスレッドにハンドルを返します。

**戻り値**

**ハンドル**

**ZwCurrentThread**現在のスレッドを表す特殊なハンドル値を返します。

返された値が true のハンドルではありませんが、常に、現在のスレッドを表す特殊な値。

**NtCurrentThread**と**ZwCurrentThread**同じ Windows ネイティブ システム サービス ルーチンの 2 つのバージョンします。 **NtCurrentThread** Windows カーネルのルーチンがカーネル モード ドライバーに直接アクセスします。 ただし、カーネル モード ドライバー間接的にアクセスできるこのルーチンを呼び出して、 **ZwCurrentThread**ルーチン。

カーネル モード ドライバーからの呼び出し、 **Nt_Xxx_** と**Zw_Xxx_** のバージョンの Windows のネイティブ システム サービス ルーチンは、処理と、入力パラメーターの解釈で異なった動作できます。 間のリレーションシップの詳細については、 **Nt_Xxx_** と**Zw_Xxx_** 、ルーチンのバージョンを参照してください[を使用して Nt と Zw バージョンのネイティブ システム サービス ルーチン](using-nt-and-zw-versions-of-the-native-system-services-routines.md).

すべてのオペレーティング システムがサポートされています。

IRQL:任意のレベル










