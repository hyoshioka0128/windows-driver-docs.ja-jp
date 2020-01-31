---
title: バグチェック 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION
description: DRIVER_VERIFIER_DETECTED_VIOLATION バグチェックの値は0x000000C4 です。 これは、ドライバーの検証ツールによって検出された致命的なエラーの一般的なバグチェックコードです。
ms.assetid: 7814f827-05fc-419b-b428-4565978bbb52
keywords:
- バグチェック 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION
- DRIVER_VERIFIER_DETECTED_VIOLATION
ms.date: 01/28/2020
topic_type:
- apiref
api_name:
- DRIVER_VERIFIER_DETECTED_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c5b33af05f23102b994a738f6a1d30e9ff750729
ms.sourcegitcommit: 70c8e83900015eaea013fb742e5e137cfd08ca98
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2020
ms.locfileid: "76885361"
---
# <a name="bug-check-0xc4-driver_verifier_detected_violation"></a>バグチェック 0xC4: ドライバー\_VERIFIER\_検出された\_違反

ドライバー\_VERIFIER\_検出されました\_違反バグチェックの値は0x000000C4 です。 これは、ドライバーの検証ツールによって検出された致命的なエラーの一般的なバグチェックコードです。 詳細については、「[ドライバーの検証機能が有効になっている場合のバグチェックの処理](handling-a-bug-check-when-driver-verifier-is-enabled.md)」を参照してください。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

## <a name="driver_verifier_detected_violation-parameters"></a>DRIVER\_VERIFIER\_検出された\_違反パラメーター

パラメーター1は違反の種類を識別します。 残りのパラメーターの意味は、パラメーター1の値によって異なります。 パラメーター値については、次の表で説明します。

**注**  このテーブルの5つの列すべてを表示できない場合は、次の操作を試してください。
- ブラウザーウィンドウを拡張して、最大サイズにします。
- テーブルにカーソルを置き、方向キーを使用して左右にスクロールします。

### <a name="0x00-to-0x70"></a>0x00 から0x70 へ

|パラメーター1|パラメータ 2|パラメーター3|パラメーター4|エラーの原因|
|--- |--- |--- |--- |--- |
|0x00|現在の IRQL|プールの種類|バイト数|ドライバーがゼロバイトプール割り当てを要求しました。|
|0x01|現在の IRQL|プールの種類|割り当てのサイズ (バイト単位)|ドライバーは、IRQL > APC_LEVEL でページングされたメモリを割り当てようとしました。|
|0x02|現在の IRQL|プールの種類|割り当てのサイズ (バイト単位)|ドライバーは、IRQL > DISPATCH_LEVEL で非ページメモリを割り当てようとしました。|
|0x03| | | |呼び出し元は、の複数のページを割り当てようとしていますが、プールを成功させる必要がありますが、1ページはこの API で許可されている最大数です。 |
|0x10|無効なアドレス|0|0|ドライバーは、割り当て呼び出しから返されなかったアドレスを解放しようとしました。|
|0x11|現在の IRQL|プールの種類|プールのアドレス|ドライバーは、IRQL > APC_LEVEL でページプールを解放しようとしました。|
|0x12|現在の IRQL|プールの種類|プールのアドレス|ドライバーは、IRQL > DISPATCH_LEVEL の非ページプールを解放しようとしました。|
|0x13 または0x14|予約済み|プールヘッダーへのポインター|プールヘッダーの内容|ドライバーは既に解放されているメモリプールを解放しようとしました。|
|0x15|タイマーの入力|プールの種類|解放されるプールアドレス|呼び出し元が解放しようとしているプールには、アクティブなタイマーが含まれています。|
|0x16|予約済み|プールアドレス|0|ドライバーが無効なアドレスでプールを解放しようとしたか、ドライバーが無効なパラメーターをメモリルーチンに渡しました。|
|0X17|リソースエントリ | プールの種類 |解放されるプールアドレス |呼び出し元が解放しようとしているプールには、アクティブなリソースグループが含まれています。 |
|0x30|現在の IRQL|要求された IRQL|0|ドライバーが[Keraiseirql](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)に無効なパラメーターを渡しました。 (パラメーターが、現在の IRQL より小さい値か、HIGH_LEVEL より大きい値です。 初期化されていないパラメーターを使用したことが原因である可能性があります)。|
|0x31|現在の IRQL|要求された IRQL|0: 新しい IRQL が正しくありません 1: DPC ルーチン内で新しい IRQL が無効です|ドライバーが[Ke-irql](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql~r1)に無効なパラメーターを渡しました。 (パラメーターが、現在の IRQL より大きい値か、HIGH_LEVEL より大きい値です。 初期化されていないパラメーターを使用したことが原因である可能性があります)。|
|~|現在の IRQL|スピンロックアドレス|0|ドライバーは、DISPATCH_LEVEL 以外の IRQL で[KeReleaseSpinLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)を呼び出しました。 (これは、スピンロックが二重にリリースされていることが原因である可能性があります)。|
|0x33|現在の IRQL|高速ミューテックスアドレス|0|ドライバーは、IRQL > APC_LEVEL を含む高速ミューテックスを取得しようとしました。|
|0x34|現在の IRQL|スレッド APC の無効化カウント|高速ミューテックスアドレス|ドライバーは、APC_LEVEL 以外の IRQL で高速ミューテックスを解放しようとしました。|
|0x35|現在の IRQL|スピンロックアドレス|古い IRQL|カーネルは、IRQL が DISPATCH_LEVEL と等しくないスピンロックを解放しました。|
|0x36|現在の IRQL|スピンロック番号|古い IRQL|カーネルは、DISPATCH_LEVEL と等しくない IRQL を持つキューに置かれたスピンロックを解放しました。|
|0x37|現在の IRQL|スレッド APC の無効化カウント|リソース|ドライバーはリソースを取得しようとしましたが、Apc が無効になっていません。|
|0x38|現在の IRQL|スレッド APC の無効化カウント|リソース|ドライバーはリソースを解放しようとしましたが、Apc は無効になっていません。|
|0x39)|現在の IRQL|スレッド APC の無効化カウント|ロック|ドライバーは、エントリの APC_LEVEL と等しくない IRQL を持つミューテックス "unsafe" を取得しようとしました。|
|0x3A|現在の IRQL|スレッド APC の無効化カウント|ロック|ドライバーは、エントリの APC_LEVEL と等しくない IRQL を持つミューテックス "unsafe" を解放しようとしました。|
|0x3B|現在の IRQL|待機するオブジェクト|タイムアウトパラメーター|KeWaitXxx ルーチンは DISPATCH_LEVEL 以降で呼び出されています。|
|0X3c です|ルーチンに渡されたハンドル|［オブジェクトの種類］|0|ドライバーは、不適切なハンドルで[Obreferenceobjectbyhandle](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)を呼び出しました。|
|0x3D|0|0|無効なリソースのアドレス|ドライバーが不適切な (整列されていない) リソースを[ExAcquireResourceExclusive](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)に渡しました。|
|0x3E|0|0|0|このドライバーは、現在クリティカルなリージョンに存在しないスレッドの[KeLeaveCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)を呼び出しました。|
|0x3F|オブジェクトのアドレス|新しいオブジェクト参照の数。 -1: 逆参照ケース 1: 参照ケース|0|ドライバーは、参照カウントが0のオブジェクトに[Obreferenceobject](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)を適用しました。または、 [ObDereferenceObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)が参照カウントが0のオブジェクトに適用されたドライバーです。|
|0x40|現在の IRQL|スピンロックアドレス|0|[KeAcquireSpinLockAtDpcLevel](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel)というドライバーは、IRQL < DISPATCH_LEVEL を呼び出しました。|
|0x41|現在の IRQL|スピンロックアドレス|0|[KeReleaseSpinLockFromDpcLevel](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)というドライバーは、IRQL < DISPATCH_LEVEL を呼び出しました。|
|0x42|現在の IRQL|スピンロックアドレス|0|[KeAcquireSpinLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)というドライバーは、IRQL > DISPATCH_LEVEL を呼び出しました。|
|0x51|割り当てのベースアドレス|割り当てを超える参照のアドレス|課金されるバイト数|割り当ての終了後に書き込んだ後に、ドライバーがメモリを解放しようとしました。 このパラメーターを使用したバグチェックは、ドライバー検証ツールのプール追跡オプションがアクティブな場合にのみ行われます。|
|0x52|割り当てのベースアドレス|ハッシュエントリ|課金されるバイト数|割り当ての終了後に書き込んだ後に、ドライバーがメモリを解放しようとしました。 このパラメーターを使用したバグチェックは、ドライバー検証ツールのプール追跡オプションがアクティブな場合にのみ行われます。|
|0x53|割り当てのベースアドレス|Header|予約済み|割り当ての終了後に書き込んだ後に、ドライバーがメモリを解放しようとしました。 このパラメーターを使用したバグチェックは、ドライバー検証ツールのプール追跡オプションがアクティブな場合にのみ行われます。|
|0x54|割り当てのベースアドレス|予約済み|プールのハッシュサイズ|割り当ての終了後に書き込んだ後に、ドライバーがメモリを解放しようとしました。 このパラメーターを使用したバグチェックは、ドライバー検証ツールのプール追跡オプションがアクティブな場合にのみ行われます。|
|0x59|割り当てのベースアドレス|Listindex|予約済み|割り当ての終了後に書き込んだ後に、ドライバーがメモリを解放しようとしました。 このパラメーターを使用したバグチェックは、ドライバー検証ツールのプール追跡オプションがアクティブな場合にのみ行われます。|
|0x60|ページプールから割り当てられたバイト数|非ページプールから割り当てられたバイト数|解放されなかった割り当ての合計数|ドライバーは、最初にプール割り当てを解放せずにアンロードされています。 このパラメーターを使用したバグチェックは、ドライバー検証ツールのプール追跡オプションがアクティブな場合にのみ行われます。|
|0x61|ページプールから割り当てられたバイト数|非ページプールから割り当てられたバイト数|解放されなかった割り当ての合計数|ドライバーのスレッドが、ドライバーのアンロード中にプールのメモリを割り当てようとしています。 このパラメーターを使用したバグチェックは、ドライバー検証ツールのプール追跡オプションがアクティブな場合にのみ行われます。|
|0x62|ドライバーの名前|予約済み|ページングされたプールと非ページプールを含む、解放されなかった割り当ての合計数|ドライバーは、最初にプール割り当てを解放せずにアンロードされています。 このパラメーターを使用したバグチェックは、ドライバー検証ツールのプール追跡オプションがアクティブな場合にのみ行われます。 バグチェックの原因となった割り当てに関する情報を入力します。|
|0x6F|MDL アドレス|ロックされている物理ページ|システムの最上位の物理ページ|MmProbeAndLockPages PFN データベースにないページで呼び出されました。 これは通常、独自のプライベート dualport RAM をロックするために、このルーチンを呼び出すドライバーです。  これは必要ではないだけでなく、連続していない物理 RAM があるコンピューター上のメモリを破壊することもできます。|

