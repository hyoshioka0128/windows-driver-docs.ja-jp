---
title: Storport ドライバーのサポート ルーチン
description: Storport ミニポートドライバーのルーチンと、SCSI ポートドライバーと Storport ドライバーの設計の違いについて説明します。
ms.assetid: 15f20a83-43cc-40d4-8fa6-031affca5ee2
keywords:
- Storport ドライバーのサポート ルーチン
- ストレージ WDK
- ストレージサポートルーチン
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1e50cb088b585af1eb4ec1eb9f523388aeb6e26e
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252394"
---
# <a name="storport-driver-support-routines"></a>Storport ドライバーのサポート ルーチン

このページには、システムによって提供される Storport ドライバーによって提供されるサポートルーチンが一覧表示されます。

Storport ドライバーミニポートルーチンの一覧については、「 [Storport ミニポートドライバールーチン](storport-miniport-driver-routines.md)」を参照してください。

## <a name="direct-memory-access-support-routines"></a>ダイレクトメモリアクセスのサポートルーチン

Storport ドライバーは、次のダイレクトメモリアクセス (DMA) のサポートルーチンを提供します。

| ルーチン | 説明 |
| ------- | ----------- |
| **StorPortBuildScatterGatherList** | 指定されたデータバッファーのスキャッター/ギャザーリストを作成します。 |
| **StorPortGetScatterGatherList** | 指定された SCSI 要求ブロック (SRB) に関連付けられているスキャッター/ギャザーリストを取得します。 |
| **StorPortPutScatterGatherList** | **StorPortBuildScatterGatherList**ルーチンの呼び出しによって以前に作成された、スキャッター/ギャザーリストに関連付けられているすべてのリソースを解放します。 |

## <a name="general-support-routines"></a>一般的なサポートルーチン

Storport には、次の一般的なサポートルーチンが用意されています。

| ルーチン | 説明 |
| ------- | ----------- |
| **StorPortDebugPrint** | デバッガーがアタッチされている場合は、デバッグ文字列をカーネルデバッガーに出力します。 |
| **StorPortEtwEvent2** | ストレージトレースチャネルに Windows イベントトレーシング (ETW) イベントを発行します。 ミニポートでは、2つの汎用 ETW パラメーターをログに記録できます。 ETW パラメーターは、2つの名前と値のペアで表されます。 |
| **StorPortEtwEvent4** | ETW イベントをストレージトレースチャネルに発行します。 ミニポートでは、4つの汎用 ETW パラメーターをログに記録できます。 ETW パラメーターは、4つの名前と値のペアで表されます。 |
| **StorPortEtwEvent8** | ETW イベントをストレージトレースチャネルに発行します。 ミニポートでは、8つの汎用 ETW パラメーターをログに記録できます。 ETW パラメーターは、8つの名前と値のペアで表されます。 |
| **StorPortGetActivityIdSrb** | 要求ブロックに関連付けられている ETW アクティビティ ID を取得します。 |
| **StorPortGetDeviceObjects** | アダプターデバイススタックに関連付けられているデバイスオブジェクトを返します。 返されるデバイスオブジェクトは、アダプターの機能オブジェクトと物理デバイスオブジェクト、および機能デバイスオブジェクトがアタッチされているデバイスオブジェクトです。 |
| **StorPortGetSystemPortNumber** | ストレージアダプターのシステム割り当てポート番号を取得します。 |
| **StorPortInitializeSListHead** | Storport で管理される単一のリンクリストの先頭を初期化します。 |
| **StorPortInterlockedFlushSList** | Storport で管理された単一のリンクリストからすべての項目を削除します。 マルチプロセッサシステムでリストへのアクセスが同期されている |
| **StorPortInterlockedPopEntrySList** | Storport によって管理される単一のリンクリストの先頭から項目を削除します。 リストへのアクセスは、マルチプロセッサシステムで同期されています。  |
| **StorPortInterlockedPushEntrySList** | Storport で管理される単一のリンクリストの先頭に項目を挿入します。 リストへのアクセスは、マルチプロセッサシステムで同期されています。 |
| **StorPortInvokeAcpiMethod** | ストレージデバイスの ACPI メソッドを実行します。 |
| **StorPortIsCurrentOsInstallationUpgrade** | Windows の現在のインストールが以前のバージョンからのアップグレードであるかどうかを確認します。 |
| **StorPortIsDeviceOperationAllowed** | 特定のデバイス管理クラスに対する操作が許可されているかどうかをミニポートが判断できるようにします。 |
| **StorPortLogError** | エラーが発生したことをポートドライバーに通知します。 |
| **StorPortLogSystemEvent** | ミニポートドライバーが Windows カーネルイベント機能の機能に完全にアクセスできるようにします。これにより、ミニポートドライバーは、記憶域の問題のトラブルシューティングに非常に役立つイベントログエントリを作成できます。 **Storportlogerror**の代わりに、より優れた代替手段を提供します。 |
| **StorPortQueryDepthSList** | Storport で管理される単一のリンクリスト内のエントリの数を取得します。 |
| **StorPortQueryPerformanceCounter** | クエリを行って、現在のシステムパフォーマンスカウンター値を返します。 |
| **StorPortQuerySystemTime** | 現在のシステム時刻を取得します。 |
| **StorPortRegistryRead** | 指定されたデバイスと値のレジストリデータを読み取ります。 |
| **StorPortRegistryReadAdapterKey** | HKLM/CurrentControlSet/Enum/\<Instance path >/DeviceParameters/.... にある、レジストリにあるハードウェアまたはデバイスのレジストリアダプターキーを読み取ります。|
| **StorPortRegistryWriteAdapterKey** | HKLM/CurrentControlSet/Enum/\<Instance path >/DeviceParameters/.... のレジストリにあるハードウェアまたはデバイスのレジストリアダプターキーを書き込みます。 |
| **StorPortRegistryWrite** | 指定したバッファーに格納されているレジストリデータを ASCII から Unicode に変換し、そのデータをミニポートドライバーの HBA 別ストレージ領域に書き込みます。 |

