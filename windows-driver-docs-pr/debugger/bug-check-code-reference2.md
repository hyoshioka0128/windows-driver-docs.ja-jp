---
title: バグ チェック コード リファレンス
description: ここでは、ブルースクリーンに渡されるパラメーターなど、一般的なバグチェックについて説明します。
ms.assetid: DBA85578-97CF-4BD7-A67D-1C7AD2E9B2BB
ms.date: 02/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: 07a5afbc115331b6b2e8ff726bfa2806c19e278a
ms.sourcegitcommit: f931a1bad4132c07be5966b428c77745c96bcba4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2020
ms.locfileid: "77248035"
---
# <a name="bug-check-code-reference"></a>バグ チェック コード リファレンス

ここでは、青のバグチェック画面にエラーコードと共に表示されるパラメーターなど、一般的なバグチェックコードについて説明します。 このセクションでは、バグチェックにつながるエラーを診断する方法と、エラーに対処するための方法についても説明します。

> [!NOTE] 
> このトピックはプログラマーを対象としています。 システムにバグチェックコードを含むブルースクリーンが表示されているお客様の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://go.microsoft.com/fwlink/p/?linkid=183646)」を参照してください。

この参照に特定のバグチェックコードが表示されない場合は、次の構文 (カーネルモードの場合) を使用して、Windows デバッガー (WinDbg) の[ **! analyze**](-analyze.md)拡張機能を使用して、`<code>` をバグチェックコードに置き換えます。

`!analyze -show <code>`

このコマンドを入力すると、WinDbg は、指定されたバグチェックコードに関する情報を表示します。 既定の基数 (基数) が16でない場合は、プレフィックスが**0x**で `<code>` ます。

次の表は、各バグチェックコードのコードと名前を示しています。

