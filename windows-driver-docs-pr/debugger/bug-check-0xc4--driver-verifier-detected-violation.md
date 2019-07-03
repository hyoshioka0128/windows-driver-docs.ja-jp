---
title: バグ チェック 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION
description: DRIVER_VERIFIER_DETECTED_VIOLATION のバグ チェックでは、0x000000C4 の値を持ちます。 これは、Driver Verifier で見つかった致命的なエラーの一般的なバグ チェック コードです。
ms.assetid: 7814f827-05fc-419b-b428-4565978bbb52
keywords:
- バグ チェック 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION
- DRIVER_VERIFIER_DETECTED_VIOLATION
ms.date: 10/04/2017
topic_type:
- apiref
api_name:
- DRIVER_VERIFIER_DETECTED_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 21761e4ab4de109b4186a0d6448d24f27ad004cb
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518947"
---
# <a name="bug-check-0xc4-driververifierdetectedviolation"></a>バグ チェック 0xC4:ドライバー\_VERIFIER\_検出\_違反


ドライバー\_VERIFIER\_検出\_違反のバグ チェックが 0x000000C4 の値を持ちます。 これは、Driver Verifier で見つかった致命的なエラーの一般的なバグ チェック コードです。 詳細については、次を参照してください。[をバグ チェック時にドライバーの検証ツールの処理が有効になっている](handling-a-bug-check-when-driver-verifier-is-enabled.md)します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="driververifierdetectedviolation-parameters"></a>ドライバー\_VERIFIER\_検出\_違反パラメーター


パラメーター 1 では、違反の種類を識別します。 残りのパラメーターの意味は、パラメーター 1 の値によって異なります。 パラメーターの値は、次の表で説明します。

**注**  このテーブルのすべての 5 つの列を表示する問題が発生した場合は、次を実行してください。
-   最大化、ブラウザー ウィンドウを展開します。
-   テーブルにカーソルを置きおよび左と右にスクロールする矢印キーを使用します。
 