## <a name="io-request-processing-support-routines"></a>I/o 要求処理のサポートルーチン

Storport には、次の i/o 要求処理サポートルーチンが用意されています。

| ルーチン | 説明 |
| ------- | ----------- |
| **StorPortBusy** | アダプターが現在ビジー状態であることをポートドライバーに通知し、未処理の要求を処理します。 |
| **StorPortCompleteRequest** | SRB status 値を SrbStatus に設定して、すべての未処理の要求を完了します。 |
| **StorPortCompleteServiceIrp** | HwStorProcessServiceRequest コールバックルーチンで受信した要求を完了する必要がある場合に、Storport 仮想ミニポートドライバーによって呼び出されます。 |
| **StorPortDeviceBusy** | 指定された論理ユニットが現在ビジー状態であることをポートドライバに通知し、未処理の要求を処理します。 |
| **StorPortDeviceReady** | 指定された論理ユニットが新しい要求を処理する準備ができていることをポートドライバーに通知します。 |
| **StorPortFreeWorker** | **Storportinitializeworker**ルーチンによって以前に割り当てられた Storport 作業項目を解放します。 |
| **StorPortGetRequestInfo** | SCSI 要求ブロック (SRB) に関連付けられている IO 要求情報を取得し、STOR_REQUEST_INFO 構造体で返します。 |
| **StorPortInitializeWorker** | システムワーカースレッドで実行される新しい Storport 作業項目を作成します。 |
| **StorPortQueueWorkItem** | システムワーカースレッドのコンテキスト内で実行されるように Storport 作業項目をスケジュールします。 |
| **StorPortPause** | 指定された期間、アダプターを一時停止します。 |
| **StorPortPauseDevice** | 指定された期間、特定の論理ユニットデバイスを一時停止します。 |
| **StorPortReady** | アダプターがビジー状態ではなくなったことをポートドライバーに通知します。 |
| **StorPortResume** | 一時停止しているアダプターを再開します。 |
| **StorPortResumeDevice** | 以前に一時停止した論理ユニットを再開します。 |

## <a name="initialization-support-routines"></a>初期化のサポートルーチン

Storport ドライバーには、次の初期化サポートルーチンが用意されています。

