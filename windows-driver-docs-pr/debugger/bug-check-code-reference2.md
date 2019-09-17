---
title: バグ チェック コード リファレンス
description: ここでは、ブルースクリーンに渡されるパラメーターなど、一般的なバグチェックについて説明します。
ms.assetid: DBA85578-97CF-4BD7-A67D-1C7AD2E9B2BB
ms.date: 02/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: b284c0beb6e4d7a60c59feed071e50f98c54e7ac
ms.sourcegitcommit: f91a0fd22f46be44839d2a22a21f59fad900ce90
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71020991"
---
# <a name="bug-check-code-reference"></a>バグ チェック コード リファレンス

ここでは、青のバグチェック画面にエラーコードと共に表示されるパラメーターなど、一般的なバグチェックコードについて説明します。 このセクションでは、バグチェックにつながるエラーを診断する方法と、エラーに対処するための方法についても説明します。

> [!NOTE] 
> このトピックはプログラマーを対象としています。 システムにバグチェックコードを含むブルースクリーンが表示されているお客様の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://go.microsoft.com/fwlink/p/?linkid=183646)」を参照してください。

この参照に特定のバグチェックコードが表示されない場合は、次の構文 (カーネルモードの場合) を使用して、Windows デバッガー (WinDbg) で`<code>` [ **! analyze**](-analyze.md)拡張機能を使用し、をバグチェックコードに置き換えます。

`!analyze -show <code>`

このコマンドを入力すると、WinDbg は、指定されたバグチェックコードに関する情報を表示します。 既定の number base (基数) が16でない場合は`<code>` 、 **0x**でプレフィックスを付けます。

次の表は、各バグチェックコードのコードと名前を示しています。