### <a name="0x70-to-0x91"></a>0x70 を0x91 に

|パラメーター1|パラメータ 2|パラメーター3|パラメーター4|エラーの原因|
|--- |--- |--- |--- |--- |
|0x70|現在の IRQL|MDL アドレス|アクセスモード|[MmProbeAndLockPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)というドライバーは、IRQL > DISPATCH_LEVEL を呼び出しました。|
|0x71|現在の IRQL|MDL アドレス|プロセスアドレス|MmProbeAndLockProcessPages というドライバーは、IRQL > DISPATCH_LEVEL を呼び出しました。|
|0x72|現在の IRQL|MDL アドレス|プロセスアドレス|MmProbeAndLockSelectedPages というドライバーは、IRQL > DISPATCH_LEVEL を呼び出しました。|
|0x73|現在の IRQL|32ビット Windows:64 ビット Windows での物理アドレスの低32ビット:64 ビットの物理アドレス|バイト数|IRQL > DISPATCH_LEVEL の[Mmmapiospace](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace)というドライバーが使用されています。|
|0x74|現在の IRQL|MDL アドレス|アクセスモード|ドライバーは、IRQL > DISPATCH_LEVEL を使用してカーネルモードで[MmMapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages)を呼び出しました。|
|0x75|現在の IRQL|MDL アドレス|アクセスモード|ドライバーは、IRQL > APC_LEVEL を持つユーザーモードでの[MmMapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages)を呼び出しました。|
|0x76|現在の IRQL|MDL アドレス|アクセスモード|ドライバーは、IRQL > DISPATCH_LEVEL を使用してカーネルモードで[MmMapLockedPagesSpecifyCache](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache)を呼び出しました。|
|0x77|現在の IRQL|MDL アドレス|アクセスモード|ドライバーは、IRQL > APC_LEVEL を持つユーザーモードでの[MmMapLockedPagesSpecifyCache](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache)を呼び出しました。|
|0x78|現在の IRQL|MDL アドレス|0|[MmUnlockPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages)というドライバーは、IRQL > DISPATCH_LEVEL を呼び出しました。|
|0x79|現在の IRQL|マップされていない仮想アドレス|MDL アドレス|ドライバーは、IRQL > DISPATCH_LEVEL を使用してカーネルモードで[MmUnmapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmaplockedpages)を呼び出しました。|
|0X7a)|現在の IRQL|マップされていない仮想アドレス|MDL アドレス|ドライバーは、IRQL > APC_LEVEL を持つユーザーモードでの[MmUnmapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmaplockedpages)を呼び出しました。|
|0x7B|現在の IRQL|マップされていない仮想アドレス|バイト数|[Mmunmapiospace](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace)と IRQL > APC_LEVEL というドライバーが使用されています。|
|0x7C|MDL アドレス|MDL フラグ|0|このドライバーは[MmUnlockPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages)という名前で、ページが正常にロックされていない MDL を渡しました。|
|0x7D|MDL アドレス|MDL フラグ|0|このドライバーは[MmUnlockPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages)という名前で、ページプールからのページを含む MDL を渡しました。 (ロックを解除することはできません)。|
|0x7E|現在の IRQL|DISPATCH_LEVEL|0|[MmAllocatePagesForMdl](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdl)、 [MmAllocatePagesForMdlEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdlex)、または[mmfreeDISPATCH_LEVEL](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreepagesfrommdl)というドライバーは、IRQL > と呼ばれていました。|
|0x7F|現在の IRQL|MDL アドレス|MDL フラグ|ドライバーは[BuildMdlForNonPagedPool](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool)という名前で、ページプールからページを持つ MDL を渡しました。|
|0x80|現在の IRQL|イベントアドレス|0|[KeSetEvent](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)というドライバーは、IRQL > DISPATCH_LEVEL を呼び出しました。|
|0x81|MDL アドレス|MDL フラグ|0|ドライバーは[MmMapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages)を呼び出しました。 (BugCheckOnFailure パラメーターを FALSE に設定して、代わりに[MmMapLockedPagesSpecifyCache](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache)を使用する必要があります)。|
|0x82|MDL アドレス|MDL フラグ|0|ドライバーは、BugCheckOnFailure パラメーターが TRUE と等しい[MmMapLockedPagesSpecifyCache](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache)を呼び出しました。 (このパラメーターは FALSE に設定する必要があります)。|
|0x83|マップする物理アドレス範囲の開始|マップするバイト数|ロックダウンされていない最初のページフレーム番号|MDL ページをロックダウンせずに、 [Mmmapiospace](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace)というドライバーが呼び出されました。 この呼び出しを行う前に、マップされている物理アドレス範囲によって表される物理ページがロックダウンされている必要があります。|
|0x85|MDL アドレス|マップするページ数|ロックダウンされていない最初のページフレーム番号|ドライバーは、MDL ページをロックダウンせずに[MmMapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages)を呼び出しました。|
|0x89|MDL アドレス|MDL 内のメモリ以外のページへのポインター|MDL 内のメモリ以外のページ番号|MDL は "i/o" とマークされていませんが、メモリ以外のページアドレスが含まれています。|
|0x91|予約済み|予約済み|予約済み|ドライバーは、オペレーティングシステムでサポートされていないメソッドを使用してスタックを切り替えました。 カーネルモードスタックを拡張する唯一の方法として、 [Keexpandkernel Stackand吹き出し](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keexpandkernelstackandcallout)を使用する方法があります。|

### <a name="0xa0-to-0x140"></a>0xA0 ~ 0xa0