| ルーチン | 説明 |
| ------- | ----------- |
| **Storportenableveinitialization** | ミニポートの初期化中に、ミニポートの HwStorPassiveInitializeRoutine コールバックルーチンを PASSIVE_LEVEL で実行できるようにします。 |
| **StorPortGetActiveGroupCount** | システム内に存在するプロセッサグループの数を返します。 |
| **StorPortGetActiveNodeCount** | システム内に存在するノードの数を返します。 |
| **StorPortGetBusData** | HBA を初期化するために必要なバス固有の構成情報を取得します。 |
| **StorPortGetCurrentProcessorNumber** | カーネルから現在のプロセッサ番号を取得します。 |
| **StorPortGetGroupAffinity** | 要求されたグループ内のアクティブなプロセッサのマスクを構築します。 |
| **StorPortGetHighestNodeNumber** | システムで使用可能な最大ノード番号を返します。 |
| **StorPortGetLogicalProcessorRelationship** | 指定された1つ以上の型のリレーションシップ情報を返します。 これらの種類には、ホストシステム内のグループ、物理パッケージ、およびノードが含まれます。 返される情報には、ホストシステムの論理プロセッサで構成されるプロセッサ関係マスクが含まれます。 これらの論理プロセッサは、指定されたリレーションシップの種類を共有します。 |
| **StorPortGetLogicalUnit** | ミニポートドライバーの論理ユニットごとのストレージ領域へのポインターを返します。 |
| **StorPortGetNodeAffinity** | 要求された non-uniform memory access (NUMA) ノードにアクティブなプロセッサのマスクを構築します。 |
| **StorPortGetStartIoPerfParams** | 指定された i/o 要求のパフォーマンスパラメーターを STARTIO_PERFORMANCE_PARAMETERS 構造体に配置します。 |
| **StorPortInitialize** | ポートドライバーのパラメーターと拡張データを初期化します。 また、 **StorPortInitilize**は、ミニポートドライバーから提供されたアダプター情報も保存します。 |
| **StorPortInitializePerfOpts** | ミニポートドライバーと Storport ドライバーが PERF_CONFIGURATION_DATA 構造体を使用してサポートするパフォーマンスの最適化を初期化します。 |
| **StorPortSetAdapterBusType** | 現在の構成に応じてアダプターの BusType を調整するために使用します。 このルーチンを使用して BusType を設定すると、ドライバーを再インストールしなくても、ミニポート INF で設定されたグローバルプロパティを上書きすることができます。 これは、RAID のサポートや、バスの種類が異なる複数のアダプターのサポートなどのシナリオで役立ちます。 |
| **Storportsetbusa Offset** | バス固有の構成情報を書き込みます。 |
| **StorPortSetDeviceQueueDepth** | 指定されたデバイスのデバイスキューの最大深度を設定します。 |
| **StorPortSetPowerSettingNotificationGuids** | ミニポートで電源設定の通知を受信できるようにします。 ミニポートは、電源変更通知を受信するための電源設定を識別する Guid の配列を登録します。 |
| **StorPortSetUnitAttributes** | ストレージユニットデバイスの電源属性を Storport ドライバーに登録します。 |

## <a name="interrupt-support-routines"></a>割り込みサポートルーチン

Storport ドライバーには、次の割り込みサポートルーチンが用意されています。

| ルーチン | 説明 |
| ------- | ----------- |
| **StorPortGetMSIInfo** | 指定したメッセージのメッセージシグナル割り込み (MSI) 情報を取得します。 |
| **StorPortSynchronizeAccess** | ミニポートドライバーのデバイス拡張機能への同期アクセスを提供します。 |
| **Storport初期化 Edpc** | StorPort 遅延プロシージャ呼び出し (DPC) を初期化します。 |
| **StorPortIssueDpc** | Storport DPC を発行します。 |
| **StorPortStallExecution** | ミニポートドライバーを停止します。 |

## <a name="locking-support-routines"></a>ロックのサポートルーチン

Storport ドライバーには、次のロックサポートルーチンが用意されています。

| ルーチン | 説明 |
| ------- | ----------- |
| **StorPortAcquireMSISpinLock** | 指定したメッセージに関連付けられているメッセージシグナル割り込み (MSI) スピンロックを取得します。 |
| **StorPortAcquireSpinLock** | 指定したスピンロックを取得します。 |
| **StorPortReleaseMSISpinLock** | 指定したメッセージに対して以前に取得した MSI スピンロックを解放します。 |
| **StorPortReleaseSpinLock ロック** | **StorPortAcquireSpinLock**によって取得されたスピンロックを解放します。 |

## <a name="memory-management-support-routines"></a>メモリ管理のサポートルーチン

Storport ドライバーでは、次のようなメモリ管理ルーチンがサポートされています。

