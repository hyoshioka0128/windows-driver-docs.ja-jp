---
title: ファイルシステムランタイムライブラリのサポートルーチン
description: ファイルシステムランタイムライブラリのサポートルーチン
ms.assetid: e3c2e109-891a-494a-b62c-e6ccc7afc9d8
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: c4858296e65e288f9d84bdf18793b7755d210bbc
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955784"
---
# <a name="file-system-runtime-library-support-routines"></a>ファイルシステムランタイムライブラリのサポートルーチン

次のシステム指定のファイルシステムランタイムライブラリサポート関数とマクロは、カーネルモードのファイルシステムおよびファイルシステムフィルタードライバーによって呼び出すことができます。 これらはアルファベット順に表示されます。

**ヘッダーファイル:** *ntifs*

** プレフィックス:FsRtl * Xxx @ no__t-0 @ no__t-1

| 関数またはマクロ | 説明 |
| ----------------- | ----------- |
| **FsRtlAcknowledgeEcp** | 追加の作成パラメーター (ECP) コンテキスト構造を確認済みとしてマークします。 |
| **FsRtlAcquireFileExclusive** | システム用に予約されています。 |
| **FsRtlAddLargeMcbEntry** | 既存のマップコントロールブロック (MCB) に新しいマッピングを追加します。 |
| **FsRtlAddMcbEntry** | 使われていません。 |
| **FsRtlAddToTunnelCache** | ファイルの名前が変更されたとき、または削除されたときにディレクトリから削除されたファイル名をキャッシュします。 |
| **FsRtlAllocateExtraCreateParameter** | ユーザー定義の追加作成パラメーター (ECP) コンテキスト構造にメモリを割り当て、その構造体へのポインターを生成します。 |
| **FsRtlAllocateExtraCreateParameterFromLookasideList** | 追加の作成パラメーター (ECP) コンテキスト構造に対して指定されたルックアサイドリストからメモリプールを割り当て、その構造体へのポインターを生成します。 |
| **FsRtlAllocateExtraCreateParameterList** | ECP_LIST 構造体にページプールメモリを割り当て、その構造体へのポインターを生成します。 |
| **FsRtlAllocateFileLock** | 新しい FILE_LOCK 構造体を割り当て、初期化します。 |
| **FsRtlAllocatePool** | 使われていません。 |
| **FsRtlAllocatePoolWithQuota** | 使われていません。 |
| **FsRtlAllocatePoolWithQuotaTag** | プールメモリ、現在のプロセスに対する課金クォータを割り当てます。 |
| **FsRtlAllocatePoolWithTag** | プールのメモリを割り当てます。 |
| **FsRtlAllocateResource** | 使われていません。 |
| **FsRtlAreNamesEqual** | 2つの Unicode 文字列が等しいかどうかを判断します。 |
| **FsRtlAreThereCurrentFileLocks** | 指定したファイルのバイト範囲ロックが存在するかどうかを確認します。 |
| **FsRtlAreThereCurrentOrInProgressFileLocks** | ファイルに対してバイト範囲ロックが割り当てられているかどうか、またはそのファイルに対して実行中のロック操作があるかどうかを確認します。
| **Fsrtlareingfilelocks** | ファイルロックキューで待機中のファイルロックを確認します。 |
| **Fsrtlarevolumestartupの実行が完了しました** | ボリュームスタートアップアプリケーションが処理を完了したかどうかを判断します。 |
| **FsRtlBalanceReads** | は、ミラー化されたドライブからの読み取りを負荷分散することが安全であることを、フォールトトレラントディスクドライバーに通知します。 |
| **FsRtlCancellableWaitForMultipleObjects** | 1つ以上のディスパッチャーオブジェクトで、キャンセル可能な待機操作 (終了できる待機) を実行します。 |
| **FsRtlCancellableWaitForSingleObject** | ディスパッチャーオブジェクトで、キャンセル可能な待機操作 (終了できる待機) を実行します。 |
| **FsRtlChangeBackingFileObject** | 現在のファイルオブジェクトを新しいファイルオブジェクトで置き換えます。 |
| **FsRtlCheckLockForReadAccess** | 特定の IRP に関連付けられたプロセスに、ファイルのロックされた領域への読み取りアクセス権があるかどうかを判断します。 |
| **FsRtlCheckLockForWriteAccess** | 特定の IRP に関連付けられているプロセスに、ファイルのロックされた領域への書き込みアクセス権があるかどうかを判断します。 |
| **FsRtlCheckLockForOplockRequest** | ファイルの割り当てサイズ内のロックを確認します。 ファイルロックオブジェクトは、oplock 要求が許可されないようにするバイト範囲ロックがあるかどうかをチェックします。 |
| **FsRtlCheckOplock** | ファイル i/o 操作の IRP を、ファイルの現在の便宜的ロック (oplock) 状態と同期します。 |
| **FsRtlCheckOplockEx** | ファイル i/o 操作の IRP を、ファイルの現在の便宜的ロック (oplock) 状態と同期します。 |
| **FsRtlCheckUpperOplock** | サブシステムが変更状態を保持している場合に、セカンダリまたは階層化されたファイルシステムに便宜的ロック (oplock) チェックを提供します。 |
| **FsRtlCompleteRequest** | 指定された状態で IRP を完了します。 |
| **FsRtlCopyRead** | キャッシュされたファイルからユーザーバッファーにデータをコピーします。 |
| **FsRtlCopyWrite** | ユーザーバッファーからキャッシュされたファイルにデータをコピーします。 |
| **FsRtlCreateSectionForDataScan** | セクションオブジェクトを作成します。 このルーチンは細心の注意を払って使用してください。 |
| **FsRtlCurrentBatchOplock** | ファイルシステムまたはフィルタードライバーは、このルーチンを呼び出して、ファイルにバッチまたはフィルターの便宜的ロック (oplock) があるかどうかを判断します。 |
| **FsRtlCurrentOplock** | ファイルシステムまたはフィルタードライバーは、このルーチンを呼び出して、ファイルに便宜的ロック (oplock) があるかどうかを判断します。 |
| **FsRtlCurrentOplockH** | ファイルシステムまたはフィルタードライバーは、このルーチンを呼び出して、ファイルに CACHE_HANDLE_LEVEL 便宜ロック (oplock) があるかどうかを判断します。 |
| **FsRtlDeleteExtraCreateParameterLookasideList** | 追加のパラメーター (ECP) ルックアサイドリストを解放します。 |
| **FsRtlDeleteKeyFromTunnelCache** | 削除されるディレクトリ内のファイルのトンネルキャッシュエントリを削除します。 |
| **FsRtlDeleteTunnelCache** | トンネルキャッシュを削除します。 |
| **FsRtlDeregisterUncProvider** | 解除は、マルチ UNC プロバイダー (MUP) を使用して汎用名前付け規則 (UNC) プロバイダーとして登録されているリダイレクターを使用します。 |
| **FsRtlDissectDbcs** | ANSI または2バイト文字セット (DBCS) のパス名文字列を指定すると、このルーチンは2つの文字列を返します。1つは文字列で見つかった最初のファイル名、もう1つはパス名文字列の残りの未解析部分を含んでいます。 |
| **FsRtlDissectName** | Unicode のパス名文字列を指定すると、このルーチンは2つの文字列を返します。1つは文字列で見つかった最初のファイル名、もう1つはパス名文字列の残りの未解析部分を含んでいる文字列です。 |
| **ワイルドカードによる Fsrtl@ Dbcsa** | ANSI または2バイト文字セット (DBCS) の文字列にワイルドカード文字が含まれているかどうかを判断します。 |
| **FsRtlDoesNameContainWildCards** | Unicode 文字列にワイルドカード文字が含まれているかどうかを判断します。 |
| **FsRtlEnterFileSystem** | 通常のカーネルモード非同期プロシージャ呼び出し (APC) の配信を一時的に無効にします。 特別なカーネルモードの Apc は引き続き配信されます。
| **FsRtlExitFileSystem** | 前の**Fsrtlenterfilesystem**の呼び出しによって無効にされた通常のカーネルモード apc の配信を再度有効にします。 |
| **FsRtlFastCheckLockForRead** | 指定したプロセスに、ファイルのロックされたバイト範囲への読み取りアクセス権があるかどうかを判断します。 |
| **FsRtlFastCheckLockForWrite** | 指定したプロセスに、ファイルのロックされたバイト範囲への書き込みアクセス権があるかどうかを判断します。 |
| **FsRtlFastLock** | ファイルシステムおよびフィルタードライバーによって、ファイルストリームのバイト範囲ロックを要求するために使用されます。 |
| **FsRtlFastUnlockAll** | ファイルについて、指定したプロセスによって取得されたすべてのバイト範囲ロックを解放します。 |
| **FsRtlFastUnlockAllByKey** | ファイルの指定したキー値を使用して、指定したプロセスによって取得されたすべてのバイト範囲ロックを解放します。 |
| **FsRtlFastUnlockSingle** | 指定したプロセスによって取得されたバイト範囲ロックを、指定したキー値、ファイルオフセット、および長さを使用して解放します。 |
| **FsRtlFindExtraCreateParameter** | 指定した ECP リスト内で、指定した型の ECP コンテキスト構造を検索し、見つかった場合は、この構造体へのポインターを返します。 |
| **FsRtlFindInTunnelCache** | 指定した名前と一致する、トンネルキャッシュ内の一致するエントリを検索します。 |
| **FsRtlFreeExtraCreateParameter** | ECP コンテキスト構造のメモリを解放します。 |
| **FsRtlFreeExtraCreateParameterList** | 余分な作成パラメーター (ECP) のリスト構造を解放します。 |
| **FsRtlFreeFileLock** | ファイルのロック構造を初期化前して解放します。 |
| **FsRtlGetEcpListFromIrp** | 指定された IRP_MJ_CREATE 操作に関連付けられている追加の create parameter (ECP) コンテキスト構造リストへのポインターを返します。 |
| **FsRtlGetFileSize サイズ** | ファイルのサイズを取得するために使用します。 |
| **FsRtlGetNextExtraCreateParameter** | 指定された ECP リスト内の次の (または最初の) extra 作成パラメーター (ECP) コンテキスト構造へのポインターを返します。 |
| **FsRtlGetNextFileLock** | 指定したファイルに現在存在するバイト範囲ロックを列挙するために使用します。 |
| **FsRtlGetNextLargeMcbEntry** | マップコントロールブロック (MCB) から割り当ての実行を取得します。 |
| **FsRtlGetNextMcbEntry** | 使われていません。 |
| **FsRtlGetPerFileContextPointer** | 開いているファイルの*FileContextSupportPointer*を返します。 |
| **FsRtlGetPerStreamContextPointer** | ファイルストリームのファイルシステムのストリームコンテキストを返します。 |
| **FsRtlGetSectorSizeInformation** | 記憶域ボリュームの物理的および論理的なセクターサイズ情報を取得します。 |
| **FsRtlGetSupportedFeatures** | 指定されたデバイスオブジェクトに接続されているボリュームのサポートされている機能を返します。 |
| **Fsrtlincreの Ccfastmdlreadwait** | プロセッサ制御ブロック (PRCB) オブジェクトのキャッシュマネージャーの CcFastMdlReadWait パフォーマンスカウンターメンバーをインクリメントします。 |
| **Fsrtlincrebf Ccfastreadnotif** | キャッシュマネージャーのシステムカウンターのプロセッサごとの制御ブロックで、 **Ccfastreadnotpossible**パフォーマンスカウンターをインクリメントします。 |
| **Fsrtlincreの Ccfastreadnowait** | キャッシュマネージャーのシステムカウンターのプロセッサごとの制御ブロックで**Ccfastreadnowait**パフォーマンスカウンターをインクリメントします。 |
| **Fsrtlincreの Ccfastreadresourcemiss** | キャッシュマネージャーのシステムカウンターのプロセッサごとの制御ブロックで、 **Ccfastreadnotpossible**パフォーマンスカウンターをインクリメントします。 |
| **Fsrtlincreの Ccfastreadwait** | キャッシュマネージャーのシステムカウンターのプロセッサごとの制御ブロックで**Ccfastreadwait**パフォーマンスカウンターをインクリメントします。 |
| **FsRtlInitExtraCreateParameterLookasideList** | 固定サイズの1つ以上の追加の作成パラメーターコンテキスト構造 (ECPs) の割り当てに使用される、ページングまたは非ページプールのルックアサイドリストを初期化します。 |
| **FsRtlInitializeExtraCreateParameter** | 余分な作成パラメーター (ECP) コンテキスト構造を初期化します。 |
| **FsRtlInitializeExtraCreateParameterList** | 余分な create parameter (ECP) コンテキスト構造リストを初期化します。 |
| **FsRtlInitializeFileLock** | FILE_LOCK 構造体を初期化します。 |
| **Fsrtlinitializelarge b** | マップコントロールブロック (MCB) 構造体を初期化します。 |
| **Fsrtlinitializemc b** | 使われていません。 |
| **FsRtlInitializeOplock** | 便宜的ロック (oplock) ポインターを初期化します。 |
| **FsRtlInitializeTunnelCache** | ボリュームの新しいトンネルキャッシュを初期化します。 |
| **FsRtlInitPerFileContext** | FSRTL_PER_FILE_CONTEXT 構造体を初期化します。 |
| **FsRtlInitPerFileObjectContext** | FSRTL_PER_FILEOBJECT_CONTEXT 構造体を初期化します。 |
| **FsRtlInitPerStreamContext** | フィルタードライバーコンテキスト構造を初期化します。 |
| **FsRtlInsertExtraCreateParameter** | 追加の作成パラメーター (ECP) のコンテキスト構造を ECP リストに挿入します。 |
| **FsRtlInsertPerFileContext** | ファイルのドライバーによって指定されたコンテキストオブジェクトに FSRTL_PER_FILE_CONTEXT オブジェクトを関連付けます。 |
| **FsRtlInsertPerFileObjectContext** | "レガシ" ファイルシステムフィルタードライバーの場合、 | \* * FsRtlInsertPerFileObjectContext 関数は、コンテキスト情報をファイルオブジェクトに関連付けます。 |
| **FsRtlInsertPerStreamContext** | ファイルシステムフィルタードライバーのストリームごとのコンテキスト構造をファイルストリームに関連付けます。 |
| **FsRtlIsAnsiCharacterLegal** | 文字が有効な ANSI 文字かどうかを判断します。 |
| **FsRtlIsAnsiCharacterLegalFat** | ANSI 文字が FAT ファイル名に対して有効かどうかを判断します。 |
| **FsRtlIsAnsiCharacterLegalHpfs** | ANSI 文字が HPFS ファイル名に対して有効かどうかを判断します。 |
| **FsRtlIsAnsiCharacterLegalNtfs** | ANSI 文字が NTFS ファイル名に対して有効かどうかを判断します。 |
| **FsRtlIsAnsiCharacterLegalNtfsStream** | ANSI 文字が NTFS ストリーム名に対して有効かどうかを判断します。 |
| **FsRtlIsAnsiCharacterWild** | ANSI 文字がワイルドカード文字かどうかを判断します。 |
| **FsRtlIsDbcsInExpression** | ANSI または2バイト文字セット (DBCS) 文字列が、指定されたパターンに一致するかどうかを判断します。 |
| **FsRtlIsEcpAcknowledged** | 指定された追加の作成パラメーター (ECP) コンテキスト構造が確認済みとしてマークされているかどうかを判断します。 |
| **FsRtlIsEcpFromUserMode** | 特別な作成パラメーター (ECP) コンテキスト構造がユーザーモードで発生したかどうかを判断します。 |
| **FsRtlIsFatDbcsLegal** | 指定された ANSI または2バイト文字セット (DBCS) 文字列が有効な FAT ファイル名であるかどうかを判断します。 |
| **FsRtlIsHpfsDbcsLegal** | 指定された ANSI または2バイト文字セット (DBCS) の文字列が、有効な HPFS ファイル名であるかどうかを判断します。 |
| **FsRtlIsLeadDbcsCharacter** | 文字が2バイト文字セット (DBCS) の先頭バイト (文字の最初のバイト) であるかどうかを判断します。 |
| **FsRtlIsNameInExpression** | Unicode 文字列が指定したパターンに一致するかどうかを判断します。 |
| **FsRtlIsNtstatusExpected** | 指定された例外が例外フィルターによって処理されるかどうかを判断します。 |
| **FsRtlIsPagingFile** | 指定されたファイルがページングファイルであるかどうかを判断します。 |
| **FsRtlIssueDeviceIoControl** | 同期デバイス i/o 制御要求をターゲットデバイスオブジェクトに送信します。 |
| **FsRtlIsSystemPagingFile** | 指定されたファイルが現在システムページングファイルであるかどうかを判断します。 |
| **FsRtlIsTotalDeviceFailure** | メディアまたはその他のハードウェア障害が発生したかどうかを判断します。 |
| **FsRtlIsUnicodeCharacterWild** | Unicode 文字がワイルドカード文字かどうかを判断します。 |
| **FsRtlLogCcFlushError** | 失われた遅延書き込みエラーをログに記録し、ユーザーにダイアログボックスを表示します。 |
| **FsRtlLookupLargeMcbEntry** | 仮想ブロック番号 (VBN) とマップコントロールブロック (MCB) を指定すると、このルーチンは、MCB で、指定された VBN に対応するマッピング情報を検索します。 |
| **FsRtlLookupLastLargeMcbEntry** | マップコントロールブロック (MCB) に格納されている最後のマッピングエントリを取得します。 |
| **FsRtlLookupLastLargeMcbEntryAndIndex** | 指定されたマップコントロールブロック (MCB) に格納されている最後のマッピングエントリを取得します。 |
| **Fsrtlstmcbentry** | 使われていません。 |
| **FsRtlLookupMcbEntry** | 使われていません。 |
| **FsRtlLookupPerFileContext** | 指定されたファイルに関連付けられている FSRTL_PER_FILE_CONTEXT オブジェクトへのポインターを返します。 |
| **FsRtlLookupPerFileObjectContext** | "レガシ" ファイルシステムフィルタードライバーの場合、この関数は、以前にファイルオブジェクトに関連付けられたコンテキスト情報を取得します。 |
| **FsRtlLookupPerStreamContext** | ファイルストリームのストリームごとのコンテキスト構造を取得します。 |
| **FsRtlLookupPerStreamContextInternal** | システム用に予約されています。 |
| **FsRtlMdlReadCompleteDev** | **Fsrtlmdlreaddev**ルーチンが開始した読み取り操作を完了します。 |
| **FsRtlMdlReadDev** | ファイルキャッシュ内の指定されたバイト範囲を直接指すメモリ記述子リスト (MDL) を返します。 |
| **FsRtlMdlReadEx** | 高速キャッシュされた MDL 読み取りを実行します。 要求されたデータがキャッシュされていない場合、ルーチンは IRP ベースの MDL 読み取り操作に戻ります。 |
| **FsRtlMdlWriteCompleteDev** | 割り当てられている**リソースを解放**します。 |
| **FsRtlMupGetProviderIdFromName** | ネットワークリダイレクターのデバイス名からマルチ UNC プロバイダー (MUP) に登録されているネットワークリダイレクターのプロバイダー id を取得します。 |
| **FsRtlMupGetProviderInfoFromFileObject** | リモートファイルシステム上にあるファイルのファイルオブジェクトから、マルチ UNC プロバイダー (MUP) に登録されているネットワークリダイレクターに関する情報を取得します。 |
| **FsRtlNormalizeNtstatus** | 任意の例外を、例外フィルターによって処理される状態値に変換します。 |
| **FsRtlNotifyCleanup** | ファイルオブジェクトへの最後のハンドルが解放されると、このルーチンは、指定された通知リストからファイルオブジェクトの通知構造 (存在する場合) を削除します。 |
| **FsRtlNotifyCleanupAll** | 指定された通知リストのすべてのメンバーを表示します。 |
| **FsRtlNotifyFilterChangeDirectory** | IRP_MN_NOTIFY_CHANGE_DIRECTORY 要求の notify 構造体を作成し、指定した通知リストに追加します。 |
| **FsRtlNotifyFilterReportChange** | 指定された通知リストで保留中の IRP_MN_NOTIFY_CHANGE_DIRECTORY 要求を完了します。 |
| **FsRtlNotifyFullChangeDirectory** | 通知要求の通知構造を作成し、指定した通知リストに追加します。 |
| **FsRtlNotifyFullReportChange** | 保留中の通知変更 Irp を完了します。 |
| **FsRtlNotifyInitializeSync** | 通知リストの同期オブジェクトを割り当て、初期化します。 |
| **FsRtlNotifyUninitializeSync** | 通知リストの同期オブジェクトの割り当てを解除します。 |
| **FsRtlNotifyVolumeEvent** | ボリュームイベントが発生していることを登録済みのアプリケーションに通知します。 |
| **FsRtlNotifyVolumeEventEx** | ボリュームイベントが発生していることを登録済みのアプリケーションに通知します。 ボリュームイベントには、ロック、ロック解除、マウント、または読み取り専用のボリュームが含まれます。 |
| **FsRtlNumberOfRunsInLargeMcb** | マップコントロールブロック (MCB) 内の実行の数を返します。 |
| **FsRtlNumberOfRunsInMcb** | 使われていません。 |
| **FsRtlOplockBreakH** | CACHE_HANDLE_LEVEL 便宜ロック (oplock) を解除します。 |
| **FsRtlOplockBreakToNone** | 使われていません。 |
| **FsRtlOplockBreakToNoneEx** | Oplock キーに関係なく、すべての便宜的ロック (oplock) を直ちに中断します。 |
| **FsRtlOplockFsctrl** | ファイルシステムまたはフィルタードライバーの代わりに、さまざまな便宜的ロック (oplock) 操作を実行します。 |
| **FsRtlOplockFsctrlEx** | ファイルシステムまたはフィルタードライバーの代わりに、さまざまな便宜的ロック (oplock) 操作を実行します。 |
| **FsRtlOplockIsFastIoPossible** | ファイルの便宜的ロック (oplock) の状態をチェックして、ファイルで高速 i/o を実行できるかどうかを判断します。 |
| **FsRtlOplockIsSharedRequest** | 便宜的ロック (oplock) に対する要求が共有 oplock を必要とするかどうかを判断します。 |
| **FsRtlOplockKeysEqual** | 2つのファイルオブジェクトのファイルオブジェクト拡張子に格納されている便宜的ロック (oplock) キーを比較します。 |
| **FsRtlPostPagingFileStackOverflow** | ページングファイルのスタックオーバーフロー項目をスタックオーバーフロースレッドにポストします。 |
| **FsRtlPostStackOverflow** | スタックオーバーフロー項目をスタックオーバーフロースレッドにポストします。 |
| **Fsrtlを備えた Mdlwritedev** | キャッシュに直接データを書き込むために、キャッシュされたファイルデータの指定した範囲を指すメモリ記述子リスト (MDLs) のリンクリストを返します。 |
| **Fsrtl/Lwriteex** | キャッシュに直接データを書き込むために、キャッシュされたファイルデータの指定した範囲を指すメモリ記述子リスト (MDLs) のリンクリストを返します。 書き込みのキャッシュサポートが使用できない場合、ルーチンは IRP ベースの MDL 書き込み操作に戻ります。 |
| **FsRtlPrepareToReuseEcp** | 追加の作成パラメーター (ECP) コンテキスト構造をリセットし、再利用できるように準備します。 |
| **FsRtlPrivateLock** | 使われていません。 |
| **FsRtlProcessFileLock** | ファイルロック操作の IRP を処理し、完了します。 |
| **FsRtlQueryCachedVdl** | キャッシュされたファイルの現在の有効なデータ長 (VDL) を取得します。 |
| **FsRtlRegisterFileSystemFilterCallbacks バック** | ファイルシステムフィルタードライバーとファイルシステムは、このルーチンを呼び出して、基になるファイルシステムが特定の操作を実行するときに呼び出される通知コールバックルーチンを登録します。 |
| **Fsrtlregisterprovider** | ネットワークリダイレクターを、システムの複数の UNC プロバイダー (MUP) と共に汎用名前付け規則 (UNC) プロバイダーとして登録します。 |
| **Fsrtlregisterprovider Ex** | ネットワークリダイレクターを、システムの複数の UNC プロバイダー (MUP) と共に汎用名前付け規則 (UNC) プロバイダーとして登録します。 |
| **FsRtlReleaseFile** | システム用に予約されています。 |
| **FsRtlRemoveDotsFromPath** | 不要な '. ' と '.. ' の出現を削除します 指定されたパスからです。 |
| **FsRtlRemoveExtraCreateParameter** | Ecp リストで ECP コンテキスト構造を検索します。見つかった場合は、ecp リストから切り離します。 |
| **FsRtlRemoveLargeMcbEntry** | マップコントロールブロック (MCB) から1つ以上のマッピングを削除します。 |
| **FsRtlRemoveMcbEntry** | 使われていません。 |
| **FsRtlRemovePerFileContext** | ファイルに関連付けられている**FSRTL_PER_FILE_CONTEXT オブジェクト**へのポインターを返します。 **Fsrtlremoveperfilecontext**は、関連するドライバー固有のコンテキスト情報と共に、使用しているリストから**FSRTL_PER_FILE_CONTEXT**オブジェクトを削除します。 |
| **FsRtlRemovePerFileObjectContext** | "従来の" ファイルシステムフィルタードライバーの場合、この関数は、ファイルごとのオブジェクトコンテキスト情報の構造体を、以前にファイルオブジェクトに関連付けられたファイル単位オブジェクトコンテキストのリストから解除します。 |
| **FsRtlRemovePerStreamContext** | ストリームごとのコンテキスト構造体を、ファイルストリームに関連付けられたストリームごとのコンテキストのリストから削除します。 |
| **FsRtlResetLargeMcb** | マップコントロールブロック (MCB) 構造体を切り捨て、ゼロのマッピングペアを格納します。 マッピングペアの配列は圧縮されません。 |
| **FsRtlSetEcpListIntoIrp** | 余分な create parameter (ECP) コンテキスト構造リストを IRP_MJ_CREATE 操作にアタッチします。 |
| **Fsrtlsetupadvanced ヘッダー** | フィルターコンテキストで使用するために、ファイルシステムによって * * FSRTL_ADVANCED_FCB_HEADER 構造体を初期化するために使用されます。 |
| **Fsrtlsetupadvanced Headerex** | を初期化するためにファイルシステムによって使用されます。 | ストリームとファイルコンテキストの両方で使用する**FSRTL_ADVANCED_FCB_HEADER**構造体。 |
| **FsRtlSplitLargeMcb** | マップコントロールブロック (MCB) 内のマッピングに穴を挿入します。 |
| **FsRtlSupportsPerFileContexts** | 指定した FILE_OBJECT に関連付けられているファイルシステムで、ファイルごとのコンテキスト情報がサポートされているかどうかを確認します。 |
| **FsRtlSupportsPerStreamContexts** | ファイルシステムが、指定されたファイルストリームのストリームごとのコンテキストをサポートするかどうかを判断します。 |
| **FsRtlTeardownPerFileContexts** | ファイルシステムは、ファイル制御ブロック (FCB) 構造に関連付けられている**FSRTL_PER_FILE_CONTEXT**オブジェクトを解放するために、このルーチンを呼び出します。 |
| **FsRtlTeardownPerStreamContexts** | 指定したに関連付けられているストリームごとのコンテキスト構造体をすべて解放します。 | \* * FsRtl_ADVANCED_FCB_HEADER 構造体。 |
| **FsRtlTestAnsiCharacter** | ANSI 文字または2バイト文字セット (DBCS) 文字が、指定された条件を満たすかどうかを判断します。 |
| **FsRtlTruncateLargeMcb** | 大きなマップコントロールブロック (MCB) を切り捨てます。 |
| **FsRtlTruncateMcb** | 使われていません。 |
| **FsRtlUninitializeFileLock** | 初期化前 FILE_LOCK 構造体。 |
| **Fsrtlun初期化 Elarge** | 初期化前は、大きなマップコントロールブロック (MCB) を指定します。 |
| **Fsrtlunの初期化 (Emc b)** | 使われていません。 |
| **FsRtlUninitializeOplock** | 初期化前を便宜的ロック (oplock) ポインターにします。 |
| **FsRtlUpperOplockFsctrl**セカンダリまたは階層化されたファイルシステムの便宜的ロック (oplock) 要求と受信確認を処理します。 |
| **FsRtlValidateReparsePointBuffer**| 指定された再解析ポイントバッファーが有効であることを確認します。 |