| コード       | 名前                                                                                                                                              |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| 0x00000001 | [**APC\_インデックス\_の不一致**](bug-check-0x1--apc-index-mismatch.md)                                                                                  |
| 0x00000002 | [**デバイス\_\_キュー\_がビジー状態です**](bug-check-0x2--device-queue-not-busy.md)                                                                           |
| 0x00000003 | [**無効\_な\_アフィニティセット**](bug-check-0x3--invalid-affinity-set.md)                                                                              |
| 0x00000004 | [**無効\_な\_データアクセス\_トラップ**](bug-check-0x4--invalid-data-access-trap.md)                                                                     |
| 0x00000005 | [**プロセス\_の\_アタッチ\_試行が無効です**](bug-check-0x5--invalid-process-attach-attempt.md)                                                         |
| 0x00000006 | [**無効\_な\_プロセスデタッチ\_試行**](bug-check-0x6--invalid-process-detach-attempt.md)                                                         |
| 0x00000007 | [**無効\_な\_ソフトウェアの割り込み**](bug-check-0x7--invalid-software-interrupt.md)                                                                  |
| 0x00000008 | [**ディスパッチ\_\_レベル以外の IRQL\_** ](bug-check-0x8--irql-not-dispatch-level.md)                                                                       |
| 0x00000009 | [**IRQL\_が\_大きくない\_か等しい\_** ](bug-check-0x9--irql-not-greater-or-equal.md)                                                                  |
| Stop | [**IRQL\_が少ない\_か等しい\_\_** ](bug-check-0xa--irql-not-less-or-equal.md)                                                                        |
| 0x0000000B | [**例外\_処理\_のサポート\_なし**](bug-check-0xb--no-exception-handling-support.md)                                                           |
| 0x0000000C | [**最大\_待機\_オブジェクト\_を超えました**](bug-check-0xc--maximum-wait-objects-exceeded.md)                                                           |
| 0x0000000D | [**MUTEX\_レベル\_番号違反\_** ](bug-check-0xd--mutex-level-number-violation.md)                                                             |
| 0x0000000E | [**ユーザー\_モードコンテキスト\_がありません\_** ](bug-check-0xe--no-user-mode-context.md)                                                                             |
| 0x0000000F | [**スピン\_\_ロック\_は既に所有されています**](bug-check-0xf--spin-lock-already-owned.md)                                                                       |
| 0x00000010 | [**スピン\_\_ロック\_が所有されていません**](bug-check-0x10--spin-lock-not-owned.md)                                                                              |
| 0x00000011 | [**スレッド\_が\_ミューテックス\_を所有していません**](bug-check-0x11--thread-not-mutex-owner.md)                                                                        |
| 0x00000012 | [**トラップ\_の\_原因不明**](bug-check-0x12--trap-cause-unknown.md)                                                                                 |
| 0x00000013 | [**空\_の\_スレッドREAPER\_リスト**](bug-check-0x13--empty-thread-reaper-list.md)                                                                    |
| 0x00000014 | [**CREATE\_DELETE\_\_ロックがロックされ\_ていません**](bug-check-0x14--create-delete-lock-not-locked.md)                                                         |
| 0x00000015 | [**KMODE\_から\_\_最後に呼び出された\_機会**](bug-check-0x15--last-chance-called-from-kmode.md)                                                         |
| 0x00000016 | [**CID\_ハンドル\_の作成**](bug-check-0x16--cid-handle-creation.md)                                                                               |
| 0x00000017 | [**CID\_ハンドル\_の削除**](bug-check-0x17--cid-handle-deletion.md)                                                                               |
| 0x00000018 | [**ポインター\_に\_よる参照**](bug-check-0x18--reference-by-pointer.md)                                                                             |
| 0x00000019 | [**無効\_な\_プールヘッダー**](bug-check-0x19--bad-pool-header.md)                                                                                       |
| 0x0000001A | [**メモリ\_管理**](bug-check-0x1a--memory-management.md)                                                                                    |
| 0x0000001B | [**PFN\_共有\_数**](bug-check-0x1b--pfn-share-count.md)                                                                                       |
| 0x0000001C | [**PFN\_参照\_カウント**](bug-check-0x1c--pfn-reference-count.md)                                                                               |
| 0x0000001D | [**使用\_可能\_な\_スピンロックがありません**](bug-check-0x1d--no-spin-lock-available.md)                                                                        |
| 0x0000001E | [**KMODE\_例外\_は\_処理されません**](bug-check-0x1e--kmode-exception-not-handled.md)                                                              |
| 0x0000001F | [**共有\_リソース\_のCONV\_エラー**](bug-check-0x1f--shared-resource-conv-error.md)                                                                |
| 0x00000020 | [**終了\_中\_に\_保留中のカーネル APC\_** ](bug-check-0x20--kernel-apc-pending-during-exit.md)                                                       |
| 0x00000021 | [**クォータ\_のアンダーフロー**](bug-check-0x21--quota-underflow.md)                                                                                        |
| 0x00000022 | [**ファイル\_システム**](bug-check-0x22--file-system.md)                                                                                                |
| 0x00000023 | [**FAT\_ファイル\_システム**](bug-check-0x23--fat-file-system.md)                                                                                       |
| 0x00000024 | [**NTFS\_ファイル\_システム**](bug-check-0x24--ntfs-file-system.md)                                                                                     |
| 0x00000025 | [**NPFS\_ファイル\_システム**](bug-check-0x25--npfs-file-system.md)                                                                                     |
| 0x00000026 | [**CDFS\_ファイル\_システム**](bug-check-0x26--cdfs-file-system.md)                                                                                     |
| 0x00000027 | [**RDR\_ファイル\_システム**](bug-check-0x27--rdr-file-system.md)                                                                                       |
| 0x00000028 | [ **\_アクセス\_トークンが破損しています**](bug-check-0x28--corrupt-access-token.md)                                                                             |
| 0x00000029 | [**セキュリティ\_システム**](bug-check-0x29--security-system.md)                                                                                        |
| 0x0000002A | [**不整合\_のある IRP**](bug-check-0x2a--inconsistent-irp.md)                                                                                      |
| 0x0000002B | [**パニック\_スタック\_スイッチ**](bug-check-0x2b--panic-stack-switch.md)                                                                                 |
| 0x0000002C | [**内部\_ポート\_ドライバー**](bug-check-0x2c--port-driver-internal.md)                                                                             |
| 0x0000002D | [**SCSI\_ディスク\_ドライバー\_の内部**](bug-check-0x2d--scsi-disk-driver-internal.md)                                                                  |
| 0x0000002E | [**データ\_バス\_エラー**](bug-check-0x2e--data-bus-error.md)                                                                                         |
| 0x0000002F | [**命令\_バス\_エラー**](bug-check-0x2f--instruction-bus-error.md)                                                                           |
| 0x00000030 | [**無効な\_\_コンテキストの\_セット**](bug-check-0x30--set-of-invalid-context.md)                                                                        |
| 0x00000031 | [**フェーズ 0\_の\_初期化に失敗しました**](bug-check-0x31--phase0-initialization-failed.md)                                                             |
| 0x00000032 | [**PHASE1\_の\_初期化に失敗しました**](bug-check-0x32--phase1-initialization-failed.md)                                                             |
| 0x00000033 | [**予期\_し\_ない初期化呼び出し**](bug-check-0x33--unexpected-initialization-call.md)                                                         |
| 0x00000034 | [**キャッシュ\_マネージャー**](bug-check-0x34--cache-manager.md)                                                                                            |
| 0x00000035 | [ **\_\_IRPスタック\_の場所がこれ以上ありません\_** ](bug-check-0x35--no-more-irp-stack-locations.md)                                                             |
| 0x00000036 | [**デバイス\_参照\_\_カウントが0で\_はありません**](bug-check-0x36--device-reference-count-not-zero.md)                                                     |
| 0x00000037 | [**フロッピー\_の\_内部エラー**](bug-check-0x37--floppy-internal-error.md)                                                                           |
| 0x00000038 | [**シリアル\_ドライバー\_の内部**](bug-check-0x38--serial-driver-internal.md)                                                                         |
| 0x00000039 | [**システム\_終了\_の所有\_ミューテックス**](bug-check-0x39--system-exit-owned-mutex.md)                                                                      |
| 0x0000003A | [**システム\_の\_アン\_ワインド前のユーザー**](bug-check-0x3a--system-unwind-previous-user.md)                                                              |
| 0x0000003B | [**システム\_サービス\_の例外**](bug-check-0x3b--system-service-exception.md)                                                                     |
| 0x0000003C | [**割り込み\_の\_アンワインドが試行されました**](bug-check-0x3c--interrupt-unwind-attempted.md)                                                                 |
| 0x0000003D | [**割り込み\_\_例外\_は処理されませんでした**](bug-check-0x3d--interrupt-exception-not-handled.md)                                                      |
| 0x0000003E | [**マルチ\_プロセッサ\_構成\_はサポートされていません**](bug-check-0x3e--multiprocessor-configuration-not-supported.md)                                |
| 0x0000003F | [ **\_システム\_PTEはこれ以上ありませ\_ん**](bug-check-0x3f--no-more-system-ptes.md)                                                                              |
| 0x00000040 | [**ターゲット\_\_MDL\_が小さすぎます**](bug-check-0x40--target-mdl-too-small.md)                                                                            |
| 0x00000041 | [**プールを空にする必要があります\_\_\_** ](bug-check-0x41--must-succeed-pool-empty.md)                                                                      |
| 0x00000042 | [**ATDISK\_ドライバー\_内部**](bug-check-0x42--atdisk-driver-internal.md)                                                                         |
| 0x00000043 | [**その\_よう\_なパーティションはありません**](bug-check-0x43--no-such-partition.md)                                                                                   |
| 0x00000044 | [**複数\_の\_IRP完了\_要求**](bug-check-0x44--multiple-irp-complete-requests.md)                                                        |
| 0x00000045 | [**システム\_マップ\_REGSが不十分\_です**](bug-check-0x45--insufficient-system-map-regs.md)                                                            |
| 0x00000046 | [**DEREF\_不明\_なログオン\_セッション**](bug-check-0x46--deref-unknown-logon-session.md)                                                              |
| 0x00000047 | [**参照\_の\_不明\_なログオンセッション**](bug-check-0x47--ref-unknown-logon-session.md)                                                                  |
| 0x00000048 | [**完了\_した\_\_IRP\_で状態をキャンセル**](bug-check-0x48--cancel-state-in-completed-irp.md)                                                         |
| 0x00000049 | [**割り込み\_\_\_がオフのページフォールト\_** ](bug-check-0x49--page-fault-with-interrupts-off.md)                                                       |
| 0x0000004A | [**システム\_\_\_サービスで\_の IRQL GT ゼロ\_** ](bug-check-0x4a--irql-gt-zero-at-system-service.md)                                                      |
| 0x0000004B | [**ストリーム\_の\_内部エラー**](bug-check-0x4b--streams-internal-error.md)                                                                         |
| 0x0000004C | [**致命的\_な\_未処理\_のハードエラー**](bug-check-0x4c--fatal-unhandled-hard-error.md)                                                                |
| 0x0000004D | [**使用\_できる\_ページはありません**](bug-check-0x4d--no-pages-available.md)                                                                                 |
| 0x0000004E | [**PFN\_LIST\_が破損しています**](bug-check-0x4e--pfn-list-corrupt.md)                                                                                     |
| 0x0000004F | [**NDIS\_内部\_エラー**](bug-check-0x4f--ndis-internal-error.md)                                                                               |
| 0x00000050 | [**ページング\_\_\_される領域内のページフォールト\_** ](bug-check-0x50--page-fault-in-nonpaged-area.md)                                                             |
| 0x00000051 | [**レジストリ\_エラー**](bug-check-0x51--registry-error.md)                                                                                          |
| 0x00000052 | [**メール\_スロット\_ファイルシステム**](bug-check-0x52--mailslot-file-system.md)                                                                             |
| 0x00000053 | [ **\_ブート\_デバイスがありません**](bug-check-0x53--no-boot-device.md)                                                                                         |
| 0x00000054 | [**LM\_サーバー\_の内部\_エラー**](bug-check-0x54--lm-server-internal-error.md)                                                                    |
| 0x00000055 | [**データ\_の\_一貫性の例外**](bug-check-0x55--data-coherency-exception.md)                                                                     |
| 0x00000056 | [**命令\_の\_一貫性の例外**](bug-check-0x56--instruction-coherency-exception.md)                                                       |
| 0x00000057 | [**XNS\_内部\_エラー**](bug-check-0x57--xns-internal-error.md)                                                                                 |
| 0x00000058 | [**FTDISK\_の\_内部エラー**](bug-check-0x58--ftdisk-internal-error.md)                                                                           |
| 0x00000059 | [**ピン\_ボール\_ファイルシステム**](bug-check-0x59--pinball-file-system.md)                                                                               |
| 0x0000005A | [**重要\_な\_サービスが失敗しました**](bug-check-0x5a--critical-service-failed.md)                                                                       |
| 0x0000005B | [**ENV\_VARの\_設定に失敗しました\_** ](bug-check-0x5b--set-env-var-failed.md)                                                                                |
| 0x0000005C | [**HAL\_の\_初期化に失敗しました**](bug-check-0x5c--hal-initialization-failed.md)                                                                   |
| 0x0000005D | [**サポート\_されていないプロセッサ**](bug-check-0x5d--unsupported-processor.md)                                                                            |
| 0x0000005E | [**オブジェクト\_の\_初期化に失敗しました**](bug-check-0x5e--object-initialization-failed.md)                                                             |
| 0x0000005F | [**セキュリティ\_の\_初期化に失敗しました**](bug-check-0x5f--security-initialization-failed.md)                                                         |
| 0x00000060 | [**プロセス\_の\_初期化に失敗しました**](bug-check-0x60--process-initialization-failed.md)                                                           |
| 0x00000061 | [**HAL1\_の\_初期化に失敗しました**](bug-check-0x61--hal1-initialization-failed.md)                                                                 |
| 0x00000062 | [**OBJECT1\_の\_初期化に失敗しました**](bug-check-0x62--object1-initialization-failed.md)                                                           |
| 0x00000063 | [**SECURITY1\_の\_初期化に失敗しました**](bug-check-0x63--security1-initialization-failed.md)                                                       |
| 0x00000064 | [**シンボリック\_を\_初期化できませんでした**](bug-check-0x64--symbolic-initialization-failed.md)                                                         |
| 0x00000065 | [**MEMORY1\_の\_初期化に失敗しました**](bug-check-0x65--memory1-initialization-failed.md)                                                           |
| 0x00000066 | [**キャッシュ\_の\_初期化に失敗しました**](bug-check-0x66--cache-initialization-failed.md)                                                               |
| 0x00000067 | [**構成\_の\_初期化に失敗しました**](bug-check-0x67--config-initialization-failed.md)                                                             |
| 0x00000068 | [**ファイル\_の\_初期化に失敗しました**](bug-check-0x68--file-initialization-failed.md)                                                                 |
| 0x00000069 | [**IO1\_の\_初期化に失敗しました**](bug-check-0x69--io1-initialization-failed.md)                                                                   |
| 0x0000006A | [**LPC\_の\_初期化に失敗しました**](bug-check-0x6a--lpc-initialization-failed.md)                                                                   |
| 0x0000006B | [**PROCESS1\_の初期化\_に関する FAILE**](bug-check-0x6b--process1-initialization-failed.md)D                                                         |
| 0x0000006C | [**REFMON\_の\_初期化に失敗しました**](bug-check-0x6c--refmon-initialization-failed.md)                                                             |
| 0x0000006D | [**SESSION1\_の\_初期化に失敗しました**](bug-check-0x6d--session1-initialization-failed.md)                                                         |
| 0x0000006E | [**SESSION2\_の\_初期化に失敗しました**](bug-check-0x6e--session2-initialization-failed.md)                                                         |
| 0x0000006F | [**SESSION3\_の\_初期化に失敗しました**](bug-check-0x6f--session3-initialization-failed.md)                                                         |
| 0x00000070 | [**SESSION4\_の\_初期化に失敗しました**](bug-check-0x70--session4-initialization-failed.md)                                                         |
| 0x00000071 | [**SESSION5\_の\_初期化に失敗しました**](bug-check-0x71--session5-initialization-failed.md)                                                         |
| 0x00000072 | [**ドライブ\_文字の\_割り当てに失敗しました\_** ](bug-check-0x72--assign-drive-letters-failed.md)                                                              |
| 0x00000073 | [**構成\_リスト\_が失敗しました**](bug-check-0x73--config-list-failed.md)                                                                                 |
| 0x00000074 | [**システム\_構成情報\_が正しくありません\_** ](bug-check-0x74--bad-system-config-info.md)                                                                        |
| 0x00000075 | [**構成\_を\_書き込めません**](bug-check-0x75--cannot-write-configuration.md)                                                                 |
| 0x00000076 | [**プロセス\_に\_ロック\_されたページがあります**](bug-check-0x76--process-has-locked-pages.md)                                                                    |
| 0x00000077 | [**カーネル\_スタック\_INPAGE\_エラー**](bug-check-0x77--kernel-stack-inpage-error.md)                                                                  |
| 0x00000078 | [**フェーズ 0\_例外**](bug-check-0x78--phase0-exception.md)                                                                                      |
| 0x00000079 | [**一致\_しない HAL**](bug-check-0x79--mismatched-hal.md)                                                                                          |
| 0x0000007A | [**カーネル\_データ\_INPAGE\_エラー**](bug-check-0x7a--kernel-data-inpage-error.md)                                                                    |
| 0x0000007B | [**アクセス\_不可能\_ブートデバイス**](bug-check-0x7b--inaccessible-boot-device.md)                                                                     |
| 0x0000007C | [**バグコード\_NDIS\_ドライバー**](bug-check-0x7c--bugcode-ndis-driver.md)                                                                               |
| 0x0000007D | [**より\_多く\_のメモリをインストールする**](bug-check-0x7d--install-more-memory.md)                                                                               |
| 0x0000007E | [**システム\_スレッド\_の例外\_は処理されません\_** ](bug-check-0x7e--system-thread-exception-not-handled.md)                                             |
| 0x0000007F | [**予期\_し\_ない\_カーネルモードトラップです**](bug-check-0x7f--unexpected-kernel-mode-trap.md)                                                              |
| 0x00000080 | [**NMI\_ハードウェア\_障害**](bug-check-0x80--nmi-hardware-failure.md)                                                                             |
| 0x00000081 | [**スピン\_ロック\_の初期\_化に失敗した**](bug-check-0x81--spin-lock-init-failure.md)                                                                        |
| 0x00000082 | [**DFS\_ファイル\_システム**](bug-check-0x82--dfs-file-system.md)                                                                                       |
| 0x00000085 | [**セットアップ\_エラー**](bug-check-0x85--setup-failure.md)                                                                                            |
| 0x0000008B | [**MBR\_チェック\_サムの不一致**](bug-check-0x8b--mbr-checksum-mismatch.md)                                                                           |
| 0x0000008E | [**カーネル\_モード\_\_例外は処理\_されません**](bug-check-0x8e--kernel-mode-exception-not-handled.md)                                                 |
| 0x0000008F | [**PP0\_の\_初期化に失敗しました**](bug-check-0x8f--pp0-initialization-failed.md)                                                                   |
| 0x00000090 | [**PP1\_の\_初期化に失敗しました**](bug-check-0x90--pp1-initialization-failed.md)                                                                   |
| 0x00000092 | [**MP\_\_システムの\_アップドライバ\_** ](bug-check-0x92--up-driver-on-mp-system.md)                                                                       |
| 0x00000093 | [**無効\_な\_カーネルハンドル**](bug-check-0x93--invalid-kernel-handle.md)                                                                           |
| 0x00000094 | [**終了\_時に\_\_カーネルスタックがロックされまし\_た**](bug-check-0x94--kernel-stack-locked-at-exit.md)                                                             |
| 0x00000096 | [**無効\_な\_ワークキュー\_項目**](bug-check-0x96--invalid-work-queue-item.md)                                                                      |
| 0x00000097 | [**バインド\_さ\_れたイメージはサポートされません**](bug-check-0x97--bound-image-unsupported.md)                                                                       |
| 0x00000098 | [ **\_\_NT評価\_期間の終了\_** ](bug-check-0x98--end-of-nt-evaluation-period.md)                                                             |
| 0x00000099 | [**リージョン\_また\_は\_セグメントが無効です**](bug-check-0x99--invalid-region-or-segment.md)                                                                  |
| 0x0000009A | [**システム\_ライセンス\_違反**](bug-check-0x9a--system-license-violation.md)                                                                     |
| 0x0000009B | [**UDF\_ファイル\_システム**](bug-check-0x9b--udfs-file-system.md)                                                                                     |
| 0x0000009C | [**コンピューター\_チェック\_の例外**](bug-check-0x9c--machine-check-exception.md)                                                                       |
| 0x0000009E | [**ユーザー\_モード\_のヘルス\_モニター**](bug-check-0x9e--user-mode-health-monitor.md)                                                                    |
| 0x0000009F | [**ドライバー\_の\_電源状態\_のエラー**](bug-check-0x9f--driver-power-state-failure.md)                                                                |
| 0x000000A0 | [**内部\_電源\_エラー**](bug-check-0xa0--internal-power-error.md)                                                                             |
| 0x000000A1 | [**PCI\_バス\_ドライバー内部\_** ](bug-check-0xa1--pci-bus-driver-internal.md)                                                                      |
| 0x000000A2 | [**メモリ\_イメージ\_が壊れています**](bug-check-0xa2--memory-image-corrupt.md)                                                                             |
| 0x000000A3 | [**ACPI\_ドライバー\_の内部**](bug-check-0xa3--acpi-driver-internal.md)                                                                             |
| 0x000000A4 | [**CNSS\_ファイル\_システム\_フィルター**](bug-check-0xa4--cnss-file-system-filter.md)                                                                      |
| 0x000000A5 | [**ACPI\_BIOS\_エラー**](bug-check-0xa5--acpi-bios-error.md)                                                                                       |
| 0x000000A7 | [**不適切\_な EXHANDLE**](bug-check-0xa7--bad-exhandle.md)                                                                                              |
| 0x000000AB | [**セッション\_は\_終了時に\_有効な\_プール\_を持っています**](bug-check-0xab--session-has-valid-pool-on-exit.md)                                                      |
| 0x000000AC | [**HAL\_の\_メモリ割り当て**](bug-check-0xac--hal-memory-allocation.md)                                                                           |
| 0x000000AD | [**ビデオ\_ドライバー\_デバッグレポート\_要求\_** ](bug-check-0xad--video-driver-debug-report-request.md)                                                 |
| 0x000000B1 | [**検出\_さ\_れた違反の BGI**](bug-check-0xb1--bgi-detected-violation.md)                                                                         |
| 0x000000B4 | [**ビデオ\_ドライバー\_の初期化\_エラー**](bug-check-0xb4--video-driver-init-failure.md)                                                                  |
| 0x000000B8 | [**DPC\_から\_の\_切り替えを試行しました**](bug-check-0xb8--attempted-switch-from-dpc.md)                                                                  |
| 0x000000B9 | [**チップ\_セット\_検出エラー**](bug-check-0xb9--chipset-detected-error.md)                                                                         |
| 0x000000BA | [**セッション\_に\_は終了時に\_\_有効なビューがあり\_ます**](bug-check-0xba--session-has-valid-views-on-exit.md)                                                    |
| 0x000000BB | [**ネットワーク\_ブート\_を初期化\_できませんでした**](bug-check-0xbb--network-boot-initialization-failed.md)                                                |
| 0x000000BC | [**ネットワーク\_ブート\_の重複\_アドレス**](bug-check-0xbc--network-boot-duplicate-address.md)                                                        |
| 0x000000BD | [**無効\_な\_休止状態**](bug-check-0xbd--invalid-hibernated-state.md)                                                                     |
| 0x000000BE | [**読み取り\_専用\_\_メモリへの書き込みを試行しました\_** ](bug-check-0xbe--attempted-write-to-readonly-memory.md)                                               |
| 0x000000BF | [**ミューテックス\_は\_既に所有されています**](bug-check-0xbf--mutex-already-owned.md)                                                                               |
| 0x000000C1 | [**特別\_な\_プール\_でメモリ\_の破損が検出されました**](bug-check-0xc1--special-pool-detected-memory-corruption.md)                                     |
| 0x000000C2 | [**無効\_な\_プール呼び出し**](bug-check-0xc2--bad-pool-caller.md)                                                                                       |
| 0x000000C4 | [**ドライバー\_検証\_ツール\_が違反を検出しました**](bug-check-0xc4--driver-verifier-detected-violation.md)                                                |
| 0x000000C5 | [**ドライバー\_が\_破損した EXPOOL**](bug-check-0xc5--driver-corrupted-expool.md)                                                                       |
| 0x000000C6 | [**解放\_\_\_されたプールの変更を検出したドライバー\_** ](bug-check-0xc6--driver-caught-modifying-freed-pool.md)                                               |
| 0x000000C7 | [**タイマー\_また\_はDPC\_が無効です**](bug-check-0xc7--timer-or-dpc-invalid.md)                                                                            |
| 0x000000C8 | [**IRQL\_予期\_しない値**](bug-check-0xc8--irql-unexpected-value.md)                                                                           |
| 0x000000C9 | [**ドライバー\_検証\_ツールの\_IOMANAGER 違反**](bug-check-0xc9--driver-verifier-iomanager-violation.md)                                              |
| 0x000000CA | [**PNP\_で\_検出\_された致命的なエラー**](bug-check-0xca--pnp-detected-fatal-error.md)                                                                    |
| 0x000000CB | [ **\_実行中\_のドライバー\_のロック\_されたページ\_** ](bug-check-0xcb--driver-left-locked-pages-in-process.md)                                            |
| 0x000000CC | [**解放\_\_\_され\_た特殊なプールでのページフォールト\_** ](bug-check-0xcc--page-fault-in-freed-special-pool.md)                                                  |
| 0x000000CD | [**ページ\_\_フォールト\_が割り当て終了\_を超えています\_** ](bug-check-0xcd--page-fault-beyond-end-of-allocation.md)                                            |
| 0x000000CE | [**保留\_中\_\_の操作\_をキャンセルせずにドライバーがアンロードされた\_** ](bug-check-0xce--driver-unloaded-without-cancelling-pending-operations.md)        |
| 0x000000CF | [**ターミナル\_サーバー\_ドライバー\_が正しく\_ないメモリ参照を作成しまし\_た\_** ](bug-check-0xcf--terminal-server-driver-made-incorrect-memory-reference.md)     |
| 0x000000D0 | [**ドライバー\_が\_破損した MMPOOL**](bug-check-0xd0--driver-corrupted-mmpool.md)                                                                       |
| 0x000000D1 | [**ドライバー\_の\_IRQLが\_少ないか等しい\_\_** ](bug-check-0xd1--driver-irql-not-less-or-equal.md)                                                        |
| 0x000000D2 | [**バグコード\_ID\_ドライバー**](bug-check-0xd2--bugcode-id-driver.md)                                                                                   |
| 0x000000D3 | [**ドライバー\_の\_部分\_は\_、非ページである必要があります**](bug-check-0xd3--driver-portion-must-be-nonpaged.md)                                                     |
| 0x000000D4 | [**不適切\_\_\_\_\_なドライバーのアンロードを検出\_した、発生した IRQL のシステムスキャン\_\_** ](bug-check-0xd4--system-scan-at-raised-irql-caught-improper-driver-unlo.md) |
| 0x000000D5 | [**解放\_\_\_され\_た特殊な\_プールのドライバーページエラー\_** ](bug-check-0xd5--driver-page-fault-in-freed-special-pool.md)                                   |
| 0x000000D6 | [**割り当て\_の\_終了\_を超え\_たドライバー\_ページのエラー\_** ](bug-check-0xd6--driver-page-fault-beyond-end-of-allocation.md)                             |
| 0x000000D7 | [**無効な\_\_ビューをマップ解除した\_ドライバー**](bug-check-0xd7--driver-unmapping-invalid-view.md)                                                          |
| 0x000000D8 | [**ドライバー\_で\_過剰\_な PTE が使用されています**](bug-check-0xd8--driver-used-excessive-ptes.md)                                                                |
| 0x000000D9 | [**ロック\_さ\_れ\_たページのトラッカーの破損**](bug-check-0xd9--locked-pages-tracker-corruption.md)                                                      |
| 0x000000DA | [**システム\_PTE\_の誤用**](bug-check-0xda--system-pte-misuse.md)                                                                                   |
| 0x000000DB | [**ドライバー\_が\_破損している SYSPTES**](bug-check-0xdb--driver-corrupted-sysptes.md)                                                                     |
| 0x000000DC | [**ドライバー\_が\_無効\_なスタックアクセス**](bug-check-0xdc--driver-invalid-stack-access.md)                                                              |
| 0x000000DE | [**ファイル\_\_領域で\_プールが破損しています\_** ](bug-check-0xde--pool-corruption-in-file-area.md)                                                           |
| 0x000000DF | [ **\_ワーカースレッドの中継を\_** 行う](bug-check-0xdf--impersonating-worker-thread.md)                                                               |
| 0x000000E0 | [**ACPI\_BIOS\_の致命的\_なエラー**](bug-check-0xe0--acpi-bios-fatal-error.md)                                                                          |
| 0x000000E1 | [**無効\_\_\_なIRQL\_で、ワーカースレッドが返されました\_** ](bug-check-0xe1--worker-thread-returned-at-bad-irql.md)                                              |
| 0x000000E2 | [**手動\_で\_開始されたクラッシュ**](bug-check-0xe2--manually-initiated-crash.md)                                                                     |
| 0x000000E3 | [**リソース\_が\_所有されていません**](bug-check-0xe3--resource-not-owned.md)                                                                                 |
| 0x000000E4 | [**ワーカー\_が無効です**](bug-check-0xe4--worker-invalid.md)                                                                                          |
| 0x000000E6 | [**ドライバー\_の\_検証\_ツールの DMA 違反**](bug-check-0xe6--driver-verifier-dma-violation.md)                                                          |
| 0x000000E7 | [**無効\_な\_浮動\_小数点の状態**](bug-check-0xe7--invalid-floating-point-state.md)                                                            |
| 0x000000E8 | [**ファイル\_\_\_が開かれると無効なキャンセル\_** ](bug-check-0xe8--invalid-cancel-of-file-open.md)                                                             |
| 0x000000E9 | [**アクティブ\_な\_EXワーカー\_スレッド\_の終了**](bug-check-0xe9--active-ex-worker-thread-termination.md)                                             |
| 0x000000EA | [**デバイス\_\_\_ドライバーでのスレッドスタック\_** ](bug-check-0xea--thread-stuck-in-device-driver.md)                                                         |
| 0x000000EB | [**ダーティ\_マップ\_ページ\_の輻輳**](bug-check-0xeb--dirty-mapped-pages-congestion.md)                                                          |
| 0x000000EC | [**セッション\_の\_終了\_時\_に\_有効な特殊なプールがある\_** ](bug-check-0xec--session-has-valid-special-pool-on-exit.md)                                     |
| 0x000000ED | [**UNMOUNTABLE\_ブート\_ボリューム**](bug-check-0xed--unmountable-boot-volume.md)                                                                       |
| 0x000000EF | [**重要\_な\_プロセス**](bug-check-0xef--critical-process-died.md)                                                                           |
| 0x000000F0 | [**ストレージ\_ミニ\_ポートエラー**](bug-check-0xf0--storage-miniport-error.md)                                                                         |
| 0x000000F1 | [**検出\_さ\_れた\_SCSI 検証ツールの違反**](bug-check-0xf1--scsi-verifier-detected-violation.md)                                                    |
| 0x000000F2 | [**ハードウェア\_割り込み\_ストーム**](bug-check-0xf2--hardware-interrupt-storm.md)                                                                     |
| 0x000000F3 | [**正常\_シャットダウン**](bug-check-0xf3--disorderly-shutdown.md)                                                                                |
| 0x000000F4 | [**重要\_な\_オブジェクトの終了**](bug-check-0xf4--critical-object-termination.md)                                                               |
| 0x000000F5 | [**FLTMGR\_ファイル\_システム**](bug-check-0xf5--fltmgr-file-system.md)                                                                                 |
| 0x000000F6 | [**PCI\_検証\_ツール\_で違反が検出されました**](bug-check-0xf6--pci-verifier-detected-violation.md)                                                      |
| 0x000000F7 | [**ドライバー\_の過剰\_実行\_スタックバッファー**](bug-check-0xf7--driver-overran-stack-buffer.md)                                                              |
| 0x000000F8 | [**RAMDISK\_\_ブート\_の初期化に失敗しました**](bug-check-0xf8--ramdisk-boot-initialization-failed.md)                                                |
| 0x000000F9 | [**ボリューム\_\_\_\_\_を開くためにドライバーから状態の再解析が返されました\_** ](bug-check-0xf9--driver-returned-status-reparse-for-volume-open.md)                     |
| 0x000000FA | [**HTTP\_ドライバー\_が破損しています**](bug-check-0xfa---http-driver-corrupted.md)                                                                          |
| 0x000000FC | [**NOEXECUTE\_\_\_メモリの実行\_を試みました**](bug-check-0xfc---attempted-execute-of-noexecute-memory.md)                                        |
| 0x000000FD | [**ダーティ\_NOWRITE\_ページ\_の輻輳**](bug-check-0xfd---dirty-nowrite-pages-congestion.md)                                                       |
| 0x000000FE | [**バグコード\_の\_USB ドライバー**](bug-check-0xfe--bugcode-usb-driver.md)                                                                                 |
| 0x000000FF | [**予約\_キュー\_のオーバーフロー**](bug-check-0xff---reserve-queue-overflow.md)                                                                        |
| 0x00000100 | [**ローダー\_ブロック\_の不一致**](bug-check-0x100---loader-block-mismatch.md)                                                                         |
| 0x00000101 | [**クロック\_ウォッチ\_ドッグのタイムアウト**](bug-check-0x101---clock-watchdog-timeout.md)                                                                       |
| 0x00000102 | [**DPC\_ウォッチ\_ドッグのタイムアウト**](bug-check-0x102--dpc-watchdog-timeout.md)                                                                            |
| 0x00000103 | [**MUP\_ファイル\_システム**](bug-check-0x103---mup-file-system.md)                                                                                     |
| 0x00000104 | [**AGP\_無効\_アクセス**](bug-check-0x104---agp-invalid-access.md)                                                                               |
| 0x00000105 | [**AGP\_GART\_の破損**](bug-check-0x105---agp-gart-corruption.md)                                                                             |
| 0x00000106 | [**AGP\_の\_不正再プログラミング**](bug-check-0x106---agp-illegally-reprogrammed.md)                                                               |
| 0x00000108 | [**サード\_パーティ\_のファイル\_システムエラー\_** ](bug-check-0x108--third-party-file-system-failure.md)                                                    |
| 0x00000109 | [**重大\_な\_構造の破損**](bug-check-0x109---critical-structure-corruption.md)                                                         |
| 0x0000010A | [**アプリ\_の\_タグ\_付けを初期化できませんでした**](bug-check-0x10a---app-tagging-initialization-failed.md)                                                |
| 0x0000010C | [**FSRTL\_EXTRA\_作成パラメーター\_違反\_** ](bug-check-0x10c---fsrtl-extra-create-parameter-violation.md)                                     |
| 0x0000010D | [**WDF\_違反**](bug-check-0x10d---wdf-violation.md)                                                                                          |
| 0x0000010E | [**内部\_の\_ビデオ\_メモリ管理**](bug-check-0x10e---video-memory-management-internal.md)                                                  |
| 0x0000010F | [**リソース\_マネージャー\_の例外\_は処理されません\_** ](bug-check-0x10f---resource-manager-exception-not-handled.md)                                     |
| 0x00000111 | [**再帰\_NMI**](bug-check-0x111---recursive-nmi.md)                                                                                          |
| 0x00000112 | [**MSRPC\_の\_状態違反**](bug-check-0x112---msrpc-state-violation.md)                                                                         |
| 0x00000113 | [**VIDEO\_DXGKRNL\_の致命的\_なエラー**](bug-check-0x113---video-dxgkrnl-fatal-error.md)                                                                |
| 0x00000114 | [**ビデオ\_シャドウ\_ドライバの\_致命的\_なエラー**](bug-check-0x114---video-shadow-driver-fatal-error.md)                                                   |
| 0x00000115 | [**AGP\_内部**](bug-check-0x115---agp-internal.md)                                                                                            |
| 0x00000116 | [**VIDEO\_TDR\_の失敗**](bug-check-0x116---video-tdr-failure.md)                                                                                     |
| 0x00000117 | [**VIDEO\_TDR\_TIMEOUT\_が検出されました**](bug-check-0x117---video-tdr-timeout-detected.md)                                                              |
| 0x00000119 | [**ビデオ\_スケジューラ\_の内部\_エラー**](bug-check-0x119---video-scheduler-internal-error.md)                                                      |
| 0x0000011A | [**EM\_の\_初期化エラー**](bug-check-0x11a---em-initialization-failure.md)                                                                 |
| 0x0000011B | [**キャンセル\_\_\_ロックを保持しているドライバーが返されました\_** ](bug-check-0x11b---driver-returned-holding-cancel-lock.md)                                           |
| 0x0000011C | [**CM\_\_\_\_で保護されたストレージへの書き込みを試行しました\_** ](bug-check-0x11c--attempted-write-to-cm-protected-storage.md)                                   |
| 0x0000011D | [**イベント\_トレース\_の致命的\_なエラー**](bug-check-0x11d---event-tracing-fatal-error.md)                                                                |
| 0x0000011E | [ **\_再帰\_エラーが多すぎ\_ます**](bug-check-0x11e--too-many-recursive-faults.md)                                                                |
| 0x0000011F | [**無効\_な\_ドライバーハンドル**](bug-check-0x11f--invalid-driver-handle.md)                                                                         |
| 0x00000120 | [**BITLOCKER\_の\_致命的なエラー**](bug-check-0x120--bitlocker-fatal-error-.md)                                                                        |
| 0x00000121 | [**ドライバー\_違反**](bug-check-0x121---driver-violation.md)                                                                                    |
| 0x00000122 | [**WHEA\_内部\_エラー**](bug-check-0x122---whea-internal-error.md)                                                                             |
| 0x00000123 | [**暗号化\_自己\_テスト\_の失敗**](bug-check-0x123--crypto-self-test-failure-.md)                                                                 |
| 0x00000124 | [**WHEA\_修正\_不可能エラー**](bug-check-0x124---whea-uncorrectable-error.md)                                                                   |
| 0x00000125 | [**NMR\_無効\_な状態**](bug-check-0x125--nmr-invalid-state.md)                                                                                 |
| 0x00000126 | [**NETIO\_無効\_なプール\_呼び出し元**](bug-check-0x126--netio-invalid-pool-caller.md)                                                                |
| 0x00000127 | [**ページ\_が\_ゼロではありません**](bug-check-0x127---page-not-zero.md)                                                                                         |
| 0x00000128 | [**無効\_\_\_なIO\_優先度で返されたワーカースレッド\_\_** ](bug-check-0x128--worker-thread-returned-with-bad-io-priority.md)                          |
| 0x00000129 | [**無効\_\_\_\_なページングIO\_優先度で返されたワーカースレッド\_\_** ](bug-check-0x129--worker-thread-returned-with-bad-paging-io-priority.md)           |
| 0x0000012A | [**MUI\_は\_有効\_なシステム\_言語ではありません**](bug-check-0x12a--mui-no-valid-system-language.md)                                                          |
| 0x0000012B | [**障害\_が\_発生\_したハードウェアの破損ページ**](bug-check-0x12b---faulty-hardware-corrupted-page.md)                                                      |
| 0x0000012C | [**EXFAT\_ファイル\_システム**](bug-check-0x12c---exfat-file-system.md)                                                                                 |
| 0x0000012D | [**VOLSNAP\_オーバーラップ\_テーブルアクセス\_** ](bug-check-0x12d--volsnap-overlapped-table-access.md)                                                     |
| 0x0000012E | [**無効\_な\_MDL 範囲**](bug-check-0x12e--invalid-mdl-range.md)                                                                                  |
| 0x0000012F | [**VHD\_\_ブート\_の初期化に失敗しました**](bug-check-0x12f--vhd-boot-initialization-failed.md)                                                       |
| 0x00000130 | [**動的\_な\_ADDプロセッサ\_の不一致**](bug-check-0x130--dynamic-add-processor-mismatch.md)                                                       |
| 0x00000131 | [**無効\_な\_拡張プロセッサ\_の状態**](bug-check-0x131--invalid-extended-processor-state.md)                                                   |
| 0x00000132 | [**リソース\_所有\_者\_のポインターが無効です**](bug-check-0x132--resource-owner-pointer-invalid.md)                                                       |
| 0x00000133 | [**DPC\_ウォッチ\_ドッグ違反**](bug-check-0x133-dpc-watchdog-violation.md)                                                                         |
| 0x00000134 | [**EXTENDER\_のドライブ**](bug-check-0x134--drive-extender.md)                                                                                         |
| 0x00000135 | [**レジストリ\_フィルター\_ドライバー\_の例外**](bug-check-0x135--registry-filter-driver-exception.md)                                                   |
| 0x00000136 | [**VHD\_ブート\_ホスト\_ボリュームに十分な\_領域がありません\_\_** ](bug-check-0x136--vhd-boot-host-volume-not-enough-space.md)                                      |
| 0x00000137 | [**WIN32K\_ハンドル\_マネージャー**](bug-check-0x137--win32k-handle-manager.md)                                                                          |
| 0x00000138 | [**GPIO\_コントローラー\_ドライバーエラー\_** ](bug-check-0x138-gpio-controller-driver-error.md)                                                            |
| 0x00000139 | [**カーネル\_セキュリティ\_チェック\_の失敗**](bug-check-0x139--kernel-security-check-failure.md)                                              |
| 0x0000013A | [**カーネル\_モード\_のヒープ\_の破損**](bug-check-0x13a--kernel-mode-heap-corruption.md)                                                             |
| 0x0000013B | [**パッシブ\_割り込み\_エラー**](bug-check-0x13b--passive-interrupt-error.md)                                                                      |
| 0x0000013C | [**無効\_な\_IO\_ブースト状態**](bug-check-0x13c--invalid-io-boost-state.md)                                                                       |
| 0x0000013D | [**重大\_な\_初期化エラー**](bug-check-0x13d--critical-initialization-failure.md)                                                      |
| 0x00000140 | [**ストレージ\_デバイス\_異常が\_が検出されました**](bug-check-0x140--storage-device-abnormality-detected.md)                                             |
| 0x00000141 | [**ビデオ\_エンジン\_のタイムアウト\_が検出されました**](bug-check-0x141---video-engine-timeout-detected.md)                                                        |
| 0x00000142 | [**VIDEO\_TDR\_アプリケーション\_がブロックされました**](bug-check-0x142--video-tdr-application-blocked.md)                                                         |
| 0x00000143 | [**内部\_の\_プロセッサドライバー**](bug-check-0x143--processor-driver-internal.md)                                                                  |
| 0x00000144 | [**バグコード\_USB3\_ドライバー**](bug-check-0x144--bugcode-usb3-driver.md)                                                                              |
| 0x00000145 | [**セキュア\_ブート\_違反**](bug-check-0x145--secure-boot-violation-.md)                                                                         |
| 0x00000147 | [**異常\_な\_リセットが検出されました**](bug-check-0x147--abnormal-reset-detected.md)                                                                      |
| 0x00000149 | [**REFS\_ファイル\_システム**](bug-check-0x149--refs-file-system.md)                                                                                    |
| 0x0000014A | [**カーネル\_WMI\_内部**](bug-check-0x14a--kernel-wmi-internal.md)                                                                              |
| 0x0000014B | [**SOC\_サブ\_システムの障害**](bug-check-0x14b--soc-subsystem-failure.md)                                                                          |
| 0x0000014C | [**致命的\_な\_異常リセット\_エラー**](bug-check-0x14c--fatal-abnormal-reset-error.md)                                                               |
| 0x0000014D | [**例外\_スコープ\_が無効です**](bug-check-0x14d--exception-scope-invalid.md)                                                                      |
| 0x0000014E | [**SOC\_重大\_なデバイス\_が削除されました**](bug-check-0x14e--soc-critical-device-removed.md)                                                             |
| 0x0000014F | [**PDC\_ウォッチ\_ドッグのタイムアウト**](bug-check-0x14f--pdc-watchdog-timeout.md)                                                                            |
| 0x00000150 | [**TCPIP\_による\_AC\_NIC\_の\_アクティブな参照のリーク**](bug-check-0x150--tcpip-aoac-nic-active-reference-leak.md)                                         |
| 0x00000151 | [**サポート\_さ\_れていない命令モード**](bug-check-0x151--unsupported-instruction-mode.md)                                                            |
| 0x00000152 | [**プッシュ\_ロック\_フラグが無効\_です**](bug-check-0x152--invalid-push-lock-flags.md)                                                                     |
| 0x00000153 | [**スレッド\_\_\_の終了\_時に\_カーネルロックエントリがリークした\_** ](bug-check-0x153--kernel-lock-entry-leaked-on-thread-termination.md)                    |
| 0x00000154 | [**予期\_し\_ないストアの例外**](bug-check-0x154--unexpected-store-exception.md)                                                                |
| 0x00000155 | [**OS\_データ\_の改ざん**](bug-check-0x155--os-data-tampering.md)                                                                                  |
| 0x00000156 | [**WINSOCK\_で\_ハングし\_た CLOSESOCKET\_LIVEDUMP が検出されました**](bug-check-0x156--winsock-detected-hung-closesocket-livedump.md)                              |
| 0x00000157 | [**カーネル\_スレッド\_優先度\_フロア違反\_** ](bug-check-0x157--kernel-thread-priority-floor-violation.md)                                      |
| 0x00000158 | [**無効\_な\_IOMMUページ\_フォールト**](bug-check-0x158--illegal-iommu-page-fault.md)                                                                   |
| 0x00000159 | [**HAL\_の\_無効\_な IOMMU ページ\_フォールト**](bug-check-0x159--hal-illegal-iommu-page-fault.md)                                                          |
| 0x0000015A | [**SDBUS\_の\_内部エラー**](bug-check-0x15a--sdbus-internal-error.md)                                                                            |
| 0x0000015B | [**システム\_\_\_\_ページ優先度\_がアクティブな状態で返されたワーカースレッド\_\_** ](bug-check-0x15b--worker-thread-returned-with-system-page-priority-active.md) |
| 0x0000015C | [**PDC\_ウォッチ\_ドッグタイムアウト\_LIVEDUMP**](bug-check-0x15c--pdc-watchdog-timeout-livedump.md)              
| 0x0000015D | [**SOC\_サブ\_システムエラー\_LIVEDUMP**](bug-check-0x15d-soc-subsystem-failure-livedump.md)              
| 0x0000015E | [**バグコード\_NDIS\_ドライバー\_ライブダンプ\_** ](bug-check-0x15e-bugcode-ndis-driver-live-dump.md)                                                         |
| 0x0000015F | [**コネクト\_スタンバイ\_ウォッチドッグ\_タイムアウトLIVEDUMP\_** ](bug-check-0x15f--connected-standby-watchdog-timeout-livedump.md)                            |
| 0x00000160 | [**WIN32K\_アトミック\_チェック\_の失敗**](bug-check-0x160--win32k-atomic-check-failure.md)                                                             |
| 0x00000161 | [**ライブ\_システム\_ダンプ**](bug-check-0x161--live-system-dump.md)                                                                                    |
| 0x00000162 | [**カーネル\_の\_自動\_ブー\_スト\_の無効なロックの解放**](bug-check-0x162--kernel-auto-boost-invalid-lock-release.md)                                     |
| 0x00000163 | [**ワーカー\_スレッド\_のテスト\_条件**](bug-check-0x162--worker-thread-test-condition.md)                                                           |
| 0x00000164 | [**WIN32K\_の\_重大なエラー**](bug-check-0x164--win32k-critical-failure.md)                                                                      |
| 0x00000165 | [**クラスター\_CSV\_ステータス\_IOタイムアウトLIVEDUMP\_\_** ](bug-check-0x165--cluster-csv-staus-io-timeout-livedump.md)                                      | 
| 0x00000166 | [**クラスター\_リソース\_呼び出しタイムアウト\_LIVEDUMP\_** ](bug-check-0x166--cluster-resource-call-timeout-livedump.md)                                      |
| 0x00000167 | [**クラスター\_CSV\_スナップショットデバイス\_情報\_のタイムアウト LIVEDUMP\_\_** ](bug-check-0x167--cluster-csv-snapshot-device-info-timeout-livedump.md)              |    
| 0x00000168 | [**クラスター\_CSV\_状態\_遷移タイムアウトLIVEDUMP\_\_** ](bug-check-0x168--cluster-csv-state-transition-timeout-livedump.md)                       |   
| 0x00000169 | [**クラスター\_CSV\_ボリュームの\_到着LIVEDUMP\_** ](bug-check-0x169--cluster-csv-volume-arival-livedump.md)                                             |      
| 0x0000016A | [**クラスター\_CSV\_ボリュームの\_削除LIVEDUMP\_** ](bug-check-0x16a--cluster-csv-volume-removal-livedump.md)                                            |    
| 0x0000016B | [**クラスター\_CSV\_クラスターウォッチ\_ドッグLIVEDUMP\_** ](bug-check-0x16b--cluster-csv-cluster-watchdog-livedump.md)                                       |   
| 0x0000016C | [**ラン\_ダウン\_保護\_フラグが無効です**](bug-check-0x16c--invalid-rundown-protection-flags.md)                                                   |
| 0x0000016D | [**スロット\_アロケーター\_フラグが無効\_です**](bug-check-0x16d--invalid-slot-allocator-flags.md)                                                           |
| 0x0000016E | [**÷\_無効\_なリリース**](bug-check-0x16e--eresource-invalid-release.md)                                                                  |
| 0x0000016F | [**クラスター\_CSV\_状態の移行\_間隔のタイムアウト\_LIVEDUMP\_\_** ](bug-check-0x16f--cluster-csv-state-transistion-interval-livedump.md)           |
| 0x00000170 | [**CRYPTO\_LIBRARY\_の内部\_エラー**](bug-check-0x170--crypto-library-internal-error.md)                                                         |
| 0x00000171 | [**クラスター\_CSV\_CLUSSVC\_切断ウォッチ\_ドッグ**](bug-check-0x171--cluster-csv-clussvc-disconnect-watchdog.md)                                    |
| 0x00000173 | [**COREMSGCALL\_内部\_エラー**](bug-check-0x173--coremsgcall-internal-error.md)                                                                |
| 0x00000174 | [**COREMSG\_内部\_エラー**](bug-check-0x174--coremsg-internal-error.md)                                                                        |
| 0x00000175 | [**以前\_の\_致命的\_な異常リセット\_エラー**](bug-check-0x175--previous-fatal-abnormal-reset-error.md)                                            |
| 0x00000178 | [**ELAM\_ドライバー\_が\_致命的\_なエラーを検出しました**](bug-check-0x175--elam-driver-detected-fatal-error.md)                                                  |
| 0x00000179 | [**CLUSTER\_CLUSPORT\_STATUS\_IOTIMEOUTLIVEDUMP\_\_** ](bug-check-0x179--cluster-clusport-status-io-timeout-livedump.md)                           |
| 0x0000017B | [**プロファイラー\_の\_構成が無効です**](bug-check-0x17b--profiler-configuration-illegal.md)                                                        | 
| 0x0000017C | [**PDC\_ロック\_ウォッチドッグ\_LIVEDUMP**](bug-check-0x17c--pdc-lock-watchdog-livedump.md)                                                               | 
| 0x0000017D | [**PDC\_の\_予期\_しない失効 LIVEDUMP**](bug-check-0x17d-unexpected-revocation-livedump.md)                                                    | 
| 0x0000017E | [**マイクロ\_コード\_リビジョンが一致しません**](bug-check-0x17e--microcode-revision-mismatch.md)                                                              | 
| 0x00000187 | [**ビデオ\_DWMINIT\_タイムアウト\_フォールバック\_BDD**](bug-check-0x187--video-dwminit-timeout-fallback-bdd.md)                                              |
| 0x00000188 | [**クラスター\_CSVFS\_LIVEDUMP**](bug-check-0x188--cluster-csvfs-livedump.md)                                                                        |
| 0x00000189 | [ **\_オブジェクト\_ヘッダーが正しくありません**](bug-check-0x189--bad-object-header.md)                                                                                  |
| 0x0000018B | [**セキュリティ\_で\_保護されたカーネルエラー**](bug-check-0x18b--secure-kernel-error.md)                                                                              |
| 0x0000018C | [**HYPERGUARD\_違反**](bug-check-0x18c--hyperguard-violation.md)                                                                              |   
| 0x0000018D | [**セキュリティ\_で\_保護されていないエラー**](bug-check-0x18d--secure-fault-unhandled.md)                                                                        | 
| 0x0000018E | [**カーネル\_パーティション\_参照違反\_** ](bug-check-0x18e--kernel-partition-reference-violation.md)                                           |
| 0x00000190 | [**WIN32K\_重大\_なエラー\_LIVEDUMP**](bug-check-0x190--win32k-critical-failure-livedump.md)                                                   |
| 0x00000191 | [**PF\_の\_検出された破損**](bug-check-0x191--pf-detected-corruption.md)                                                                        |
| 0x00000192 | [**発生\_\_\_\_\_\_した IRQL によるカーネルの自動ブーストロックの取得\_** ](bug-check-0x192--kernel-auto-boost-lock-acquisition-with-raised-irql.md)         |
| 0x00000193 | [**VIDEO\_DXGKRNL\_LIVEDUMP**](bug-check-0x192--video-dxgkrnl-livedump.md)                                                                        |
| 0x00000195 | [**SMB\_サーバー\_LIVEDUMP**](bug-check-0x195--smb-server-livedump.md)                                                                              |
| 0x00000196 | [**ローダー\_の\_ロールバックが検出されました**](bug-check-0x196--loader-rollback-detected.md)                                                                    |
| 0x00000197 | [**WIN32K\_の\_セキュリティエラー**](bug-check-0x197--win32k-security-failure.md)                                                                      |
| 0x00000198 | [**UFX\_LIVEDUMP**](bug-check-0x198--ufx-livedump.md)                                                                                             |
| 0x00000199 | [**使用\_中の\_\_カーネルストレージ\_スロット**](bug-check-0x199--kernel-storage-slot-in-use.md)                                                              |
| 0x0000019A | [**サイロ\_へ\_の\_アタッチ中に\_ワーカースレッドが\_返されました\_** ](bug-check-0x19a--worker-thread-returned-while-attached-to-silo.md)                      |
| 0x0000019B | [**TTM\_の\_致命的なエラー**](bug-check-0x19b--ttm-fatal-error.md)                                                                                      |
| 0x0000019C | [**WIN32K\_電源\_ウォッチドッグ\_のタイムアウト**](bug-check-0x19c--win32k-power-watchdog-timeout.md)                                                         |
| 0x0000019D | [**クラスター\_SVHDX\_LIVEDUMP**](bug-check-0x19d--cluster-svhdx-livedump.md)                                                                        |
| 0x000001A0 | [**TTM\_ウォッチ\_ドッグのタイムアウト**](bug-check-0x1a0--ttm-watchdog-timeout.md)                                                                            |
| 0x000001A3 | [**呼び出し\_でウォッチ\_ドッグ\_\_タイムアウト\_LIVEDUMPが返されませんでした\_** ](bug-check-0x1a3--call-has-not-returned-watchdog-timeout-livedump.md)                  |
| 0x000001A4 | [**DRIPS\_SW\_HW分岐\_LIVEDUMP\_** ](bug-check-0x1a4--drips-sw-hw-divergence-livedump.md)                                                    |
| 0x000001A5 | [**USB\_DRIPS\_ブロックの\_突然の\_削除 LIVEDUMP\_** ](bug-check-0x1a5--usb-drips-blocker-surprise-removal-livedump.md)                           |
| 0x000001A6 | [**BLUETOOTH\_エラー\_回復LIVEDUMP\_** ](bug-check-0x1a6--bluetooth-error-recovery-livedump.md)                                                 |
| 0x000001A7 | [**SMB\_リダイレクター\_LIVEDUMP**](bug-check-0x1A7--smb-redirector-livedump.md)                                                                       |
| 0x000001A8 | [**VIDEO\_DXGKRNL\_BLACKSCREEN\_LIVEDUMP\_** ](bug-check-0x1a8--video-dxgkrnl-black-screen-livedump.md)                                            |
| 0x000001B0 | [**VIDEO_MINIPORT_FAILED_LIVEDUMP**](bug-check-0x1b0--video-miniport-failed-livedump.md)                                                          |
| 0x000001C4 | [**ドライバー\_検証\_ツール\_が違反\_LIVEDUMP を検出しました**](bug-check-0x1c4--driver-verifier-detected-violation-livedump.md)                            |
| 0x000001C5 | [**IO\_THREADPOOL\_デッドロック\_LIVEDUMP**](bug-check-0x1c5--io-threadpool-deadlock-livedump.md)                                                     |
| 0x000001C6 | [**FAST\_\_÷\_の前提条件違反**](bug-check-0x1c6--fast-eresource-precondition-violation.md)                                         |
| 0x000001C7 | [**データ\_構造の\_破損を格納する\_** ](bug-check-0x1c7--store-data-structure-corruption.md)                                                     |
| 0x000001C8 | [**手動\_で\_開始\_さ\_れた電源ボタンの保持**](bug-check-0x1c8--manually-initiated-power-button-hold.md)                                          |
| 0x000001C9 | [**ユーザー\_モード\_のヘルス\_モニターLIVEDUMP\_** ](bug-check-0x1c9--user-mode-health-monitor-livedump.md)                                                |
| 0x000001CA | [**合成\_ウォッチ\_ドッグのタイムアウト**](bug-check-0x1ca--synthetic-watchdog-timeout.md)                                                                |
| 0x000001CB | [**無効\_な\_サイロデタッチ**](bug-check-0x1cb--invalid-silo-detach.md)                                                                              |
| 0x000001CC | [**EXRESOURCE_TIMEOUT_LIVEDUMP**](bug-check-0x1cc--exresource-timeout-livedump.md)                                                                |
| 0x000001CD | [**コール\_バック\_STACK_ADDRESS が無効です**](bug-check-0x1cd--invalid-callback-stack-address.md)                                                        |
| 0x000001CE | [**無効\_な\_カーネルスタック\_アドレス**](bug-check-0x1ce--invalid-kernel-stack-address.md)                                                           |
| 0x000001CF | [**ハードウェア\_ウォッチ\_ドッグのタイムアウト**](bug-check-0x1cf--hardware-watchdog-timeout.md)                                                                  |  
| 0x000001D0 | [**CPI\_ファームウェア\_ウォッチドッグ\_のタイムアウト**](bug-check-0x1d0--acpi-firmware-watchdog-timeout.md)                                                        |
| 0x000001D1 | [**テレメトリ\_アサート\_LIVEDUMP**](bug-check-0x1d1--telemetry-asserts-livedump.md)                                                                |
| 0x000001D2 | [**ワーカー\_\_スレッド\_の状態が無効です**](bug-check-0x1d2--worker-thread-invalid-state.md)                                                             |
| 0x000001D3 | [**WFP\_の\_無効な操作**](bug-check-0x1d3--wfp-invalid-operation.md)                                                                          |
| 0x000001D4 | [**UCMUCSI\_LIVEDUMP**](bug-check-0x1d4--ucmusci-livedump.md)                                                                                     |
| 0x000001D5 | [**DRIVER_PNP_WATCHDOG**](bug-check-0x1d5--driver-pnp-watchdog.md)                                                                                |
| 0x000001D6 | [**既定\_\_\_\_以外のワークロード\_クラスで返されるワーカースレッド\_\_** ](bug-check-0x1d6--worker-thread-returned-with-non-default-workload-class.md)   |
| 0x000001D7 | [**EFS\_の\_致命的なエラー**](bug-check-0x1d7--efs-fatal-error.md)                                                                                      |
| 0x000001D8 | [**UCMUCSI\_の失敗**](bug-check-0x1d8--ucmucsi-failure.md)                                                                                       |
| 0x000001D9 | [**HAL\_の\_IOMMU内部\_エラー**](bug-check-0x1d8--ucmucsi-failure.md)                                                                            |
| 0x000001DB | [**IPI\_ウォッチ\_ドッグのタイムアウト**](bug-check-0x1db--ipi-watchdog-timeout.md)                                                                            |
| 0x000001DC | [**DMA_COMMON_BUFFER_VECTOR_ERROR**](bug-check-0x1dc--dma-common-buffer-vector-error.md)                                                          |
| 0x00000356 | [**XBOX\_ERACTRL\_CSタイムアウト\_** ](bug-check-0x356--xbox-eractrl-cs-timeout.md)                                                                     |
| 0x00000BFE | [**BC\_BLUETOOTH\_検証ツール\_のエラー**](bug-check-0xbfe--bc-bluetooth-verifier-fault.md)                                                             |
| 0x00000BFF | [**BC\_BTHMINI\_検証\_ツールのエラー**](bug-check-0xbff--bc-bthmini-verifier-fault.md)                                                                 |
| 0x00020001 | [**ハイパー\_バイザーエラー**](bug-check-0x20001--hypervisor-error.md)                                                                                   |
| 0x1000007E | [**システム\_スレッド\_の例外\_\_が処理\_されませんでした M**](bug-check-0x1000007e--system-thread-exception-not-handled-m.md)                                  |
| 0x1000007F | [**予期\_し\_ない\_カーネルモードトラップ\_M**](bug-check-0x1000007f--unexpected-kernel-mode-trap-m.md)                                                   |
| 0x1000008E | [**カーネル\_モード\_例外\_が処理さ\_れませんでした M\_** ](bug-check-0x1000008e--kernel-mode-exception-not-handled-m.md)                                      |
| 0x100000EA | [**デバイス\_ドライバー\_\_\_Mで\_のスレッドスタック**](bug-check-0x100000ea--thread-stuck-in-device-driver-m.md)                                              |
| 0x4000008A | [ **\_保持\_されて\_いるスレッド終了ミューテックス**](bug-check-0x4000008a--thread-terminate-held-mutex.md)                                                        |
| 0xC0000218 | [**ステータス\_はレジストリ\_\_ファイルを読み込めませ\_ん**](bug-check-0xc0000218--status-cannot-load-registry-file.md)                                             |
| 0xC000021A | [**WINLOGON\_の\_致命的なエラー**](bug-check-0xc000021a--winlogin-fatal-error.md)                                              |
| 0xC0000221 | [**ステータス\_\_イメージ\_のチェックサムが一致しません**](bug-check-0xc0000221--status-image-checksum-mismatch.md)                                                  |
| 0xDEADDEAD | [**手動\_で\_開始された CRASH1**](bug-check-0xdeaddead--manually-initiated-crash1.md)                                                             |