| ルーチン | 説明 |
| ------- | ----------- |
| **StorPortAllocateContiguousMemorySpecifyCacheNode** | 物理的に連続する、非ページメモリの範囲を割り当てます。 |
| **StorPortAllocateMdl** | 指定された非ページプールメモリを記述する MDL を割り当てます。 |
| **StorPortAllocatePool** | 連続していない非ページプールメモリのブロックを割り当てます。 |
| **StorPortAllocateRegistryBuffer** | ミニポートがレジストリデータの読み取りと書き込みに使用できるバッファーを割り当てます。 |
| **StorPortBuildMdlForNonPagedPool** | 関連する非ページメモリを記述するように MDL を更新します。 |
| **StorPortConvertUlongToPhysicalAddress** | 符号なし long アドレスを物理アドレスに変換します。 |
| **StorPortConvertPhysicalAddressToULong64** | 物理アドレスを ULONG64 値に変換します。 |
| **StorPortFreeMdl** | 非ページプールメモリを記述するメモリ記述子リスト (MDL) を解放します。 |
| **StorPortFreeContiguousMemorySpecifyCache** | システムアドレス空間のページングされていない部分にある、非キャッシュメモリの範囲の割り当てを解除します。 |
| **StorPortFreePool** | **StorPortAllocatePool**ルーチンの呼び出しによって以前に割り当てられたメモリブロックを解放します。 |
| **StorPortFreeRegistryBuffer** | レジストリデータを格納するために割り当てられたバッファーを解放します。 |
| **StorPortGetDataInBufferMdl** | SCSI 要求ブロック (SRB) の入力データバッファーに関連付けられている MDL を返します。 |
| **StorPortGetDataInBufferScatterGatherList** | SCSI 要求ブロック (SRB) の入力データバッファーに関連付けられているスキャッター/ギャザーリストを返します。 |
| **StorPortGetDataInBufferSystemAddress** | SCSI 要求ブロック (SRB) の入力データバッファーのシステムアドレスを返します。 |
| **StorPortGetOriginalMdl** | 指定された SRB に関連付けられている MDL を返します。 |
| **StorPortGetVirtualAddress** | 指定された物理アドレスにマップされる仮想アドレスを取得します。 |
| **StorPortGetPhysicalAddress** | 指定された仮想アドレス範囲を DMA 操作の物理アドレス範囲に変換します。 |
| **StorPortGetSystemAddress** | 指定された SCSI 要求ブロック (SRB) のデータバッファーのシステム領域内の仮想アドレスを返します。 |
| **Storportget出 Achedexテンション** | CPU およびデバイスによって共有される、キャッシュされていない共通バッファーを割り当てます。 |
| **StorPortMarkDumpMemory** | ミニポートは、ダンプファイルまたは休止状態ファイルに使用されているメモリをマークする必要があります。 マークされたメモリは保持され、休止状態からの再開操作の後も有効なままです。 マークするメモリは、 **Storportmarkdumpmemory**への呼び出しでアドレスと範囲の長さによって指定されます。 |
| **StorPortMoveMemory** | バッファー間でメモリをコピーします。 |

## <a name="notification-support-routines"></a>通知サポートルーチン

Storport ドライバーには、次の通知サポートルーチンが用意されています。

| ルーチン | 説明 |
| ------- | ----------- |
| **StorPortAsyncNotificationDetected** | 記憶装置の状態変更イベントを Storport ドライバーに通知します。 |
| **StorPortNotification** | 特定のイベントおよび条件を Storport ドライバーに通知します。 |
| **StorPortStateChangeDetected** | 論理ユニット番号 (LUN)、ホストバスアダプター (HBA) ポート、またはターゲットデバイスの状態変更を Storport ポートドライバーに通知します。 |

## <a name="port-and-register-io-support-routines"></a>ポートおよび登録 i/o サポートルーチン

Storport ドライバーは、次のポートを提供し、i/o サポートルーチンを登録します。