|パラメーター 1|パラメータ 2|3 番目のパラメーター|パラメーター 4|エラーの原因|
|--- |--- |--- |--- |--- |
|0x00|現在の IRQL|プールの種類|0|ドライバーは、ゼロ バイトのプール割り当てを要求します。|
|0x01|現在の IRQL|プールの種類|(バイト単位) の割り当てのサイズ|ドライバー IRQL でページングされたメモリを割り当てようとした > APC_LEVEL します。|
|0x02|現在の IRQL|プールの種類|(バイト単位) の割り当てのサイズ|ドライバーは IRQL で非ページ メモリを割り当てようとした > DISPATCH_LEVEL します。|
|0x10|アドレスが正しくありません。|0|0|ドライバーは、割り当ての呼び出しから返されませんでしたアドレスを解放しようとしました。|
|0x11|現在の IRQL|プールの種類|プールのアドレス|IRQL でページ プール空きしようとしているドライバー > APC_LEVEL します。|
|0x12|現在の IRQL|プールの種類|プールのアドレス|非ページ プールの IRQL を解放しようとしているドライバー > DISPATCH_LEVEL します。|
|0x13、または 0x14|予約済み|プールのヘッダーへのポインター|プールのヘッダーの内容|ドライバーは、既に解放されているメモリ プールを解放しようとしました。|
|0x16|予約済み|プールのアドレス|0|ドライバーが、不適切なアドレスでプールを解放しようとしています。 または、ドライバーでは、メモリ ルーチンに無効なパラメーターが渡されます。|
|0x30|現在の IRQL|要求された IRQL|0|ドライバーに無効なパラメーターを渡された[KeRaiseIrql](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirql)します。 (パラメーターは、現在の IRQL より小さい値または HIGH_LEVEL より大きい値のいずれかをしました。 これは、場合があります、初期化されていないパラメーターを使用した結果。)|
|0x31|現在の IRQL|要求された IRQL|0:新しい IRQL が、不適切な 1 です。新しい IRQL が DPC ルーチン内で無効です。|ドライバーに無効なパラメーターを渡された[KeLowerIrql](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kelowerirql~r1)します。 (パラメーターは、現在の IRQL より大きい値または HIGH_LEVEL より大きい値のいずれかをしました。 これは、場合があります、初期化されていないパラメーターを使用した結果。)|
|0x32|現在の IRQL|スピン ロック アドレス|0|ドライバーと呼ばれる[KeReleaseSpinLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock) DISPATCH_LEVEL 以外 IRQL でします。 (ことが考えられますスピン ロックの二重解放します。)|
|0x33|現在の IRQL|高速なミュー テックスのアドレス|0|ミュー テックスを高速な IRQL を取得しようとしているドライバー > APC_LEVEL します。|
|0x34|現在の IRQL|高速なミュー テックスのアドレス|0|ドライバーでは、IRQL APC_LEVEL 以外での高速なミュー テックスを解放しようとしています。|
|0x35|現在の IRQL|スピン ロック アドレス|古い IRQL|カーネルは、等しくない DISPATCH_LEVEL IRQL でスピン ロックをリリースしました。|
|0x36|現在の IRQL|スピン ロック数|古い IRQL|カーネルは、IRQL が等しくない DISPATCH_LEVEL でキューに置かれたスピン ロックをリリースしました。|
|0x37|現在の IRQL|スレッドの APC の無効化の数|リソース|ドライバーが、リソースの取得を試みましたが、Apc が無効になっていません。|
|0x38|現在の IRQL|スレッドの APC の無効化の数|リソース|ドライバーが、リソースを解放しようとしましたが、Apc が無効になっていません。|
|0x39|現在の IRQL|スレッドの APC の無効化の数|ミュー テックス|ドライバーは、「アンセーフ」IRQL が等しくない APC_LEVEL エントリでミュー テックスを取得しようとしました。|
|0x3A|現在の IRQL|スレッドの APC の無効化の数|ミュー テックス|ドライバーは、「アンセーフ」IRQL が等しくない APC_LEVEL エントリでミュー テックスを解放しようとしました。|
|0x3c です.|ルーチンに渡されるハンドル|オブジェクトの種類|0|ドライバーと呼ばれる[ObReferenceObjectByHandle](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)不適切なハンドルを使用します。|
|0x3D|0|0|無効なリソースのアドレス|ドライバーが正しくありません (固定) リソースを渡された[ExAcquireResourceExclusive](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)します。|
|0x3E|0|0|0|ドライバーと呼ばれる[KeLeaveCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleavecriticalregion)は現在、クリティカル領域内にないスレッド。|
|0x3F|オブジェクトのアドレス|新しいオブジェクト参照の数。 -1: 逆参照する場合は 1 ケースの参照。|0|適用されるドライバー [ObReferenceObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject)を 0、または適用されるドライバーの参照カウントを持つオブジェクトを[ObDereferenceObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)参照カウントが 0 のオブジェクトにします。|
|0x40|現在の IRQL|スピン ロック アドレス|0|ドライバーと呼ばれる[KeAcquireSpinLockAtDpcLevel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlockatdpclevel) IRQL で < DISPATCH_LEVEL します。|
|0x41|現在の IRQL|スピン ロック アドレス|0|ドライバーと呼ばれる[KeReleaseSpinLockFromDpcLevel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlockfromdpclevel) IRQL で < DISPATCH_LEVEL します。|
|0x42|現在の IRQL|スピン ロック アドレス|0|ドライバーと呼ばれる[KeAcquireSpinLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock) IRQL で > DISPATCH_LEVEL します。|
|0x51|ベース アドレスの割り当て|割り当てを超えた参照のアドレス|課金のバイト数|ドライバーは、割り当ての末尾を越えて書き込みが行われた後にメモリを解放しようとしています。 このパラメーターでのバグ チェックでは、Driver Verifier のプールの追跡オプションがアクティブな場合にのみ発生します。|
|0x52|ベース アドレスの割り当て|予約済み|課金のバイト数|ドライバーは、割り当ての末尾を越えて書き込みが行われた後にメモリを解放しようとしています。 このパラメーターでのバグ チェックでは、Driver Verifier のプールの追跡オプションがアクティブな場合にのみ発生します。|
|0x53、0x54、または 0x59|ベース アドレスの割り当て|予約済み|予約済み|ドライバーは、割り当ての末尾を越えて書き込みが行われた後にメモリを解放しようとしています。 このパラメーターでのバグ チェックでは、Driver Verifier のプールの追跡オプションがアクティブな場合にのみ発生します。|
|0x60 です。|ページ プールから割り当てられたバイト数|非ページ プールから割り当てられたバイト数|解放されていない割り当ての合計数|アンロード最初に割り当てられたプールを解放せずに、ドライバーを作成しています。 このパラメーターでのバグ チェックでは、Driver Verifier のプールの追跡オプションがアクティブな場合にのみ発生します。|
|0x61|ページ プールから割り当てられたバイト数|非ページ プールから割り当てられたバイト数|解放されていない割り当ての合計数|ドライバーのスレッドが、ドライバーをアンロード中に、プールのメモリを割り当てるしようとしています。 このパラメーターでのバグ チェックでは、Driver Verifier のプールの追跡オプションがアクティブな場合にのみ発生します。|
|0x62|ドライバーの名前|予約済み|解放されず、ページおよび非ページの両方のプールを含む割り当ての合計数|アンロード最初に割り当てられたプールを解放せずに、ドライバーを作成しています。 このパラメーターでのバグ チェックでは、Driver Verifier のプールの追跡オプションがアクティブな場合にのみ発生します。|
|0x70|現在の IRQL|MDL アドレス|アクセス モード|ドライバーと呼ばれる[MmProbeAndLockPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages) IRQL で > DISPATCH_LEVEL します。|
|0x71|現在の IRQL|MDL アドレス|プロセスのアドレス|IRQL で MmProbeAndLockProcessPages と呼ばれるドライバー > DISPATCH_LEVEL します。|
|0x72|現在の IRQL|MDL アドレス|プロセスのアドレス|IRQL で MmProbeAndLockSelectedPages と呼ばれるドライバー > DISPATCH_LEVEL します。|
|0x73|現在の IRQL|32 ビット Windows の場合。物理アドレスで 64 ビット Windows の 32 ビットの不足: 64 ビットの物理アドレス|バイト数|ドライバーと呼ばれる[MmMapIoSpace](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmapiospace) IRQL で > DISPATCH_LEVEL します。|
|0x74|現在の IRQL|MDL アドレス|アクセス モード|ドライバーと呼ばれる[MmMapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmaplockedpages) IRQL をカーネル モードで > DISPATCH_LEVEL します。|
|0x75|現在の IRQL|MDL アドレス|アクセス モード|ドライバーと呼ばれる[MmMapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmaplockedpages) IRQL をユーザー モードで > APC_LEVEL します。|
|0x76|現在の IRQL|MDL アドレス|アクセス モード|ドライバーと呼ばれる[MmMapLockedPagesSpecifyCache](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmaplockedpagesspecifycache) IRQL をカーネル モードで > DISPATCH_LEVEL します。|
|0x77|現在の IRQL|MDL アドレス|アクセス モード|ドライバーと呼ばれる[MmMapLockedPagesSpecifyCache](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmaplockedpagesspecifycache) IRQL をユーザー モードで > APC_LEVEL します。|
|0x78|現在の IRQL|MDL アドレス|0|ドライバーと呼ばれる[MmUnlockPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunlockpages) IRQL で > DISPATCH_LEVEL します。|
|0x79|現在の IRQL|マップ解除されている仮想アドレス|MDL アドレス|ドライバーと呼ばれる[MmUnmapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunmaplockedpages) IRQL をカーネル モードで > DISPATCH_LEVEL します。|
|0x7A|現在の IRQL|マップ解除されている仮想アドレス|MDL アドレス|ドライバーと呼ばれる[MmUnmapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunmaplockedpages) IRQL をユーザー モードで > APC_LEVEL します。|
|0x7B|現在の IRQL|マップ解除されている仮想アドレス|バイト数|ドライバーと呼ばれる[MmUnmapIoSpace](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunmapiospace) IRQL で > APC_LEVEL します。|
|0x7C|MDL アドレス|MDL フラグ|0|ドライバーと呼ばれる[MmUnlockPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunlockpages)MDL のページがロックされていたことはありませんが正常に渡されます。|
|0x7D|MDL アドレス|MDL フラグ|0|ドライバーと呼ばれる[MmUnlockPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunlockpages)ページが、非ページ プールから、MDL を渡されます。 (これらべきではロックされていなかった。)|
|0x7E|現在の IRQL|DISPATCH_LEVEL|0|ドライバーと呼ばれる[MmAllocatePagesForMdl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatepagesformdl)、 [MmAllocatePagesForMdlEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatepagesformdlex)、または[MmFreePagesFromMdl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmfreepagesfrommdl) IRQL で > DISPATCH_LEVEL します。|
|0x7F|現在の IRQL|MDL アドレス|MDL フラグ|ドライバーと呼ばれる[BuildMdlForNonPagedPool](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmbuildmdlfornonpagedpool) MDL ページが、ページ プールから渡されるとします。|
|0x80|現在の IRQL|イベントのアドレス|0|ドライバーと呼ばれる[KeSetEvent](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent) IRQL で > DISPATCH_LEVEL します。|
|0x81|MDL アドレス|MDL フラグ|0|ドライバーと呼ばれる[MmMapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmaplockedpages)します。 (使用する必要があります[MmMapLockedPagesSpecifyCache](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmaplockedpagesspecifycache) BugCheckOnFailure パラメーターを FALSE に設定した代わりに、します)。|
|0x82|MDL アドレス|MDL フラグ|0|ドライバーと呼ばれる[MmMapLockedPagesSpecifyCache](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmaplockedpagesspecifycache)を TRUE に等しい BugCheckOnFailure パラメーターを使用します。 (このパラメーターは FALSE に設定する必要があります)。|
|0x83|マップする物理アドレスの範囲の開始|マップするバイト数|最初のページをロックされていないフレーム番号|ドライバーと呼ばれる[MmMapIoSpace](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmapiospace)せず MDL ページ ロックされていること。 マップされる物理アドレスの範囲によって表される物理ページする必要がありますがロックダウンされてこの呼び出しを行う前にします。|
|0x85|MDL アドレス|マップするページ数|最初のページをロックされていないフレーム番号|ドライバーと呼ばれる[MmMapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmaplockedpages)せず MDL ページ ロックされていること。|
|0x89|MDL アドレス|MDL でないメモリ ページへのポインター|MDL でないメモリ ページ数|MDL が"I/O"としてマークされていないが、非メモリ ページのアドレスが含まれています。|
|0x91|予約済み|予約済み|予約済み|ドライバーは、オペレーティング システムによってサポートされていないメソッドを使用してスタックを切り替えられます。 使用してカーネル モード スタックを拡張する唯一の方法は、 [KeExpandKernelStackAndCallout](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keexpandkernelstackandcallout)します。|
|0xA0 (Windows Server 2003 およびそれ以降のオペレーティング システムのみ)|読み取りまたは書き込み要求を行う IRP へのポインター|下のデバイスのデバイス オブジェクト|エラーが検出されたセクターの数|ハード ディスク上、巡回冗長検査 (CRC) エラーが検出されました。 このパラメーターでのバグ チェックでは、Driver Verifier のディスクの整合性チェック オプションがアクティブな場合にのみ発生します。|
|0xA1 (Windows Server 2003 およびそれ以降のオペレーティング システムのみ)|読み取りまたは書き込み要求を行う IRP のコピーです。 (実際の IRP が完了しました。)|下のデバイスのデバイス オブジェクト|エラーが検出されたセクターの数|CRC エラーは、(非同期に) セクターで検出されました。 このパラメーターでのバグ チェックでは、Driver Verifier のディスクの整合性チェック オプションがアクティブな場合にのみ発生します。|
|0xA2 (Windows Server 2003 およびそれ以降のオペレーティング システムのみ)|IRP の読み取りまたは書き込み要求、またはこの IRP のコピーを行う|下のデバイスのデバイス オブジェクト|エラーが検出されたセクターの数|CRCDISK チェックサムのコピーが一致しません。 これは、ページング エラーである可能性があります。 このパラメーターでのバグ チェックでは、Driver Verifier のディスクの整合性チェック オプションがアクティブな場合にのみ発生します。|
|0xB0 (Windows Vista およびそれ以降のオペレーティング システムのみ)|MDL アドレス|MDL フラグ|不適切な MDL フラグ|ドライバーと呼ばれる[MmProbeAndLockPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)の MDL が正しくないフラグを使用します。 たとえば、ドライバーに渡さによって作成された、MDL [MmBuildMdlForNonPagedPool](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmbuildmdlfornonpagedpool) MmProbeAndLockPages にします。|
|0xB1 (Windows Vista およびそれ以降のオペレーティング システムのみ)|MDL アドレス|MDL フラグ|不適切な MDL フラグ|無効なフラグで MDL の MmProbeAndLockProcessPages と呼ばれるドライバー。 たとえば、ドライバーに渡さによって作成された、MDL [MmBuildMdlForNonPagedPool](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmbuildmdlfornonpagedpool) MmProbeAndLockProcessPages にします。|
|0xB2 (Windows Vista およびそれ以降のオペレーティング システムのみ)|MDL アドレス|MDL フラグ|不適切な MDL フラグ|ドライバーと呼ばれる[MmMapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmaplockedpages)の MDL が正しくないフラグを使用します。 たとえば、ドライバーでは、システム アドレスに既にマップされているまたは MmMapLockedPages にロックされませんでしたが、MDL が渡されます。|
|0xB3 (Windows Vista およびそれ以降のオペレーティング システムのみ)|MDL アドレス|MDL フラグ|不足している MDL フラグが (少なくとも 1 つが必要です)|ドライバーと呼ばれる[MmMapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmaplockedpages)の MDL が正しくないフラグを使用します。 たとえば、ドライバーでは、MmMapLockedPages にロックされていない、MDL が渡されます。|
|繰り返し、0xB4 (Windows Vista およびそれ以降のオペレーティング システムのみ)|MDL アドレス|MDL フラグ|予期しないの部分的な MDL フラグ|ドライバーと呼ばれる[MmUnlockPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunlockpages)部分的な MDL の。 部分的な MDL は 1 つによって作成された[IoBuildPartialMdl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildpartialmdl)します。|
|(Windows Vista およびそれ以降のオペレーティング システムのみ) は 0xb8 と|MDL アドレス|MDL フラグ|予約済み|MDL によって記述されるページは引き続きマップされます。 ドライバーは、IoFreeMdl を呼び出す前に、ページをマップ解除する必要があります。|
|0xC0 (Windows Vista およびそれ以降のオペレーティング システムのみ)|IRP のアドレス|予約済み|予約済み|ドライバーと呼ばれる[保留](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)に割り込みを無効になっています。|
|0xC1 (Windows Vista およびそれ以降のオペレーティング システムのみ)|ドライバーのディスパッチ ルーチンのアドレス|予約済み|予約済み|ドライバーのディスパッチ ルーチンが返されましたに割り込みを無効になっています。|
|0xC2 (Windows Vista およびそれ以降のオペレーティング システムのみ)|予約済み|予約済み|予約済み|ドライバーでは、割り込みを無効にした後に、高速の I/O のディスパッチ ルーチンが呼び出されます。|
|(Windows Vista およびそれ以降のオペレーティング システムのみ) は 0xc3 です.|ドライバーの高速の I/O ディスパッチ ルーチンのアドレス|予約済み|予約済み|割り込みを無効になっているドライバーの高速の I/O ディスパッチ ルーチンが返されました。|
|0xC5 (Windows Vista およびそれ以降のオペレーティング システムのみ)|ドライバーのディスパッチ ルーチンのアドレス|現在のスレッドの APC の無効化の数|スレッドの APC がドライバーのディスパッチ ルーチンを呼び出す前に数を無効にします。|ドライバーのディスパッチ ルーチンには、スレッドの APC の無効化の数が変更されました。 APC の無効化カウントがデクリメントされますドライバーを呼び出すたびに[KeEnterCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)、 [FsRtlEnterFileSystem](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlenterfilesystem)、または、ミュー テックスを取得します。 APC の無効化の数には、ドライバーを呼び出すたびがインクリメントされます[KeLeaveCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleavecriticalregion)、 [KeReleaseMutex](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasemutex)、または[FsRtlExitFileSystem](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlexitfilesystem)します。 これらの呼び出しは、ペアで常にする必要があります、APC の無効化の数はスレッドが終了したときに、その 0 にする必要があります。 負の値は、ドライバーにそれらを再度有効にすることがなく APC 呼び出しが無効になっていることを示します。 正の値は、逆が true であることを示します。|
|0xC6 (Windows Vista およびそれ以降のオペレーティング システムのみ)|ドライバーの高速の I/O ディスパッチ ルーチンのアドレス|現在のスレッドの APC の無効化の数|スレッドの APC が高速の I/O ドライバーのディスパッチ ルーチンを呼び出す前に数を無効にします。|ドライバーの高速の I/O ディスパッチ ルーチンには、スレッドの APC の無効化の数が変更されました。 APC の無効化カウントがデクリメントされますドライバーを呼び出すたびに[KeEnterCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)、 [FsRtlEnterFileSystem](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlenterfilesystem)、または、ミュー テックスを取得します。 APC の無効化の数には、ドライバーを呼び出すたびがインクリメントされます[KeLeaveCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleavecriticalregion)、 [KeReleaseMutex](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasemutex)、または[FsRtlExitFileSystem](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlexitfilesystem)します。 これらの呼び出しは、ペアで常にする必要があります、APC の無効化の数はスレッドが終了したときに、その 0 にする必要があります。 負の値は、ドライバーにそれらを再度有効にすることがなく APC 呼び出しが無効になっていることを示します。 正の値は、逆が true であることを示します。|
|0 xca (Windows Vista およびそれ以降のオペレーティング システムのみ)|ルック アサイド リストのアドレス|予約済み|予約済み|ドライバーがルック アサイド リストの再初期化しようとしました。|
|0xCB (Windows Vista およびそれ以降のオペレーティング システムのみ)|ルック アサイド リストのアドレス|予約済み|予約済み|ドライバーが初期化されていないルック アサイド リストを削除しようとしました。|
|0 xcc (Windows Vista およびそれ以降のオペレーティング システムのみ)|ルック アサイド リストのアドレス|プールの割り当ての開始アドレス|プールの割り当てのサイズ|ドライバーがアクティブなルック アサイド リストを含むプールの割り当てを解放しようとしました。|
|0 xcd (Windows Vista およびそれ以降のオペレーティング システムのみ)|ルック アサイド リストのアドレス|呼び出し元によって指定されたブロック サイズ|サポートされているブロック サイズを最小値|ドライバーがアロケーション ブロック サイズが小さすぎるとルック アサイド リストを作成しようとしました。|
|0xD0 (Windows Vista およびそれ以降のオペレーティング システムのみ)|次の構造体のアドレス|予約済み|予約済み|ドライバーが、次の構造を再初期化しようとしました。|
|0xD1 (Windows Vista およびそれ以降のオペレーティング システムのみ)|次の構造体のアドレス|予約済み|予約済み|ドライバーが初期化されていない、次の構造を削除しようとしました。|
|0xD2 (Windows Vista およびそれ以降のオペレーティング システムのみ)|次の構造体のアドレス|プールの割り当ての開始アドレス|プールの割り当てのサイズ|ドライバーがアクティブなスケジュール作成構造体を含むプールの割り当てを解放しようとしました。|
|0xD5 (Windows Vista およびそれ以降のオペレーティング システムのみ)|ドライバーのチェック ビルド バージョンで作成された IO_REMOVE_LOCK 構造体のアドレス|現在[IoReleaseRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelock)タグ|予約済み|現在[IoReleaseRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelock)タグが、以前と一致しない[IoAcquireRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)タグ。 チェック ビルドで呼び出す IoReleaseRemoveLock ドライバーがない場合、パラメーター 2 は、ドライバーの代わりに、ドライバーの検証ツールによって作成されたシャドウ IO_REMOVE_LOCK 構造体のアドレスになります。 この場合は、Driver Verifier は、すべての削除ロック Api のロックのアドレスを置き換えるためには、ドライバーによって使用される IO_REMOVE_LOCK 構造体のアドレスはまったく、使用されることはできません。 このパラメーターでのバグ チェックでは、Driver Verifier の I/O の検証オプションがアクティブな場合にのみ発生します。|
|ように (Windows Vista およびそれ以降のオペレーティング システムのみ)|ドライバーのチェック ビルド バージョンで作成された IO_REMOVE_LOCK 構造体のアドレス|前に一致しないタグ[IoAcquireRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)タグ|以前[IoAcquireRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)タグ|現在[IoReleaseRemoveLockAndWait](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelockandwait)タグが、以前と一致しない[IoAcquireRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)タグ。 場合、ドライバーの呼び出し元[IoReleaseRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelock)チェックのビルドでないパラメーター 2 は、ドライバーの代わりに、ドライバーの検証ツールによって作成されたシャドウ IO_REMOVE_LOCK 構造体のアドレス。 この場合は、Driver Verifier は、すべての削除ロック Api のロックのアドレスを置き換えるためには、ドライバーによって使用される IO_REMOVE_LOCK 構造体のアドレスはまったく、使用されることはできません。 このパラメーターでのバグ チェックでは、Driver Verifier の I/O の検証オプションがアクティブな場合にのみ発生します。|
|0xD7 (Windows 7 オペレーティング システム以降のみ)|Driver Verifier によって内部的に使用されるチェック ビルドの削除ロックの構造体のアドレス|ドライバーによって指定されるロックの解除構造体のアドレス|予約済み|呼び出された後も、ロックの解除が再初期化することはできません[IoReleaseRemoveLockAndWait](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelockandwait)他のスレッドにそのロックを使うことがまだ可能性があるため、(呼び出して[IoAcquireRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock))。 ドライバーはする必要があります、そのデバイスの拡張機能内でロックの解除を割り当てるし、1 回だけ初期化します。 ロックは、デバイスの拡張機能と共に削除されます。|
|0 xda (Windows Vista およびそれ以降のオペレーティング システムのみ)|ドライバーの開始アドレス|ドライバー内部の WMI コールバック アドレス|予約済み|WMI のコールバック関数を登録解除がないドライバーをアンロードしようとしました。|
|0 xdb (Windows Vista およびそれ以降のオペレーティング システムのみ)|デバイス オブジェクトのアドレス|予約済み|予約済み|WMI から登録解除がないデバイス オブジェクトを削除する試行されました。|
|0xDC (Windows Vista およびそれ以降のオペレーティング システムのみ)|予約済み|予約済み|予約済み|RegHandle 値が無効ですが、関数のパラメーターとして指定された[EtwUnregister](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-etwunregister)します。|
|0 xdd を設定 (Windows Vista およびそれ以降のオペレーティング システムのみ)|EtwRegister への呼び出しのアドレス|アンロードのドライバーの開始アドレス|Windows 8 およびそれ以降のバージョンでは、このパラメーターは、ETW RegHandle 値です。|呼び出さずにドライバーをアンロードしよう[EtwUnregister](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-etwunregister)します。|
|0 xdf (Windows 7 オペレーティング システム以降のみ)|同期オブジェクトのアドレス|同期オブジェクトは、アドレス スペースのセッションでです。 同期オブジェクトは、別のセッションまたはセッションの仮想アドレス空間がないシステムのスレッドから操作できるため、セッションのアドレス空間では許可されません。|
|0xE0 (Windows Vista およびそれ以降のオペレーティング システムのみ)|パラメーターとして使用されるユーザー モード アドレス|パラメーターとして使用されるアドレス範囲のバイト単位のサイズ|予約済み|ユーザー モード アドレスをパラメーターとして指定されているオペレーティング システム カーネル関数を呼び出しが行われました。|
|0xE1 (Windows Vista およびそれ以降のオペレーティング システムのみ)|同期オブジェクトのアドレス|予約済み|予約済み|アドレスが無効であるか、ページングを同期オブジェクトが検出されました。|
|0 xe2 (Windows Vista およびそれ以降のオペレーティング システムのみ)|IRP のアドレス|ユーザー モード アドレス IRP に存在します。|予約済み|-> Requestormode での Irp で IRP kernelmode であるに設定がユーザー モード アドレスをそのメンバーの 1 つとしてが見つかりました。|
|0xE3 (Windows Vista およびそれ以降のオペレーティング システムのみ)|API への呼び出しのアドレス|API のパラメーターとして使用されるユーザー モード アドレス|予約済み|ドライバーは、パラメーターとしてユーザー モード アドレスを使用してカーネル モード ZwXxx ルーチンへの呼び出しをしました。|
|0xE4 (Windows Vista およびそれ以降のオペレーティング システムのみ)|API への呼び出しのアドレス|形式が正しくない UNICODE_STRING 構造体のアドレス|予約済み|ドライバーは、パラメーターとして形式が正しくない UNICODE_STRING 構造でのカーネル モード ZwXxx ルーチンへの呼び出しをしました。|
|0xE5 (Windows Vista およびそれ以降のオペレーティング システムのみ)|現在の IRQL|予約済み|予約済み|不適切な IRQL でカーネル api 呼び出しが行われました。|
|0xE6 (Windows Vista およびそれ以降のオペレーティング システムのみ)|Zw API 呼び出しを行うドライバー内部アドレスします。|現在の IRQL|特別なカーネル Apc です。|IRQL でカーネル Zw API が呼び出されていない = PASSIVE_LEVEL と特別なカーネル Apc を有効にします。|
|0 xea (Windows Vista およびそれ以降のオペレーティング システムのみ)|現在の IRQL|スレッドの APC の無効化の数|Pushlock のアドレス|ドライバーは Apc が有効になっている、pushlock を取得しようとしています。|
|0xEB (Windows Vista およびそれ以降のオペレーティング システムのみ)|現在の IRQL|スレッドの APC の無効化の数|Pushlock のアドレス|ドライバーは、Apc が有効になっている、pushlock を解放しようとしました。|
|(Windows Vista およびそれ以降のオペレーティング システムのみ) は 0xf0 です.|コピー先のバッファーのアドレス|ソース バッファーのアドレス|コピーするバイト数|ドライバーには、重複するソースと変換先のバッファーを使用して、memcpy 関数が呼び出されます。|
|0xF5 (Windows Vista およびそれ以降のオペレーティング システムのみ)|NULL ハンドルのアドレス|オブジェクトの種類|予約済み|ドライバーには NULL を識別するハンドルが渡される[ObReferenceObjectByHandle](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)します。|
|0xF6 (Windows 7 オペレーティング システムおよびそれ以降)|参照されている値を処理します。|現在のプロセスのアドレス|ドライバーが正しくない参照を実行する内部アドレスします。|ドライバーは、カーネル モードとして、ユーザー モードのハンドルを参照します。|
|0xF7 (Windows 7 オペレーティング システムおよびそれ以降)|呼び出し元によって指定された値を処理します。|呼び出し元によって指定されたオブジェクトの種類|呼び出し元によって指定されたアクセス モード|ドライバーは、システム プロセスのコンテキストでのカーネル ハンドルのユーザー モードの参照を試みています。|
|0xFA (Windows 7 オペレーティング システムおよびそれ以降)|完了ルーチンのアドレス。|完了ルーチンを呼び出す前に、IRQL の値|完了ルーチンを呼び出した後、現在の IRQL 値|ルーチンの IRQL と一致する IRQL で返される IRP の完了ルーチンが呼び出されました。|
|0xFB (Windows 7 オペレーティング システムおよびそれ以降)|完了ルーチンのアドレス|現在のスレッドの APC の無効化の数|スレッドの APC IRP の完了ルーチンを呼び出す前に、カウントを無効にします。|スレッドの APC の無効化の数は、ドライバーの IRP の完了ルーチンによって変更されました。 APC の無効化カウントがデクリメントされますドライバーを呼び出すたびに[KeEnterCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)、 [FsRtlEnterFileSystem](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlenterfilesystem)、または、ミュー テックスを取得します。 APC の無効化の数には、ドライバーを呼び出すたびがインクリメントされます[KeLeaveCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleavecriticalregion)、 [KeReleaseMutex](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasemutex)、または[FsRtlExitFileSystem](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlexitfilesystem)します。 これらの呼び出しは、ペアで常にする必要があります、APC の無効化の数はスレッドが終了したときに、その 0 にする必要があります。 負の値は、ドライバーにそれらを再度有効にすることがなく APC 呼び出しが無効になっていることを示します。 正の値は、逆が true であることを示します。|
|0x105 (Windows 7 オペレーティング システムおよびそれ以降)|IRP のアドレス|ドライバーでは、IoFreeIrp ではなく ExFreePool を使用して、IRP をリリースします。|
|0x10A (Windows 7 オペレーティング システムおよびそれ以降)|ドライバーは、アイドル状態のプロセスにプールに対するクォータを請求しようとします。|
|0x10B (Windows 7 オペレーティング システムおよびそれ以降)|ドライバーは、DPC ルーチンからプールに対するクォータを請求しようとします。 これが、現在のプロセスのコンテキストが定義されているためには正しくありません。|
|0x110 (Windows 7 オペレーティング システムおよびそれ以降)|割り込みサービス ルーチンのアドレス|ISR を実行する前に保存された拡張コンテキストのアドレス|ISR を実行後に、拡張コンテキストのアドレスは保存されました|ドライバーの割り込みサービス ルーチン (ISR) には、拡張のスレッド コンテキストが破損しています。|
|0x111 (Windows 7 オペレーティング システムおよびそれ以降)|割り込みサービス ルーチンのアドレス|IRQL ISR を実行する前に|IRQL ISR を実行した後|割り込みサービス ルーチンには、変更された IRQL が返されます。|
|0x115 (Windows 7 オペレーティング システムおよびそれ以降)|デッドロックがシャット ダウンを担当するスレッドのアドレス|Driver Verifier には、システムは、20 分以上かかっているし、シャット ダウンが完了していないことが検出されました。|
|0x11A (Windows 7 オペレーティング システムおよびそれ以降)|現在の IRQL|ドライバーは、IRQL で KeEnterCriticalRegion を呼び出す > APC_LEVEL します。|
|0x11B (Windows 7 オペレーティング システムおよびそれ以降)|現在の IRQL|ドライバーは、IRQL で KeLeaveCriticalRegion を呼び出す > APC_LEVEL します。|
|0x120 (Windows 7 オペレーティング システムおよびそれ以降)|IRQL の値のアドレス|上で待機するオブジェクトのアドレス|タイムアウト値のアドレス|IRQL でスレッドが待機する > DISPATCH_LEVEL します。 Kewaitforsingleobject の 1 または KeWaitForMultipleObjects の呼び出し元は、IRQL で実行する必要があります < = DISPATCH_LEVEL します。|
|0x121 (Windows 7 オペレーティング システムおよびそれ以降)|IRQL の値のアドレス|上で待機するオブジェクトのアドレス|タイムアウト値のアドレス|IRQL equals DISPATCH_LEVEL でスレッドが待機して、タイムアウト値は NULL です。 Kewaitforsingleobject の 1 または KeWaitForMultipleObjects の呼び出し元は、IRQL で実行できる < = DISPATCH_LEVEL します。 NULL ポインターは、タイムアウトの指定した場合、呼び出し元のスレッドは、オブジェクトがシグナル状態になるまで待機状態に残ります。|
|0x122 (Windows 7 オペレーティング システムおよびそれ以降)|IRQL の値のアドレス|上で待機するオブジェクトのアドレス|タイムアウト値のアドレス|DISPATCH_LEVEL でスレッドが待機して、タイムアウト値がゼロ (0) と等しくないです。 場合、タイムアウト! = 0、kewaitforsingleobject の 1 または KeWaitForMultipleObjects の呼び出し元は、IRQL で実行する必要があります < APC_LEVEL を = です。|
|0x123 (Windows 7 オペレーティング システムおよびそれ以降)|上で待機するオブジェクトのアドレス|Kewaitforsingleobject の 1 または KeWaitForMultipleObjects の呼び出し元がユーザー モードでは、として、待機を指定するが、オブジェクトが、カーネル スタックにします。|
|0x130 (Windows 7 オペレーティング システムおよびそれ以降)|作業項目のアドレス|作業項目は、アドレス スペースのセッションでは。 作業項目は、別のセッションまたはセッションの仮想アドレス空間がないシステムのスレッドから操作できるため、セッションのアドレス空間では許可されません。|
|0x131 (Windows 7 オペレーティング システムおよびそれ以降)|作業項目のアドレス|作業項目は、ページング可能なメモリがします。 作業項目は、DISPATCH_LEVEL でカーネルを使用するために、非ページング メモリに存在する必要です。|
|0x135|IRP のアドレス|間 (ミリ秒) の数が許可されている、 [IoCancelIrp](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocancelirp)呼び出しとこの IRP の完了|取り消された IRP では、ドライバーが取り消された IRP の完了に予想よりも長くなります。 予定時刻では完了しませんでした。|
|0x13A|解放されてプールのブロックのアドレス|値が正しくありません。|正しくない値のアドレス|ドライバーが呼び出されて[ExFreePool](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool) Driver Verifier は、プールの使用状況を追跡するために使用される内部値のいずれかでエラーを検出したとします。|
|0x13B|解放されてプールのブロックのアドレス|正しくない値のアドレス|不適切なメモリのページへのポインターのアドレス|ドライバーが呼び出されて[ExFreePool](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool) Driver Verifier は、プールの使用状況を追跡するために使用される内部値のいずれかでエラーを検出したとします。|
|0x13C|解放されてプールのブロックのアドレス|値が正しくありません。|正しくない値のアドレス|ドライバーが呼び出されて[ExFreePool](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool) Driver Verifier は、プールの使用状況を追跡するために使用される内部値のいずれかでエラーを検出したとします。|
|0x13D|解放されてプールのブロックのアドレス|正しくない値のアドレス|正しい値が必要としました。|ドライバーが呼び出されて[ExFreePool](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool) Driver Verifier は、プールの使用状況を追跡するために使用される内部値のいずれかでエラーを検出したとします。|
|0x13E|呼び出し元で指定されたプールのブロック アドレス|Driver Verifier によって追跡されるブロックのアドレスのプール|Driver Verifier によって追跡されたプールのブロックのアドレスへのポインター|プールのブロックの呼び出し元で指定されたアドレス[ExFreePool](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool) Driver Verifier によって追跡されるアドレスとは異なります。|
|0x13F|解放されてプールのブロックのアドレス|解放されるバイト数|Driver Verifier によって追跡されるバイト数へのポインター|呼び出しで解放されるメモリのバイト数[ExFreePool](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool) Driver Verifier によって追跡されるバイト数とは異なります。|
|0x140|現在の IRQL|MDL アドレス|この MDL に関連付けられている仮想アドレス|ロックされていない MDL はメモリ ページング可能なまたは購入から構築されています。|
|0x1000 |リソースのアドレス|予約済み|予約済み|自己デッドロックが発生します。現在のスレッドが再帰的にしようとしたリソースを取得します。 このパラメーターでのバグ チェックでは、Driver Verifier のデッドロック検出オプションがアクティブな場合にのみ発生します。|
|0x1001 |最終的なデッドロックの原因となったリソースのアドレス|予約済み|予約済み|デッドロック:ロック階層の違反が検出されました。 このパラメーターでのバグ チェックでは、Driver Verifier のデッドロック検出オプションがアクティブな場合にのみ発生します。 (使用して、 [! デッドロック](-deadlock.md)についてさらに拡張機能です)。|
|0x1002 |リソースのアドレス|予約済み|予約済み|初期化されていないリソース:リソースが最初に初期化されていないことがなく取得されました。 このパラメーターでのバグ チェックでは、Driver Verifier のデッドロック検出オプションがアクティブな場合にのみ発生します。|
|0x1003 |アドレスが解放されるリソースのデッドロック|最初に解放されている必要のあるリソースのアドレス|予約済み|予期しないリリース:間違った順序でリソースがリリースされました。 このパラメーターでのバグ チェックでは、Driver Verifier のデッドロック検出オプションがアクティブな場合にのみ発生します。|
|0x1004 |リソースのアドレス|リソースを取得したスレッドのアドレス|現在のスレッドのアドレス|予期しないスレッド:間違ったスレッドでは、リソースを解放します。 このパラメーターでのバグ チェックでは、Driver Verifier のデッドロック検出オプションがアクティブな場合にのみ発生します。|
|0x1005 |リソースのアドレス|予約済み|予約済み|複数の初期化:リソースは、1 つ以上の時間に初期化されます。 このパラメーターでのバグ チェックでは、Driver Verifier のデッドロック検出オプションがアクティブな場合にのみ発生します。|
|0x1007 |リソースのアドレス|予約済み|予約済み|取得していないリソース:取得する前に、リソースが解放されます。 このパラメーターでのバグ チェックでは、Driver Verifier のデッドロック検出オプションがアクティブな場合にのみ発生します。|
|0x1008 (Windows 7 オペレーティング システムおよびそれ以降)|ロックのアドレス|Driver Verifier の内部データ|Driver Verifier の内部データ|ドライバーは、このロックの種類に一致しない API を使用してロックを取得しようとしました。|
|0x1009 (Windows 7 オペレーティング システムおよびそれ以降)|ロックのアドレス|Driver Verifier の内部データ|Driver Verifier の内部データ|ドライバーは、このロックの種類に一致しない API を使用してロックを解放しようとしました。|
|0x100A (Windows 7 オペレーティング システムおよびそれ以降)|所有者のスレッドのアドレス|Driver Verifier の内部データ|終了したスレッドは、ロックを所有しています。|
|0x100B (Windows 7 オペレーティング システムおよびそれ以降)|ロックのアドレス|所有者のスレッドのアドレス|Driver Verifier の内部アドレス|削除ロックのスレッドによって所有されています。|
|0xA001 (オペレーティング システムを Windows 8.1 以降)|NetBufferList オブジェクトへのポインター|仮想スイッチのオブジェクト (場合 NULL 以外) へのポインター|予約済み (未使用)|VM のスイッチ:呼び出し元が指定 NetBufferList SourceHandle を設定する必要があります。 参照してください、 [AllocateNetBufferListForwardingContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)ルーチン。|
|0xA002 (オペレーティング システムを Windows 8.1 以降)|NetBufferList オブジェクトへのポインター|仮想スイッチのオブジェクト (場合 NULL 以外) へのポインター。|予約済み (未使用)|VM のスイッチ:指定された呼び出し元 NetBufferList の転送の詳細は 0 ではありません。 参照してください、 [AllocateNetBufferListForwardingContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)ルーチン。|
|0xA003 (オペレーティング システムを Windows 8.1 以降)|NetBufferList オブジェクトへのポインター|仮想スイッチのオブジェクト (場合 NULL 以外) へのポインター。|予約済み (未使用)|VM のスイッチ:呼び出し元には、パケット ヘッダーまたは NULL であるルーティングのコンテキストでの NetBufferList が提供されます。 参照してください[拡張可能スイッチのデータ パスのパケットの管理ガイドライン](https://docs.microsoft.com/windows-hardware/drivers/network/packet-management-guidelines-for-the-extensible-switch-data-path)します。|
|0xA004 (オペレーティング システムを Windows 8.1 以降)|無効なポートの ID|NIC のインデックス|仮想スイッチのオブジェクト (場合 NULL 以外) へのポインター。|VM のスイッチ:呼び出し元は、無効なポートと NIC のインデックスの組み合わせを指定します。 参照してください[HYPER-V 拡張可能なスイッチ ポートとネットワーク アダプターの状態](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)します。|
|0xA005 (オペレーティング システムを Windows 8.1 以降)|NetBufferList オブジェクトへのポインター|宛先一覧へのポインター。|仮想スイッチのオブジェクト (場合 NULL 以外) へのポインター。|VM のスイッチ:呼び出し元は、無効な宛先を指定します。 参照してください[AddNetBufferListDestination](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)と[UpdateNetBufferListDestinations](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)します。|
|0xA006 (オペレーティング システムを Windows 8.1 以降)|NetBufferList オブジェクトへのポインター|仮想スイッチのオブジェクト (場合 NULL 以外) へのポインター。|予約済み (未使用)|VM のスイッチ:呼び出し元は、無効なソース NIC またはポート オブジェクトを指定します。 参照してください[HYPER-V 拡張可能なスイッチ ポートとネットワーク アダプターの状態](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)します。|
|0xA007 (オペレーティング システムを Windows 8.1 以降)|NetBufferList オブジェクトへのポインター|仮想スイッチのオブジェクト (場合 NULL 以外) へのポインター。|予約済み (未使用)|VM のスイッチ:呼び出し元は指定、無効なターゲット一覧です。 参照してください[AddNetBufferListDestination](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)と[UpdateNetBufferListDestinations](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)します。|
|0xA008 (オペレーティング システムを Windows 8.1 以降)|親 NIC オブジェクト|NIC のインデックス|仮想スイッチのオブジェクト (場合 NULL 以外) へのポインター。|VM のスイッチ:許可されていない場合、NIC を参照しようとしています。 参照してください[HYPER-V 拡張可能なスイッチ ポートとネットワーク アダプターの状態](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)します。|
|0xA009 (オペレーティング システムを Windows 8.1 以降)|参照されているポート|仮想スイッチのオブジェクト (場合 NULL 以外) へのポインター|予約済み (未使用)|VM のスイッチ:許可されていない場合、ポートを参照しようとしてください。 参照してください[HYPER-V 拡張可能なスイッチ ポートとネットワーク アダプターの状態](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)します。|
|0xA00A (オペレーティング システムを Windows 8.1 以降)|NetBufferList オブジェクトへのポインター|ContextTypeInfo オブジェクト|予約済み (未使用)|VM のスイッチ:エラーのコンテキストは既に設定されています。 参照してください[SetNetBufferListSwitchContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_set_net_buffer_list_switch_context)します。|
|0xA00B (オペレーティング システムを Windows 8.1 以降)|NetBufferList オブジェクトへのポインター|NDIS_SWITCH_REPORT_FILTERED_NBL_FLAGS_*|仮想スイッチのオブジェクト (場合 NULL 以外) へのポインター|VM のスイッチ:指定された無効な方向 NetBufferList を削除します。 参照してください[ReportFilteredNetBufferLists](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)します。|
|0xA00C (オペレーティング システムを Windows 8.1 以降)|NetBufferList オブジェクトへのポインター|フラグの値を送信します。|仮想スイッチのオブジェクト (場合 NULL 以外) へのポインター|VM のスイッチ:NetBufferList チェーンは、NDIS_SEND_FLAGS_SWITCH_SINGLE_SOURCE フラグが設定されている場合に、複数のソース ポートが。 参照してください[HYPER-V 拡張可能スイッチ送受信フラグ](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-send-and-receive-flags)します。|
|0xA00D (オペレーティング システムを Windows 8.1 以降)|NetBufferList オブジェクトへのポインター|仮想スイッチのコンテキストへのポインター|仮想スイッチのオブジェクト (場合 NULL 以外) へのポインター|VM のスイッチ:NDIS_RECEIVE_FLAGS_SWITCH_DESTINATION_GROUP フラグが設定されている場合、チェーン内の 1 つまたは複数の NetBufferLists から無効なターゲットがあります。 参照してください[HYPER-V 拡張可能スイッチ送受信フラグ](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-send-and-receive-flags)します。|
|0x2000 (Windows 7 オペレーティング システムおよびそれ以降)|渡される最初の引数、 [StorPortInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitialize)ルーチン。 このパラメーターは、オペレーティング システムは、ミニポート ドライバーの最初の引数のミニポート ドライバーに渡されるドライバー オブジェクトへのポインター [DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン。|渡される 2 番目の引数、 [StorPortInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitialize)ルーチン。 このパラメーターに渡されるオペレーティング システムのコンテキスト情報へのポインターは、2 番目の引数のミニポート ドライバーのミニポート ドライバー [DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン。|予約済み|Storport ミニポート ドライバーに無効な引数 (NULL ポインター) を渡される、 [StorPortInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitialize)ルーチン。|
|0x00020002 (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlApcLte](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlapclte)します。 このルールは、ドライバーを呼び出す必要がありますを指定します[ObGetObjectSecurity](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obgetobjectsecurity)と[ObReleaseObjectSecurity](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreleaseobjectsecurity)場合にのみ IRQL < APC_LEVEL を = です。|
|0x00020003 (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlDispatch](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqldispatch)します。 IrqlDispatch ルール、ドライバーが特定のルーチンを呼び出す必要がありますを指定する場合にのみ IRQL = DISPATCH_LEVEL|
|0x00020004 (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlExAllocatePool](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexallocatepool)します。 IrqlExAllocatePool ルールでは、ドライバーを呼び出すことを指定します[exallocatepoolwithtag に](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)と[ExAllocatePoolWithTagPriority](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtagpriority) IRQL で場合にのみ < = DISPATCH_LEVEL します。|
|0x00020005 (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlExApcLte1](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexapclte1)します。 IrqlExApcLte1 ルールは、ドライバーを呼び出す ExAcquireFastMutex と ExTryToAcquireFastMutex IRQL でのみを指定します < APC_LEVEL を = です。|
|0x00020006 (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlExApcLte2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。 IrqlExApcLte2 ルールを指定、ドライバーが、特定のルーチンを呼び出す場合にのみ IRQL < APC_LEVEL を = です。|
|0x00020007 (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlExApcLte3](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexapclte3)します。 IrqlExApcLte3 ルール、ドライバーが特定のエグゼクティブ サポート ルーチンを呼び出す必要がありますを指定する場合にのみ IRQL < APC_LEVEL を =。|
|0x00020008 (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlExPassive](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexpassive)します。 IrqlExPassive ルール、ドライバーが特定のエグゼクティブ サポート ルーチンを呼び出す必要がありますを指定する場合にのみ IRQL PASSIVE_LEVEL を =。|
|0x00020009 (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlIoApcLte](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlioapclte)します。 IrqlIoApcLte ルール、ドライバーが特定の I/O マネージャー ルーチンを呼び出す必要がありますを指定する場合にのみ IRQL < APC_LEVEL を =。|
|0x0002000A (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlIoPassive1](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive1)します。 IrqlIoPassive1 ルール、ドライバーが特定の I/O マネージャー ルーチンを呼び出す必要がありますを指定する場合にのみ IRQL PASSIVE_LEVEL を =。|
|0x0002000B (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlIoPassive2](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive2)します。 IrqlIoPassive2 ルール、ドライバーが特定の I/O マネージャー ルーチンを呼び出す必要がありますを指定する場合にのみ IRQL PASSIVE_LEVEL を =。|
|0x0002000C (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlIoPassive3](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive3)します。 IrqlIoPassive3 ルール、ドライバーが特定の I/O マネージャー ルーチンを呼び出す必要がありますを指定する場合にのみ IRQL PASSIVE_LEVEL を =。|
|0x0002000D (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlIoPassive4](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive4)します。 IrqlIoPassive4 ルール、ドライバーが特定の I/O マネージャー ルーチンを呼び出す必要がありますを指定する場合にのみ IRQL PASSIVE_LEVEL を =。|
|0x0002000E (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlIoPassive5](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive5)します。 IrqlIoPassive5 ルール、ドライバーが特定の I/O マネージャー ルーチンを呼び出す必要がありますを指定する場合にのみ IRQL PASSIVE_LEVEL を =。|
|0x0002000F (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlKeApcLte1](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkeapclte1)します。 IrqlKeApcLte1 ルール、ドライバーが特定のカーネル ルーチンを呼び出す必要がありますを指定する場合にのみ IRQL < APC_LEVEL を =。|
|0x00020010 (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlKeApcLte2](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkeapclte2)します。 IrqlKeApcLte2 ルール、ドライバーが特定のカーネル ルーチンを呼び出す必要がありますを指定する場合にのみ IRQL < APC_LEVEL を =。|
|0x00020011 (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlKeDispatchLte](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkedispatchlte)します。 IrqlKeDispatchLte ルール、ドライバーが特定のカーネル ルーチンを呼び出す必要がありますを指定する場合にのみ IRQL < = DISPATCH_LEVEL します。|
|0x00020015 (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlKeReleaseSpinLock](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkereleasespinlock)します。 IrqlKeReleaseSpinLock ルール、ドライバーが KeReleaseSpinLock を呼び出す必要がありますを指定する場合にのみ IRQL = DISPATCH_LEVEL します。|
|0x00020016 (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlKeSetEvent](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkesetevent)します。 IrqlKeSetEvent ルールでは、ことを指定します、 [KeSetEvent](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent)ルーチンは、IRQL でだけ呼び出されます。 < 待機は、IRQL で FALSE に設定されている場合は、DISPATCH_LEVEL を = < 待機が TRUE に設定されている場合は、APC_LEVEL を = です。|
|0x00020019 (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlMmApcLte](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlmmapclte)します。 IrqlMmApcLte ルールでは、こと、ドライバーする必要がありますルーチンを呼び出す特定のメモリ マネージャーを指定する場合にのみ IRQL < APC_LEVEL を = です。|
|0x0002001A (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlMmDispatch](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlmmdispatch)します。 IrqlMmDispatch ルールでは、ドライバーを呼び出す必要がありますを指定します[MmFreeContiguousMemory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmfreecontiguousmemory)場合にのみ IRQL = DISPATCH_LEVEL します。|
|0x0002001B (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlObPassive](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlobpassive)します。 IrqlObPassive ルールでは、ドライバーを呼び出す必要がありますを指定します[ObReferenceObjectByHandle](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)場合にのみ IRQL PASSIVE_LEVEL を = です。|
|0x0002001C (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlPsPassive](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlpspassive)します。 IrqlPsPassive ルール呼び出すを指定すること、ドライバーする必要があります特定のプロセスとスレッド マネージャー ルーチン場合にのみ IRQL PASSIVE_LEVEL を = です。|
|0x0002001D (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー DDI 準拠の規則に違反して[IrqlReturn](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlreturn)します。|
|0x0002001E (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlRtlPassive](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlrtlpassive)します。 IrqlRtlPassive ルールでは、ドライバーを呼び出す必要がありますを指定します[RtlDeleteRegistryValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtldeleteregistryvalue)場合にのみ IRQL PASSIVE_LEVEL を = です。|
|0x0002001F (Windows 8 オペレーティング システムおよびそれ以降)|違反したルールの条件を説明する文字列へのポインター。|省略可能なポインターを規則には、variable(s) を記述します。|予約済み|ドライバー DDI 準拠の規則に違反して[IrqlZwPassive](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlzwpassive)します。 IrqlZwPassive ルールでは、ドライバーを呼び出す必要がありますを指定します[ZwClose](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)場合にのみ IRQL PASSIVE_LEVEL を = です。|
|0x00020022 (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|予約済み (未使用)|予約済み (未使用)|ドライバー DDI 準拠の規則に違反して[IrqlIoDispatch](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliodispatch)します。|
|0x00040003 (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー DDI 準拠の規則に違反して[CriticalRegions](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-criticalregions)します。|
|0x00040006 (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー DDI 準拠の規則に違反して[QueuedSpinLock](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-queuedspinlock)します。|
|0x00040007 (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー DDI 準拠の規則に違反して[QueuedSpinLockRelease](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-queuedspinlockrelease)します。|
|0x00040009 (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー DDI 準拠の規則に違反して[スピンロック](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-spinlock)します。|
|0x0004000B (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー DDI 準拠の規則に違反して[SpinlockRelease](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-spinlockrelease)します。|
|0x0004000E (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー DDI 準拠の規則に違反して[GuardedRegions](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-guardedregions)します。|
|0x0004100B (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|予約済み|予約済み|ドライバー DDI 準拠の規則に違反して[RequestedPowerIrp](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-requestedpowerirp)します。|
|0x0004100F (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー DDI 準拠の規則に違反して[IoSetCompletionExCompleteIrp](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-iosetcompletionexcompleteirp)します。|
|0x00043006 (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|予約済み|予約済み|ドライバー DDI 準拠の規則に違反して[PnpRemove](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-pnpremove)します。|
|0x00091001 (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー DDI 準拠の規則に違反して[NdisOidComplete](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoidcomplete)します。|
|0x00091002 (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー DDI 準拠の規則に違反して[NdisOidDoubleComplete](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoiddoublecomplete)します。|
|0x0009100E (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー DDI 準拠の規則に違反して[NdisOidDoubleRequest](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoiddoublerequest)します。|
|0x00092003 (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー NDIS/WIFI 検証規則に違反して[NdisTimedOidComplete](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimedoidcomplete)します。|
|0x0009200D (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー NDIS/WIFI 検証規則に違反して[NdisTimedDataSend](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimeddatasend)します。|
|0x0009200F (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー NDIS/WIFI 検証規則に違反して[NdisTimedDataHang](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimeddatahang)します。|
|0x00093004 (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー NDIS/WIFI 検証規則に違反して[WlanAssociation](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlanassociation)します。|
|0x00093005 (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー NDIS/WIFI 検証規則に違反して[WlanConnectionRoaming](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlanconnectionroaming)します。|
|0x00093006 (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー NDIS/WIFI 検証規則に違反して[WlanDisassociation](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlandisassociation)します。|
|0x00094007 (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー NDIS/WIFI 検証規則に違反して[WlanTimedAssociation](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedassociation)します。|
|0x00094008 (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー NDIS/WIFI 検証規則に違反して[WlanTimedConnectionRoaming](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedconnectionroaming)します。|
|0x00094009 (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー NDIS/WIFI 検証規則に違反して[WlanTimedConnectRequest](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedconnectrequest)します。|
|0x0009400B (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー NDIS/WIFI 検証規則に違反して[WlanTimedLinkQuality](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedlinkquality)します。|
|0x0009400C (オペレーティング システムを Windows 8.1 以降)|違反したルールの条件を説明する文字列へのポインター。|内部ルールの状態のアドレス (2 番目の引数。 ruleinfo)。|補足的な状態のアドレス (3 番目の引数。 ruleinfo)。|ドライバー NDIS/WIFI 検証規則に違反して[WlanTimedScan](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedscan)します。|




<a name="cause"></a>原因
-----

原因の詳細については、パラメーター セクション内の各コードの説明を参照してください。 詳細についてを使用して取得できます、 [ **。-v を分析**](-analyze.md)拡張機能。

<a name="resolution"></a>解決方法
----------

このバグ チェックは、Driver Verifier が 1 つまたは複数のドライバーを監視するように指示された場合にのみ発生します。 Driver Verifier の使用は意図しない、非アクティブ化する必要があります。 この問題の原因となったドライバーを削除しても検討する可能性があります。

ドライバー開発者の場合は、このバグ チェックで得られた情報を使用して、コードで、バグを修正します。

詳細については、Driver Verifier は、次を参照してください。、 [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier) Windows Driver Kit (WDK) のセクション。

<a name="remarks"></a>注釈
-------

\_プール\_Ntddk.h の種類のコードが列挙されます。 具体的には、 **0**非ページ プールを示します (ゼロ) と**1**ページ プール (1 つ) ことを示します。

*(Windows 8 および Windows の以降のバージョン)* 場合[DDI 準拠の検査](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)実行、バグ チェック[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)のドライバのソース コードと (パラメーター 1 の値によって識別される) の原因となった DDI 準拠規則を指定バグ チェックします。 Static Driver Verifier は、ソース コードで、問題の原因を特定するのに役立ちます。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[バグ チェック時にドライバー検証機能を処理が有効になっています。](handling-a-bug-check-when-driver-verifier-is-enabled.md)

 

 




