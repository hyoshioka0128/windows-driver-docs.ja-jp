---
title: Surface Team ドライバー開発ベスト プラクティス
description: Surface Team ドライバー開発のベストプラクティス-ドライバー開発者が回避する一般的な間違い。
ms.assetid: f4847954-8e29-48bb-b9ae-873fc7c29b2d
keywords:
- ドライバー開発のベストプラクティス
ms.date: 08/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: 31961b6f47067d7c5702d65de5b6212821677e54
ms.sourcegitcommit: 46853426563bfac36651565181d7edac339f63af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74261432"
---
# <a name="surface-team-driver-development-best-practices"></a>Surface Team ドライバー開発ベスト プラクティス

## <a name="introduction"></a>概要

これらのドライバー開発ガイドラインは、Microsoft のドライバー開発者によって長年にわたって開発されました。 ドライバーの適切とレッスンが学習された時間の経過と共に、これらのレッスンはこの一連のガイダンスとして取り込まれ、進化しました。 これらのベストプラクティスは、独自の Surface ハードウェアエクスペリエンスをサポートするデバイスドライバーコードを開発および管理するために、Microsoft Surface ハードウェアチームによって使用されます。

一連のガイドラインと同様に、正当な例外と、同じように有効な別の方法があります。 これらのガイドラインを開発標準に組み込むか、開発環境と独自の要件に合わせてドメイン固有のガイドラインを開始することを検討してください。 

## <a name="common-mistakes-made-by-driver-developers"></a>ドライバー開発者によって行われる一般的な間違い

### <a name="handling-io"></a>I/o の処理