| コード       | Name                                                                                                                                              |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| 0x00000001 | [**APC\_インデックス\_不一致**](bug-check-0x1--apc-index-mismatch.md)                                                                                  |
| 0x00000002 | [**デバイス\_キュー\_\_ビジー状態です**](bug-check-0x2--device-queue-not-busy.md)                                                                           |
| 0x00000003 | [**無効な\_関係\_セット**](bug-check-0x3--invalid-affinity-set.md)                                                                              |
| 0x00000004 | [ **\_データ\_アクセス\_トラップが無効です**](bug-check-0x4--invalid-data-access-trap.md)                                                                     |
| 0x00000005 | [**無効な\_プロセス\_アタッチ\_試行**](bug-check-0x5--invalid-process-attach-attempt.md)                                                         |
| 0x00000006 | [**無効な\_プロセス\_デタッチ\_試行**](bug-check-0x6--invalid-process-detach-attempt.md)                                                         |
| 0x00000007 | [**無効な\_ソフトウェア\_割り込み**](bug-check-0x7--invalid-software-interrupt.md)                                                                  |
| 0x00000008 | [**IRQL\_ディスパッチ\_レベル\_いません**](bug-check-0x8--irql-not-dispatch-level.md)                                                                       |
| 0x00000009 | [**IRQL\_\_より大きい\_または\_等しい**](bug-check-0x9--irql-not-greater-or-equal.md)                                                                  |
| Stop | [**IRQL\_少ない\_または\_等しい\_ない**](bug-check-0xa--irql-not-less-or-equal.md)                                                                        |
| 0x0000000B | [ **\_サポートの処理\_\_例外はありません**](bug-check-0xb--no-exception-handling-support.md)                                                           |
| 0x0000000C | [ **\_オブジェクト\_最大\_待機しています**](bug-check-0xc--maximum-wait-objects-exceeded.md)                                                           |
| 0x0000000D | [**MUTEX\_レベル\_NUMBER\_違反**](bug-check-0xd--mutex-level-number-violation.md)                                                             |
| 0x0000000E | [ **\_ユーザー\_モード\_コンテキストがありません**](bug-check-0xe--no-user-mode-context.md)                                                                             |
| 0x0000000F | [**既に\_所有されているスピン\_ロック\_** ](bug-check-0xf--spin-lock-already-owned.md)                                                                       |
| 0x00000010 | [**スピン\_ロック\_\_所有されていません**](bug-check-0x10--spin-lock-not-owned.md)                                                                              |
| 0x00000011 | [**スレッド\_\_MUTEX\_所有者ではありません**](bug-check-0x11--thread-not-mutex-owner.md)                                                                        |
| 0x00000012 | [**トラップ\_原因\_不明**](bug-check-0x12--trap-cause-unknown.md)                                                                                 |
| 0x00000013 | [**空の\_スレッド\_REAPER\_LIST**](bug-check-0x13--empty-thread-reaper-list.md)                                                                    |
| 0x00000014 | [**ロック\_ロックされていない\_ロック\_作成\_削除**](bug-check-0x14--create-delete-lock-not-locked.md)                                                         |
| 0x00000015 | [ **\_KMODE から\_呼び出された最後の\_\_** ](bug-check-0x15--last-chance-called-from-kmode.md)                                                         |
| 0x00000016 | [**CID\_\_作成の処理**](bug-check-0x16--cid-handle-creation.md)                                                                               |
| 0x00000017 | [**CID\_\_削除の処理**](bug-check-0x17--cid-handle-deletion.md)                                                                               |
| 0x00000018 | [ **\_ポインターによる\_の参照**](bug-check-0x18--reference-by-pointer.md)                                                                             |
| 0x00000019 | [ **\_プール\_ヘッダーが正しくありません**](bug-check-0x19--bad-pool-header.md)                                                                                       |
| 0x0000001A | [**メモリ\_管理**](bug-check-0x1a--memory-management.md)                                                                                    |
| 0x0000001B | [**PFN\_共有の\_数**](bug-check-0x1b--pfn-share-count.md)                                                                                       |
| 0x0000001C | [**PFN\_参照\_カウント**](bug-check-0x1c--pfn-reference-count.md)                                                                               |
| 0x0000001D | [ **\_スピン\_ロック\_使用できません**](bug-check-0x1d--no-spin-lock-available.md)                                                                        |
| 0x0000001E | [**KMODE\_例外\_\_処理されません**](bug-check-0x1e--kmode-exception-not-handled.md)                                                              |
| 0x0000001F | [**共有\_リソース\_CONV\_エラー**](bug-check-0x1f--shared-resource-conv-error.md)                                                                |
| 0x00000020 | [**カーネル\_APC\_保留中の\_\_終了中**](bug-check-0x20--kernel-apc-pending-during-exit.md)                                                       |
| 0x00000021 | [**クォータの\_アンダーフロー**](bug-check-0x21--quota-underflow.md)                                                                                        |
| 0x00000022 | [**ファイル\_システム**](bug-check-0x22--file-system.md)                                                                                                |
| 0x00000023 | [**FAT\_ファイル\_システム**](bug-check-0x23--fat-file-system.md)                                                                                       |
| 0x00000024 | [**NTFS\_ファイル\_システム**](bug-check-0x24--ntfs-file-system.md)                                                                                     |
| 0x00000025 | [**NPFS\_ファイル\_システム**](bug-check-0x25--npfs-file-system.md)                                                                                     |
| 0x00000026 | [**CDFS\_ファイル\_システム**](bug-check-0x26--cdfs-file-system.md)                                                                                     |
| 0x00000027 | [**RDR\_ファイル\_システム**](bug-check-0x27--rdr-file-system.md)                                                                                       |
| 0x00000028 | [ **\_アクセス\_トークンが壊れています**](bug-check-0x28--corrupt-access-token.md)                                                                             |
| 0x00000029 | [**セキュリティ\_システム**](bug-check-0x29--security-system.md)                                                                                        |
| 0x0000002A | [ **\_IRP に整合性がありません**](bug-check-0x2a--inconsistent-irp.md)                                                                                      |
| 0x0000002B | [**パニック\_STACK\_スイッチ**](bug-check-0x2b--panic-stack-switch.md)                                                                                 |
| 0x0000002C | [**ポート\_ドライバー\_内部**](bug-check-0x2c--port-driver-internal.md)                                                                             |
| 0x0000002D | [**SCSI\_ディスク\_ドライバー\_内部**](bug-check-0x2d--scsi-disk-driver-internal.md)                                                                  |
| 0x0000002E | [**データ\_バス\_エラー**](bug-check-0x2e--data-bus-error.md)                                                                                         |
| 0x0000002F | [**命令\_BUS\_エラー**](bug-check-0x2f--instruction-bus-error.md)                                                                           |
| 0x00000030 | [**無効な\_コンテキストの\_の設定\_** ](bug-check-0x30--set-of-invalid-context.md)                                                                        |
| 0x00000031 | [**フェーズ 0\_の初期化\_に失敗しました**](bug-check-0x31--phase0-initialization-failed.md)                                                             |
| 0x00000032 | [**PHASE1\_の初期化\_に失敗しました**](bug-check-0x32--phase1-initialization-failed.md)                                                             |
| 0x00000033 | [**予期しない\_初期化\_呼び出し**](bug-check-0x33--unexpected-initialization-call.md)                                                         |
| 0x00000034 | [**キャッシュ\_マネージャー**](bug-check-0x34--cache-manager.md)                                                                                            |
| 0x00000035 | [ **\_IRP\_スタック\_の場所を\_ません**](bug-check-0x35--no-more-irp-stack-locations.md)                                                             |
| 0x00000036 | [**デバイス\_参照\_カウント\_0\_ない**](bug-check-0x36--device-reference-count-not-zero.md)                                                     |
| 0x00000037 | [**フロッピー\_内部\_エラー**](bug-check-0x37--floppy-internal-error.md)                                                                           |
| 0x00000038 | [**シリアル\_ドライバー\_内部**](bug-check-0x38--serial-driver-internal.md)                                                                         |
| 0x00000039 | [**ミューテックス\_所有\_システム\_終了**](bug-check-0x39--system-exit-owned-mutex.md)                                                                      |
| 0x0000003A | [**システム\_前の\_ユーザー\_アンワインド**](bug-check-0x3a--system-unwind-previous-user.md)                                                              |
| 0x0000003B | [**システム\_サービス\_例外**](bug-check-0x3b--system-service-exception.md)                                                                     |
| 0x0000003C | [**中断\_のアンワインド\_試行**](bug-check-0x3c--interrupt-unwind-attempted.md)                                                                 |
| 0x0000003D | [**割り込み\_例外\_\_処理されません**](bug-check-0x3d--interrupt-exception-not-handled.md)                                                      |
| 0x0000003E | [**マルチプロセッサ\_構成\_\_サポートされていません**](bug-check-0x3e--multiprocessor-configuration-not-supported.md)                                |
| 0x0000003F | [ **\_システム\_の\_はありません**](bug-check-0x3f--no-more-system-ptes.md)                                                                              |
| 0x00000040 | [**ターゲット\_MDL\_が小さすぎる\_** ](bug-check-0x40--target-mdl-too-small.md)                                                                            |
| 0x00000041 | [ **\_プール\_空に\_必要があります**](bug-check-0x41--must-succeed-pool-empty.md)                                                                      |
| 0x00000042 | [**ATDISK\_ドライバー\_内部**](bug-check-0x42--atdisk-driver-internal.md)                                                                         |
| 0x00000043 | [ **\_パーティションには\_がありません**](bug-check-0x43--no-such-partition.md)                                                                                   |
| 0x00000044 | [**複数の\_IRP\_\_要求を完了しました**](bug-check-0x44--multiple-irp-complete-requests.md)                                                        |
| 0x00000045 | [ **\_システム\_マップ\_REGS が不十分です**](bug-check-0x45--insufficient-system-map-regs.md)                                                            |
| 0x00000046 | [**DEREF\_ログオン\_セッション\_不明です**](bug-check-0x46--deref-unknown-logon-session.md)                                                              |
| 0x00000047 | [**参照\_不明\_ログオン\_セッション**](bug-check-0x47--ref-unknown-logon-session.md)                                                                  |
| 0x00000048 | [ **\_完了\_IRP で\_状態\_を取り消す**](bug-check-0x48--cancel-state-in-completed-irp.md)                                                         |
| 0x00000049 | [ **\_割り込み\_オフになっているページ\_フォールト\_** ](bug-check-0x49--page-fault-with-interrupts-off.md)                                                       |
| 0x0000004A | [ **\_システム\_サービスでは、IRQL\_GT\_ゼロ\_** ](bug-check-0x4a--irql-gt-zero-at-system-service.md)                                                      |
| 0x0000004B | [**内部\_エラー\_ストリーム**](bug-check-0x4b--streams-internal-error.md)                                                                         |
| 0x0000004C | [**致命的な\_処理されていない\_ハード\_エラー**](bug-check-0x4c--fatal-unhandled-hard-error.md)                                                                |
| 0x0000004D | [ **\_ページ\_使用できません**](bug-check-0x4d--no-pages-available.md)                                                                                 |
| 0x0000004E | [**PFN\_リスト\_破損しています**](bug-check-0x4e--pfn-list-corrupt.md)                                                                                     |
| 0x0000004F | [**NDIS\_内部\_エラー**](bug-check-0x4f--ndis-internal-error.md)                                                                               |
| 0x00000050 | [ **\_非ページ\_領域でのページ\_エラー\_** ](bug-check-0x50--page-fault-in-nonpaged-area.md)                                                             |
| 0x00000051 | [**レジストリ\_エラー**](bug-check-0x51--registry-error.md)                                                                                          |
| 0x00000052 | [**メールスロット\_ファイル\_システム**](bug-check-0x52--mailslot-file-system.md)                                                                             |
| 0x00000053 | [ **\_ブート\_デバイスがありません**](bug-check-0x53--no-boot-device.md)                                                                                         |
| 0x00000054 | [**LM\_SERVER\_内部\_エラー**](bug-check-0x54--lm-server-internal-error.md)                                                                    |
| 0x00000055 | [**データ\_一貫性\_例外**](bug-check-0x55--data-coherency-exception.md)                                                                     |
| 0x00000056 | [**命令\_一貫性\_例外**](bug-check-0x56--instruction-coherency-exception.md)                                                       |
| 0x00000057 | [**XNS\_内部\_エラー**](bug-check-0x57--xns-internal-error.md)                                                                                 |
| 0x00000058 | [**FTDISK\_内部\_エラー**](bug-check-0x58--ftdisk-internal-error.md)                                                                           |
| 0x00000059 | [**ピンピン\_ファイル\_システム**](bug-check-0x59--pinball-file-system.md)                                                                               |
| 0x0000005A | [**重大な\_サービス\_に失敗しました**](bug-check-0x5a--critical-service-failed.md)                                                                       |
| 0x0000005B | [ **\_ENV\_VAR\_を設定できませんでした**](bug-check-0x5b--set-env-var-failed.md)                                                                                |
| 0x0000005C | [**HAL\_初期化\_に失敗しました**](bug-check-0x5c--hal-initialization-failed.md)                                                                   |
| 0x0000005D | [**サポートされていない\_プロセッサ**](bug-check-0x5d--unsupported-processor.md)                                                                            |
| 0x0000005E | [**オブジェクト\_初期化\_に失敗しました**](bug-check-0x5e--object-initialization-failed.md)                                                             |
| 0x0000005F | [**セキュリティ\_の初期化\_失敗しました**](bug-check-0x5f--security-initialization-failed.md)                                                         |
| 0x00000060 | [**プロセス\_初期化\_に失敗しました**](bug-check-0x60--process-initialization-failed.md)                                                           |
| 0x00000061 | [**HAL1\_の初期化\_に失敗しました**](bug-check-0x61--hal1-initialization-failed.md)                                                                 |
| 0x00000062 | [**OBJECT1\_の初期化\_に失敗しました**](bug-check-0x62--object1-initialization-failed.md)                                                           |
| 0x00000063 | [**SECURITY1\_の初期化\_に失敗しました**](bug-check-0x63--security1-initialization-failed.md)                                                       |
| 0x00000064 | [**シンボリック\_初期化\_に失敗しました**](bug-check-0x64--symbolic-initialization-failed.md)                                                         |
| 0x00000065 | [**MEMORY1\_の初期化\_に失敗しました**](bug-check-0x65--memory1-initialization-failed.md)                                                           |
| 0x00000066 | [**キャッシュ\_の初期化\_に失敗しました**](bug-check-0x66--cache-initialization-failed.md)                                                               |
| 0x00000067 | [**構成\_の初期化\_に失敗しました**](bug-check-0x67--config-initialization-failed.md)                                                             |
| 0x00000068 | [**ファイル\_初期化\_に失敗しました**](bug-check-0x68--file-initialization-failed.md)                                                                 |
| 0x00000069 | [**IO1\_の初期化\_に失敗しました**](bug-check-0x69--io1-initialization-failed.md)                                                                   |
| 0x0000006A | [**LPC\_初期化\_に失敗しました**](bug-check-0x6a--lpc-initialization-failed.md)                                                                   |
| 0x0000006B | [**PROCESS1\_の初期化\_FAILE**](bug-check-0x6b--process1-initialization-failed.md)A                                                         |
| 0x0000006C | [**REFMON\_初期化\_に失敗しました**](bug-check-0x6c--refmon-initialization-failed.md)                                                             |
| 0x0000006D | [**SESSION1\_の初期化\_に失敗しました**](bug-check-0x6d--session1-initialization-failed.md)                                                         |
| 0x0000006E | [**SESSION2\_の初期化\_に失敗しました**](bug-check-0x6e--session2-initialization-failed.md)                                                         |
| 0x0000006F | [**SESSION3\_の初期化\_に失敗しました**](bug-check-0x6f--session3-initialization-failed.md)                                                         |
| 0x00000070 | [**SESSION4\_の初期化\_に失敗しました**](bug-check-0x70--session4-initialization-failed.md)                                                         |
| 0x00000071 | [**SESSION5\_の初期化\_に失敗しました**](bug-check-0x71--session5-initialization-failed.md)                                                         |
| 0x00000072 | [ **\_ドライブ\_文字の割り当て\_失敗しました**](bug-check-0x72--assign-drive-letters-failed.md)                                                              |
| 0x00000073 | [**構成\_一覧を\_できませんでした**](bug-check-0x73--config-list-failed.md)                                                                                 |
| 0x00000074 | [**無効な\_システム\_構成\_情報**](bug-check-0x74--bad-system-config-info.md)                                                                        |
| 0x00000075 | [ **\_構成\_書き込むことができません**](bug-check-0x75--cannot-write-configuration.md)                                                                 |
| 0x00000076 | [**プロセス\_に\_ページが\_ロックされています**](bug-check-0x76--process-has-locked-pages.md)                                                                    |
| 0x00000077 | [**カーネル\_スタック\_INPAGE\_エラー**](bug-check-0x77--kernel-stack-inpage-error.md)                                                                  |
| 0x00000078 | [**フェーズ 0\_例外**](bug-check-0x78--phase0-exception.md)                                                                                      |
| 0x00000079 | [ **\_HAL が一致しません**](bug-check-0x79--mismatched-hal.md)                                                                                          |
| 0x0000007A | [**カーネル\_データ\_INPAGE\_エラー**](bug-check-0x7a--kernel-data-inpage-error.md)                                                                    |
| 0x0000007B | [**ブート\_デバイスにアクセスできない\_** ](bug-check-0x7b--inaccessible-boot-device.md)                                                                     |
| 0x0000007C | [ **\_NDIS\_ドライバーのバグコード**](bug-check-0x7c--bugcode-ndis-driver.md)                                                                               |
| 0x0000007D | [ **\_メモリの\_をインストールする**](bug-check-0x7d--install-more-memory.md)                                                                               |
| 0x0000007E | [**システム\_スレッド\_例外\_処理\_れていません**](bug-check-0x7e--system-thread-exception-not-handled.md)                                             |
| 0x0000007F | [**予期しない\_カーネル\_モード\_トラップ**](bug-check-0x7f--unexpected-kernel-mode-trap.md)                                                              |
| 0x00000080 | [**NMI\_ハードウェア\_障害**](bug-check-0x80--nmi-hardware-failure.md)                                                                             |
| 0x00000081 | [**スピン\_ロック\_INIT\_エラー**](bug-check-0x81--spin-lock-init-failure.md)                                                                        |
| 0x00000082 | [**DFS\_ファイル\_システム**](bug-check-0x82--dfs-file-system.md)                                                                                       |
| 0x00000085 | [**セットアップ\_エラー**](bug-check-0x85--setup-failure.md)                                                                                            |
| 0x0000008B | [**MBR\_チェックサム\_不一致**](bug-check-0x8b--mbr-checksum-mismatch.md)                                                                           |
| 0x0000008E | [**カーネル\_モード\_例外\_処理\_れていません**](bug-check-0x8e--kernel-mode-exception-not-handled.md)                                                 |
| 0x0000008F | [**PP0\_の初期化\_に失敗しました**](bug-check-0x8f--pp0-initialization-failed.md)                                                                   |
| 0x00000090 | [**PP1\_の初期化\_に失敗しました**](bug-check-0x90--pp1-initialization-failed.md)                                                                   |
| 0x00000092 | [ **\_MP\_システム上の\_ドライバー\_** ](bug-check-0x92--up-driver-on-mp-system.md)                                                                       |
| 0x00000093 | [ **\_カーネル\_ハンドルが無効です**](bug-check-0x93--invalid-kernel-handle.md)                                                                           |
| 0x00000094 | [**カーネル\_スタック\_\_終了時にロックされた\_** ](bug-check-0x94--kernel-stack-locked-at-exit.md)                                                             |
| 0x00000096 | [**無効な\_作業\_キュー\_項目**](bug-check-0x96--invalid-work-queue-item.md)                                                                      |
| 0x00000097 | [**バインドされた\_イメージ\_サポートされていません**](bug-check-0x97--bound-image-unsupported.md)                                                                       |
| 0x00000098 | [ **\_NT\_評価\_期間の終了\_** ](bug-check-0x98--end-of-nt-evaluation-period.md)                                                             |
| 0x00000099 | [**無効な\_領域\_または\_セグメント**](bug-check-0x99--invalid-region-or-segment.md)                                                                  |
| 0x0000009A | [**システム\_ライセンス\_違反**](bug-check-0x9a--system-license-violation.md)                                                                     |
| 0x0000009B | [**UDF\_ファイル\_システム**](bug-check-0x9b--udfs-file-system.md)                                                                                     |
| 0x0000009C | [**コンピューター\_チェック\_例外**](bug-check-0x9c--machine-check-exception.md)                                                                       |
| 0x0000009E | [**ユーザー\_モード\_正常性\_モニター**](bug-check-0x9e--user-mode-health-monitor.md)                                                                    |
| 0x0000009F | [**ドライバー\_電源\_状態\_エラー**](bug-check-0x9f--driver-power-state-failure.md)                                                                |
| 0x000000A0 | [**内部\_電源\_エラー**](bug-check-0xa0--internal-power-error.md)                                                                             |
| 0x000000A1 | [**PCI\_BUS\_ドライバー\_内部**](bug-check-0xa1--pci-bus-driver-internal.md)                                                                      |
| 0x000000A2 | [**メモリ\_イメージ\_破損しています**](bug-check-0xa2--memory-image-corrupt.md)                                                                             |
| 0x000000A3 | [**ACPI\_ドライバー\_内部**](bug-check-0xa3--acpi-driver-internal.md)                                                                             |
| 0x000000A4 | [**CNSS\_ファイル\_システム\_フィルター**](bug-check-0xa4--cnss-file-system-filter.md)                                                                      |
| 0x000000A5 | [**ACPI\_BIOS\_エラー**](bug-check-0xa5--acpi-bios-error.md)                                                                                       |
| 0x000000A7 | [**不適切な\_EXHANDLE です**](bug-check-0xa7--bad-exhandle.md)                                                                                              |
| 0x000000AB | [**セッション\_は\_終了時に有効な\_プール\_\_** ](bug-check-0xab--session-has-valid-pool-on-exit.md)                                                      |
| 0x000000AC | [**HAL\_メモリ\_割り当て**](bug-check-0xac--hal-memory-allocation.md)                                                                           |
| 0x000000AD | [**ビデオ\_ドライバー\_デバッグ\_レポート\_要求**](bug-check-0xad--video-driver-debug-report-request.md)                                                 |
| 0x000000B1 | [**BGI\_検出\_違反**](bug-check-0xb1--bgi-detected-violation.md)                                                                         |
| 0x000000B4 | [**ビデオ\_ドライバー\_INIT\_エラー**](bug-check-0xb4--video-driver-init-failure.md)                                                                  |
| 0x000000B8 | [ **\_DPC からの\_の切り替え\_試行しました**](bug-check-0xb8--attempted-switch-from-dpc.md)                                                                  |
| 0x000000B9 | [**チップセット\_\_エラーが検出されました**](bug-check-0xb9--chipset-detected-error.md)                                                                         |
| 0x000000BA | [**セッション\_には\_終了時\_有効な\_ビューが\_** ](bug-check-0xba--session-has-valid-views-on-exit.md)                                                    |
| 0x000000BB | [**ネットワーク\_ブート\_の初期化\_失敗しました**](bug-check-0xbb--network-boot-initialization-failed.md)                                                |
| 0x000000BC | [**ネットワーク\_ブート\_重複する\_アドレス**](bug-check-0xbc--network-boot-duplicate-address.md)                                                        |
| 0x000000BD | [**無効な\_休止状態\_状態**](bug-check-0xbd--invalid-hibernated-state.md)                                                                     |
| 0x000000BE | [**読み取り専用\_メモリ\_への\_書き込み\_試行しました**](bug-check-0xbe--attempted-write-to-readonly-memory.md)                                               |
| 0x000000BF | [**ミューテックスは既に所有\_\_** ](bug-check-0xbf--mutex-already-owned.md)                                                                               |
| 0x000000C1 | [**特別な\_プール\_検出されたメモリ\_破損\_** ](bug-check-0xc1--special-pool-detected-memory-corruption.md)                                     |
| 0x000000C2 | [ **\_プール\_呼び出し元が正しくありません**](bug-check-0xc2--bad-pool-caller.md)                                                                                       |
| 0x000000C4 | [**DRIVER\_VERIFIER\_検出された\_違反**](bug-check-0xc4--driver-verifier-detected-violation.md)                                                |
| 0x000000C5 | [**ドライバー\_\_EXPOOL に破損しています**](bug-check-0xc5--driver-corrupted-expool.md)                                                                       |
| 0x000000C6 | [**プール\_\_解放**](bug-check-0xc6--driver-caught-modifying-freed-pool.md)された\_を変更するためにドライバー\_キャッチされました左右                                               |
| 0x000000C7 | [**タイマー\_または\_DPC\_無効**](bug-check-0xc7--timer-or-dpc-invalid.md)                                                                            |
| 0x000000C8 | [**IRQL\_予期しない\_値です**](bug-check-0xc8--irql-unexpected-value.md)                                                                           |
| 0x000000C9 | [**IOMANAGER\_違反\_ドライバー\_検証**](bug-check-0xc9--driver-verifier-iomanager-violation.md)                                              |
| 0x000000CA | [**PNP\_\_致命的\_エラーが検出されました**](bug-check-0xca--pnp-detected-fatal-error.md)                                                                    |
| 0x000000CB | [ **\_プロセスで\_ロックされている\_\_ページの\_ドライバー**](bug-check-0xcb--driver-left-locked-pages-in-process.md)                                            |
| 0x000000CC | [ **\_解放された\_特別な\_プールのページ\_フォールト\_** ](bug-check-0xcc--page-fault-in-freed-special-pool.md)                                                  |
| 0x000000CD | [ **\_割り当ての\_終了\_を超えるページ\_フォールト\_** ](bug-check-0xcd--page-fault-beyond-end-of-allocation.md)                                            |
| 0x000000CE | [ **\_保留中の\_操作をキャンセル\_ない状態で、ドライバー\_アンロード\_** ](bug-check-0xce--driver-unloaded-without-cancelling-pending-operations.md)        |
| 0x000000CF | [**ターミナル\_SERVER\_ドライバー\_\_正しくない\_メモリ\_参照**](bug-check-0xcf--terminal-server-driver-made-incorrect-memory-reference.md)     |
| 0x000000D0 | [**ドライバー\_\_MMPOOL に破損しています**](bug-check-0xd0--driver-corrupted-mmpool.md)                                                                       |
| 0x000000D1 | [**ドライバー\_IRQL\_\_少ない\_または\_等しい**](bug-check-0xd1--driver-irql-not-less-or-equal.md)                                                        |
| 0x000000D2 | [**バグコード\_ID\_ドライバー**](bug-check-0xd2--bugcode-id-driver.md)                                                                                   |
| 0x000000D3 | [**ドライバー\_部分\_を非ページ化\_\_必要があります**](bug-check-0xd3--driver-portion-must-be-nonpaged.md)                                                     |
| 0x000000D4 | [**システム\_スキャン\_\_発生した\_IRQL\_\_不適切な\_ドライバー\_アンロード**](bug-check-0xd4--system-scan-at-raised-irql-caught-improper-driver-unlo.md) |
| 0x000000D5 | [**ドライバー\_ページ\_フォールト\_\_解放され\_特別な\_プール**](bug-check-0xd5--driver-page-fault-in-freed-special-pool.md)                                   |
| 0x000000D6 | [**ドライバー\_ページ\_フォールト\_\_割り当ての\_エンド\_を超えています**](bug-check-0xd6--driver-page-fault-beyond-end-of-allocation.md)                             |
| 0x000000D7 | [**無効な\_ビュー\_マッピングを解除\_ドライバー**](bug-check-0xd7--driver-unmapping-invalid-view.md)                                                          |
| 0x000000D8 | [**過剰\_の PTE\_使用されているドライバー\_** ](bug-check-0xd8--driver-used-excessive-ptes.md)                                                                |
| 0x000000D9 | [**ロックされた\_ページ\_トラッカー\_破損**](bug-check-0xd9--locked-pages-tracker-corruption.md)                                                      |
| 0x000000DA | [**システム\_の PTE\_誤用**](bug-check-0xda--system-pte-misuse.md)                                                                                   |
| 0x000000DB | [**ドライバー\_破損\_SYSPTES**](bug-check-0xdb--driver-corrupted-sysptes.md)                                                                     |
| 0x000000DC | [**ドライバー\_無効な\_スタック\_アクセス**](bug-check-0xdc--driver-invalid-stack-access.md)                                                              |
| 0x000000DE | [**プール\_破損\_\_ファイル\_領域**](bug-check-0xde--pool-corruption-in-file-area.md)                                                           |
| 0x000000DF | [ **\_WORKER\_スレッド**を行う](bug-check-0xdf--impersonating-worker-thread.md)                                                               |
| 0x000000E0 | [**ACPI\_BIOS\_致命的\_エラー**](bug-check-0xe0--acpi-bios-fatal-error.md)                                                                          |
| 0x000000E1 | [**ワーカー\_スレッド\_\_不良\_IRQL に\_返されました**](bug-check-0xe1--worker-thread-returned-at-bad-irql.md)                                              |
| 0x000000E2 | [**手動\_開始\_クラッシュ**](bug-check-0xe2--manually-initiated-crash.md)                                                                     |
| 0x000000E3 | [**リソース\_\_所有されていません**](bug-check-0xe3--resource-not-owned.md)                                                                                 |
| 0x000000E4 | [**ワーカー\_無効です**](bug-check-0xe4--worker-invalid.md)                                                                                          |
| 0x000000E6 | [**ドライバー\_VERIFIER\_DMA\_違反**](bug-check-0xe6--driver-verifier-dma-violation.md)                                                          |
| 0x000000E7 | [ **\_浮動\_POINT\_の状態が無効です**](bug-check-0xe7--invalid-floating-point-state.md)                                                            |
| 0x000000E8 | [ **\_ファイル\_開いている\_無効なキャンセル\_** ](bug-check-0xe8--invalid-cancel-of-file-open.md)                                                             |
| 0x000000E9 | [**ACTIVE\_EX\_ワーカー\_スレッド\_終了**](bug-check-0xe9--active-ex-worker-thread-termination.md)                                             |
| 0x000000EA | [ **\_デバイス\_ドライバーのスレッド\_スタック\_スタック**](bug-check-0xea--thread-stuck-in-device-driver.md)                                                         |
| 0x000000EB | [**ダーティ\_マップされた\_ページ\_輻輳**](bug-check-0xeb--dirty-mapped-pages-congestion.md)                                                          |
| 0x000000EC | [**セッション\_は\_終了時に特別な\_プール\_\_有効\_** ](bug-check-0xec--session-has-valid-special-pool-on-exit.md)                                     |
| 0x000000ED | [**UNMOUNTABLE\_のブート\_ボリューム**](bug-check-0xed--unmountable-boot-volume.md)                                                                       |
| 0x000000EF | [**重要な\_プロセス\_** ](bug-check-0xef--critical-process-died.md)                                                                           |
| 0x000000F0 | [**ストレージ\_ミニポート\_エラー**](bug-check-0xf0--storage-miniport-error.md)                                                                         |
| 0x000000F1 | [**SCSI\_検証ツール\_検出された\_違反**](bug-check-0xf1--scsi-verifier-detected-violation.md)                                                    |
| 0x000000F2 | [**ハードウェア\_割り込み\_嵐**](bug-check-0xf2--hardware-interrupt-storm.md)                                                                     |
| 0x000000F3 | [**無効\_シャットダウン**](bug-check-0xf3--disorderly-shutdown.md)                                                                                |
| 0x000000F4 | [**重大な\_オブジェクト\_終了**](bug-check-0xf4--critical-object-termination.md)                                                               |
| 0x000000F5 | [**FLTMGR\_ファイル\_システム**](bug-check-0xf5--fltmgr-file-system.md)                                                                                 |
| 0x000000F6 | [**PCI\_VERIFIER\_検出された\_違反**](bug-check-0xf6--pci-verifier-detected-violation.md)                                                      |
| 0x000000F7 | [**ドライバー\_オーバー実行\_スタック\_バッファー**](bug-check-0xf7--driver-overran-stack-buffer.md)                                                              |
| 0x000000F8 | [**RAMDISK\_ブート\_の初期化\_失敗しました**](bug-check-0xf8--ramdisk-boot-initialization-failed.md)                                                |
| 0x000000F9 | [ **\_ボリューム\_開いている状態\_再解析\_\_\_ドライバーが返されました**](bug-check-0xf9--driver-returned-status-reparse-for-volume-open.md)                     |
| 0x000000FA | [**HTTP\_ドライバー\_破損しています**](bug-check-0xfa---http-driver-corrupted.md)                                                                          |
| 0x000000FC | [ **\_NOEXECUTE\_メモリの\_の実行\_試行しました**](bug-check-0xfc---attempted-execute-of-noexecute-memory.md)                                        |
| 0x000000FD | [**ダーティ\_NOWRITE\_ページ\_輻輳**](bug-check-0xfd---dirty-nowrite-pages-congestion.md)                                                       |
| 0x000000FE | [**USB\_ドライバー\_バグコード**](bug-check-0xfe--bugcode-usb-driver.md)                                                                                 |
| 0x000000FF | [ **\_キューの予約\_オーバーフロー**](bug-check-0xff---reserve-queue-overflow.md)                                                                        |
| 0x00000100 | [**ローダー\_ブロック\_不一致**](bug-check-0x100---loader-block-mismatch.md)                                                                         |
| 0x00000101 | [**時計\_ウォッチドッグ\_タイムアウト**](bug-check-0x101---clock-watchdog-timeout.md)                                                                       |
| 0x00000102 | [**DPC\_ウォッチドッグ\_タイムアウト**](bug-check-0x102--dpc-watchdog-timeout.md)                                                                            |
| 0x00000103 | [**MUP\_ファイル\_システム**](bug-check-0x103---mup-file-system.md)                                                                                     |
| 0x00000104 | [**AGP\_無効な\_アクセス**](bug-check-0x104---agp-invalid-access.md)                                                                               |
| 0x00000105 | [**AGP\_GART\_破損**](bug-check-0x105---agp-gart-corruption.md)                                                                             |
| 0x00000106 | [**AGP\_不正\_再プログラミング**](bug-check-0x106---agp-illegally-reprogrammed.md)                                                               |
| 0x00000108 | [**サードパーティの\_ファイル\_システム\_障害\_** ](bug-check-0x108--third-party-file-system-failure.md)                                                    |
| 0x00000109 | [**重大な\_構造\_破損**](bug-check-0x109---critical-structure-corruption.md)                                                         |
| 0x0000010A | [**アプリ\_タグ付け\_初期化\_失敗しました**](bug-check-0x10a---app-tagging-initialization-failed.md)                                                |
| 0x0000010C | [**FSRTL\_余分\_作成\_パラメーター\_違反**](bug-check-0x10c---fsrtl-extra-create-parameter-violation.md)                                     |
| 0x0000010D | [**WDF\_違反**](bug-check-0x10d---wdf-violation.md)                                                                                          |
| 0x0000010E | [**ビデオ\_メモリ\_管理\_内部**](bug-check-0x10e---video-memory-management-internal.md)                                                  |
| 0x0000010F | [**リソース\_マネージャー\_例外\_処理\_れていません**](bug-check-0x10f---resource-manager-exception-not-handled.md)                                     |
| 0x00000111 | [**再帰\_NMI**](bug-check-0x111---recursive-nmi.md)                                                                                          |
| 0x00000112 | [**MSRPC\_状態\_違反**](bug-check-0x112---msrpc-state-violation.md)                                                                         |
| 0x00000113 | [**VIDEO\_DXGKRNL\_致命的\_エラー**](bug-check-0x113---video-dxgkrnl-fatal-error.md)                                                                |
| 0x00000114 | [**ビデオ\_シャドウ\_ドライバー\_致命的な\_エラー**](bug-check-0x114---video-shadow-driver-fatal-error.md)                                                   |
| 0x00000115 | [**AGP\_内部**](bug-check-0x115---agp-internal.md)                                                                                            |
| 0x00000116 | [**ビデオ\_TDR\_エラー**](bug-check-0x116---video-tdr-failure.md)                                                                                     |
| 0x00000117 | [**ビデオ\_TDR\_タイムアウト\_検出されました**](bug-check-0x117---video-tdr-timeout-detected.md)                                                              |
| 0x00000119 | [**ビデオ\_SCHEDULER\_内部\_エラー**](bug-check-0x119---video-scheduler-internal-error.md)                                                      |
| 0x0000011A | [**EM\_初期化\_失敗**](bug-check-0x11a---em-initialization-failure.md)                                                                 |
| 0x0000011B | [**ドライバー\_が\_キャンセル\_ロックを保持\_返されました**](bug-check-0x11b---driver-returned-holding-cancel-lock.md)                                           |
| 0x0000011C | [ **\_CM\_保護されている\_ストレージへの\_の書き込み\_試行しました**](bug-check-0x11c--attempted-write-to-cm-protected-storage.md)                                   |
| 0x0000011D | [**イベント\_トレース\_致命的\_エラー**](bug-check-0x11d---event-tracing-fatal-error.md)                                                                |
| 0x0000011E | [**多数の\_再帰\_フォールト\_** ](bug-check-0x11e--too-many-recursive-faults.md)                                                                |
| 0x0000011F | [ **\_ドライバー\_ハンドルが無効です**](bug-check-0x11f--invalid-driver-handle.md)                                                                         |
| 0x00000120 | [**BITLOCKER\_致命的な\_エラー**](bug-check-0x120--bitlocker-fatal-error-.md)                                                                        |
| 0x00000121 | [**ドライバー\_違反**](bug-check-0x121---driver-violation.md)                                                                                    |
| 0x00000122 | [**WHEA\_内部\_エラー**](bug-check-0x122---whea-internal-error.md)                                                                             |
| 0x00000123 | [**暗号化\_自己\_テスト\_エラー**](bug-check-0x123--crypto-self-test-failure-.md)                                                                 |
| 0x00000124 | [**WHEA\_修正不可能\_エラー**](bug-check-0x124---whea-uncorrectable-error.md)                                                                   |
| 0x00000125 | [**NMR\_無効な\_状態**](bug-check-0x125--nmr-invalid-state.md)                                                                                 |
| 0x00000126 | [**NETIO\_無効な\_プール\_呼び出し元**](bug-check-0x126--netio-invalid-pool-caller.md)                                                                |
| 0x00000127 | [**ページ\_\_0 ではありません**](bug-check-0x127---page-not-zero.md)                                                                                         |
| 0x00000128 | [**ワーカー\_スレッド\_\_返されましたが、正しくない\_IO\_優先度\_で返されました**](bug-check-0x128--worker-thread-returned-with-bad-io-priority.md)                          |
| 0x00000129 | [**ワーカー\_スレッド\_\_返されました。\_不良\_ページング\_IO\_PRIORITY**](bug-check-0x129--worker-thread-returned-with-bad-paging-io-priority.md)           |
| 0x0000012A | [**MUI\_\_有効な\_システム\_言語**](bug-check-0x12a--mui-no-valid-system-language.md)                                                          |
| 0x0000012B | [**障害が発生した\_ハードウェア\_破損している\_ページ**](bug-check-0x12b---faulty-hardware-corrupted-page.md)                                                      |
| 0x0000012C | [**EXFAT\_ファイル\_システム**](bug-check-0x12c---exfat-file-system.md)                                                                                 |
| 0x0000012D | [ **\_テーブル\_アクセス\_重複する VOLSNAP**](bug-check-0x12d--volsnap-overlapped-table-access.md)                                                     |
| 0x0000012E | [ **\_MDL\_範囲が無効です**](bug-check-0x12e--invalid-mdl-range.md)                                                                                  |
| 0x0000012F | [**VHD\_ブート\_の初期化\_失敗しました**](bug-check-0x12f--vhd-boot-initialization-failed.md)                                                       |
| 0x00000130 | [**動的\_\_プロセッサの追加\_不一致**](bug-check-0x130--dynamic-add-processor-mismatch.md)                                                       |
| 0x00000131 | [**無効な\_拡張\_プロセッサ\_の状態**](bug-check-0x131--invalid-extended-processor-state.md)                                                   |
| 0x00000132 | [**リソース\_所有者\_ポインター\_無効です**](bug-check-0x132--resource-owner-pointer-invalid.md)                                                       |
| 0x00000133 | [**DPC\_ウォッチドッグ\_違反**](bug-check-0x133-dpc-watchdog-violation.md)                                                                         |
| 0x00000134 | [**EXTENDER\_ドライブ**](bug-check-0x134--drive-extender.md)                                                                                         |
| 0x00000135 | [**レジストリ\_フィルター\_ドライバー\_例外**](bug-check-0x135--registry-filter-driver-exception.md)                                                   |
| 0x00000136 | [**VHD\_ブート\_ホスト\_ボリューム\_十分な\_領域がありません**](bug-check-0x136--vhd-boot-host-volume-not-enough-space.md)\_                                      |
| 0x00000137 | [ **\_マネージャーを処理する WIN32K\_** ](bug-check-0x137--win32k-handle-manager.md)                                                                          |
| 0x00000138 | [**GPIO\_CONTROLLER\_ドライバー\_エラー**](bug-check-0x138-gpio-controller-driver-error.md)                                                            |
| 0x00000139 | [**カーネル\_セキュリティ\_チェック\_エラー**](bug-check-0x139--kernel-security-check-failure.md)                                              |
| 0x0000013A | [**カーネル\_モード\_ヒープ\_破損**](bug-check-0x13a--kernel-mode-heap-corruption.md)                                                             |
| 0x0000013B | [**パッシブ\_割り込み\_エラー**](bug-check-0x13b--passive-interrupt-error.md)                                                                      |
| 0x0000013C | [**無効な\_IO\_\_状態のブースト**](bug-check-0x13c--invalid-io-boost-state.md)                                                                       |
| 0x0000013D | [**重大な\_初期化\_失敗**](bug-check-0x13d--critical-initialization-failure.md)                                                      |
| 0x00000140 | [**記憶域\_デバイス\_異常が\_検出されました**](bug-check-0x140--storage-device-abnormality-detected.md)                                             |
| 0x00000141 | [**ビデオ\_エンジン\_タイムアウト\_検出されました**](bug-check-0x141---video-engine-timeout-detected.md)                                                        |
| 0x00000142 | [**ビデオ\_TDR\_アプリケーション\_ブロックされています**](bug-check-0x142--video-tdr-application-blocked.md)                                                         |
| 0x00000143 | [**プロセッサ\_ドライバー\_内部**](bug-check-0x143--processor-driver-internal.md)                                                                  |
| 0x00000144 | [**USB3\_ドライバー\_バグコード**](bug-check-0x144--bugcode-usb3-driver.md)                                                                              |
| 0x00000145 | [**セキュア\_ブート\_違反**](bug-check-0x145--secure-boot-violation-.md)                                                                         |
| 0x00000147 | [**異常な\_リセット\_検出されました**](bug-check-0x147--abnormal-reset-detected.md)                                                                      |
| 0x00000149 | [**REFS\_ファイル\_システム**](bug-check-0x149--refs-file-system.md)                                                                                    |
| 0x0000014A | [**カーネル\_WMI\_内部**](bug-check-0x14a--kernel-wmi-internal.md)                                                                              |
| 0x0000014B | [**SOC\_サブシステム\_エラー**](bug-check-0x14b--soc-subsystem-failure.md)                                                                          |
| 0x0000014C | [**致命的な\_異常\_リセット\_エラー**](bug-check-0x14c--fatal-abnormal-reset-error.md)                                                               |
| 0x0000014D | [**例外\_スコープ\_無効です**](bug-check-0x14d--exception-scope-invalid.md)                                                                      |
| 0x0000014E | [**SOC\_重要な\_デバイス\_削除されました**](bug-check-0x14e--soc-critical-device-removed.md)                                                             |
| 0x0000014F | [**PDC\_ウォッチドッグ\_タイムアウト**](bug-check-0x14f--pdc-watchdog-timeout.md)                                                                            |
| 0x00000150 | [**TCP/IP\_\_NIC\_アクティブ\_参照\_リーク**](bug-check-0x150--tcpip-aoac-nic-active-reference-leak.md)                                         |
| 0x00000151 | [**サポートされていない\_命令\_モード**](bug-check-0x151--unsupported-instruction-mode.md)                                                            |
| 0x00000152 | [**無効な\_プッシュ\_ロック\_フラグ**](bug-check-0x152--invalid-push-lock-flags.md)                                                                     |
| 0x00000153 | [**カーネル\_ロック\_エントリ\_\_リークした\_スレッド\_終了**](bug-check-0x153--kernel-lock-entry-leaked-on-thread-termination.md)                    |
| 0x00000154 | [**予期しない\_ストア\_例外**](bug-check-0x154--unexpected-store-exception.md)                                                                |
| 0x00000155 | [**OS\_データ\_改ざん**](bug-check-0x155--os-data-tampering.md)                                                                                  |
| 0x00000156 | [**WINSOCK\_\_ハング\_、LIVEDUMP\_検出されました**](bug-check-0x156--winsock-detected-hung-closesocket-livedump.md)                              |
| 0x00000157 | [**カーネル\_スレッド\_優先順位\_フロア\_違反**](bug-check-0x157--kernel-thread-priority-floor-violation.md)                                      |
| 0x00000158 | [**無効な\_IOMMU\_ページ\_エラー**](bug-check-0x158--illegal-iommu-page-fault.md)                                                                   |
| 0x00000159 | [ **\_無効な\_、IOMMU\_ページ\_フォールトの HAL**](bug-check-0x159--hal-illegal-iommu-page-fault.md)                                                          |
| 0x0000015A | [**SDBUS\_内部\_エラー**](bug-check-0x15a--sdbus-internal-error.md)                                                                            |
| 0x0000015B | [**ワーカー\_スレッド\_\_システム\_ページ\_PRIORITY\_ACTIVE に\_返されました**](bug-check-0x15b--worker-thread-returned-with-system-page-priority-active.md) |
| 0x0000015C | [**PDC\_ウォッチドッグ\_タイムアウト\_LIVEDUMP**](bug-check-0x15c--pdc-watchdog-timeout-livedump.md)              
| 0x0000015D | [**SOC\_サブシステム\_エラー\_LIVEDUMP**](bug-check-0x15d-soc-subsystem-failure-livedump.md)              
| 0x0000015E | [**コード\_NDIS\_ドライバー\_ライブ\_ダンプのバグ**](bug-check-0x15e-bugcode-ndis-driver-live-dump.md)                                                         |
| 0x0000015F | [**コネクト\_スタンバイ\_ウォッチドッグ\_タイムアウト\_LIVEDUMP**](bug-check-0x15f--connected-standby-watchdog-timeout-livedump.md)                            |
| 0x00000160 | [**WIN32K\_アトミック\_チェック\_失敗**](bug-check-0x160--win32k-atomic-check-failure.md)                                                             |
| 0x00000161 | [**ライブ\_システム\_ダンプ**](bug-check-0x161--live-system-dump.md)                                                                                    |
| 0x00000162 | [**カーネル\_自動\_ブースト\_無効\_ロック\_リリース**](bug-check-0x162--kernel-auto-boost-invalid-lock-release.md)                                     |
| 0x00000163 | [**ワーカー\_スレッド\_テスト\_条件**](bug-check-0x162--worker-thread-test-condition.md)                                                           |
| 0x00000164 | [**WIN32K\_重大な\_障害**](bug-check-0x164--win32k-critical-failure.md)                                                                      |
| 0x00000165 | [**クラスター\_CSV\_状態\_IO\_タイムアウト\_LIVEDUMP**](bug-check-0x165--cluster-csv-staus-io-timeout-livedump.md)                                      | 
| 0x00000166 | [**クラスター\_リソース\_呼び出し\_タイムアウト\_LIVEDUMP**](bug-check-0x166--cluster-resource-call-timeout-livedump.md)                                      |
| 0x00000167 | [**クラスター\_CSV\_スナップショット\_デバイス\_情報\_タイムアウト\_LIVEDUMP**](bug-check-0x167--cluster-csv-snapshot-device-info-timeout-livedump.md)              |    
| 0x00000168 | [**クラスター\_CSV\_状態\_移行\_タイムアウト\_LIVEDUMP**](bug-check-0x168--cluster-csv-state-transition-timeout-livedump.md)                       |   
| 0x00000169 | [**クラスター\_CSV\_ボリューム\_到着\_LIVEDUMP**](bug-check-0x169--cluster-csv-volume-arival-livedump.md)                                             |      
| 0x0000016A | [**クラスター\_CSV\_ボリューム\_削除\_LIVEDUMP**](bug-check-0x16a--cluster-csv-volume-removal-livedump.md)                                            |    
| 0x0000016B | [**クラスター\_CSV\_クラスター\_ウォッチドッグ\_LIVEDUMP**](bug-check-0x16b--cluster-csv-cluster-watchdog-livedump.md)                                       |   
| 0x0000016C | [**無効な\_ランダウン\_保護\_フラグ**](bug-check-0x16c--invalid-rundown-protection-flags.md)                                                   |
| 0x0000016D | [ **\_スロット\_アロケーター\_フラグが無効です**](bug-check-0x16d--invalid-slot-allocator-flags.md)                                                           |
| 0x0000016E | [ **%\_無効な\_リリース**](bug-check-0x16e--eresource-invalid-release.md)                                                                  |
| 0x0000016F | [**クラスター\_CSV\_状態\_移行\_間隔\_タイムアウト\_LIVEDUMP**](bug-check-0x16f--cluster-csv-state-transistion-interval-livedump.md)           |
| 0x00000170 | [**暗号化\_ライブラリ\_内部\_エラー**](bug-check-0x170--crypto-library-internal-error.md)                                                         |
| 0x00000171 | [**クラスター\_CSV\_CLUSSVC\_切断\_ウォッチドッグ**](bug-check-0x171--cluster-csv-clussvc-disconnect-watchdog.md)                                    |
| 0x00000173 | [**COREMSGCALL\_内部\_エラー**](bug-check-0x173--coremsgcall-internal-error.md)                                                                |
| 0x00000174 | [**COREMSG\_内部\_エラー**](bug-check-0x174--coremsg-internal-error.md)                                                                        |
| 0x00000175 | [**前の\_致命的な\_異常\_リセット\_エラー**](bug-check-0x175--previous-fatal-abnormal-reset-error.md)                                            |
| 0x00000178 | [**ELAM\_ドライバー\_検出され\_致命的な\_エラーが発生しました**](bug-check-0x175--elam-driver-detected-fatal-error.md)                                                  |
| 0x00000179 | [**クラスター\_CLUSPORT\_状態\_IO\_タイムアウト\_LIVEDUMP**](bug-check-0x179--cluster-clusport-status-io-timeout-livedump.md)                           |
| 0x0000017B | [**プロファイラー\_構成\_無効です**](bug-check-0x17b--profiler-configuration-illegal.md)                                                        | 
| 0x0000017C | [**PDC\_ロック\_ウォッチドッグ\_LIVEDUMP**](bug-check-0x17c--pdc-lock-watchdog-livedump.md)                                                               | 
| 0x0000017D | [**PDC\_予期しない\_の失効\_LIVEDUMP**](bug-check-0x17d-unexpected-revocation-livedump.md)                                                    | 
| 0x0000017E | [**マイクロコード\_リビジョン\_不一致**](bug-check-0x17e--microcode-revision-mismatch.md)                                                              | 
| 0x00000187 | [**ビデオ\_DWMINIT\_タイムアウト\_フォールバック\_BDD**](bug-check-0x187--video-dwminit-timeout-fallback-bdd.md)                                              |
| 0x00000188 | [**クラスター\_CSVFS\_LIVEDUMP**](bug-check-0x188--cluster-csvfs-livedump.md)                                                                        |
| 0x00000189 | [ **\_オブジェクト\_ヘッダーに問題があります**](bug-check-0x189--bad-object-header.md)                                                                                  |
| 0x0000018B | [**セキュリティで保護された\_カーネル\_エラー**](bug-check-0x18b--secure-kernel-error.md)                                                                              |
| 0x0000018C | [**HYPERGUARD\_違反**](bug-check-0x18c--hyperguard-violation.md)                                                                              |   
| 0x0000018D | [**セキュリティで保護された\_フォールト\_未処理の場合**](bug-check-0x18d--secure-fault-unhandled.md)                                                                        | 
| 0x0000018E | [**カーネル\_パーティション\_参照\_違反**](bug-check-0x18e--kernel-partition-reference-violation.md)                                           |
| 0x00000190 | [**WIN32K\_重大な\_障害\_LIVEDUMP**](bug-check-0x190--win32k-critical-failure-livedump.md)                                                   |
| 0x00000191 | [**PF\_検出\_破損**](bug-check-0x191--pf-detected-corruption.md)                                                                        |
| 0x00000192 | [**カーネル\_自動\_ブースト\_ロック\_取得\_\_発生\_発生**](bug-check-0x192--kernel-auto-boost-lock-acquisition-with-raised-irql.md)         |
| 0x00000193 | [**ビデオ\_DXGKRNL\_LIVEDUMP**](bug-check-0x192--video-dxgkrnl-livedump.md)                                                                        |
| 0x00000195 | [**SMB\_サーバー\_LIVEDUMP**](bug-check-0x195--smb-server-livedump.md)                                                                              |
| 0x00000196 | [**ローダー\_ロールバック\_検出されました**](bug-check-0x196--loader-rollback-detected.md)                                                                    |
| 0x00000197 | [**WIN32K\_セキュリティ\_の失敗**](bug-check-0x197--win32k-security-failure.md)                                                                      |
| 0x00000198 | [**UFX\_LIVEDUMP**](bug-check-0x198--ufx-livedump.md)                                                                                             |
| 0x00000199 | [ **\_使用中のカーネル\_ストレージ\_スロット\_** ](bug-check-0x199--kernel-storage-slot-in-use.md)                                                              |
| 0x0000019A | [ **\_サイロにアタッチされた\_を\_しているときに、ワーカー\_スレッド\_\_が返されました**](bug-check-0x19a--worker-thread-returned-while-attached-to-silo.md)                      |
| 0x0000019B | [**TTM\_致命的な\_エラー**](bug-check-0x19b--ttm-fatal-error.md)                                                                                      |
| 0x0000019C | [**WIN32K\_POWER\_ウォッチドッグ\_タイムアウト**](bug-check-0x19c--win32k-power-watchdog-timeout.md)                                                         |
| 0x0000019D | [**クラスター\_SVHDX\_LIVEDUMP**](bug-check-0x19d--cluster-svhdx-livedump.md)                                                                        |
| 0x000001A0 | [**TTM\_ウォッチドッグ\_タイムアウト**](bug-check-0x1a0--ttm-watchdog-timeout.md)
| 0x000001A1 | [**WIN32K\_吹き出し\_ウォッチドッグ\_LIVEDUMP**](bug-check-0x1a1--win32k-callout-watchdog-livedump.md)
| 0x000001A2 | [**WIN32K\_コールアウト\_ウォッチドッグ\_バグチェック**](bug-check-0x1a2--win32k-callout-watchdog-bugcheck.md)
| 0x000001A3 | [ **\_呼び出し\_ウォッチドッグ\_タイムアウト\_LIVEDUMP が\_返され\_いません**](bug-check-0x1a3--call-has-not-returned-watchdog-timeout-livedump.md)                  |
| 0x000001A4 | [**DRIPS\_SW\_HW\_相違\_LIVEDUMP**](bug-check-0x1a4--drips-sw-hw-divergence-livedump.md)                                                    |
| 0x000001A5 | [**USB\_DRIPS\_ブロック\_突然\_削除\_LIVEDUMP**](bug-check-0x1a5--usb-drips-blocker-surprise-removal-livedump.md)                           |
| 0x000001A6 | [**BLUETOOTH\_エラー\_回復\_LIVEDUMP**](bug-check-0x1a6--bluetooth-error-recovery-livedump.md)                                                 |
| 0x000001A7 | [**SMB\_リダイレクター\_LIVEDUMP**](bug-check-0x1A7--smb-redirector-livedump.md)                                                                       |
| 0x000001A8 | [**VIDEO\_DXGKRNL\_BLACK\_画面\_LIVEDUMP**](bug-check-0x1a8--video-dxgkrnl-black-screen-livedump.md)                                            |
| 0x000001B0 | [**VIDEO_MINIPORT_FAILED_LIVEDUMP**](bug-check-0x1b0--video-miniport-failed-livedump.md)                                                          |
| 0x000001C4 | [**DRIVER\_VERIFIER\_検出された\_違反\_LIVEDUMP**](bug-check-0x1c4--driver-verifier-detected-violation-livedump.md)                            |
| 0x000001C5 | [**IO\_THREADPOOL\_デッドロック\_LIVEDUMP**](bug-check-0x1c5--io-threadpool-deadlock-livedump.md)                                                     |
| 0x000001C6 | [ **\_の高速な\_の前提条件\_違反**](bug-check-0x1c6--fast-eresource-precondition-violation.md)                                         |
| 0x000001C7 | [**データ\_構造の\_格納\_破損**](bug-check-0x1c7--store-data-structure-corruption.md)                                                     |
| 0x000001C8 | [**手動\_開始\_電源\_ボタン\_保持**](bug-check-0x1c8--manually-initiated-power-button-hold.md)                                          |
| 0x000001C9 | [**ユーザー\_モード\_HEALTH\_MONITOR\_LIVEDUMP**](bug-check-0x1c9--user-mode-health-monitor-livedump.md)                                                |
| 0x000001CA | [**統合\_ウォッチドッグ\_タイムアウト**](bug-check-0x1ca--synthetic-watchdog-timeout.md)                                                                |
| 0x000001CB | [**無効な\_サイロ\_デタッチ**](bug-check-0x1cb--invalid-silo-detach.md)                                                                              |
| 0x000001CC | [**EXRESOURCE_TIMEOUT_LIVEDUMP**](bug-check-0x1cc--exresource-timeout-livedump.md)                                                                |
| 0x000001CD | [**無効な\_コールバック\_STACK_ADDRESS**](bug-check-0x1cd--invalid-callback-stack-address.md)                                                        |
| 0x000001CE | [**無効な\_カーネル\_スタック\_アドレス**](bug-check-0x1ce--invalid-kernel-stack-address.md)                                                           |
| 0x000001CF | [**ハードウェア\_ウォッチドッグ\_タイムアウト**](bug-check-0x1cf--hardware-watchdog-timeout.md)                                                                  |  
| 0x000001D0 | [**CPI\_ファームウェア\_ウォッチドッグ\_タイムアウト**](bug-check-0x1d0--acpi-firmware-watchdog-timeout.md)                                                        |
| 0x000001D1 | [**テレメトリ\_アサート\_LIVEDUMP**](bug-check-0x1d1--telemetry-asserts-livedump.md)                                                                |
| 0x000001D2 | [**ワーカー\_スレッド\_無効な\_の状態です**](bug-check-0x1d2--worker-thread-invalid-state.md)                                                             |
| 0x000001D3 | [**WFP\_無効な\_操作**](bug-check-0x1d3--wfp-invalid-operation.md)                                                                          |
| 0x000001D4 | [**UCMUCSI\_LIVEDUMP**](bug-check-0x1d4--ucmusci-livedump.md)                                                                                     |
| 0x000001D5 | [**DRIVER_PNP_WATCHDOG**](bug-check-0x1d5--driver-pnp-watchdog.md)                                                                                |
| 0x000001D6 | [**ワーカー\_スレッド\_、\_既定\_ワークロード\_ではない\_と\_返されました。** ](bug-check-0x1d6--worker-thread-returned-with-non-default-workload-class.md)   |
| 0x000001D7 | [**EFS\_致命的な\_エラー**](bug-check-0x1d7--efs-fatal-error.md)                                                                                      |
| 0x000001D8 | [**UCMUCSI\_エラー**](bug-check-0x1d8--ucmucsi-failure.md)                                                                                       |
| 0x000001D9 | [ **\_IOMMU\_内部\_エラーの HAL**](bug-check-0x1d8--ucmucsi-failure.md)                                                                            |
| 0x000001DB | [**IPI\_ウォッチドッグ\_タイムアウト**](bug-check-0x1db--ipi-watchdog-timeout.md)                                                                            |
| 0x000001DC | [**DMA_COMMON_BUFFER_VECTOR_ERROR**](bug-check-0x1dc--dma-common-buffer-vector-error.md)                                                          |
| 0x00000356 | [**XBOX\_ERACTRL\_CS\_タイムアウト**](bug-check-0x356--xbox-eractrl-cs-timeout.md)                                                                     |
| 0x00000BFE | [**BC\_BLUETOOTH\_検証ツール\_エラー**](bug-check-0xbfe--bc-bluetooth-verifier-fault.md)                                                             |
| 0x00000BFF | [**BC\_BTHMINI\_検証ツール\_エラー**](bug-check-0xbff--bc-bthmini-verifier-fault.md)                                                                 |
| 0x00020001 | [**ハイパーバイザー\_エラー**](bug-check-0x20001--hypervisor-error.md)                                                                                   |
| 0x1000007E | [**システム\_スレッド\_例外\_\_処理されませんでした\_M**](bug-check-0x1000007e--system-thread-exception-not-handled-m.md)                                  |
| 0x1000007F | [**予期しない\_カーネル\_モード\_トラップ\_M**](bug-check-0x1000007f--unexpected-kernel-mode-trap-m.md)                                                   |
| 0x1000008E | [**カーネル\_モード\_例外\_\_処理されていません\_M**](bug-check-0x1000008e--kernel-mode-exception-not-handled-m.md)                                      |
| 0x100000EA | [**スレッド\_\_デバイス\_ドライバー\_M で\_スタックしています**](bug-check-0x100000ea--thread-stuck-in-device-driver-m.md)                                              |
| 0x4000008A | [**スレッド\_終了\_ミューテックス\_保持されています**](bug-check-0x4000008a--thread-terminate-held-mutex.md)                                                        |
| 0xC0000218 | [**ステータス\_は\_レジストリ\_ファイルの読み込みを\_できません**](bug-check-0xc0000218--status-cannot-load-registry-file.md)                                             |
| 0xC000021A | [**WINLOGON\_致命的な\_エラー**](bug-check-0xc000021a--winlogin-fatal-error.md)                                              |
| 0xC0000221 | [**ステータス\_イメージ\_チェックサム\_不一致**](bug-check-0xc0000221--status-image-checksum-mismatch.md)                                                  |
| 0xDEADDEAD | [**手動\_開始\_CRASH1**](bug-check-0xdeaddead--manually-initiated-crash1.md)                                                             |