|パラメーター1|パラメータ 2|パラメーター3|パラメーター4|エラーの原因|
|--- |--- |--- |--- |--- |
|0xA0|読み取りまたは書き込み要求を行っている IRP へのポインター|下位デバイスのデバイスオブジェクト|エラーが検出されたセクターの数|ハードディスクで巡回冗長検査 (CRC) エラーが検出されました。 このパラメーターを使用したバグチェックは、ドライバー検証ツールのディスク整合性チェックオプションがアクティブな場合にのみ行われます。|
|0xA1|読み取りまたは書き込み要求を行っている IRP のコピー。 (実際の IRP は完了しています)。|下位デバイスのデバイスオブジェクト|エラーが検出されたセクターの数|セクター (非同期) で CRC エラーが検出されました。 このパラメーターを使用したバグチェックは、ドライバー検証ツールのディスク整合性チェックオプションがアクティブな場合にのみ行われます。|
|0xA2|読み取りまたは書き込み要求を行う IRP、またはこの IRP のコピー|下位デバイスのデバイスオブジェクト|エラーが検出されたセクターの数|CRCDISK チェックサムのコピーが一致しません。 ページングエラーが発生する可能性があります。 このパラメーターを使用したバグチェックは、ドライバー検証ツールのディスク整合性チェックオプションがアクティブな場合にのみ行われます。|
|0xB0 |MDL アドレス|MDL フラグ|無効な MDL フラグ|ドライバーは、正しくないフラグを持つ MDL の[MmProbeAndLockPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)を呼び出しました。 たとえば、ドライバーは、 [MmBuildMdlForNonPagedPool](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool)によって作成された MDL を MmProbeAndLockPages に渡しました。|
|0xB1 |MDL アドレス|MDL フラグ|無効な MDL フラグ|ドライバーは、正しくないフラグを持つ MDL の MmProbeAndLockProcessPages を呼び出しました。 たとえば、ドライバーは、 [MmBuildMdlForNonPagedPool](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool)によって作成された MDL を MmProbeAndLockProcessPages に渡しました。|
|0xB2 |MDL アドレス|MDL フラグ|無効な MDL フラグ|ドライバーは、正しくないフラグを持つ MDL の[MmMapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages)を呼び出しました。 たとえば、ドライバーが既にシステムアドレスにマップされているか、MmMapLockedPages にロックされていない MDL を渡しました。|
|0xB3 |MDL アドレス|MDL フラグ|MDL フラグが見つかりません (少なくとも1つが必要です)|ドライバーは、正しくないフラグを持つ MDL の[MmMapLockedPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages)を呼び出しました。 たとえば、ドライバーが MmMapLockedPages にロックされていない MDL を渡したとします。|
|0xB4 |MDL アドレス|MDL フラグ|予期しない部分的な MDL フラグ|このドライバーは、部分的な MDL の[MmUnlockPages](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages)を呼び出しました。 部分的な MDL は、 [Iobuildpartialmdl](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl)によって作成されたものです。|
|0xB5|MDL アドレス|MDL フラグ|予期しない部分的な MDL フラグ|MmUnmapLockedPages が部分的な MDL で呼び出されました ( [Iobuildpartialmdl](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl)で作成)。|
|0xB6|MDL アドレス|MDL フラグ|MDL フラグが見つかりません|MmUnmapLockedPages は、システムアドレスにマップされていない MDL で呼び出されました。|
|0xB7|破損した物理ページの数。|最初の破損した物理ページ。|最後に破損した物理ページ。|スリープ状態の移行中に、システム BIOS の物理メモリが破損しています。|
|0xB8 |MDL アドレス|MDL フラグ|予約済み|MDL によって記述されたページはまだマップされています。 ドライバーは、IoFreeMdl を呼び出す前にページをマップ解除する必要があります。|
|0xB9 |アドレスがマップ解除されています。|MDL のアドレス。|予約済み|無効なユーザー領域のアドレスを使用して MmUnmapLockedPages が呼び出されました。|
|0xC0 |IRP のアドレス|0|予約済み|ドライバーは、割り込みが無効になっている[IoCallDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出しました。|
|0xC1 |ドライバーディスパッチルーチンのアドレス|予約済み|予約済み|割り込みが無効になっているドライバーディスパッチルーチンが返されました。|
|0xC2 |0|0|0|ドライバーは、割り込みが無効になった後に高速 i/o ディスパッチルーチンを呼び出しました。|
|0xC3 |ドライバーの高速 i/o ディスパッチルーチンのアドレス|予約済み|予約済み|ドライバーの高速 i/o ディスパッチルーチンが返されましたが、割り込みが無効になっています。|
|0xC5 |ドライバーディスパッチルーチンのアドレス|現在のスレッドの APC の無効化カウント|ドライバーディスパッチルーチンを呼び出す前のスレッドの APC 無効化カウント|ドライバーディスパッチルーチンによって、スレッドの APC の無効化カウントが変更されました。 APC の disable count は、ドライバーが[KeEnterCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)、 [fsrtlenterfilesystem](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlenterfilesystem)を呼び出すたび、またはミューテックスを取得するたびにデクリメントされます。 APC disable count は、ドライバーが[KeLeaveCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)、 [KeReleaseMutex](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex)、または[fsrtlexitfilesystem](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlexitfilesystem)を呼び出すたびに増分されます。 これらの呼び出しは常にペアになっている必要があるため、スレッドが終了するたびに、APC の disable count をゼロにする必要があります。 負の値は、ドライバーが再度有効にすることなく、APC の呼び出しを無効にしたことを示します。 正の値は、反転が true であることを示します。|
|0xC6 |ドライバーの高速 i/o ディスパッチルーチンのアドレス|現在のスレッドの APC の無効化カウント|高速 i/o ドライバーディスパッチルーチンを呼び出す前のスレッドの APC 無効化カウント|ドライバーの高速 i/o ディスパッチルーチンによって、スレッドの APC の無効化回数が変更されました。 APC の disable count は、ドライバーが[KeEnterCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)、 [fsrtlenterfilesystem](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlenterfilesystem)を呼び出すたび、またはミューテックスを取得するたびにデクリメントされます。 APC disable count は、ドライバーが[KeLeaveCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)、 [KeReleaseMutex](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex)、または[fsrtlexitfilesystem](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlexitfilesystem)を呼び出すたびに増分されます。 これらの呼び出しは常にペアになっている必要があるため、スレッドが終了するたびに、APC の disable count をゼロにする必要があります。 負の値は、ドライバーが再度有効にすることなく、APC の呼び出しを無効にしたことを示します。 正の値は、反転が true であることを示します。|
|0xCA |ルックアサイドリストのアドレス|予約済み|予約済み|ドライバーがルックアサイドリストを再初期化しようとしました。|
|0xCB |ルックアサイドリストのアドレス|予約済み|予約済み|ドライバーは、初期化されていないルックアサイドリストを削除しようとしました。|
|0xCC |ルックアサイドリストのアドレス|プール割り当ての開始アドレス|プール割り当てのサイズ|ドライバーは、アクティブなルックアサイドリストを含むプールの割り当てを解放しようとしました。|
|0xCD |ルックアサイドリストのアドレス|呼び出し元によって指定されたブロックサイズ|サポートされている最小ブロックサイズ|ドライバーは、割り当てブロックサイズが小さすぎるルックアサイドリストを作成しようとしました。|
|0xD0 |÷の構造体のアドレス|予約済み|予約済み|ドライバーが、この構造体を再初期化しようとしました。|
|0xD1 |÷の構造体のアドレス|予約済み|予約済み|ドライバーは、初期化されていない÷構造を削除しようとしました。|
|0xD2 |÷の構造体のアドレス|プール割り当ての開始アドレス|プール割り当てのサイズ|ドライバーは、アクティブなリソース構造を含むプールの割り当てを解放しようとしました。|
|0xD5 |選択したビルドバージョンのドライバーによって作成された IO_REMOVE_LOCK 構造体のアドレス|現在の[IoReleaseRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)タグ|予約済み|現在の[IoReleaseRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)タグは、前の[IoAcquireRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)タグと一致しません。 IoReleaseRemoveLock を呼び出しているドライバーがチェックされたビルドに含まれていない場合、パラメーター2はドライバーに代わってドライバーの検証ツールによって作成されたシャドウ IO_REMOVE_LOCK 構造のアドレスです。 この場合、ドライバーによって使用される IO_REMOVE_LOCK 構造体のアドレスはまったく使用されません。これは、ドライバーの検証ツールによってすべての削除ロック Api のロックアドレスが置き換えられるためです。 このパラメーターを使用したバグチェックは、ドライバーの検証ツールの i/o 検証オプションがアクティブな場合にのみ行われます。|
|0xD6 |選択したビルドバージョンのドライバーによって作成された IO_REMOVE_LOCK 構造体のアドレス|前の[IoAcquireRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)タグに一致しないタグ|前の[IoAcquireRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)タグ|現在の[IoReleaseRemoveLockAndWait](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)タグは、前の[IoAcquireRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)タグと一致しません。 [IoReleaseRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)を呼び出しているドライバーがチェックされたビルドではない場合、パラメーター2はドライバーに代わってドライバーの検証ツールによって作成されたシャドウ IO_REMOVE_LOCK 構造のアドレスです。 この場合、ドライバーによって使用される IO_REMOVE_LOCK 構造体のアドレスはまったく使用されません。これは、ドライバーの検証ツールによってすべての削除ロック Api のロックアドレスが置き換えられるためです。 このパラメーターを使用したバグチェックは、ドライバーの検証ツールの i/o 検証オプションがアクティブな場合にのみ行われます。|
|0xD7|ドライバーの検証ツールで内部的に使用される、チェックされたビルドの削除ロック構造のアドレス|ドライバーによって指定された削除ロック構造のアドレス|予約済み|[IoReleaseRemoveLockAndWait](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)を呼び出した後でも、他のスレッドが[IoAcquireRemoveLock](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)を呼び出してそのロックを使用している可能性があるため、削除ロックを再初期化することはできません。 ドライバーは、デバイス拡張機能内に Remove ロックを割り当てて、1回だけ初期化します。 ロックは、デバイス拡張機能と共に削除されます。|
|0xDA |ドライバーの開始アドレス|ドライバー内の WMI コールバックアドレス|予約済み|WMI コールバック関数が登録解除されていないドライバーをアンロードしようとしました。|
|0xDB |デバイスオブジェクトのアドレス|予約済み|予約済み|WMI から登録解除されていないデバイスオブジェクトを削除しようとしました。|
|0xDC |予約済み|予約済み|予約済み|無効な RegHandle 値が関数[Etwunregister 解除](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-etwunregister)のパラメーターとして指定されました。|
|0xDD |EtwRegister への呼び出しのアドレス|アンロードドライバーの開始アドレス|Windows 8 以降のバージョンでは、このパラメーターは ETW RegHandle の値です。|[Etwunregister 解除](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-etwunregister)を呼び出さずにドライバーをアンロードしようとしました。|
|0xDF |同期オブジェクトアドレス|0|0|同期オブジェクトは、セッションアドレス空間にあります。 同期オブジェクトは、セッションのアドレス空間では許可されません。これは、別のセッションまたはセッションの仮想アドレス空間を持たないシステムスレッドからの操作が可能であるためです。|
|0xE0 |パラメーターとして使用されるユーザーモードアドレス|パラメーターとして使用されるアドレス範囲のサイズ (バイト単位)|予約済み|ユーザーモードアドレスをパラメーターとして指定したオペレーティングシステムカーネル関数が呼び出されました。|
|0xE1 |同期オブジェクトのアドレス|予約済み|予約済み|同期オブジェクトのアドレスが無効であるか、またはページング可能であることが検出されました。|
|0xE2 |IRP のアドレス|IRP に存在するユーザーモードアドレス|予約済み|Irp > Irp->requestormode が Kernelmode でに設定されている IRP は、そのメンバーの1つとしてユーザーモードアドレスを持っていることがわかりました。|
|0xE3 |API の呼び出しのアドレス|API でパラメーターとして使用されるユーザーモードアドレス|予約済み|ドライバーが、パラメーターとしてユーザーモードアドレスを持つカーネルモード ZwXxx ルーチンを呼び出しました。|
|0xE4 |API の呼び出しのアドレス|形式が正しくない UNICODE_STRING 構造体のアドレス|予約済み|ドライバーが、パラメーターとして不適切な形式の UNICODE_STRING 構造を持つカーネルモード ZwXxx ルーチンを呼び出しました。|
|0xE5 |現在の IRQL|予約済み|予約済み|無効な IRQL でカーネル API が呼び出されました。|
|0xE6 |Zw API 呼び出しを行うドライバー内のアドレス|現在の IRQL|特殊なカーネル Apc。|カーネル Zw API が IRQL = PASSIVE_LEVEL で呼び出されませんでした。特殊なカーネル Apc が有効になっています。|
|0xEA |現在の IRQL|スレッドの APC の無効化カウント|Pushlock のアドレス|Apc が有効になっている間に、ドライバーが pushlock を取得しようとしました。|
|0xEB |現在の IRQL|スレッドの APC の無効化カウント|Pushlock のアドレス|Apc が有効になっている間に、ドライバーが pushlock を解放しようとしました。|
|0Xf0 です |コピー先のバッファーのアドレス|ソースバッファーのアドレス|コピーするバイト数|コピー元とコピー先のバッファーが重複する memcpy 関数を呼び出したドライバー。|
|0xF5 |NULL ハンドルのアドレス|［オブジェクトの種類］|予約済み|ドライバーが[Obreferenceobjectbyhandle](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)に NULL ハンドルを渡しました。|
|0xF6 |参照されている値の処理|現在のプロセスのアドレス|無効な参照を実行するドライバー内のアドレス|ドライバーは、カーネルモードとしてユーザーモードハンドルを参照します。|
|0xF7 |呼び出し元によって指定された値を処理します|呼び出し元によって指定されたオブジェクトの種類|呼び出し元によって指定された AccessMode|ドライバーがシステムプロセスのコンテキストでカーネルハンドルのユーザーモード参照を試行しています。|
|0xFA |完了ルーチンアドレス。|完了ルーチンを呼び出す前の IRQL 値|完了ルーチンを呼び出した後の現在の IRQL 値|IRP の完了ルーチンが、ルーチンが呼び出された IRQL と異なる IRQL で返されました。|
|0xFB |完了ルーチンのアドレス|現在のスレッドの APC の無効化カウント|IRP の完了ルーチンを呼び出す前のスレッドの APC の無効化回数|スレッドの APC 無効化カウントは、ドライバーの IRP 完了ルーチンによって変更されました。 APC の disable count は、ドライバーが[KeEnterCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)、 [fsrtlenterfilesystem](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlenterfilesystem)を呼び出すたび、またはミューテックスを取得するたびにデクリメントされます。 APC disable count は、ドライバーが[KeLeaveCriticalRegion](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)、 [KeReleaseMutex](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex)、または[fsrtlexitfilesystem](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlexitfilesystem)を呼び出すたびに増分されます。 これらの呼び出しは常にペアになっている必要があるため、スレッドが終了するたびに、APC の disable count をゼロにする必要があります。 負の値は、ドライバーが再度有効にすることなく、APC の呼び出しを無効にしたことを示します。 正の値は、反転が true であることを示します。|
|0xFC |無効な API 呼び出しを行うドライバー内のアドレス。|ApcContext 値を指定します。|予約済み|サポートされていない ApcContext 値を使用して、(カーネルモードから) ZwNotifyChangeKey を呼び出しています。|

### <a name="0x105-to-0x140"></a>0x105 を0x140 に

|パラメーター1|パラメータ 2|パラメーター3|パラメーター4|エラーの原因|
|--- |--- |--- |--- |--- |
|0x105 |IRP のアドレス|0|0|ドライバーは、IoFreeIrp ではなく ExFreePool を使用して IRP を解放します。|
|0x10A |0|0|0|ドライバーは、アイドル状態のプロセスに対してプールクォータの課金を試行します。|
|0x10B |0|0|0|ドライバーは、DPC ルーチンからプールクォータの課金を試行します。 現在のプロセスコンテキストが定義されていないため、これは正しくありません。|
|0x110 |0|0|0|割り込みサービスルーチンのアドレス|ISR を実行する前に保存された拡張コンテキストのアドレス|拡張コンテキストのアドレスは、ISR の実行後に保存されました|ドライバーの割り込みサービスルーチン (ISR) によって、拡張スレッドコンテキストが破損しました。|
|0x111 |割り込みサービスルーチンのアドレス|ISR を実行する前の IRQL|ISR の実行後の IRQL|割り込みサービスルーチンが変更された IRQL を返しました。|
|0x115 |デッドロックが発生する可能性がある、シャットダウンを担当するスレッドのアドレス。|0|0|ドライバーの検証ツールによって、システムの実行時間が20分を超え、シャットダウンが完了していないことが検出されました。|
|0x11A |現在の IRQL|0|0|ドライバーは、IRQL > APC_LEVEL で KeEnterCriticalRegion を呼び出します。|
|0x11B |現在の IRQL|0|0|ドライバーは、IRQL > APC_LEVEL で KeLeaveCriticalRegion を呼び出します。|
|0x120 |IRQL 値のアドレス|待機するオブジェクトのアドレス|タイムアウト値のアドレス|スレッドは、IRQL > DISPATCH_LEVEL で待機します。 KeWaitForSingleObject または KeWaitForMultipleObjects の呼び出し元は、IRQL < = DISPATCH_LEVEL で実行する必要があります。|
|0x121 |IRQL 値のアドレス|待機するオブジェクトのアドレス|タイムアウト値のアドレス|スレッドは IRQL equals DISPATCH_LEVEL で待機し、タイムアウトは NULL になります。 KeWaitForSingleObject または KeWaitForMultipleObjects の呼び出し元は、IRQL < = DISPATCH_LEVEL で実行できます。 NULL ポインターがタイムアウトに指定されている場合、オブジェクトがシグナル状態になるまで、呼び出し元のスレッドは待機状態のままになります。|
|0x122 |IRQL 値のアドレス|待機するオブジェクトのアドレス|タイムアウト値のアドレス|スレッドが DISPATCH_LEVEL で待機し、タイムアウト値がゼロ (0) と等しくありません。 タイムアウト! = 0 の場合、KeWaitForSingleObject または KeWaitForMultipleObjects の呼び出し元は、IRQL < = APC_LEVEL で実行する必要があります。|
|0x123 |待機するオブジェクトのアドレス|0|0|KeWaitForSingleObject または KeWaitForMultipleObjects の呼び出し元が、この待機をモードとして指定しましたが、オブジェクトはカーネルスタック上にあります。|
|0x130 |作業項目のアドレス|0|0|作業項目はセッションアドレス空間にあります。 セッションアドレス空間では、別のセッションまたはセッションの仮想アドレス空間を持たないシステムスレッドから操作できるため、作業項目は許可されません。|
|0x131 |作業項目のアドレス|0|0|作業項目は、ページング可能なメモリ内にあります。 作業項目は DISPATCH_LEVEL で使用されるため、非ページングメモリ内に存在する必要があります。|
|0x135|IRP のアドレス|[Iocancelirp](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)呼び出しからこの IRP の完了までの許容時間 (ミリ秒)|0|取り消された IRP は、キャンセルされた IRP を完了するのに予想以上に長い時間がかかっていた可能性があります。|
|0x13A|解放されているプールブロックのアドレス|値が正しくありません|間違った値のアドレス|ドライバーが[Exfreepool](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)を呼び出しました。ドライバー検証ツールは、プールの使用状況を追跡するために使用される内部値の1つでエラーを検出します。|
|0x13B|解放されているプールブロックのアドレス|間違った値のアドレス|間違ったメモリページへのポインターのアドレス|ドライバーが[Exfreepool](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)を呼び出しました。ドライバー検証ツールは、プールの使用状況を追跡するために使用される内部値の1つでエラーを検出します。|
|0x13C|解放されているプールブロックのアドレス|値が正しくありません|間違った値のアドレス|ドライバーが[Exfreepool](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)を呼び出しました。ドライバー検証ツールは、プールの使用状況を追跡するために使用される内部値の1つでエラーを検出します。|
|0x13D|解放されているプールブロックのアドレス|間違った値のアドレス|正しい値が必要です。|ドライバーが[Exfreepool](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)を呼び出しました。ドライバー検証ツールは、プールの使用状況を追跡するために使用される内部値の1つでエラーを検出します。|
|0x13E|呼び出し元によって指定されたプールブロックアドレス|ドライバーの検証ツールによって追跡されたプールブロックアドレス|ドライバーの検証ツールによって追跡されるプールブロックアドレスへのポインター|[Exfreepool](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)の呼び出し元によって指定されたプールブロックアドレスが、ドライバーの検証ツールによって追跡されるアドレスと異なります。|
|0x13F|解放されているプールブロックのアドレス|解放されるバイト数|ドライバーの検証ツールによって追跡されたバイト数へのポインター|[Exfreepool](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)への呼び出しで解放されるメモリのバイト数が、ドライバーの検証ツールによって追跡されるバイト数と異なります。|
|0x140|現在の IRQL|MDL アドレス|この MDL と関連付けられた仮想アドレス|ロックされていない MDL は、ページング可能なメモリまたは tradable メモリから構築されています。|
|0x141|ドライバーが割り当てを要求した物理アドレスの最高値|割り当てるバイト数|0|ドライバーは、物理メモリを 4 GB 未満で明示的に要求しています。|

### <a name="0x1000-to-0x100b---deadlocks"></a>0x1000 から 0x100B-デッドロック

|パラメーター1|パラメータ 2|パラメーター3|パラメーター4|エラーの原因|
|--- |--- |--- |--- |--- |
|0x1000 |リソースのアドレス|予約済み|予約済み|自己デッドロック: 現在のスレッドがリソースを再帰的に取得しようとしました。 このパラメーターを使用したバグチェックは、ドライバー検証ツールのデッドロック検出オプションがアクティブな場合にのみ行われます。|
|0x1001 |デッドロックの最終的な原因であるリソースのアドレス|予約済み|予約済み|デッドロック: ロック階層違反が見つかりました。 このパラメーターを使用したバグチェックは、ドライバー検証ツールのデッドロック検出オプションがアクティブな場合にのみ行われます。 (詳細については、 [! デッドロック](-deadlock.md)拡張機能を使用してください。)|
|0x1002 |リソースのアドレス|予約済み|予約済み|初期化されていないリソース: 最初に初期化されずにリソースが取得されました。 このパラメーターを使用したバグチェックは、ドライバー検証ツールのデッドロック検出オプションがアクティブな場合にのみ行われます。|
|0x1003 |デッドロック状態になっているリソースのアドレス|最初に解放される必要があるリソースのアドレス|予約済み|予期しないリリース: リソースが正しくない順序で解放されました。 このパラメーターを使用したバグチェックは、ドライバー検証ツールのデッドロック検出オプションがアクティブな場合にのみ行われます。|
|0x1004 |リソースのアドレス|リソースを取得したスレッドのアドレス|現在のスレッドのアドレス|予期しないスレッド: 間違ったスレッドによってリソースが解放されます。 このパラメーターを使用したバグチェックは、ドライバー検証ツールのデッドロック検出オプションがアクティブな場合にのみ行われます。|
|0x1005 |リソースのアドレス|予約済み|予約済み|複数の初期化: リソースが複数回初期化されています。 このパラメーターを使用したバグチェックは、ドライバー検証ツールのデッドロック検出オプションがアクティブな場合にのみ行われます。|
|0x1007 |リソースのアドレス|予約済み|予約済み|リソースの取得解除: リソースが取得される前に解放されます。 このパラメーターを使用したバグチェックは、ドライバー検証ツールのデッドロック検出オプションがアクティブな場合にのみ行われます。|
|0x1008 |ロックアドレス|予約済み|予約済み|ドライバーは、このロックの種類に一致しない API を使用してロックを取得しようとしました。|
|0x1009 |ロックアドレス|予約済み|予約済み|ドライバーは、このロックの種類に一致しない API を使用してロックを解除しようとしました。|
|0x100A |所有者スレッドアドレス|予約済み|終了したスレッドがロックを所有しています。|
|0x100B |ロックアドレス|所有者スレッドアドレス|予約済み|削除されたロックは、まだスレッドによって所有されています。|
|0x1010 |書き込み IRP が発行されたデバイスオブジェクト。|IRP のアドレス。|MDL が記述するバッファーのシステム領域の仮想アドレス。|書き込み Irp の不変の MDL バッファーの内容が変更されました。|
|0x1011 |書き込み IRP が発行されたデバイスオブジェクト。|IRP のアドレス。|MDL が記述するバッファーのシステム領域の仮想アドレス。|Read Irp の不変の MDL バッファーの内容が、ダミーページでサポートされているディスパッチまたはバッファーで変更されました。|
|0x1012 |違反を説明する文字列へのポインター。|この破損に関係するデータ (使用されていない場合は 0)。|この破損に関係するデータ (使用されていない場合は 0)。|検証機能拡張機能の状態ストレージで破損が検出されました。|
|0x1013 |ドライバーオブジェクトへのポインター。|キャプチャされた元の i/o コールバックへのポインター。|予約済み (未使用)。|検証ツールは、キャプチャされた元の i/o コールバックで内部の破損を検出しました。|

### <a name="0x2000-to-0x2005---code-integrity-issues"></a>0x2000 から 0x2005-コードの整合性の問題

|パラメーター1|パラメータ 2|パラメーター3|パラメーター4|エラーの原因|
|--- |--- |--- |--- |--- |
|0x2000 |エラーが検出されたドライバーのコード内のアドレス。 |プールの種類。 | プールタグ (指定されている場合)。|コードの整合性の問題: 呼び出し元が実行可能なプールの種類を指定しました。 (必要な値: NonPagedPoolNx) |
|0x2001 |エラーが検出されたドライバーのコード内のアドレス。 |ページ保護 (WIN32_PROTECTION_MASK)。 | 0 |コードの整合性の問題: 呼び出し元が実行可能ページの保護を指定しました。 (必要なのは、消去された PAGE_EXECUTE * ビット) |
|0x2002 |エラーが検出されたドライバーのコード内のアドレス。 |ページの優先度 (MM_PAGE_PRIORITY、MdlMapping *)。 |0|コードの整合性の問題: 呼び出し元は、実行可能な MDL マッピングを指定しました。 (必要な値: MdlMappingNoExecute) |
|0x2003 |イメージファイル名 (Unicode 文字列)。 | セクションヘッダーのアドレス。|セクション名 (UTF-8 でエンコードされた文字列)。 |コードの整合性の問題: イメージには、実行可能ファイルと書き込み可能なセクションが含まれています。 |
|0x2004 |イメージファイル名 (Unicode 文字列)。 |セクションヘッダーのアドレス。 |セクション名 (UTF-8 でエンコードされた文字列)。 |コードの整合性の問題: イメージに、ページがアラインされていないセクションが含まれています。 |
|0x2005 |イメージファイル名 (Unicode 文字列)。 | IAT ディレクトリ。|セクション名 (UTF-8 でエンコードされた文字列)。 |コードの整合性の問題: イメージには、実行可能なセクションに配置されている IAT が含まれています。 |

### <a name="0xa001-to-0xa00d---vm-switch-issues"></a>0xA001 から 0xA00D-VM スイッチの問題

|パラメーター1|パラメータ 2|パラメーター3|パラメーター4|エラーの原因|
|--- |--- |--- |--- |--- |
|0xA001 |NetBufferList オブジェクトへのポインター|仮想スイッチオブジェクトへのポインター (NULL 以外の場合)|予約済み (未使用)|VM スイッチ: 呼び出し元が指定した NetBufferList の SourceHandle を設定する必要があります。 [AllocateNetBufferListForwardingContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)ルーチンを参照してください。|
|0xA002 |NetBufferList オブジェクトへのポインター|仮想スイッチオブジェクトへのポインター (NULL 以外の場合)。|予約済み (未使用)|VM スイッチ: 呼び出し元によって指定された NetBufferList の転送詳細が0ではありません。 [AllocateNetBufferListForwardingContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)ルーチンを参照してください。|
|0xA003 |NetBufferList オブジェクトへのポインター|仮想スイッチオブジェクトへのポインター (NULL 以外の場合)。|予約済み (未使用)|VM スイッチ: 呼び出し元が、パケットヘッダーまたはルーティングコンテキストが NULL の NetBufferList を提供しました。 [拡張可能なスイッチのデータパスについては、「パケット管理のガイドライン」を](https://docs.microsoft.com/windows-hardware/drivers/network/packet-management-guidelines-for-the-extensible-switch-data-path)参照してください。|
|0xA004 |無効なポートの ID|NIC インデックス|仮想スイッチオブジェクトへのポインター (NULL 以外の場合)。|VM スイッチ: 呼び出し元によって、無効なポートと NIC インデックスの組み合わせが指定されました。 「 [Hyper-v 拡張可能スイッチポートとネットワークアダプターの状態」を](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)参照してください。|
|0xA005 |NetBufferList オブジェクトへのポインター|対象のリストへのポインター。|仮想スイッチオブジェクトへのポインター (NULL 以外の場合)。|VM スイッチ: 呼び出し元によって無効な宛先が指定されました。 「 [AddNetBufferListDestination](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination) 」および「 [Updatenetbufferlistdestinations](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)」を参照してください。|
|0xA006 |NetBufferList オブジェクトへのポインター|仮想スイッチオブジェクトへのポインター (NULL 以外の場合)。|予約済み (未使用)|VM スイッチ: 呼び出し元が、無効なソース NIC またはポートオブジェクトを指定しました。 「 [Hyper-v 拡張可能スイッチポートとネットワークアダプターの状態」を](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)参照してください。|
|0xA007 |NetBufferList オブジェクトへのポインター|仮想スイッチオブジェクトへのポインター (NULL 以外の場合)。|予約済み (未使用)|VM スイッチ: 呼び出し元により、無効な宛先リストが指定されました。 「 [AddNetBufferListDestination](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination) 」および「 [Updatenetbufferlistdestinations](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)」を参照してください。|
|0xA008 |親 NIC オブジェクト|NIC インデックス|仮想スイッチオブジェクトへのポインター (NULL 以外の場合)。|VM スイッチ: 許可されていないときに NIC を参照しようとしています。 「 [Hyper-v 拡張可能スイッチポートとネットワークアダプターの状態」を](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)参照してください。|
|0xA009 |参照されているポート|仮想スイッチオブジェクトへのポインター (NULL 以外の場合)|予約済み (未使用)|VM スイッチ: 許可されていないときにポートを参照しようとしました。 「 [Hyper-v 拡張可能スイッチポートとネットワークアダプターの状態」を](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)参照してください。|
|0xA00A |NetBufferList オブジェクトへのポインター|ContextTypeInfo オブジェクト|予約済み (未使用)|VM スイッチ: エラーコンテキストが既に設定されています。 「 [SetNetBufferListSwitchContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_set_net_buffer_list_switch_context)」を参照してください。|
|0xA00B |NetBufferList オブジェクトへのポインター|NDIS_SWITCH_REPORT_FILTERED_NBL_FLAGS_ *|仮想スイッチオブジェクトへのポインター (NULL 以外の場合)|VM スイッチ: ドロップ NetBufferList に指定された方向が無効です。 「 [ReportFilteredNetBufferLists](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)」を参照してください。|
|0xA00C |NetBufferList オブジェクトへのポインター|送信フラグの値|仮想スイッチオブジェクトへのポインター (NULL 以外の場合)|VM スイッチ: NDIS_SEND_FLAGS_SWITCH_SINGLE_SOURCE フラグが設定されている場合、NetBufferList chain には複数のソースポートがあります。 「 [Hyper-v 拡張可能スイッチの送信フラグと受信フラグ」を](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-send-and-receive-flags)参照してください。|
|0xA00D |NetBufferList オブジェクトへのポインター|仮想スイッチコンテキストへのポインター|仮想スイッチオブジェクトへのポインター (NULL 以外の場合)|VM スイッチ: NDIS_RECEIVE_FLAGS_SWITCH_DESTINATION_GROUP フラグが設定されている場合、チェーン内の1つ以上の NetBufferLists に無効な宛先があります。 「 [Hyper-v 拡張可能スイッチの送信フラグと受信フラグ」を](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-send-and-receive-flags)参照してください。|
|0xA00E|NetBufferLists オブジェクトへのポインター。 |仮想スイッチコンテキストへのポインター。 |仮想スイッチオブジェクトへのポインター (NULL 以外の場合)。 |VM スイッチ: VMS_NBL_ROUTING_CONTEXT_FLAG_NO_WNV_PROCESSING フラグが設定されている場合、WNV を介して NetBufferList を完了しようとしています。|

### <a name="0x00020002-to-0x00020022---ddi-compliance-rule-violations"></a>0x00020002 0x00020022-DDI コンプライアンス規則違反

|パラメーター1|パラメータ 2|パラメーター3|パラメーター4|エラーの原因|
|--- |--- |--- |--- |--- |
|0x00020002 |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlApcLte](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlapclte)に違反しました。 この規則は、IRQL < = APC_LEVEL の場合にのみ、ドライバーが[Obgetobjectsecurity](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obgetobjectsecurity)および[obgetobjectsecurity](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreleaseobjectsecurity)を呼び出す必要があることを指定します。|
|0x00020003 |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[Irqldispatch](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqldispatch)に違反しました。 IrqlDispatch ルールでは、ドライバーが特定のルーチンを呼び出す必要があることを指定します。 IRQL = DISPATCH_LEVEL|
|0x00020004 |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlExAllocatePool](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexallocatepool)に違反しました。 IrqlExAllocatePool 規則は、IRQL < = DISPATCH_LEVEL の場合にのみ、ドライバーが[Exallocatepoolwithtag](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)と[Exallocatepoolwithtagpriority](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority)を呼び出すように指定します。|
|0x00020005 |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlExApcLte1](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexapclte1)に違反しました。 IrqlExApcLte1 規則は、ドライバーが ExAcquireFastMutex と ExTryToAcquireFastMutex を呼び出すことを指定します。これは、IRQL < = APC_LEVEL でのみ行います。|
|0x00020006 |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlExApcLte2](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)に違反しました。 IrqlExApcLte2 規則は、IRQL < = APC_LEVEL の場合にのみ、ドライバーが特定のルーチンを呼び出すように指定します。|
|0x00020007 |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlExApcLte3](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexapclte3)に違反しました。 IrqlExApcLte3 規則は、IRQL < = APC_LEVEL の場合にのみ、ドライバーが特定のエグゼクティブサポートルーチンを呼び出す必要があることを指定します。|
|0x00020008 |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlExPassive](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexpassive)に違反しました。 IrqlExPassive 規則は、IRQL = PASSIVE_LEVEL 場合にのみ、ドライバーが特定のエグゼクティブサポートルーチンを呼び出す必要があることを指定します。|
|0x00020009 |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlIoApcLte](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlioapclte)に違反しました。 IrqlIoApcLte 規則は、IRQL < = APC_LEVEL の場合にのみ、ドライバーが特定の i/o マネージャールーチンを呼び出す必要があることを指定します。|
|0x0002000A |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlIoPassive1](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive1)に違反しました。 IrqlIoPassive1 規則は、IRQL = PASSIVE_LEVEL 場合にのみ、ドライバーが特定の i/o マネージャールーチンを呼び出す必要があることを指定します。|
|0x0002000B |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlIoPassive2](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive2)に違反しました。 IrqlIoPassive2 規則は、IRQL = PASSIVE_LEVEL 場合にのみ、ドライバーが特定の i/o マネージャールーチンを呼び出す必要があることを指定します。|
|0x0002000C |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlIoPassive3](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive3)に違反しました。 IrqlIoPassive3 規則は、IRQL = PASSIVE_LEVEL 場合にのみ、ドライバーが特定の i/o マネージャールーチンを呼び出す必要があることを指定します。|
|0x0002000D |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlIoPassive4](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive4)に違反しました。 IrqlIoPassive4 規則は、IRQL = PASSIVE_LEVEL 場合にのみ、ドライバーが特定の i/o マネージャールーチンを呼び出す必要があることを指定します。|
|0x0002000E |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlIoPassive5](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive5)に違反しました。 IrqlIoPassive5 規則は、IRQL = PASSIVE_LEVEL 場合にのみ、ドライバーが特定の i/o マネージャールーチンを呼び出す必要があることを指定します。|
|0x0002000F |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlKeApcLte1](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkeapclte1)に違反しました。 IrqlKeApcLte1 規則は、IRQL < = APC_LEVEL の場合にのみ、ドライバーが特定のカーネルルーチンを呼び出す必要があることを指定します。|
|0x00020010 |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlKeApcLte2](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkeapclte2)に違反しました。 IrqlKeApcLte2 規則は、IRQL < = APC_LEVEL の場合にのみ、ドライバーが特定のカーネルルーチンを呼び出す必要があることを指定します。|
|0x00020011 |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlKeDispatchLte](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkedispatchlte)に違反しました。 IrqlKeDispatchLte 規則は、IRQL < = DISPATCH_LEVEL の場合にのみ、ドライバーが特定のカーネルルーチンを呼び出す必要があることを指定します。|
|0x00020015 |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlKeReleaseSpinLock](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkereleasespinlock)に違反しました。 IrqlKeReleaseSpinLock 規則は、IRQL = DISPATCH_LEVEL 場合にのみ、ドライバーが KeReleaseSpinLock を呼び出す必要があることを指定します。|
|0x00020016 |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlKeSetEvent](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkesetevent)に違反しました。 IrqlKeSetEvent ルールは、wait が FALSE に設定されている場合に、 [KeSetEvent](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)ルーチンが irql < = DISPATCH_LEVEL でのみ呼び出されることを指定します。また、WAIT が TRUE に設定されている場合は、irql < = APC_LEVEL を指定します。|
|0x00020019 |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンスルール[Irqlmmapclte](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlmmapclte)に違反しました。 IrqlMmApcLte ルールでは、IRQL < = APC_LEVEL の場合にのみ、ドライバーが特定のメモリマネージャールーチンを呼び出す必要があることを指定します。|
|0x0002001A |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[Irqlmmdispatch](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlmmdispatch)に違反しました。 IrqlMmDispatch ルールでは、IRQL = DISPATCH_LEVEL の場合にのみ、ドライバーが[MmFreeContiguousMemory](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreecontiguousmemory)を呼び出す必要があることを指定します。|
|0x0002001B |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlObPassive](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlobpassive)に違反しました。 IrqlObPassive 規則は、IRQL = PASSIVE_LEVEL 場合にのみ、ドライバーが[Obreferenceobjectbyhandle](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)を呼び出す必要があることを指定します。|
|0x0002001C |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlPsPassive](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlpspassive)に違反しました。 IrqlPsPassive 規則は、IRQL = PASSIVE_LEVEL 場合にのみ、ドライバーが特定のプロセスおよびスレッドマネージャールーチンを呼び出す必要があることを指定します。|
|0x0002001D |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[Irqlreturn](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlreturn)に違反しました。|
|0x0002001E |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlRtlPassive](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlrtlpassive)に違反しました。 IrqlRtlPassive 規則は、IRQL = PASSIVE_LEVEL 場合にのみ、ドライバーが[RtlDeleteRegistryValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtldeleteregistryvalue)を呼び出す必要があることを指定します。|
|0x0002001F |違反した規則条件を説明する文字列へのポインター。|ルールの状態変数へのポインター (省略可能)。|予約済み|このドライバーは、DDI コンプライアンス規則[IrqlZwPassive](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlzwpassive)に違反しました。 IrqlZwPassive 規則は、IRQL = PASSIVE_LEVEL 場合にのみ、ドライバーが[Zwclose](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)を呼び出す必要があることを指定します。|
|0x00020022 |違反した規則条件を説明する文字列へのポインター。|予約済み (未使用)|予約済み (未使用)|このドライバーは、DDI コンプライアンス規則[IrqlIoDispatch](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliodispatch)に違反しました。|
|0x00020023 |違反した規則条件を説明する文字列へのポインター。 |予約済み (未使用)。 |予約済み (未使用)。 |このドライバーは、DDI コンプライアンス規則[IrqlIoRtlZwPassive](https://docs.microsoft.com/windows-hardware/drivers/devtest/irql-rule-set--wdm-)に違反しました。 IrqlIoRtlZwPassive 規則は、ドライバーが IRQL = PASSIVE_LEVEL で実行されている場合にのみ、規則に記載されている DDIs を呼び出すように指定します。|
|0x00020024 |違反した規則条件を説明する文字列へのポインター。 |予約済み (未使用)。 |予約済み (未使用)。 |このドライバーは、DDI コンプライアンス規則[Irqlntifsapcpassive](https://docs.microsoft.com/windows-hardware/drivers/devtest/irql-rule-set--wdm-)に違反しています。 IrqlNtifsApcPassive 規則では、ドライバーが IRQL = PASSIVE_LEVEL または IRQL < = APC_LEVEL のいずれかで実行されている場合にのみ、規則に記載されている DDIs を呼び出すように指定します。|
|0x00020025 |違反した規則条件を説明する文字列へのポインター。 |予約済み (未使用)。 |予約済み (未使用)。 |このドライバーは、DDI コンプライアンス規則[IrqlKeMore](https://docs.microsoft.com/windows-hardware/drivers/devtest/irql-rule-set--wdm-)に違反しました。 IrqlKeMore 規則は、これらの DDIs に必要な IRQL の規則に示されている DDIs をドライバーが呼び出すことを指定します。|

### <a name="0x00040003-to-0x00043006---ddi-compliance-rule-violations"></a>0x00040003 から 0x00043006-DDI コンプライアンス規則違反

|パラメーター1|パラメータ 2|パラメーター3|パラメーター4|エラーの原因|
|--- |--- |--- |--- |--- |
|0x00040003 |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[CriticalRegions](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-criticalregions)に違反しました。|
|0x00040006 |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[QueuedSpinLock](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-queuedspinlock)に違反しました。|
|0x00040007 |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[QueuedSpinLockRelease](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-queuedspinlockrelease)に違反しました。|
|0x00040009 |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンスルール[スピンロック](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-spinlock)に違反しました。|
|0x0004000A | 違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (2 番目の引数は! ruleinfo)|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[SpinlockRelease](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-spinlockrelease)に違反しました。|
|0x0004000E |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[GuardedRegions](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-guardedregions)に違反しました。|
|0x0004100B |違反した規則条件を説明する文字列へのポインター。|予約済み (未使用)|予約済み (未使用)|このドライバーは、DDI コンプライアンスルール[Requestedpowerirp](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-requestedpowerirp)に違反しました。|
|0x0004100F |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[IoSetCompletionExCompleteIrp](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-iosetcompletionexcompleteirp)に違反しました。|
|0x00043006 |違反した規則条件を説明する文字列へのポインター。|予約済み (未使用)|予約済み (未使用)|このドライバーは、DDI コンプライアンス規則[PnpRemove](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-pnpremove)に違反しました。|

### <a name="0x00081001-to-0x00082005---avstream-driver-compliance-rule-violations"></a>0x00081001 ~ 0x00081001-AVStream ドライバーのコンプライアンス規則違反

|パラメーター1|パラメータ 2|パラメーター3|パラメーター4|エラーの原因|
|--- |--- |--- |--- |--- |
|0x00081001 |違反した規則条件を説明する文字列へのポインター。 |内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[KsDeviceMutex](https://docs.microsoft.com/windows-hardware/drivers/devtest/ks-ksdevicemutex)に違反しました。|
|0x00081002 |違反した規則条件を説明する文字列へのポインター。 |内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI のコンプライアンス規則[Ksstreamポインタの複製](https://docs.microsoft.com/windows-hardware/drivers/devtest/ks-ksstreampointerclone)に違反しました。|
|0x00081003 |違反した規則条件を説明する文字列へのポインター。 |予約済み (未使用)|予約済み (未使用)|このドライバーは、DDI コンプライアンス規則[Ksstreampointerlock ロック](https://docs.microsoft.com/windows-hardware/drivers/devtest/ks-ksstreampointerlock)に違反しました。|
|0x00081004 |違反した規則条件を説明する文字列へのポインター。 |内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[Ksstreamポインタ unlock](https://docs.microsoft.com/windows-hardware/drivers/devtest/ks-ksstreampointerunlock)に違反しました。|
|0x00081005 |違反した規則条件を説明する文字列へのポインター。 |予約済み (未使用)|予約済み (未使用)|このドライバーは、DDI コンプライアンス規則[Kscallbackreturn](https://docs.microsoft.com/windows-hardware/drivers/devtest/ks-kscallbackreturn)に違反しました。|
|0x00081006 |違反した規則条件を説明する文字列へのポインター。 |内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[Ksirqldevicecallbacks](https://docs.microsoft.com/windows-hardware/drivers/devtest/ks-ksirqldevicecallbacks)に違反しました。|
|0x00081007 |違反した規則条件を説明する文字列へのポインター。 |内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[Ksirqlfiltercallbacks バック](https://docs.microsoft.com/windows-hardware/drivers/devtest/ks-ksirqlfiltercallbacks)に違反しました。|
|0x00081008 |違反した規則条件を説明する文字列へのポインター。 |内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[Ksirqlpincallbacks バック](https://docs.microsoft.com/windows-hardware/drivers/devtest/ks-ksirqlpincallbacks)に違反しました。|
|0x00081009 |違反した規則条件を説明する文字列へのポインター。 |予約済み (未使用)|予約済み (未使用)|このドライバーは、DDI コンプライアンス規則[KsIrqlDDIs](https://docs.microsoft.com/windows-hardware/drivers/devtest/ks-ksirqlddis)に違反しました。|
|0x0008100A |違反した規則条件を説明する文字列へのポインター。 |内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[Ksfiltermutex](https://docs.microsoft.com/windows-hardware/drivers/devtest/ks-ksfiltermutex)に違反しました。|
|0x0008100B |違反した規則条件を説明する文字列へのポインター。 |内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[Ksprocessingmutex](https://docs.microsoft.com/windows-hardware/drivers/devtest/ks-ksprocessingmutex)に違反しました。|
|0x0008100C |違反した規則条件を説明する文字列へのポインター。 |内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[Ksinvalidstreampointer](https://docs.microsoft.com/windows-hardware/drivers/devtest/rules-for-avstream-drivers)に違反しました。|
|0x00082001 |違反した規則条件を説明する文字列へのポインター。 |内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[KsTimedPinSetDeviceState](https://docs.microsoft.com/windows-hardware/drivers/devtest/ks-kstimedpinsetdevicestate)に違反しました。|
|0x00082002 |違反した規則条件を説明する文字列へのポインター。 |内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[KsTimedDeviceCallbacks](https://docs.microsoft.com/windows-hardware/drivers/devtest/ks-kstimeddevicecallbacks)に違反しました。|
|0x00082003 |違反した規則条件を説明する文字列へのポインター。 |内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[KsTimedFilterCallbacks](https://docs.microsoft.com/windows-hardware/drivers/devtest/ks-kstimedfiltercallbacks)に違反しました。|
|0x00082004 |違反した規則条件を説明する文字列へのポインター。 |内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[KsTimedPinCallbacks](https://docs.microsoft.com/windows-hardware/drivers/devtest/ks-kstimedpincallbacks)に違反しました。|
|0x00082005 |違反した規則条件を説明する文字列へのポインター。 |内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[KsTimedProcessingMutex](https://docs.microsoft.com/windows-hardware/drivers/devtest/ks-kstimedprocessingmutex)に違反しました。|


### <a name="0x00091001-to-0x0009400c---ndis-ddi-compliance-rule-violations"></a>0x00091001 から 0X00091001-NDIS DDI コンプライアンス規則違反

|パラメーター1|パラメータ 2|パラメーター3|パラメーター4|エラーの原因|
|--- |--- |--- |--- |--- |
|0x00091001 |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[NdisOidComplete](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoidcomplete)に違反しました。|
|0x00091002 |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[NdisOidDoubleComplete](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoiddoublecomplete)に違反しました。|
|0x0009100E |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|このドライバーは、DDI コンプライアンス規則[NdisOidDoubleRequest](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoiddoublerequest)に違反しました。|
|0x00092003 |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|ドライバーが NDIS/WIFI 検証ルール[NdisTimedOidComplete](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimedoidcomplete)に違反しました。|
|0x0009200D |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|ドライバーが NDIS/WIFI 検証ルール[NdisTimedDataSend](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimeddatasend)に違反しました。|
|0x0009200F |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|ドライバーが NDIS/WIFI 検証ルール[NdisTimedDataHang](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimeddatahang)に違反しました。|
|0x00092010 |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。 |ドライバーが NDIS/WIFI 検証ルール[NdisFilterTimedPauseComplete](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndisfiltertimedpausecomplete-)に違反しました。|
|0x00092011 |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。 |ドライバーが NDIS/WIFI 検証ルール[NdisFilterTimedDataSend](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndisfiltertimeddatasend)に違反しました。|
|0x00092012 |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。 |ドライバーが NDIS/WIFI 検証ルール[NdisFilterTimedDataReceive](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndisfiltertimeddatareceive)に違反しました。|
|0x00093004 |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|ドライバーが NDIS/WIFI 検証ルール[WlanAssociation](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlanassociation)に違反しました。|
|0x00093005 |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|ドライバーが NDIS/WIFI 検証ルール[WlanConnectionRoaming](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlanconnectionroaming)に違反しました。|
|0x00093006 |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|ドライバーが NDIS/WIFI 検証ルール[WlanDisassociation](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlandisassociation)に違反しました。|
|0x00093101|違反した規則条件を説明する文字列へのポインター。 |予約済み (未使用)|予約済み (未使用)|ドライバーが NDIS/WIFI 検証ルール[WlanAssert](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification-rule-set)に違反しました。|
|0x00094007 |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|ドライバーが NDIS/WIFI 検証ルール[WlanTimedAssociation](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedassociation)に違反しました。|
|0x00094008 |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|ドライバーが NDIS/WIFI 検証ルール[WlanTimedConnectionRoaming](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedconnectionroaming)に違反しました。|
|0x00094009 |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|ドライバーが NDIS/WIFI 検証ルール[WlanTimedConnectRequest](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedconnectrequest)に違反しました。|
|0x0009400B |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|ドライバーが NDIS/WIFI 検証ルール[WlanTimedLinkQuality](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedlinkquality)に違反しました。|
|0x0009400C |違反した規則条件を説明する文字列へのポインター。|内部規則の状態のアドレス (! ruleinfo の2番目の引数)。|補足状態のアドレス (! ruleinfo の3番目の引数)。|ドライバーが NDIS/WIFI 検証ルール[WlanTimedScan](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wlantimedscan)に違反しました。|

<a name="cause"></a>原因
-----

原因の説明については、「Parameters」セクションの各コードの説明を参照してください。 詳細については、 [ **! analyze-v**](-analyze.md)拡張機能を使用して取得できます。

<a name="resolution"></a>解像度
----------

このバグチェックは、ドライバーの検証ツールで1つ以上のドライバーを監視するように指示されている場合にのみ発生します。 ドライバーの検証ツールを使用しない場合は、非アクティブ化する必要があります。 また、この問題の原因となったドライバーを削除することも考えられます。

ドライバーライターの場合は、このバグチェックで取得した情報を使用して、コード内のバグを修正します。

ドライバーの検証機能の詳細については、「 [Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)」を参照してください。

<a name="remarks"></a>注釈
-------

\_プール\_型コードは Ntddk で列挙されます。 特に、 **0** (ゼロ) は非ページプールを示し、 **1** (1) はページプールを示します。

*(Windows 8 以降のバージョンの windows)* [DDI 準拠の確認](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)でバグチェックが行われる場合は、ドライバーのソースコードに対して[静的ドライバー検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)を実行し、バグチェックの原因となった ddi コンプライアンス規則 (パラメーター1の値によって識別される) を指定します。 静的ドライバーの検証ツールは、ソースコード内の問題の原因を特定するのに役立ちます。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目

[ドライバーの検証機能が有効になっている場合のバグチェックの処理](handling-a-bug-check-when-driver-verifier-is-enabled.md)
