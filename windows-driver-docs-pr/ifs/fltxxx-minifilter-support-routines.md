---
title: ミニフィルタードライバーのサポートルーチン
description: ミニフィルタードライバーのサポートルーチン
ms.assetid: ef3db0c7-7892-44dc-90ab-a1046e7d4af8
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: ba8c38d7558af2d431ddc7fa865c355132f05523
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955786"
---
# <a name="fltxxx-minifilter-support-routines"></a>FltXxx ミニフィルターサポートルーチン

次のシステム提供の**Flt**_Xxx_は、カーネルモードのミニフィルタードライバーで呼び出すことができますが、その他のデバイスドライバーは呼び出せません。 これらはアルファベット順に表示されます。

**ヘッダーファイル:** *fltkernel .h*

**プレフィックス: Flt**_Xxx_

| 関数またはマクロ | 説明 |
| ----------------- | ----------- |
| **FLT_IS_FASTIO_OPERATION** | 指定されたコールバックデータ構造が高速 i/o 操作を表すかどうかを判断します。 |
| **FLT_IS_FS_FILTER_OPERATION** | 指定したコールバックデータ構造が従来のファイルシステムフィルター (FSFilter) コールバック操作を表すかどうかを判断します。 |
 | **FLT_IS_IRP_OPERATION** | 指定されたコールバックデータ構造が i/o 要求パケット (IRP) ベースの i/o 操作を表すかどうかを判断します。 |
 | **FLT_IS_REISSUED_IO** | 指定したコールバックデータ構造が、再発行された i/o 操作を表すかどうかを判断します。 |
 | **FLT_IS_SYSTEM_BUFFER** | コールバックデータ構造内のシステムバッファーフラグをテストします。 |
 | **FltAcknowledgeEcp** | 追加の作成パラメーターコンテキスト構造 (ECP) を確認済みとしてマークします。 |
 | **FltAcquirePushLockExclusive** | 呼び出し元のスレッドによって排他的にアクセスするために、指定されたプッシュロックを取得します。 |
 | **FltAcquirePushLockShared** | 呼び出し元のスレッドによって共有アクセスに対して指定されたプッシュロックを取得します。 |
 | **FltAcquireResourceExclusive** | 呼び出し元のスレッドによって排他的にアクセスするために、指定されたリソースを取得します。 |
 | **FltAcquireResourceShared** | 呼び出し元のスレッドによって共有アクセス用に指定されたリソースを取得します。 |
 | **FltAdjustDeviceStackSizeForIoRedirection** | ソースデバイススタックのサイズを増やして、ターゲットスタックがソーススタックよりも深い場合に、指定したソースインスタンスから指定したターゲットインスタンスにミニフィルターで i/o をリダイレクトできるようにします。 |
 | **FltAllocateCallbackData** | ミニフィルタードライバーで i/o 要求を開始するために使用できるコールバックデータ構造を割り当てます。 |
 | **FltAllocateCallbackDataEx** | コールバックデータ構造体を割り当て、ミニフィルタードライバーが i/o 要求を開始するために使用できる追加の構造体のメモリを事前に割り当てることができます。 |
 | **FltAllocateContext** | 指定されたコンテキスト型のコンテキスト構造体を割り当てます。 |
 | **FltAllocateDeferredIoWorkItem** | 遅延 i/o 作業項目を割り当てます。 |
| **FltAllocateExtraCreateParameter** | ユーザー定義の追加作成パラメーター (ECP) コンテキスト構造にページングされたメモリプールを割り当て、その構造体へのポインターを生成します。 |
 | **FltAllocateExtraCreateParameterFromLookasideList** | 追加の作成パラメーター (ECP) コンテキスト構造に対して指定されたルックアサイドリストからメモリプールを割り当て、その構造体へのポインターを生成します。 |
 | **FltAllocateExtraCreateParameterList** | 余分な作成パラメーター (ECP) のリスト構造にページプールメモリを割り当て、その構造体へのポインターを生成します。 |
 | **FltAllocateFileLock** | 新しい FILE_LOCK 構造体を割り当て、初期化します。 |
 | **FltAllocateGenericWorkItem** | 汎用作業項目を割り当てます。 |
 | **FltAllocatePoolAlignedWithTag** | 非キャッシュ i/o 操作で使用するために、デバイスに固定されたバッファーを割り当てます。 |
 | **FltApplyPriorityInfoThread** | 優先順位情報をスレッドに適用するために、ミニフィルタードライバーによって使用されます。 |
 | **FltAttachVolume** | 新しいミニフィルタードライバーインスタンスを作成し、指定したボリュームに接続します。 |
 | **FltAttachVolumeAtAltitude** | フィルタドライバーの INF ファイルの設定を上書きして、指定した高度にミニフィルタードライバーインスタンスをボリュームにアタッチするデバッグサポートルーチン。 |
 | **FltBuildDefaultSecurityDescriptor** | FltCreateCommunicationPort で使用するための既定のセキュリティ記述子を構築**します。** |
 | **FltCancelFileOpen** | 新しく開かれたファイルまたは作成されたファイルを閉じます。 |
 | **FltCancelIo** | I/o 操作をキャンセルします。 |
 | **FltCancellableWaitForMultipleObjects** | 1つ以上のディスパッチャーオブジェクトで、キャンセル可能な待機操作 (終了できる待機) を実行します。 |