1. 長さを検証せずに、Ioctl から取得されたバッファーにアクセスしています。 「[バッファーのサイズを確認できませんでした](https://docs.microsoft.com/windows-hardware/drivers/kernel/failure-to-check-the-size-of-buffers)。」を参照してください。
2. ユーザースレッドまたはランダムスレッドコンテキストのコンテキストでブロッキング i/o を実行します。 「[カーネルディスパッチャーオブジェクトの概要」を](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-kernel-dispatcher-objects)参照してください。
3. 同期 i/o を別のドライバーに送信すると、タイムアウトはありません。 「 [I/o 要求を同期的に送信](https://docs.microsoft.com/windows-hardware/drivers/wdf/sending-i-o-requests-synchronously)する」を参照してください。
4. セキュリティへの影響を理解せずに、io Ioctl を使用しません。 「[バッファーと直接 i/o の両方を使用する」を](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-neither-buffered-nor-direct-i-o)参照してください。
5. [Wdfrequestforwardtoioqueue](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)の戻り値の状態を確認していないか、エラーを正しく処理しなかったため、WDFREQUESTs が破棄されました。
6. キャンセル不可能な状態で、WDFREQUEST をキューの外部に保持します。 I/o[キューの管理](https://docs.microsoft.com/windows-hardware/drivers/wdf/managing-i-o-queues)、 [I/o 要求の完了](https://docs.microsoft.com/windows-hardware/drivers/wdf/completing-i-o-requests)、および[i/o 要求のキャンセル](https://docs.microsoft.com/windows-hardware/drivers/wdf/canceling-i-o-requests)に関する記事をご覧ください。
7. IoQueues を使用する代わりに、Mark/UnmarkCancelable を使用してキャンセルを管理しようとしています。 「[フレームワークキューオブジェクト](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-queue-objects)」を参照してください。
8. ファイルハンドルのクリーンアップ操作と終了操作の違いを知ることはできません。 「[クリーンアップおよび終了操作の処理中のエラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-handling-cleanup-and-close-operations)」を参照してください。
9. 見落としの可能性を再帰、i/o の完了と完了ルーチンからの再送信を行います。
10. WDFQUEUEs の電源管理属性については、明示的ではありません。 電源管理の選択を明確に文書化することはできません。 これは、WDF ドライバーでのバグチェック0x9F の主な原因です[。ドライバー\_電源\_状態\_エラー](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x9f--driver-power-state-failure)です。 デバイスが削除されると、フレームワークは、削除プロセスのさまざまな段階で、電源管理キューと非電源管理キューから IO を削除します。 非電力管理キューは、最後の IRP\_が\_削除\_デバイスを受信したときに消去されます。 そのため、非電力管理キューで i/o を保持している場合は、デッドロックを避けるために、 [EvtDeviceSelfManagedIoFlush](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)のコンテキストで i/o を明示的に消去することをお勧めします。
11. Irp を処理する規則に従っていません。 「[クリーンアップおよび終了操作の処理中のエラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-handling-cleanup-and-close-operations)」を参照してください。

### <a name="synchronization"></a>同期

1. 保護を必要としないコードに対してロックを保持します。 一部の操作だけを保護する必要がある場合は、関数全体のロックを保持しないでください。
2. ロックが保持されているドライバーを呼び出します。 これは、デッドロックの主な原因です。
3. インタロックされたプリミティブを使用して、ミューテックス、セマフォ、スピンロックなどの適切なシステム指定のロックを使用する代わりに、ロックスキームを作成します。 「 [Mutex オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-mutex-objects)」、「[セマフォオブジェクト](https://docs.microsoft.com/windows-hardware/drivers/kernel/semaphore-objects)」、および「[スピンロックの概要](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-spin-locks)」を参照してください。
4. ロックダウンを使用して、何らかの種類のパッシブロックが適切になるようにします。 「[高速ミューテックスと保護](https://docs.microsoft.com/windows-hardware/drivers/kernel/fast-mutexes-and-guarded-mutexes)されたミューテックスおよび[イベントオブジェクト](https://docs.microsoft.com/windows-hardware/drivers/kernel/event-objects)」を参照してください。 ロックに関するその他のパースペクティブについては、OSR の記事「[同期の状態](https://www.osr.com/nt-insider/2015-issue3/the-state-of-synchronization/)」を確認してください。
5. 影響について完全に理解していない状態で、WDF の同期と実行レベルのモデルにオプトインします。 「 [Framework のロックの使用」を](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-framework-locks)参照してください。 ドライバーがハードウェアと直接通信するモノリシックトップレベルドライバーでない限り、再帰に起因するデッドロックが発生する可能性があるため、WDF 同期を無効にしないでください。
6. 重大な領域を入力せずに、複数のスレッドのコンテキストで KEVENT、セマフォ、、UnsafeFastMutex を取得しています。 この操作を行うと、これらのロックを保持しているスレッドが中断される可能性があるため、DOS 攻撃につながる可能性があります。 「[同期の手法](https://docs.microsoft.com/windows-hardware/drivers/kernel/synchronization-techniques)」を参照してください。
7. イベントがまだ使用されている間に、スレッドスタックで KEVENT を割り当てて呼び出し元に戻す。 通常は、 [IoBuildSyncronousFsdRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)または[IoBuildDeviceIoControlRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)と共に使用します。 これらの呼び出しの呼び出し元は、IRP が完了したときに i/o マネージャーがイベントを通知するまで、スタックからアンワインドされないようにする必要があります。
8. ディスパッチルーチンで無期限に待機しています。 一般に、ディスパッチルーチンのあらゆる種類の待機は、悪い方法です。
9. オブジェクトを削除する前に、オブジェクトの有効性を不適切に確認しています (blah = = NULL の場合)。 これは、通常、作成者が、オブジェクトの有効期間を制御するコードを完全に理解していないことを意味します。

### <a name="object-management"></a>オブジェクト管理

1. WDF オブジェクトを明示的に親にできません。 「[フレームワークオブジェクトの概要」を](https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects)参照してください。
2. 有効期間の管理を向上させ、メモリ使用量を最適化するオブジェクトとの親子関係ではなく、WDF オブジェクトを WDFDRIVER にします。
たとえば、IOTARGET ではなく WDFREQUEST に親の WDFREQUEST を使用します。 「[一般的なフレームワークオブジェクトの使用](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-general-framework-objects)」、「フレームワーク[オブジェクトのライフサイクル](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-life-cycle)」、および「[フレームワークオブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/wdf/summary-of-framework-objects)」を参照してください。
3. ドライバー間でアクセスされる共有メモリリソースのランダウン防止を実行していません。 「 [Exinitializer Erundownprotection 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializerundownprotection)」を参照してください。
4. 前の作業項目が既にキューに存在するか、既に実行中であるときに、同じ作業項目を誤ってキューに登録します。 これは、キューに入れられたすべての作業項目が実行されることをクライアントが想定する場合に、問題になる可能性があります。 「 [Framework workitem の使用」を](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-framework-work-items)参照してください。 作業項目のキューの詳細については、「ドライバーモジュールフレームワーク (DMF) プロジェクト <https://github.com/Microsoft/DMF>」の「 [dmf\_QueuedWorkitem](https://github.com/Microsoft/DMF/blob/master/Dmf/Modules.Library/Dmf_QueuedWorkItem.md)モジュール」を参照してください。
5. タイマーが処理することが予想されるメッセージを送信する前にタイマーをキューに置いています。 「[タイマーの使用」を](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-timers)参照してください。
6. 作業項目で操作を実行します。この操作は、完了までに時間がかかるか、無期限に実行されます。
7. 大量の作業項目がキューに格納されるようなソリューションを設計する。 悪意のある人がアクションを制御できる場合 (たとえば、i/o ごとに新しい作業項目をキューに追加するドライバーに i/o をポンプする場合)、システムまたは DOS 攻撃が応答しなくなる可能性があります。 「 [Framework 作業項目の使用」を](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-framework-work-items)参照してください。
8. オブジェクトを削除する前に、作業項目の DPC コールバックが完了するまで実行されているとは限りません。 「 [DPC ルーチン](https://docs.microsoft.com/windows-hardware/drivers/kernel/guidelines-for-writing-dpc-routines)と[WdfDpcCancel 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nf-wdfdpc-wdfdpccancel)の記述に関するガイドライン」を参照してください。
9. 短時間でも非ポーリングタスクでも作業項目を使用するのではなく、スレッドを作成します。 「[システムワーカースレッド](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-worker-threads)」を参照してください。
10. ドライバーを削除またはアンロードする前に、スレッドが完了まで実行されていることを確認してください。 スレッドランダウン同期の詳細については、ドライバーモジュールフレームワーク (DMF) プロジェクト https://github.com/Microsoft/DMFの[DMF_Thread](https://github.com/Microsoft/DMF/blob/master/Dmf/Modules.Library/Dmf_Thread.md)モジュールに関連付けられているコードを参照してください。 
11. 1つのドライバーを使用して、異なるが相互に依存し、グローバル変数を使用して情報を共有するデバイスを管理します。

### <a name="memory"></a>メモリ

1. 可能であれば、受動実行コードをページング可能なものとしてマークしないでください。 ドライバーコードのページングにより、ドライバーのコードフットプリントのサイズを小さくすることができるため、他の用途のためにシステム領域が解放されます。 IRQL \>= ディスパッチ\_レベルを発生させるか、または発生した IRQL で呼び出すことができるコードは、慎重にマークしてください。 [コードとデータをページング可能に](https://docs.microsoft.com/windows-hardware/drivers/kernel/when-should-code-and-data-be-pageable-)し、[ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/making-drivers-pageable)をページング可能にして、[ページングできるコードを検出](https://docs.microsoft.com/windows-hardware/drivers/kernel/detecting-code-that-can-be-pageable)するタイミングについては、「」を参照してください。
2. スタックで大きな構造体を宣言する場合は、代わりにヒープ/poolinstead 使用する必要があります。 「[カーネルスタックの使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-the-kernel-stack)」および「[システム領域メモリの割り当て](https://docs.microsoft.com/windows-hardware/drivers/kernel/allocating-system-space-memory)」を参照してください。
3. WDF オブジェクトコンテキストを不必要にゼロにする。 これは、メモリが自動的にゼロになるタイミングを明確に把握できないことを示している可能性があります。

### <a name="general-driver-guidelines"></a>一般的なドライバーのガイドライン

1. WDM と WDF プリミティブの混合。 WDF プリミティブを使用できる WDM プリミティブを使用します。 WDF プリミティブを使用すると、そのようなことを防ぎ、デバッグ機能が向上し、さらに重要なことにより、ドライバーをユーザーモードに移植できるようになります。
2. 必要でない場合は、FDOs に名前を付け、シンボリックリンクを作成します。 「[ドライバーアクセス制御の管理](https://docs.microsoft.com/windows-hardware/drivers/driversecurity/driver-security-checklist#manage-driver-access-control)」を参照してください。
3. サンプルドライバーから、Guid とその他の定数値をコピーして使用します。
4. ドライバープロジェクトで、ドライバーモジュールフレームワーク (DMF) オープンソースコードを使用することを検討してください。 DMF は、WDF ドライバー開発者に追加機能を有効にする WDF の拡張機能です。 「[ドライバーモジュールフレームワークの概要](https://blogs.windows.com/windowsdeveloper/2018/08/15/introducing-driver-module-framework/)」を参照してください。
5. レジストリをプロセス間通知メカニズムとして使用するか、メールボックスとして使用します。 別の方法については、dmf プロジェクト <https://github.com/Microsoft/DMF>で使用できる[dmf\_NotifyUserWithEvent](https://github.com/Microsoft/DMF/blob/master/Dmf/Modules.Library/Dmf_NotifyUserWithEvent.md)および[Dmf\_Notifyuserwithevent](https://github.com/Microsoft/DMF/blob/master/Dmf/Modules.Library/Dmf_NotifyUserWithRequest.md)モジュールを参照してください。
6. システムの初期ブートフェーズ中に、レジストリのすべての部分がアクセスできることを前提としています。
7. 別のドライバーまたはサービスの読み込み順序に依存しています。 読み込み順序はドライバーの制御外で変更される可能性があるため、これによって最初に動作するドライバーが生成されますが、それ以降は予測できないパターンで失敗します。
8. WDF など、既に使用可能なドライバーライブラリを再作成する場合は、「ドライバー[での pnp と電源管理のサポート](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-pnp-and-power-management-in-your-driver)」で説明されている pnp や、「[ドライバーのバスインターフェイスを使用した OSR」の記事で説明されているように、バスインターフェイスで提供される pnp を提供します。ドライバー通信](https://www.osr.com/nt-insider/2014-issue2/using-bus-interfaces-driver-driver-communication/)。

### <a name="pnppower"></a>PnP/電源

1. Pnp デバイスの変更通知を登録していない、別のドライバーとの非 pnp のフレンドリな方法でのやり取り。 「[デバイスインターフェイスの変更通知の登録」を](https://docs.microsoft.com/windows-hardware/drivers/kernel/registering-for-device-interface-change-notification)参照してください。
2. デバイスを列挙し、それらの間に電源の依存関係を作成するための ACPI ノードの作成。バスドライバーまたはシステムによって提供されるソフトウェアデバイス作成インターフェイスを使用して、スマートな方法で PNP と電源の依存関係を作成します。 「[関数ドライバーでの PnP と電源管理のサポート](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-pnp-and-power-management-in-function-drivers)」を参照してください。
3. デバイスを非 disableable することをマークする-ドライバーの更新時に強制的に再起動します。
4. デバイスマネージャーでデバイスを非表示にする。 「[デバイスマネージャーからのデバイスの非表示」を](https://docs.microsoft.com/windows-hardware/drivers/kernel/hiding-devices-from-device-manager)参照してください。
5. このドライバーは、デバイスの1つのインスタンスに対してのみ使用されることを前提としています。
6. ドライバーがアンロードされないことを前提としています。 「 [PnP ドライバーのアンロードルーチン](https://docs.microsoft.com/windows-hardware/drivers/kernel/pnp-driver-s-unload-routine)」を参照してください。
7. 擬似インターフェイスの到着通知を処理していません。 このような状況が発生する可能性があり、ドライバーはこの状態を安全に処理することが期待されます。
8. S0 アイドル電源ポリシーを実装していません。これは、DRIPS の制約または子であるデバイスにとって重要です。 「[アイドル状態の電源ダウンをサポート](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-idle-power-down)する」を参照してください。
9. Wdfdevicestopidle の戻り値を確認しないと、WdfDeviceStopIdle/ResumeIdle 不均衡が発生し、最終的にバグチェックが9F されるため、電源参照のリークにつながります。 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)
10. リソースの再調整によって、ハードウェア/ReleaseHardware を複数回呼び出すことができることは不明です。 これらのコールバックは、ハードウェアリソースの初期化に制限する必要があります。 「 [.Evt\_WDF\_デバイス\_\_ハードウェアを準備](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)する」を参照してください。
11. ソフトウェアリソースの割り当てには、ハードウェア/ReleaseHardware を使用します。 デバイスに対する静的ソフトウェアリソース割り当ては、AddDevice または SelfManagedIoInit で、ハードウェアとの対話が必要なリソースの割り当てを行う場合に実行する必要があります。 「 [.Evt\_WDF\_デバイス\_SELF\_マネージ\_IO\_INIT](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)」を参照してください。

### <a name="coding-guidelines"></a>コーディングのガイドライン

1. 安全な文字列関数と整数関数を使用しません。 「[安全な文字列関数の使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-safe-string-functions)」および「[安全な整数関数](https://docs.microsoft.com/windows-hardware/drivers/kernel/ntintsafe-design-guide)の使用」を参照してください。
2. 定数の定義に typedef を使用しません。
3. Globals および static 変数を使用します。 グローバルにデバイスコンテキストを格納しないようにします。 グローバルは、デバイスの複数のインスタンス間で情報を共有することを目的としています。 別の方法として、WDFDRIVER オブジェクトコンテキストを使用して、デバイスの複数のインスタンス間で情報を共有することを検討してください。
4. 変数にわかりやすい名前を使用していません。
5. 名前付け変数の一貫性が保たれていません。 既存のコードを更新する場合、既存のコーディングのスタイルに従うことはできません。 たとえば、異なる関数の共通構造体に異なる変数名を使用しているとします。
6. 重要なデザインの選択にコメントを作成しない: 電源管理、ロック、状態管理、作業項目の使用、Dpc、タイマー、グローバルリソースの使用状況、リソースの事前割り当て、複雑な式、条件ステートメント。
7. 呼び出されている API の名前から明らかな内容についてコメントします。 コメントには、関数名と同じ英語の言語を使用します (「WdfDeviceCreate を呼び出すときに "デバイスオブジェクトの作成" というコメントを記述するなど)。
8. 戻り呼び出しを含むマクロは作成しないでください。 「 [Functions (C++)](https://docs.microsoft.com/cpp/cpp/functions-cpp)」を参照してください。
9. ソースコードの注釈がないか、不完全です (SAL)。 「 [Windows ドライバーの SAL 2.0 注釈」を](https://msdn.microsoft.com/windows/hardware/drivers/devtest/sal-2-annotations-for-windows-drivers)参照してください。
10. インライン関数の代わりにマクロを使用します。
11. を使用するときに、 [constexpr](https://docs.microsoft.com/cpp/cpp/constexpr-cpp?view=vs-2019)の代わりに定数にマクロを使用するC++
12. 厳密な型チェックを確実に取得するためにC++ 、コンパイラではなく C コンパイラを使用してドライバーをコンパイルします。

### <a name="error-handling"></a>エラー処理

1. 重大なドライバーエラーを報告せず、デバイスが機能していないことを適切にマークします。
2. 意味のある WIN32 エラー状態に変換する適切な NT エラー状態を返しません。 「 [NTSTATUS 値の使用」を](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-ntstatus-values)参照してください。
3. NTSTATUS マクロを使用して、システム関数の返された状態を確認することはできません。
4. 必要に応じて、状態変数またはフラグをアサートしません。
5. 競合状態を回避するためにポインターが有効かどうかを確認しています。
6. NULL ポインターに対してアサートします。 メモリにアクセスするために NULL ポインターを使用しようとすると、バグチェックが行われます。 バグチェックのパラメーターは、null ポインターを修正するために必要な情報を提供します。 [超過] を使用すると、コードに不要な ASSERT ステートメントが多数追加されると、メモリが消費され、システムが遅くなります。
7. オブジェクトコンテキストポインターでアサートします。 ドライバーフレームワークは、オブジェクトが常にコンテキストで割り当てられることを保証します。

### <a name="tracing"></a>トレース

1. WPP カスタム型を定義し、それをトレース呼び出しで使用して人間が判読できるトレースメッセージを取得することはできません。 「 [Windows ドライバーへの WPP ソフトウェアトレースの追加」を](https://docs.microsoft.com/windows-hardware/drivers/devtest/adding-wpp-software-tracing-to-a-windows-driver)参照してください。
2. IFR トレースを使用していません。 「 [KMDF および UMDF 2 ドライバーでの Inflight トレースレコーダー (IFR) の使用」を](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-wpp-software-tracing-in-kmdf-and-umdf-2-drivers)参照してください。
3. WPP トレース呼び出しで関数名を呼び出しています。 WPP は、既に関数名と行番号を追跡しています。
4. ETW イベントを使用して、パフォーマンスやその他の重要なユーザーエクスペリエンスに影響を与えることはありません。 「[カーネルモードドライバーへのイベントトレースの追加」を](https://docs.microsoft.com/windows-hardware/drivers/devtest/adding-event-tracing-to-kernel-mode-drivers)参照してください。
5. イベントログに重大なエラーが報告されず、デバイスが機能していないと適切にマークされません。

### <a name="verification"></a>検証

1. 開発およびテスト中に、標準設定と詳細設定の両方でドライバー検証ツールを実行していない。 「 [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)」を参照してください。 [詳細設定] では、リソースの低シミュレーションに関連するルールを除き、すべてのルールを有効にすることをお勧めします。 問題のデバッグを容易にするために、低リソースのシミュレーションテストを分離して実行することをお勧めします。
2. ドライバーまたはデバイスクラスで DevFund テストが実行されていません。ドライバーは、高度な検証機能の設定が有効になっているの一部です。 「[コマンドラインを使用して DevFund テストを実行する方法」を](https://docs.microsoft.com/windows-hardware/drivers/devtest/run-devfund-tests-via-the-command-line)参照してください。
3. ドライバーが HVCI に準拠しているかどうかを確認していません。 「 [HVCI ドライバーの互換性を評価](https://docs.microsoft.com/windows-hardware/drivers/driversecurity/use-device-guard-readiness-tool)する」を参照してください。
4. ユーザーモードドライバーの開発およびテスト中に、WUDFhost .exe で AppVerifier を実行しないでください。 「[アプリケーション検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/application-verifier)」を参照してください。
5. WDF オブジェクトが破棄されないように\!、実行時に[wdfpoolusage](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfpoolusage)デバッガー拡張機能を使用してメモリの使用状況をチェックしません。 メモリ、要求、作業項目は、これらの問題の一般的な被害を受けます。
6. [\!wdfkd](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)デバッガー拡張機能を使用してオブジェクトツリーを検査し、オブジェクトの親が正しく設定されていることを確認し、WDFKD、WDFKD、IO などの主要なオブジェクトの属性を確認することはできません。