| ルーチン | 説明 |
| ------- | ----------- |
| **StorPortGetDeviceBase** | I/o アドレスをシステムアドレス空間にマップします。 |
| **StorPortFreeDeviceBase** | StorPortGetDeviceBase によってマップされたデバイスの i/o メモリの範囲を解放します。 |
| **StorPortReadPortBufferUchar** | 指定されたポートアドレスから値を読み取ります。 |
| **StorPortReadPortBufferUlong** | 指定されたポートアドレスから値を読み取ります。 |
| **StorPortReadPortBufferUshort** | 指定されたポートアドレスから値を読み取ります。 |
| **StorPortReadPortUchar** | 指定されたポートアドレスから値を読み取ります。 |
| **StorPortReadPortUlong** | 指定されたポートアドレスから値を読み取ります。 |
| **StorPortReadPortUshort** | 指定されたポートアドレスから値を読み取ります。 |
| **StorPortReadRegisterBufferUchar** | 指定したレジスタアドレスから値を読み取ります。 |
| **StorPortReadRegisterBufferUlong** | 指定したレジスタアドレスから値を読み取ります。 |
| **StorPortReadRegisterBufferUlong64** | 指定した64ビットレジスタアドレスから ULONG64 値の数をバッファーに読み取ります。 |
| **StorPortReadRegisterBufferUshort** | 指定したレジスタアドレスから値を読み取ります。 |
| **StorPortReadRegisterUchar** | 指定したレジスタアドレスから値を読み取ります。 |
| **StorPortReadRegisterUlong** | 指定したレジスタアドレスから値を読み取ります。 |
| **StorPortReadRegisterUlong64** | 指定した64ビットレジスタアドレスから64ビット値を読み取ります。 |
| **StorPortReadRegisterUshort** | 指定したレジスタアドレスから値を読み取ります。 |
| **StorPortValidateRange** | I/o アドレスの指定した範囲が別のアダプターによって使用されているかどうかを判断します。 このルーチンは、Windows NT 4.0 以降のオペレーティングシステムでは廃止されています。 |
| **StorPortWritePortBufferUchar** | 指定したレジスタアドレスに値を書き込みます。 |
| **StorPortWritePortBufferUlong** | 指定したレジスタアドレスに値を書き込みます。 |
| **StorPortWritePortBufferUshort** | 指定したレジスタアドレスに値を書き込みます。 |
| **StorPortWritePortUchar** | 指定したレジスタアドレスに値を書き込みます。 |
| **StorPortWritePortUlong** | 指定したレジスタアドレスに値を書き込みます。 |
| **StorPortWritePortUshort** | 指定したレジスタアドレスに値を書き込みます。 |
| **StorPortWriteRegisterBufferUchar** | バッファーから指定された数の符号なしバイトを HBA に転送します。 |
| **StorPortWriteRegisterBufferUlong** | 指定された数の ULONG 値をバッファーから HBA に転送します。 |
| **StorPortWriteRegisterBufferUlong64** | 指定した64ビットレジスタアドレスから、いくつかの ULONG64 値を書き込みます。 |
| **StorPortWriteRegisterBufferUshort** | 指定された数の USHORT 値をバッファーから HBA に転送します。 |
| **StorPortWriteRegisterUchar** | バッファーから指定された数の文字値を、指定した HBA レジスタアドレスに転送します。 |
| **StorPortWriteRegisterUlong** | 指定された HBA レジスタアドレスに ULONG 値を転送します。 |
| **StorPortWriteRegisterUlong64** | 指定されたレジスタアドレスに ULONG64 値を書き込みます。 |
| **StorPortWriteRegisterUshort** | 指定された HBA レジスタアドレスに ULONG 値を転送します。|

## <a name="runtime-power-management-support-routines"></a>ランタイム電源管理サポートルーチン

Storport ドライバーには、次のランタイム電源管理サポートルーチンが用意されています。

| ルーチン | 説明 |
| ------- | ----------- |
| **StorPortInitializePoFxPower** | ストレージデバイスを電源管理フレームワーク (PoFx) に登録します。 |
| **StorPortPoFxActivateComponent** | ストレージデバイスの指定したコンポーネントのアクティブ化参照カウントをインクリメントします。 |
| **StorPortPoFxIdleComponent** | ストレージデバイスの指定したコンポーネントのアクティブ化参照カウントをデクリメントします。 |
| **StorPortPoFxPowerControl** | パワーエンジンプラグイン (PEP) に転送するために、電源管理フレームワーク (PoFx) に電源管理要求を送信します。 |
| **StorPortPoFxSetComponentLatency** | 指定した記憶装置コンポーネントのアイドル状態からアクティブ条件への移行で許容される最大待機時間を指定します。 |
| **StorPortPoFxSetComponentResidency** | コンポーネントがアイドル状態になった後に記憶装置コンポーネントがアイドル状態を維持する可能性のある推定時間を設定します。 |

## <a name="timer-support-routines"></a>タイマーサポートルーチン

Storport ドライバーには、次のタイマーサポートルーチンが用意されています。

| ルーチン | 説明 |
| ------- | ----------- |
| **StorPortFreeTimer** | **Storportinitializetimer**ルーチンによって以前に作成された Storport タイマーコンテキストオブジェクトを解放します。 |
| **StorPortInitializeTimer** | Storport タイマーコンテキストオブジェクトを作成します。 |
| **StorPortRequestTimer** | Storport タイマーコンテキストオブジェクトのコールバックイベントをスケジュールします。 |