**FltCancellableWaitForSingleObject** | ディスパッチャーオブジェクトで、キャンセル可能な待機操作 (終了できる待機) を実行します。 |
| **FltCbdqDisable** | ミニフィルタードライバーのコールバックデータキューを無効にします。 |
| **FltCbdqEnable** | 以前の**FltCbdqDisable**の呼び出しによって無効にされたコールバックデータキューを有効にします。 |
| **FltCbdqInitialize** | ミニフィルタードライバーのコールバックデータキューディスパッチテーブルを初期化します。 |
| **FltCbdqInsertIo** | I/o 操作のコールバックデータ構造をミニフィルタードライバーのコールバックデータキューに挿入します。 |
| **FltCbdqRemoveIo** | ミニフィルタードライバーのコールバックデータキューから特定の項目を削除します。 |
| **FltCbdqRemoveNextIo** | ミニフィルタードライバーのコールバックデータキュー内の次に一致する項目を削除します。 |
| **FltCheckAndGrowNameControl** | FLT_NAME_CONTROL 構造体のバッファーが、指定されたバイト数を保持するのに十分な大きさであるかどうかを確認します。 そうでない場合は、 **Fltcheckandgrownamecontrol**によって、システムで割り当てられたより大きなバッファーに置き換えられます。 |
| **FltCheckLockForReadAccess** | 呼び出し元が、ファイルのロックされたバイト範囲に対する読み取りアクセス権を持っているかどうかを判断します。 |
| **FltCheckLockForWriteAccess** | 呼び出し元に、ファイルのロックされたバイト範囲への書き込みアクセス権があるかどうかを判断します。 |
| **FltCheckOplock** | IRP ベースのファイル i/o 操作のコールバックデータ構造体を、ファイルの現在の便宜的ロック (oplock) 状態と同期します。 |
| **FltCheckOplockEx** | ファイルの現在の便宜的ロック (oplock) 状態を持つ IRP ベースのファイル i/o 操作のコールバックデータ構造を同期します。 |
| **Fltclearの Datadirty** | コールバックデータ構造体のコールバックダーティフラグをクリアします。 |
| **FltClearCancelCompletion** | I/o 操作に対して指定されたキャンセルルーチンをクリアします。 |
| **FltClose** | **Fltcreatefile** **FltCreateFileEx**、または**FltCreateFileEx2**によって開かれたファイルハンドルを閉じます。 |
| **FltCloseClientPort** | 通信クライアントポートを coses。 |
| **FltCloseCommunicationPort** | ミニフィルタードライバーの通信サーバーポートを閉じます。 |
| **FltCloseSectionForDataScan** | ファイルストリームに関連付けられたセクションオブジェクトを閉じます。 |
| **FltCommitComplete** | TRANSACTION_NOTIFY_COMMIT 通知を確認します。 |
| **FltCommitFinalizeComplete** | TRANSACTION_NOTIFY_COMMIT_FINALIZE 通知を確認します。 |
| **FltCompareInstanceAltitudes** | 2つのミニフィルタードライバーインスタンスの高度を比較します。 |
| **FltCompletePendedPostOperation** | ミニフィルタードライバーの postoperation コールバックルーチンで保留されていた i/o 操作の完了処理を再開します。 |
| **FltCompletePendedPreOperation** | ミニフィルタードライバーの preoperation コールバック (PFLT_PRE_OPERATION_CALLBACK) ルーチンで保留されていた i/o 操作の処理を再開します。 |
| **FltCreateCommunicationPort** | ミニフィルタードライバーがユーザーモードアプリケーションからの接続要求を受信できる通信サーバーポートを作成します。 |
| **FltCreateFile** | 新しいファイルを作成するか、既存のファイルを開きます。 |
| **FltCreateFileEx** | 新しいファイルを作成するか、既存のファイルを開きます。 |
| **FltCreateFileEx2** | 新しいファイルを作成するか、既存のファイルを開きます。 このルーチンには、省略可能な create context パラメーターも含まれています。 |
| **FltCreateMailslotFile** | 新しいメールスロットサーバーを作成するか、既存のメールスロットを開きます。 |
| **FltCreateNamedPipeFile** | 新しいパイプを作成するか、既存のパイプを開きます。 |
| **FltCreateSectionForDataScan** | ファイルのセクションオブジェクトを作成します。 フィルターマネージャーでは、必要に応じて、作成されたセクションと i/o を同期させることができます。 |
| **FltCreateSystemVolumeInformationFolder** | ファイルシステムボリュームに "システムボリューム情報" フォルダーが存在することを確認します。 フォルダーが存在しない場合は、フォルダーが作成されます。 |
| **FltCurrentBatchOplock** | ファイルにバッチまたはフィルター便宜的ロック (oplock) があるかどうかを判断します。 |
| **FltCurrentOplock** | ファイルに便宜的ロック (oplock) があるかどうかを判断します。 |
| **FltCurrentOplockH** | ファイルに CACHE_HANDLE_LEVEL 便宜的ロック (oplock) があるかどうかを判断します。 |
| **FltDecodeParameters** | I/o 操作のメモリ記述子リスト (MDL) アドレス、バッファーポインター、バッファー長、および必要なアクセスパラメーターへのポインターを返します。 このようにすると、フィルター処理ドライバーによって、MDL のアドレス、バッファーポインター、バッファーの長さ、および複数の操作の種類に対する必要なアクセスにアクセスするヘルパールーチン内のこれらのパラメーターの位置を検索する switch ステートメントが保存されます。 |
| **FltDeleteContext** | 指定されたコンテキストを削除対象としてマークします。 |
| **FltDeleteExtraCreateParameterLookasideList** | 追加のパラメーター (ECP) ルックアサイドリストを解放します。 |
| **FltDeleteFileContext** | 指定したミニフィルタードライバーが特定のファイルに対して設定したファイルコンテキストを取得または削除します。 |
| **FltDeleteInstanceContext** | 指定したインスタンスからコンテキストを削除し、コンテキストを削除対象としてマークします。 |
| **FltDeletePushLock** | 指定されたプッシュロックを削除します。 |
| **FltDeleteStreamContext** | 特定のミニフィルタードライバーインスタンスによって特定のストリームに対して設定されているコンテキストを削除し、コンテキストを削除対象としてマークします。 |
| **FltDeleteStreamHandleContext** | 特定のミニフィルタードライバーインスタンスが特定のストリームハンドルに対して設定したコンテキストを削除し、コンテキストを削除対象としてマークします。 |
| **FltDeleteTransactionContext** | 指定されたトランザクションからコンテキストを削除し、コンテキストを削除対象としてマークします。 |
| **FltDeleteVolumeContext** | 指定されたミニフィルタードライバーが特定のボリュームに対して設定したコンテキストを削除し、コンテキストを削除対象としてマークします。 |
| **FltDetachVolume** | ミニフィルタードライバーインスタンスをボリュームからデタッチします。 |
| **FltDeviceIoControlFile** | 指定されたデバイスドライバーに制御コードを直接送信し、対応するドライバーが指定されたアクションを実行します。 |
| **Fltdo補完 Processingwhensafe** | この操作を安全に行うには、はミニフィルタードライバー postoperation コールバックルーチンを実行します。 |
| **Fldisks Listintransaction** | 特定のトランザクションにミニフィルタードライバーを参加させます。 |
| **FltEnumerateFilterInformation** | システム内のすべての登録済みフィルタードライバー (ミニフィルターおよびレガシフィルタードライバーを含む) に関する情報を提供します。 |
| **FltEnumerateFilters** | システム内のすべての登録済みミニフィルタードライバーを列挙します。 |
| **FltEnumerateInstanceInformationByDeviceObject** | 指定されたデバイスオブジェクトに関連するボリュームに接続されているミニフィルタードライバーインスタンスとレガシフィルタードライバーに関する情報を提供します。 |
| **FltEnumerateInstanceInformationByFilter** | 指定されたミニフィルタードライバーのインスタンスに関する情報を提供します。 |
| **FltEnumerateInstanceInformationByVolume** | 特定のボリュームに接続されているミニフィルタードライバーインスタンスとレガシフィルタードライバー (Windows Vista のみ) に関する情報を提供します。 |
| **FltEnumerateInstanceInformationByVolumeName** | 指定した名前を使用して、ボリュームに接続されているミニフィルタードライバーインスタンスとレガシフィルタードライバーに関する情報を提供します。 |
| **FltEnumerateInstances** | 指定されたミニフィルタードライバーまたはボリュームのミニフィルタードライバーインスタンスを列挙します。 |
| **FltEnumerateVolumeInformation** | フィルターマネージャーによって認識されるボリュームに関する情報を提供します。 |
| **FltEnumerateVolumes** | システム内のすべてのボリュームを列挙します。 |
| **FltFastIoMdlRead** | ファイルキャッシュ内の指定されたバイト範囲を直接指すメモリ記述子リスト (MDL) を返します。 |
| **Fltfa/Omdlreadcomplete** | **Fltfastiomdlread**ルーチンが開始した読み取り操作を完了します。 |
| **FltFastIoMdlWriteComplete** | **FltFastIoPrepareMdlWrite**に割り当てられたリソースを解放します。 |
| **FltFastIoPrepareMdlWrite** | キャッシュに直接データを書き込むために、キャッシュされたファイルデータの指定した範囲を指すメモリ記述子リスト (MDLs) のリンクリストを返します。 |
| **FltFlushBuffers** | 指定されたファイルのフラッシュ要求をファイルシステムに送信します。 |
| **FltFindExtraCreateParameter** | 指定した ECP リスト内で、指定した型の ECP コンテキスト構造を検索し、見つかった場合は、この構造体へのポインターを返します。 |
| **FltFreeCallbackData** | **FltAllocateCallbackData**ルーチンによって割り当てられたコールバックデータ構造体を解放します。 |
| **FltFreeDeferredIoWorkItem** | **FltAllocateDeferredIoWorkItem**ルーチンによって割り当てられた作業項目を解放します。 |
| **FltFreeExtraCreateParameter** | ECP コンテキスト構造のメモリを解放します。 |
| **FltFreeExtraCreateParameterList** | 余分な作成パラメーター (ECP) のリスト構造を解放します。 |
| **FltFreeFileLock** | 初期化された FILE_LOCK 構造体を初期化前して解放します。 |
| **FltFreeGenericWorkItem** | **FltAllocateGenericWorkItem**ルーチンによって割り当てられた作業項目を解放します。 |
| **FltFreePoolAlignedWithTag** | 以前の**FltAllocatePoolAlignedWithTag**の呼び出しで割り当てられたキャッシュ固定バッファーを解放します。 |
| **FltFreeSecurityDescriptor** | **Fltbuilddefaultsecuritydescriptor**ルーチンによって割り当てられたセキュリティ記述子を解放します。 |
| **FltFsControlFile** | 指定されたファイルシステムまたはファイルシステムフィルタードライバーに制御コードを直接送信し、対応するドライバーが指定されたアクションを実行します。 |
| **FltGetActivityIdCallbackData** | ミニフィルターのコールバックデータ内の要求に関連付けられている現在のアクティビティ ID を取得します。 |
| **Fltget下端インスタンス** | 指定されたボリュームのインスタンススタックの一番下にアタッチされているミニフィルタードライバーインスタンス (存在する場合) の非透過的なインスタンスポインターを返します。 |
| **FltGetContexts** | 現在の操作に関連するオブジェクトのミニフィルタードライバーのコンテキストを取得します。 |
| **FltGetContextsEx** | 現在の操作に関連するオブジェクトのミニフィルタードライバーのコンテキストを取得します。 |
| **FltGetDestinationFileNameInformation** | 名前を変更するか、NTFS ハードリンクを作成する対象のファイルまたはディレクトリの完全な宛先パス名を構築します。 |
| **FltGetDeviceObject** | 特定のボリュームのフィルターマネージャーのボリュームデバイスオブジェクト (VDO) へのポインターを返します。 |
| **FltGetDiskDeviceObject** | 特定のボリュームに関連付けられているディスクデバイスオブジェクトへのポインターを返します。 |
| **FltGetEcpListFromCallbackData** | 指定された作成操作のコールバックデータオブジェクトに関連付けられている追加の create parameter context structure (ECP) リストへのポインターを返します。 |
| **FltGetFileContext** | 指定したミニフィルタードライバーインスタンスによってファイルに設定されたコンテキストを取得します。 |
| **FltGetFileNameFormat** | \* * FLT_FILE_NAME_OPTIONS 値の名前形式部分を返します。 |
| **FltGetFileNameInformation** | ファイルまたはディレクトリの名前情報を返します。 |
| **FltGetFileNameInformationUnsafe** | 開いているファイルまたはディレクトリの名前情報を返します。 |
| **FltGetFileNameQueryMethod** | FLT_FILE_NAME_OPTIONS 値の名前クエリメソッドの部分を返します。 |
| **FltGetFileSystemType** | ボリュームオブジェクトまたはインスタンスオブジェクトを取得し、ボリュームのファイルシステムの種類を提供します。 |
| **FltGetFilterFromInstance** | 指定されたインスタンスを作成したミニフィルタードライバーの非透過フィルターポインターを返します。 |
| **FltGetFilterFromName** | *FilterName*パラメーターの値と一致する名前を持つ、登録されているミニフィルターのフィルターポインターを返します。 |
| **FltGetFilterInformation** | ミニフィルタードライバーに関する情報を提供します。 |
| **FltGetInstanceContext** | 特定のミニフィルタードライバーによってインスタンスに設定されたコンテキストを取得します。 |
| **FltGetInstanceInformation** | ミニフィルタードライバーのインスタンスに関する情報を返します。 |
| **FltGetIoPriorityHint** | コールバックデータから IO 優先順位情報を取得します。 |
| **FltGetIoPriorityHintFromCallbackData** | コールバックデータから IO 優先順位情報を取得します。 |
| **FltGetIoPriorityHintFromFileObject** | ファイルオブジェクトから IO 優先順位情報を取得します。 |
| **FltGetIoPriorityHintFromThread** | スレッドから IO 優先順位情報を取得します。 |
| **Fltgetirpq 名** | 主要な関数コードの名前を印刷可能な文字列として返します。 |
| **Fltget小さいインスタンス** | 同じボリューム上の特定のミニフィルタードライバーインスタンスの下にアタッチされている、次に小さいミニフィルタードライバーインスタンス (存在する場合) の非透過インスタンスポインターを返します。 |
| **FltGetNewSystemBufferAddress** | ファイルシステムによって割り当てられた*AssociatedIrp*バッファーを取得します。 ミニコールバックルーチンがこの関数を呼び出します。 |
| **FltGetNextExtraCreateParameter** | 指定された ECP リスト内の次の (または最初の) 余分な作成パラメーターコンテキスト構造 (ECP) へのポインターを返します。 |
| **FltGetRequestorProcess** | 指定された i/o 操作を要求したスレッドのプロセスポインターを返します。 |
| **FltGetRequestorProcessId** | 特定の i/o 操作を要求したスレッドに関連付けられたプロセスの一意の32ビットプロセス ID を返します。 |
| **FltGetRequestorProcessIdEx** | 特定の i/o 操作を要求したスレッドに関連付けられているプロセスのカーネルモードハンドルを返します。 |
| **FltGetRequestorSessionId** | 指定された i/o 操作を最初に要求したプロセスのセッション ID を返します。 |
| **FltGetRoutineAddress** | **FltMgrRoutineName**パラメーターによって指定されたルーチンへのポインターを返します。 |
| **FltGetSectionContext** | 指定したミニフィルタードライバーインスタンスによってファイルストリームに作成されたセクションコンテキストを取得します。 |
| **FltGetStreamContext** | 指定したミニフィルタードライバーインスタンスによってファイルストリームに設定されたコンテキストを取得します。 |
| **FltGetStreamHandleContext** | 指定したミニフィルタードライバーインスタンスによってストリームハンドルに設定されたコンテキストを取得します。 |
| **FltGetSwappedBufferMdlAddress** | ミニフィルタードライバーによってスワップされたバッファーのメモリ記述子リスト (MDL) アドレスを返します。 |
| **FltGetTopInstance** | 指定されたボリュームのインスタンススタックの最上位にアタッチされているミニフィルタードライバーインスタンスの、不透明なインスタンスポインターを返します。 |
| **FltGetTransactionContext** | 指定されたミニフィルタードライバーによってトランザクションに設定されたコンテキストを取得します。 |
| **FltGetTunneledName** | 以前の**FltGetFileNameInformation**、 **FltGetFileNameInformationUnsafe**、または**FltGetDestinationFileNameInformation**の呼び出しによってファイルに返された正規化された名前を使用して、ファイルのトンネル名を取得します。 |
| **FltGetUpperInstance** | 同じボリューム上の特定のミニフィルタードライバーインスタンスの上にアタッチされている、次に大きいミニフィルタードライバーインスタンス (存在する場合) の非透過的なインスタンスポインターを返します。 |
| **FltGetVolumeContext** | 指定したミニフィルタードライバーによってボリュームに設定されたコンテキストを取得します。 |
| **FltGetVolumeFromDeviceObject** | ボリュームデバイスオブジェクト (VDO) によって表されるボリュームの不透明なポインターを返します。 |
| **FltGetVolumeFromFileObject** | 指定されたファイルストリームが存在するボリュームの非透過ポインターを返します。 |
| **FltGetVolumeFromInstance** | 指定されたミニフィルタードライバーインスタンスがアタッチされているボリュームの不透明なポインターを返します。|
| **FltGetVolumeFromName** | 名前*がボリューム名パラメーターの*値と一致するボリュームの不透明なポインターを返します。 |
| **FltGetVolumeGuidName** | 指定されたボリュームのボリューム名を、ボリュームグローバル一意識別子 (GUID) 形式で返します。 |
| **FltGetVolumeInformation** | 特定のボリュームに関する情報を提供します。 |
| **FltGetVolumeInstanceFromName** | 指定されたボリューム上の特定のミニフィルタードライバーインスタンスの、非透過のインスタンスポインターを返します。 |
| **FltGetVolumeName ボリューム** | 指定されたボリュームのボリューム名を取得します。 |
| **FltGetVolumeProperties** | 指定されたボリュームのボリュームプロパティ情報を返します。 |
| **FltInitExtraCreateParameterLookasideList** | 固定サイズの1つ以上の追加の作成パラメーターコンテキスト構造 (ECPs) の割り当てに使用される、ページ分割または非ページプールのルックアサイドリストを初期化します。 |
| **FltInitializeFileLock** | 呼び出し元がページプールから割り当てた非透過 FILE_LOCK 構造体を初期化します。 |
| **FltInitializeOplock** | 便宜的ロック (oplock) ポインターを初期化します。 |
| **FltInitializePushLock** | プッシュロック変数を初期化します。 |
| **FltInsertExtraCreateParameter** | 追加の作成パラメーター (ECP) のコンテキスト構造を ECP リストに挿入します。 |
| **FltIs32bitProcess** |現在の i/o 操作の発信元が32ビットのユーザーモードアプリケーションであるかどうかを確認します。 |
| **FltIsCallbackDataDirty** | コールバックデータ構造内の FLTFL_CALLBACK_DATA_DIRTY フラグをテストします。 |
| **FltIsDirectory** | 指定されたファイルオブジェクトがディレクトリを表しているかどうかを判断します。 |
| **FltIsEcpAcknowledged** | 指定された追加の作成パラメーターコンテキスト構造 (ECP) が確認済みとしてマークされているかどうかを判断します。 |
| **FltIsEcpFromUserMode** | 追加の作成パラメーターコンテキスト構造 (ECP) がユーザーモードで発生したかどうかを判断します。 |
| **FltIsFltMgrVolumeDeviceObject** | 指定されたデバイスオブジェクトがフィルターマネージャーに属しているかどうか、およびデバイスオブジェクトがボリュームデバイスオブジェクトであるかどうかを判断します。 |
| **FltIsIoCanceled** | IRP ベースの操作が取り消されたかどうかを確認します。 |
| **FltIsIoRedirectionAllowed** | 指定したソースフィルターインスタンスから、指定した別のフィルターインスタンスに i/o をリダイレクトできるかどうかを判断します。 |
| **FltIsIoRedirectionAllowedForOperation** | 指定した FLT_CALLBACK_DATA 構造に関連付けられているフィルターインスタンスから、指定したフィルターインスタンスに i/o をリダイレクトできるかどうかを判断します。 |
| **FltIsOperationSynchronous** | 特定のコールバックデータ構造 (FLT_CALLBACK_DATA) が、同期または非同期の i/o 操作を表すかどうかを判断します。 |
| **FltIsVolumeSnapshot** | ボリュームまたはミニフィルタードライバーインスタンスがスナップショットボリュームにアタッチされているかどうかを判断します。 |
| **FltIsVolumeWritable** | ボリュームまたはミニフィルタードライバーインスタンスに対応するディスクデバイスが書き込み可能かどうかを指定します。 |
| **FltLoadFilter** | 現在実行中のシステムにミニフィルタードライバーを動的に読み込みます。 |
| **FltLockUserBuffer** | 指定された i/o 操作のユーザーバッファーをロックします。 |
| **FltNotifyFilterChangeDirectory** | IRP_MN_NOTIFY_CHANGE_DIRECTORY 操作の通知構造体を作成し、指定した通知リストに追加します。 |
| **FltObjectDereference 参照** | 非透過のフィルター、インスタンス、またはボリュームポインターからランダウン参照を削除します。 |
| **FltObjectReference** | 非透過のフィルター、インスタンス、またはボリュームポインターにランダウン参照を追加します。 |
| **FltOpenVolume** | 指定されたミニフィルタードライバーインスタンスがアタッチされているファイルシステムボリュームのハンドルおよびファイルオブジェクトポインターを返します。 |
| **FltOplockBreakH** | 便宜的ロック (oplock) CACHE_HANDLE_LEVEL 中断します。 |
| **FltOplockBreakToNone** | Oplock キーに関係なく、すべての便宜的ロック (oplock) を直ちに中断します。 |
| **FltOplockBreakToNoneEx** | Oplock キーに関係なく、すべての便宜的ロック (oplock) を直ちに中断します。 |
| **FltOplockFsctrl** | ミニフィルタードライバーの代わりにさまざまな便宜的ロック (oplock) 操作を実行します。 |
| **FltOplockFsctrlEx** | ミニフィルタードライバーの代わりにさまざまな便宜的ロック (oplock) 操作を実行します。 |
| **FltOplockIsFastIoPossible** | ファイルの便宜的ロック (oplock) の状態をチェックして、ファイルで高速 i/o を実行できるかどうかを判断します。 |
| **FltOplockIsSharedRequest** | 便宜的ロック (oplock) に対する要求が共有 oplock を必要とするかどうかを判断します。 |
| **FltOplockKeysEqual** | 2つのファイルオブジェクトのファイルオブジェクト拡張子に格納されている便宜的ロック (oplock) キーを比較します。 |
| **FltParseFileName** | ファイル名文字列から拡張、ストリーム、および final コンポーネントを解析します。 |
| **FltParseFileNameInformation** | FLT_FILE_NAME_INFORMATION 構造体の内容を解析します。 |
| **FltPerformAsynchronousIo** | 非同期 i/o 操作を開始します。 |
| **FltPerformSynchronousIo** | **FltAllocateCallbackData**を呼び出した後に、操作のコールバックデータ構造を割り当てる同期 i/o 操作を開始します。 |
| **Fltの完了** | TRANSACTION_NOTIFY_PREPARE 通知を確認します。 |
| **FltPrepareToReuseEcp** | 追加の作成パラメーター (ECP) コンテキスト構造をリセットし、再利用できるように準備します。 |
| **FltPrePrepareComplete** | TRANSACTION_NOTIFY_PREPREPARE 通知を確認します。 |
| **FltProcessFileLock** | ファイルのロック操作を処理して完了します。 |
| **FltPropagateActivityIdToThread** | フィルター処理のコールバックデータの IRP から、現在のスレッドにアクティビティ ID を関連付けます。 |
| **FltPurgeFileNameInformationCache** | フィルターマネージャーの名前から、指定したミニフィルタードライバーインスタンスによって提供された名前から生成されたすべてのファイル名情報の構造をキャッシュします。 |
| **FltQueryDirectoryFile** | 指定されたファイルオブジェクトによって指定されたディレクトリ内のファイルに関するさまざまな種類の情報を返します。 |
| **Fltquerごみ箱** | ファイルの拡張属性 (EA) 値に関する情報を返します。 |
| **FltQueryInformationFile** | 指定されたファイルの情報を取得します。 |
| **FltQueryQuotaInformationFile** | ファイルオブジェクトに関連付けられているクォータエントリを取得します。 |
| **FltQuerySecurityObject** | オブジェクトのセキュリティ記述子のコピーを取得します。 |
| **FltQueryVolumeInformation** | 指定したインスタンスがアタッチされているボリュームに関する情報を取得します。 |
| **FltQueryVolumeInformationFile** | 指定されたファイル、ディレクトリ、記憶装置、またはボリュームのボリューム情報を取得します。 |
| **FltQueueDeferredIoWorkItem** | IRP ベースの i/o 操作をワークキューにポストします。 |
| **FltQueueGenericWorkItem** | 特定の i/o 操作に関連付けられていない作業項目を作業キューにポストします。 |
| **FltReadFile** | 開いているファイル、ストリーム、またはデバイスからデータを読み取ります。 |
| **FltReadFileEx** | 開いているファイル、ストリーム、またはデバイスからデータを読み取ります。 この関数は、 **Fltreadfile**を拡張して、マップされたバッファーアドレスの代わりに、データの読み取りに MDL をオプションで使用できるようにします。 |
| **FltReferenceContext** | コンテキスト構造の参照カウントをインクリメントします。 |
| **FltReferenceFileNameInformation** | ファイル名情報の構造体の参照カウントをインクリメントします。 |
| **FltRegisterFilter** | ミニフィルタードライバーを登録します。 |
| **FltRegisterForDataScan** | ミニフィルターインスタンスに接続されているボリュームのデータスキャンを有効にします。 |
| **FltReissueSynchronousIo** | 以前に同期された i/o 操作からのパラメーターを使用する、新しい同期 i/o 操作を開始します。 |
| **FltReleaseContext** | コンテキストの参照カウントをデクリメントします。 |
| **FltReleaseContexts** | 指定された FLT_RELATED_CONTEXTS 構造体の各コンテキストを解放します。 |
| **FltReleaseContextsEx** | 指定された FLT_RELATED_CONTEXTS_EX 構造体の各コンテキストを解放します。 |
| **FltReleaseFileNameInformation** | ファイル名情報の構造体を解放します。 |
| **FltReleasePushLock** | 現在のスレッドが所有している、指定したプッシュロックを解放します。 |
| **FltReleaseResource** | 現在のスレッドが所有している指定されたリソースを解放します。 |
| **FltRemoveExtraCreateParameter** | Ecp リストで ECP コンテキスト構造を検索します。見つかった場合は、ecp リストから切り離します。 |
| **FltRequestOperationStatusCallback** | 指定された i/o 操作のステータス情報を返します。 |
| **FltRetainSwappedBufferMdlAddress** | フィルターマネージャーが、ミニフィルタードライバーによってスワップされたバッファーのメモリ記述子リスト (MDL) を解放できないようにします。 |
| **FltRetrieveIoPriorityInfo** | スレッドから優先順位情報を取得します。 |
| **FltReuseCallbackData** | 再利用できるようにコールバックデータ構造を再初期化します。 |
| **FltRollbackComplete** | TRANSACTION_NOTIFY_ROLLBACK 通知を確認します。 |
| **FltRollbackEnlistment** | ミニフィルタードライバーに代わってトランザクションをロールバックまたは中止します。 |
| **FltSendMessage** | ミニフィルタードライバーまたはミニフィルタードライバーインスタンスの代わりに、待機中のユーザーモードアプリケーションにメッセージを送信します。 |
| **Fltsetactivityidのデータ** | フィルター処理のコールバックデータ内の IRP のアクティビティ ID を設定します。 |
| **FltSetCallbackDataDirty** | ミニフィルタードライバーの preoperation または postoperation コールバックルーチンは、コールバックデータ構造の内容が変更されたことを示すために**FltSetCallbackDataDirty**を呼び出します。 |
| **FltSetCancelCompletion** | 特定の i/o 操作が取り消された場合に呼び出されるキャンセルルーチンを指定します。 |
| **FltSetEaFile セット** | ファイルの拡張属性 (EA) の値を設定します。 |
| **FltSetEcpListIntoCallbackData** | 追加の create parameter context structure (ECP) リストを create operation callback-data オブジェクトにアタッチします。 |
| **FltSetFileContext** | ファイルのコンテキストを設定します。 |
| **FltSetInformationFile** | 指定されたファイルの情報を設定します。 |
| **FltSetInstanceContext** | ミニフィルタードライバーインスタンスのコンテキストを設定します。 |
| **FltSetIoPriorityHintIntoCallbackData** | コールバックデータの i/o 優先順位情報を設定します。 |
| **FltSetIoPriorityHintIntoFileObject** | ファイルオブジェクトの i/o 優先順位情報を設定します。 |
| **FltSetIoPriorityHintIntoThread** | スレッドの IO 優先度情報を設定します。 |
| **FltSetQuotaInformationFile** | ファイルオブジェクトのクォータエントリを変更します。 |
| **FltSetSecurityObject** | オブジェクトのセキュリティ状態を設定します。 |
| **FltSetStreamContext** | ファイルストリームのコンテキストを設定します。 |
| **FltSetStreamHandleContext** | ストリームハンドルのコンテキストを設定します。 |
| **FltSetTransactionContext** | トランザクションのコンテキストを設定します。 |
| **FltSetVolumeContext** | ボリュームのコンテキストを設定します。 |
| **FltSetVolumeInformation** | 指定したインスタンスがアタッチされているボリュームに関するさまざまな種類の情報を変更します。 |
| **FltStartFiltering** | 登録されているミニフィルタードライバーのフィルター処理を開始します。 |
| **FltSupportsFileContexts** | ファイルシステムが、指定されたファイルのファイルコンテキストをサポートするかどうかを判断します。 |
| **FltSupportsFileContextsEx** | ファイルシステムまたはフィルターマネージャーが、指定されたファイルのファイルコンテキストをサポートするかどうかを決定します。 |
| **FltSupportsStreamContexts** | 指定されたファイルオブジェクトでストリームコンテキストがサポートされているかどうかを判断します。 |
| **FltSupportsStreamHandleContexts** | 指定されたファイルオブジェクトでストリームハンドルコンテキストがサポートされているかどうかを判断します。 |
| **FltTagFile** | ファイルまたはディレクトリに再解析タグを設定します。 |
| **FltUninitializeFileLock** | FILE_LOCK 構造体を初期化前します。 |
| **FltUninitializeOplock** | 初期化前を便宜的ロック (oplock) ポインターにします。 |
| **FltUnloadFilter** | **Fltloadfilter**を呼び出してサポートミニフィルタードライバーを読み込んだミニフィルタードライバーは、 **Fltloadfilter**を呼び出してミニフィルタードライバーをアンロードできます。 |
| **FltUnregisterFilter** | 登録されているミニフィルタードライバーは、フィルターマネージャーが i/o 操作を処理するためにそれを呼び出すことができないように、 **Fltunregisterfilter**を呼び出して自身を登録解除します。 |
| **FltUntagFile** | ファイルまたはディレクトリから再解析ポイントを削除します。 |
| **FltWriteFile** | 開いているファイル、ストリーム、またはデバイスにデータを書き込みます。 |
| **FltWriteFileEx** | 開いているファイル、ストリーム、またはデバイスにデータを書き込みます。 この関数は、 **FltWriteFile**を拡張して、マップされたバッファーアドレスの代わりにデータを書き込むために MDL をオプションで使用できるようにします。 |
| **IS_ALIGNED** | 1番目の引数が、指定された2乗の境界に沿ってアラインされているかどうかを判断します。
