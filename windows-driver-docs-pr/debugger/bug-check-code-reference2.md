---
title: バグ チェック コード リファレンス
description: このセクションには、ブルー スクリーンに渡されるパラメーターを含む、バグの一般的なチェックの説明が含まれています。
ms.assetid: DBA85578-97CF-4BD7-A67D-1C7AD2E9B2BB
ms.date: 02/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4e97477c9d3f29db52840f9d6ed849b8f9a3975e
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743447"
---
# <a name="bug-check-code-reference"></a>バグ チェック コード リファレンス

このセクションでは、青のバグの確認画面でのエラー コードに表示されるパラメーターを含む共通のバグ チェック コードを説明します。 このセクションでは、バグのチェックとエラーを処理する方法を引き起こしたエラーを診断する方法についても説明します。

> [!NOTE] 
> このトピックはプログラマーを対象としています。 顧客のシステムがブルー スクリーンにバグの確認コードを表示される場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://go.microsoft.com/fwlink/p/?linkid=183646)します。

このリファレンスで特定のバグ チェックのコードが表示されない場合は、使用、 [ **! 分析**](-analyze.md)拡張機能で、Windows デバッガー (WinDbg (カーネル モードの場合) では、次の構文で置き換える)`<code>`で、バグ チェック コード:

`!analyze -show <code>`

このコマンドを入力すると、WinDbg 指定のバグ チェック コードに関する情報を表示します。 既定数ベース (基数) が 16 でない場合は、プレフィックス`<code>`で**0 x**します。

次の表では、各バグの名前とコードの確認コードを示します。

| コード       | 名前                                                                                                                                              |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| 0x00000001 | [**APC\_インデックス\_が一致しません**](bug-check-0x1--apc-index-mismatch.md)                                                                                  |
| 0x00000002 | [**デバイス\_キュー\_いない\_ビジー**](bug-check-0x2--device-queue-not-busy.md)                                                                           |
| 0x00000003 | [**無効な\_アフィニティ\_設定**](bug-check-0x3--invalid-affinity-set.md)                                                                              |
| 0x00000004 | [**INVALID\_DATA\_ACCESS\_TRAP**](bug-check-0x4--invalid-data-access-trap.md)                                                                     |
| 0x00000005 | [**無効な\_プロセス\_アタッチ\_試行**](bug-check-0x5--invalid-process-attach-attempt.md)                                                         |
| 0x00000006 | [**無効な\_プロセス\_デタッチ\_試行**](bug-check-0x6--invalid-process-detach-attempt.md)                                                         |
| 0x00000007 | [**無効な\_ソフトウェア\_を中断**](bug-check-0x7--invalid-software-interrupt.md)                                                                  |
| 0x00000008 | [**IRQL\_NOT\_DISPATCH\_LEVEL**](bug-check-0x8--irql-not-dispatch-level.md)                                                                       |
| 0x00000009 | [**IRQL\_いない\_GREATER\_または\_と等しい**](bug-check-0x9--irql-not-greater-or-equal.md)                                                                  |
| 0x0000000A | [**IRQL\_いない\_少ない\_または\_と等しい**](bug-check-0xa--irql-not-less-or-equal.md)                                                                        |
| 0x0000000B | [**いいえ\_例外\_処理\_サポート**](bug-check-0xb--no-exception-handling-support.md)                                                           |
| 0x0000000C | [**最大\_待機\_オブジェクト\_超過**](bug-check-0xc--maximum-wait-objects-exceeded.md)                                                           |
| 0x0000000D | [**ミュー テックス\_レベル\_数\_違反**](bug-check-0xd--mutex-level-number-violation.md)                                                             |
| 0x0000000E | [**いいえ\_ユーザー\_モード\_コンテキスト**](bug-check-0xe--no-user-mode-context.md)                                                                             |
| 0x0000000F | [**スピン\_ロック\_ALREADY\_所有されています。**](bug-check-0xf--spin-lock-already-owned.md)                                                                       |
| 0x00000010 | [**スピン\_ロック\_いない\_所有されています。**](bug-check-0x10--spin-lock-not-owned.md)                                                                              |
| 0x00000011 になります | [**THREAD\_NOT\_MUTEX\_OWNER**](bug-check-0x11--thread-not-mutex-owner.md)                                                                        |
| 0x00000012 | [**トラップ\_原因\_不明**](bug-check-0x12--trap-cause-unknown.md)                                                                                 |
| 0x00000013 | [**空\_スレッド\_リーパー\_一覧**](bug-check-0x13--empty-thread-reaper-list.md)                                                                    |
| 0x00000014 | [**作成\_削除\_ロック\_いない\_ロック**](bug-check-0x14--create-delete-lock-not-locked.md)                                                         |
| 0x00000015 | [**最後\_可能性\_呼び出し\_FROM\_KMODE**](bug-check-0x15--last-chance-called-from-kmode.md)                                                         |
| 0x00000016 | [**CID\_処理\_の作成**](bug-check-0x16--cid-handle-creation.md)                                                                               |
| 0x00000017 | [**CID\_処理\_削除**](bug-check-0x17--cid-handle-deletion.md)                                                                               |
| 0x00000018 | [**参照\_BY\_ポインター**](bug-check-0x18--reference-by-pointer.md)                                                                             |
| 0x00000019 | [**不適切な\_プール\_ヘッダー**](bug-check-0x19--bad-pool-header.md)                                                                                       |
| 0x0000001A | [**メモリ\_管理**](bug-check-0x1a--memory-management.md)                                                                                    |
| 0x0000001B | [**PFN\_共有\_数**](bug-check-0x1b--pfn-share-count.md)                                                                                       |
| 0x0000001C | [**PFN\_参照\_数**](bug-check-0x1c--pfn-reference-count.md)                                                                               |
| 0x0000001D | [**いいえ\_スピン\_ロック\_利用可能**](bug-check-0x1d--no-spin-lock-available.md)                                                                        |
| 0x0000001E | [**KMODE\_例外\_いない\_処理済み**](bug-check-0x1e--kmode-exception-not-handled.md)                                                              |
| 0x0000001F | [**共有\_リソース\_CONV\_エラー**](bug-check-0x1f--shared-resource-conv-error.md)                                                                |
| 0x00000020 | [**カーネル\_APC\_PENDING\_に\_終了**](bug-check-0x20--kernel-apc-pending-during-exit.md)                                                       |
| 0x00000021 | [**クォータ\_アンダー フロー**](bug-check-0x21--quota-underflow.md)                                                                                        |
| 0x00000022 | [**ファイル\_システム**](bug-check-0x22--file-system.md)                                                                                                |
| 0x00000023 | [**FAT\_ファイル\_システム**](bug-check-0x23--fat-file-system.md)                                                                                       |
| 0x00000024 | [**NTFS\_ファイル\_システム**](bug-check-0x24--ntfs-file-system.md)                                                                                     |
| 0x00000025 | [**NPFS\_ファイル\_システム**](bug-check-0x25--npfs-file-system.md)                                                                                     |
| 0x00000026 | [**CDFS\_ファイル\_システム**](bug-check-0x26--cdfs-file-system.md)                                                                                     |
| 0x00000027 | [**RDR\_ファイル\_システム**](bug-check-0x27--rdr-file-system.md)                                                                                       |
| 0x00000028 | [**破損\_アクセス\_トークン**](bug-check-0x28--corrupt-access-token.md)                                                                             |
| 0x00000029 | [**セキュリティ\_システム**](bug-check-0x29--security-system.md)                                                                                        |
| 0x0000002A | [**一貫性のない\_IRP**](bug-check-0x2a--inconsistent-irp.md)                                                                                      |
| 0x0000002B | [**パニック\_スタック\_スイッチ**](bug-check-0x2b--panic-stack-switch.md)                                                                                 |
| 0x0000002C | [**ポート\_ドライバー\_内部**](bug-check-0x2c--port-driver-internal.md)                                                                             |
| 0x0000002D | [**SCSI\_ディスク\_ドライバー\_内部**](bug-check-0x2d--scsi-disk-driver-internal.md)                                                                  |
| 0x0000002E | [**データ\_BUS\_エラー**](bug-check-0x2e--data-bus-error.md)                                                                                         |
| 0x0000002F | [**命令\_BUS\_エラー**](bug-check-0x2f--instruction-bus-error.md)                                                                           |
| 0x00000030 | [**SET\_OF\_INVALID\_CONTEXT**](bug-check-0x30--set-of-invalid-context.md)                                                                        |
| 0x00000031 | [**PHASE0\_初期化\_失敗**](bug-check-0x31--phase0-initialization-failed.md)                                                             |
| 0x00000032 | [**フェーズ 1\_初期化\_失敗**](bug-check-0x32--phase1-initialization-failed.md)                                                             |
| 0x00000033 | [**予期しない\_初期化\_を呼び出す**](bug-check-0x33--unexpected-initialization-call.md)                                                         |
| 0x00000034 | [**キャッシュ\_マネージャー**](bug-check-0x34--cache-manager.md)                                                                                            |
| 0x00000035 | [**いいえ\_詳細\_IRP\_スタック\_場所**](bug-check-0x35--no-more-irp-stack-locations.md)                                                             |
| 0x00000036 | [**デバイス\_参照\_カウント\_いない\_0**](bug-check-0x36--device-reference-count-not-zero.md)                                                     |
| 0x00000037 | [**フロッピー\_内部\_エラー**](bug-check-0x37--floppy-internal-error.md)                                                                           |
| 0x00000038 | [**シリアル\_ドライバー\_内部**](bug-check-0x38--serial-driver-internal.md)                                                                         |
| 0x00000039 | [**システム\_終了\_所有されている\_ミュー テックス**](bug-check-0x39--system-exit-owned-mutex.md)                                                                      |
| 0x0000003A | [**システム\_アンワインド\_前\_ユーザー**](bug-check-0x3a--system-unwind-previous-user.md)                                                              |
| 0x0000003B | [**システム\_サービス\_例外**](bug-check-0x3b--system-service-exception.md)                                                                     |
| 0x0000003C | [**割り込み\_アンワインド\_しようとしました**](bug-check-0x3c--interrupt-unwind-attempted.md)                                                                 |
| 0x0000003D | [**割り込み\_例外\_いない\_処理済み**](bug-check-0x3d--interrupt-exception-not-handled.md)                                                      |
| 0x0000003E | [**マルチプロセッサ\_構成\_いない\_サポートされています。**](bug-check-0x3e--multiprocessor-configuration-not-supported.md)                                |
| 0x0000003F | [**いいえ\_詳細\_システム\_PTE**](bug-check-0x3f--no-more-system-ptes.md)                                                                              |
| 0x00000040 | [**ターゲット\_MDL\_すぎます\_小さな**](bug-check-0x40--target-mdl-too-small.md)                                                                            |
| 0x00000041 | [**必要があります\_SUCCEED\_プール\_空**](bug-check-0x41--must-succeed-pool-empty.md)                                                                      |
| 0x00000042 | [**ATDISK\_ドライバー\_内部**](bug-check-0x42--atdisk-driver-internal.md)                                                                         |
| 0x00000043 | [**いいえ\_かかる\_パーティション**](bug-check-0x43--no-such-partition.md)                                                                                   |
| 0x00000044 | [**複数\_IRP\_完了\_要求**](bug-check-0x44--multiple-irp-complete-requests.md)                                                        |
| 0x00000045 | [**不足している\_システム\_マップ\_REGS**](bug-check-0x45--insufficient-system-map-regs.md)                                                            |
| 0x00000046 | [**DEREF\_不明な\_ログオン\_セッション**](bug-check-0x46--deref-unknown-logon-session.md)                                                              |
| 0x00000047 | [**REF\_不明な\_ログオン\_セッション**](bug-check-0x47--ref-unknown-logon-session.md)                                                                  |
| 0x00000048 | [**CANCEL\_STATE\_IN\_COMPLETED\_IRP**](bug-check-0x48--cancel-state-in-completed-irp.md)                                                         |
| 0x00000049 | [**ページ\_フォールト\_WITH\_割り込み\_OFF**](bug-check-0x49--page-fault-with-interrupts-off.md)                                                       |
| 0x0000004A | [**IRQL\_GT\_0\_で\_システム\_サービス**](bug-check-0x4a--irql-gt-zero-at-system-service.md)                                                      |
| 0x0000004B | [**ストリーム\_内部\_エラー**](bug-check-0x4b--streams-internal-error.md)                                                                         |
| 0x0000004C | [**致命的な\_未処理\_ハード\_エラー**](bug-check-0x4c--fatal-unhandled-hard-error.md)                                                                |
| 0x0000004D | [**いいえ\_ページ\_利用可能**](bug-check-0x4d--no-pages-available.md)                                                                                 |
| 0x0000004E | [**PFN\_一覧\_が壊れています**](bug-check-0x4e--pfn-list-corrupt.md)                                                                                     |
| 0x0000004F | [**NDIS\_内部\_エラー**](bug-check-0x4f--ndis-internal-error.md)                                                                               |
| 0x00000050 | [**ページ\_フォールト\_IN\_非ページ\_領域**](bug-check-0x50--page-fault-in-nonpaged-area.md)                                                             |
| 0x00000051 | [**レジストリ\_エラー**](bug-check-0x51--registry-error.md)                                                                                          |
| 0x00000052 | [**"メール スロット"\_ファイル\_システム**](bug-check-0x52--mailslot-file-system.md)                                                                             |
| 0x00000053 | [**いいえ\_ブート\_デバイス**](bug-check-0x53--no-boot-device.md)                                                                                         |
| 0x00000054 | [**LM\_SERVER\_内部\_エラー**](bug-check-0x54--lm-server-internal-error.md)                                                                    |
| 0x00000055 | [**データ\_コヒレンシー\_例外**](bug-check-0x55--data-coherency-exception.md)                                                                     |
| 0x00000056 | [**命令\_コヒレンシー\_例外**](bug-check-0x56--instruction-coherency-exception.md)                                                       |
| 0x00000057 | [**XNS\_内部\_エラー**](bug-check-0x57--xns-internal-error.md)                                                                                 |
| 0x00000058 | [**FTDISK\_内部\_エラー**](bug-check-0x58--ftdisk-internal-error.md)                                                                           |
| 0x00000059 | [**ピンボール\_ファイル\_システム**](bug-check-0x59--pinball-file-system.md)                                                                               |
| 0x0000005A | [**重要な\_サービス\_失敗**](bug-check-0x5a--critical-service-failed.md)                                                                       |
| 0x0000005B | [**設定\_ENV\_VAR\_失敗**](bug-check-0x5b--set-env-var-failed.md)                                                                                |
| 0x0000005C | [**HAL\_初期化\_失敗**](bug-check-0x5c--hal-initialization-failed.md)                                                                   |
| 0x0000005D | [**サポートされていない\_プロセッサ**](bug-check-0x5d--unsupported-processor.md)                                                                            |
| 0x0000005E | [**オブジェクト\_初期化\_失敗**](bug-check-0x5e--object-initialization-failed.md)                                                             |
| 0x0000005F | [**セキュリティ\_初期化\_失敗**](bug-check-0x5f--security-initialization-failed.md)                                                         |
| 0x00000060 | [**プロセス\_初期化\_失敗**](bug-check-0x60--process-initialization-failed.md)                                                           |
| 0x00000061 | [**HAL1\_初期化\_失敗**](bug-check-0x61--hal1-initialization-failed.md)                                                                 |
| 0x00000062 | [**OBJECT1\_初期化\_失敗**](bug-check-0x62--object1-initialization-failed.md)                                                           |
| 0x00000063 | [**SECURITY1\_初期化\_失敗**](bug-check-0x63--security1-initialization-failed.md)                                                       |
| 0x00000064 | [**シンボリック\_初期化\_失敗**](bug-check-0x64--symbolic-initialization-failed.md)                                                         |
| 0x00000065 | [**MEMORY1\_初期化\_失敗**](bug-check-0x65--memory1-initialization-failed.md)                                                           |
| 0x00000066 | [**キャッシュ\_初期化\_失敗**](bug-check-0x66--cache-initialization-failed.md)                                                               |
| 0x00000067 | [**CONFIG\_初期化\_失敗**](bug-check-0x67--config-initialization-failed.md)                                                             |
| 0x00000068 | [**ファイル\_初期化\_失敗**](bug-check-0x68--file-initialization-failed.md)                                                                 |
| 0x00000069 | [**IO1\_初期化\_失敗**](bug-check-0x69--io1-initialization-failed.md)                                                                   |
| 0x0000006A | [**LPC\_初期化\_失敗**](bug-check-0x6a--lpc-initialization-failed.md)                                                                   |
| 0x0000006B | [**PROCESS1\_初期化\_失敗**](bug-check-0x6b--process1-initialization-failed.md)D                                                         |
| 0x0000006C | [**REFMON\_初期化\_失敗**](bug-check-0x6c--refmon-initialization-failed.md)                                                             |
| 0x0000006D | [**SESSION1\_初期化\_失敗**](bug-check-0x6d--session1-initialization-failed.md)                                                         |
| 0x0000006E | [**SESSION2\_初期化\_失敗**](bug-check-0x6e--session2-initialization-failed.md)                                                         |
| 0x0000006F | [**SESSION3\_初期化\_失敗**](bug-check-0x6f--session3-initialization-failed.md)                                                         |
| 0x00000070 | [**SESSION4\_初期化\_失敗**](bug-check-0x70--session4-initialization-failed.md)                                                         |
| 0x00000071 | [**SESSION5\_初期化\_失敗**](bug-check-0x71--session5-initialization-failed.md)                                                         |
| 0x00000072 | [**割り当てる\_ドライブ\_文字\_失敗**](bug-check-0x72--assign-drive-letters-failed.md)                                                              |
| 0x00000073 | [**CONFIG\_一覧\_失敗**](bug-check-0x73--config-list-failed.md)                                                                                 |
| 0x00000074 | [**不適切な\_システム\_CONFIG\_情報**](bug-check-0x74--bad-system-config-info.md)                                                                        |
| 0x00000075 | [**できません\_書き込み\_構成**](bug-check-0x75--cannot-write-configuration.md)                                                                 |
| 0x00000076 | [**プロセス\_HAS\_ロック\_ページ**](bug-check-0x76--process-has-locked-pages.md)                                                                    |
| 0x00000077 | [**カーネル\_スタック\_インページ\_エラー**](bug-check-0x77--kernel-stack-inpage-error.md)                                                                  |
| 0x00000078 | [**PHASE0\_例外**](bug-check-0x78--phase0-exception.md)                                                                                      |
| 0x00000079 | [**一致しない\_HAL**](bug-check-0x79--mismatched-hal.md)                                                                                          |
| 0x0000007A | [**カーネル\_データ\_インページ\_エラー**](bug-check-0x7a--kernel-data-inpage-error.md)                                                                    |
| 0x0000007B | [**アクセスできない\_ブート\_デバイス**](bug-check-0x7b--inaccessible-boot-device.md)                                                                     |
| 0x0000007C | [**BUGCODE\_NDIS\_ドライバー**](bug-check-0x7c--bugcode-ndis-driver.md)                                                                               |
| 0x0000007D | [**インストール\_詳細\_メモリ**](bug-check-0x7d--install-more-memory.md)                                                                               |
| 0x0000007E | [**システム\_スレッド\_例外\_いない\_処理済み**](bug-check-0x7e--system-thread-exception-not-handled.md)                                             |
| 0x0000007F | [**予期しない\_カーネル\_モード\_トラップ**](bug-check-0x7f--unexpected-kernel-mode-trap.md)                                                              |
| 0x00000080 | [**NMI\_ハードウェア\_エラー**](bug-check-0x80--nmi-hardware-failure.md)                                                                             |
| 0x00000081 | [**スピン\_ロック\_INIT\_エラー**](bug-check-0x81--spin-lock-init-failure.md)                                                                        |
| 0x00000082 | [**DFS\_ファイル\_システム**](bug-check-0x82--dfs-file-system.md)                                                                                       |
| 0x00000085 | [**セットアップ\_エラー**](bug-check-0x85--setup-failure.md)                                                                                            |
| 0x0000008B | [**MBR\_チェックサム\_が一致しません**](bug-check-0x8b--mbr-checksum-mismatch.md)                                                                           |
| 0x0000008E | [**カーネル\_モード\_例外\_いない\_処理済み**](bug-check-0x8e--kernel-mode-exception-not-handled.md)                                                 |
| 0x0000008F | [**PP0\_初期化\_失敗**](bug-check-0x8f--pp0-initialization-failed.md)                                                                   |
| 0x00000090 | [**PP1\_初期化\_失敗**](bug-check-0x90--pp1-initialization-failed.md)                                                                   |
| 0x00000092 | [**\_ドライバー\_ON\_MP\_システム**](bug-check-0x92--up-driver-on-mp-system.md)                                                                       |
| 0x00000093 | [**無効な\_カーネル\_処理**](bug-check-0x93--invalid-kernel-handle.md)                                                                           |
| 0x00000094 | [**カーネル\_スタック\_ロック\_で\_終了**](bug-check-0x94--kernel-stack-locked-at-exit.md)                                                             |
| 0x00000096 | [**無効な\_作業\_キュー\_項目**](bug-check-0x96--invalid-work-queue-item.md)                                                                      |
| 0x00000097 | [**バインドされている\_イメージ\_サポートされていません**](bug-check-0x97--bound-image-unsupported.md)                                                                       |
| 0x00000098 | [**終了\_の\_NT\_評価\_期間**](bug-check-0x98--end-of-nt-evaluation-period.md)                                                             |
| 0x00000099 | [**無効な\_リージョン\_または\_セグメント**](bug-check-0x99--invalid-region-or-segment.md)                                                                  |
| 0x0000009a のエラー | [**システム\_ライセンス\_違反**](bug-check-0x9a--system-license-violation.md)                                                                     |
| 0x0000009B | [**UDF\_ファイル\_システム**](bug-check-0x9b--udfs-file-system.md)                                                                                     |
| 0x0000009c の解説 | [**マシン\_確認\_例外**](bug-check-0x9c--machine-check-exception.md)                                                                       |
| エラー 0x0000009e が発生 | [**ユーザー\_モード\_ヘルス\_モニター**](bug-check-0x9e--user-mode-health-monitor.md)                                                                    |
| 0x0000009F | [**ドライバー\_POWER\_状態\_エラー**](bug-check-0x9f--driver-power-state-failure.md)                                                                |
| 0x000000A0 | [**内部\_POWER\_エラー**](bug-check-0xa0--internal-power-error.md)                                                                             |
| 0x000000A1 | [**PCI\_BUS\_ドライバー\_内部**](bug-check-0xa1--pci-bus-driver-internal.md)                                                                      |
| 0x000000A2 | [**メモリ\_イメージ\_が壊れています**](bug-check-0xa2--memory-image-corrupt.md)                                                                             |
| 0x000000A3 | [**ACPI\_ドライバー\_内部**](bug-check-0xa3--acpi-driver-internal.md)                                                                             |
| 0x000000A4 | [**CNSS\_ファイル\_システム\_フィルター**](bug-check-0xa4--cnss-file-system-filter.md)                                                                      |
| 0x000000A5 | [**ACPI\_BIOS\_エラー**](bug-check-0xa5--acpi-bios-error.md)                                                                                       |
| 0x000000A7 | [**不適切な\_EXHANDLE**](bug-check-0xa7--bad-exhandle.md)                                                                                              |
| 0x000000AB | [**セッション\_HAS\_有効\_プール\_ON\_終了**](bug-check-0xab--session-has-valid-pool-on-exit.md)                                                      |
| 0x000000AC | [**HAL\_メモリ\_割り当て**](bug-check-0xac--hal-memory-allocation.md)                                                                           |
| 0x000000AD | [**ビデオ\_ドライバー\_デバッグ\_レポート\_要求**](bug-check-0xad--video-driver-debug-report-request.md)                                                 |
| 0x000000B1 | [**BGI\_検出\_違反**](bug-check-0xb1--bgi-detected-violation.md)                                                                         |
| 0x000000B4 | [**ビデオ\_ドライバー\_INIT\_エラー**](bug-check-0xb4--video-driver-init-failure.md)                                                                  |
| 0x000000B8 | [**試行\_スイッチ\_FROM\_DPC**](bug-check-0xb8--attempted-switch-from-dpc.md)                                                                  |
| 0x000000B9 | [**チップセット\_検出\_エラー**](bug-check-0xb9--chipset-detected-error.md)                                                                         |
| 0x000000BA | [**セッション\_HAS\_有効\_ビュー\_ON\_終了**](bug-check-0xba--session-has-valid-views-on-exit.md)                                                    |
| 0x000000BB | [**ネットワーク\_ブート\_初期化\_失敗**](bug-check-0xbb--network-boot-initialization-failed.md)                                                |
| 0x000000BC | [**NETWORK\_BOOT\_DUPLICATE\_ADDRESS**](bug-check-0xbc--network-boot-duplicate-address.md)                                                        |
| 0x000000BD | [**無効な\_HIBERNATED\_状態**](bug-check-0xbd--invalid-hibernated-state.md)                                                                     |
| 0x000000BE | [**試行\_書き込み\_TO\_READONLY\_メモリ**](bug-check-0xbe--attempted-write-to-readonly-memory.md)                                               |
| 0x000000BF | [**ミュー テックス\_ALREADY\_所有されています。**](bug-check-0xbf--mutex-already-owned.md)                                                                               |
| 0x000000C1 | [**特別な\_プール\_検出\_メモリ\_破損**](bug-check-0xc1--special-pool-detected-memory-corruption.md)                                     |
| 0x000000C2 | [**不適切な\_プール\_呼び出し元**](bug-check-0xc2--bad-pool-caller.md)                                                                                       |
| 0x000000C4 | [**ドライバー\_VERIFIER\_検出\_違反**](bug-check-0xc4--driver-verifier-detected-violation.md)                                                |
| 0x000000C5 | [**ドライバー\_破損した\_EXPOOL**](bug-check-0xc5--driver-corrupted-expool.md)                                                                       |
| 0x000000C6 | [**ドライバー\_例外が発生しました\_変更\_FREED\_フン**](bug-check-0xc6--driver-caught-modifying-freed-pool.md)L                                               |
| 0x000000C7 | [**タイマー\_または\_DPC\_が無効です**](bug-check-0xc7--timer-or-dpc-invalid.md)                                                                            |
| 0x000000C8 | [**IRQL\_予期しない\_値**](bug-check-0xc8--irql-unexpected-value.md)                                                                           |
| 0x000000C9 | [**ドライバー\_VERIFIER\_IOMANAGER\_違反**](bug-check-0xc9--driver-verifier-iomanager-violation.md)                                              |
| 0x000000CA | [**PNP\_検出\_FATAL\_エラー**](bug-check-0xca--pnp-detected-fatal-error.md)                                                                    |
| 0x000000CB | [**ドライバー\_左\_ロック\_ページ\_IN\_プロセス**](bug-check-0xcb--driver-left-locked-pages-in-process.md)                                            |
| 0x000000CC | [**ページ\_フォールト\_IN\_FREED\_特殊\_プール**](bug-check-0xcc--page-fault-in-freed-special-pool.md)                                                  |
| 0x000000CD | [**ページ\_フォールト\_を超えて\_エンド\_の\_割り当て**](bug-check-0xcd--page-fault-beyond-end-of-allocation.md)                                            |
| 0x000000CE | [**ドライバー\_UNLOADED\_せず\_CANCELLING\_PENDING\_操作**](bug-check-0xce--driver-unloaded-without-cancelling-pending-operations.md)        |
| 0x000000CF | [**ターミナル\_SERVER\_ドライバー\_加えられた\_正しくない\_メモリ\_リファレンス**](bug-check-0xcf--terminal-server-driver-made-incorrect-memory-reference.md)     |
| 0x000000D0 | [**ドライバー\_破損した\_MMPOOL**](bug-check-0xd0--driver-corrupted-mmpool.md)                                                                       |
| 0x000000D1 | [**ドライバー\_IRQL\_いない\_少ない\_または\_と等しい**](bug-check-0xd1--driver-irql-not-less-or-equal.md)                                                        |
| 0x000000D2 | [**BUGCODE\_ID\_ドライバー**](bug-check-0xd2--bugcode-id-driver.md)                                                                                   |
| 0x000000D3 | [**ドライバー\_部分\_する必要があります\_BE\_非ページ**](bug-check-0xd3--driver-portion-must-be-nonpaged.md)                                                     |
| 0x000000D4 | [**システム\_スキャン\_で\_発生\_IRQL\_例外が発生しました\_不適切な\_ドライバー\_アンロード**](bug-check-0xd4--system-scan-at-raised-irql-caught-improper-driver-unlo.md) |
| 0x000000D5 | [**ドライバー\_ページ\_フォールト\_IN\_FREED\_特殊\_プール**](bug-check-0xd5--driver-page-fault-in-freed-special-pool.md)                                   |
| 0x000000D6 | [**ドライバー\_ページ\_フォールト\_を超えて\_エンド\_の\_割り当て**](bug-check-0xd6--driver-page-fault-beyond-end-of-allocation.md)                             |
| 0x000000D7 | [**ドライバー\_UNMAPPING\_無効な\_ビュー**](bug-check-0xd7--driver-unmapping-invalid-view.md)                                                          |
| 0x000000D8 | [**ドライバー\_使用\_の過剰な\_PTE**](bug-check-0xd8--driver-used-excessive-ptes.md)                                                                |
| 0x000000D9 | [**ロックされている\_ページ\_トラッカー\_破損**](bug-check-0xd9--locked-pages-tracker-corruption.md)                                                      |
| 0x000000DA | [**システム\_PTE\_誤用**](bug-check-0xda--system-pte-misuse.md)                                                                                   |
| 0x000000DB | [**ドライバー\_破損した\_SYSPTES**](bug-check-0xdb--driver-corrupted-sysptes.md)                                                                     |
| 0x000000DC | [**ドライバー\_無効な\_スタック\_アクセス**](bug-check-0xdc--driver-invalid-stack-access.md)                                                              |
| 0x000000DE | [**プール\_破損\_IN\_ファイル\_領域**](bug-check-0xde--pool-corruption-in-file-area.md)                                                           |
| 0x000000DF | [**MPERSONATING\_ワーカー\_スレッド**](bug-check-0xdf--impersonating-worker-thread.md)                                                               |
| 0x000000E0 | [**ACPI\_BIOS\_FATAL\_エラー**](bug-check-0xe0--acpi-bios-fatal-error.md)                                                                          |
| 0x000000E1 | [**ワーカー\_スレッド\_から返された\_で\_不良\_IRQL**](bug-check-0xe1--worker-thread-returned-at-bad-irql.md)                                              |
| 0x000000E2 | [**手動で\_INITIATED\_クラッシュ**](bug-check-0xe2--manually-initiated-crash.md)                                                                     |
| 0x000000E3 | [**リソース\_いない\_所有されています。**](bug-check-0xe3--resource-not-owned.md)                                                                                 |
| 0x000000E4 | [**ワーカー\_が無効です**](bug-check-0xe4--worker-invalid.md)                                                                                          |
| 0x000000E6 | [**ドライバー\_VERIFIER\_DMA\_違反**](bug-check-0xe6--driver-verifier-dma-violation.md)                                                          |
| 0x000000E7 | [**無効な\_浮動\_ポイント\_状態**](bug-check-0xe7--invalid-floating-point-state.md)                                                            |
| 0x000000E8 | [**無効な\_キャンセル\_の\_ファイル\_開く**](bug-check-0xe8--invalid-cancel-of-file-open.md)                                                             |
| 0x000000E9 | [**アクティブな\_EX\_ワーカー\_スレッド\_終了**](bug-check-0xe9--active-ex-worker-thread-termination.md)                                             |
| 0x000000EA | [**スレッド\_STUCK\_IN\_デバイス\_ドライバー**](bug-check-0xea--thread-stuck-in-device-driver.md)                                                         |
| 0x000000EB | [**ダーティ\_マップ済み\_ページ\_輻輳**](bug-check-0xeb--dirty-mapped-pages-congestion.md)                                                          |
| 0x000000EC | [**セッション\_HAS\_有効\_特殊\_プール\_ON\_終了**](bug-check-0xec--session-has-valid-special-pool-on-exit.md)                                     |
| 0x000000ED | [**ベーシック\_ブート\_ボリューム**](bug-check-0xed--unmountable-boot-volume.md)                                                                       |
| 0x000000EF | [**重要な\_プロセス\_DIED**](bug-check-0xef--critical-process-died.md)                                                                           |
| 0x000000F0 | [**記憶域\_ミニポート\_エラー**](bug-check-0xf0--storage-miniport-error.md)                                                                         |
| 0x000000F1 | [**SCSI\_VERIFIER\_検出\_違反**](bug-check-0xf1--scsi-verifier-detected-violation.md)                                                    |
| 0x000000F2 | [**ハードウェア\_INTERRUPT\_STORM**](bug-check-0xf2--hardware-interrupt-storm.md)                                                                     |
| 0x000000F3 | [**無秩序\_シャット ダウン**](bug-check-0xf3--disorderly-shutdown.md)                                                                                |
| 0x000000F4 | [**重要な\_オブジェクト\_終了**](bug-check-0xf4--critical-object-termination.md)                                                               |
| 0x000000F5 | [**FLTMGR\_ファイル\_システム**](bug-check-0xf5--fltmgr-file-system.md)                                                                                 |
| 0x000000F6 | [**PCI\_VERIFIER\_検出\_違反**](bug-check-0xf6--pci-verifier-detected-violation.md)                                                      |
| 0x000000F7 | [**ドライバー\_OVERRAN\_スタック\_バッファー**](bug-check-0xf7--driver-overran-stack-buffer.md)                                                              |
| 0x000000F8 | [**RAMDISK\_ブート\_初期化\_失敗**](bug-check-0xf8--ramdisk-boot-initialization-failed.md)                                                |
| 0x000000F9 | [**ドライバー\_から返された\_状態\_再解析\_の\_ボリューム\_開く**](bug-check-0xf9--driver-returned-status-reparse-for-volume-open.md)                     |
| 0x000000FA | [**HTTP\_ドライバー\_破損しました。**](bug-check-0xfa---http-driver-corrupted.md)                                                                          |
| 0x000000FC | [**試行\_EXECUTE\_の\_NOEXECUTE\_メモリ**](bug-check-0xfc---attempted-execute-of-noexecute-memory.md)                                        |
| 0x000000FD | [**ダーティ\_NOWRITE\_ページ\_輻輳**](bug-check-0xfd---dirty-nowrite-pages-congestion.md)                                                       |
| 0x000000FE | [**BUGCODE\_USB\_ドライバー**](bug-check-0xfe--bugcode-usb-driver.md)                                                                                 |
| 0x000000FF | [**予約\_キュー\_オーバーフロー**](bug-check-0xff---reserve-queue-overflow.md)                                                                        |
| 0x00000100 | [**ローダー\_ブロック\_が一致しません**](bug-check-0x100---loader-block-mismatch.md)                                                                         |
| 0x00000101 | [**クロック\_ウォッチドッグ\_タイムアウト**](bug-check-0x101---clock-watchdog-timeout.md)                                                                       |
| 0x00000102 | [**DPC\_ウォッチドッグ\_タイムアウト**](bug-check-0x102--dpc-watchdog-timeout.md)                                                                            |
| 0x00000103 | [**MUP\_ファイル\_システム**](bug-check-0x103---mup-file-system.md)                                                                                     |
| 0x00000104 | [**AGP\_無効な\_アクセス**](bug-check-0x104---agp-invalid-access.md)                                                                               |
| 0x00000105 | [**AGP\_GART\_破損**](bug-check-0x105---agp-gart-corruption.md)                                                                             |
| 0x00000106 | [**AGP\_不法\_REPROGRAMMED**](bug-check-0x106---agp-illegally-reprogrammed.md)                                                               |
| 0x00000108 | [**3 番目\_パーティ\_ファイル\_システム\_エラー**](bug-check-0x108--third-party-file-system-failure.md)                                                    |
| 0x00000109 | [**重要な\_構造\_破損**](bug-check-0x109---critical-structure-corruption.md)                                                         |
| 0x0000010A | [**アプリ\_タグ付け\_初期化\_失敗**](bug-check-0x10a---app-tagging-initialization-failed.md)                                                |
| 0x0000010C | [**FSRTL\_EXTRA\_CREATE\_PARAMETER\_VIOLATION**](bug-check-0x10c---fsrtl-extra-create-parameter-violation.md)                                     |
| 0x0000010D | [**WDF\_違反**](bug-check-0x10d---wdf-violation.md)                                                                                          |
| 0x0000010E | [**ビデオ\_メモリ\_管理\_内部**](bug-check-0x10e---video-memory-management-internal.md)                                                  |
| 0x0000010F | [**リソース\_MANAGER\_例外\_いない\_処理済み**](bug-check-0x10f---resource-manager-exception-not-handled.md)                                     |
| 0x00000111 | [**再帰的な\_NMI**](bug-check-0x111---recursive-nmi.md)                                                                                          |
| 0x00000112 | [**MSRPC\_状態\_違反**](bug-check-0x112---msrpc-state-violation.md)                                                                         |
| 0x00000113 | [**ビデオ\_DXGKRNL\_FATAL\_エラー**](bug-check-0x113---video-dxgkrnl-fatal-error.md)                                                                |
| 0x00000114 | [**ビデオ\_シャドウ\_ドライバー\_FATAL\_エラー**](bug-check-0x114---video-shadow-driver-fatal-error.md)                                                   |
| 0x00000115 | [**AGP\_内部**](bug-check-0x115---agp-internal.md)                                                                                            |
| 0x00000116 | [**ビデオ\_TDR\_エラー**](bug-check-0x116---video-tdr-failure.md)                                                                                     |
| 0x00000117 | [**ビデオ\_TDR\_タイムアウト\_検出**](bug-check-0x117---video-tdr-timeout-detected.md)                                                              |
| 0x00000119 | [**ビデオ\_スケジューラ\_内部\_エラー**](bug-check-0x119---video-scheduler-internal-error.md)                                                      |
| 0x0000011A | [**EM\_初期化\_エラー**](bug-check-0x11a---em-initialization-failure.md)                                                                 |
| 0x0000011B | [**ドライバー\_から返された\_を保持している\_キャンセル\_ロック**](bug-check-0x11b---driver-returned-holding-cancel-lock.md)                                           |
| 0x0000011C | [**試行\_書き込み\_TO\_CM\_PROTECTED\_ストレージ**](bug-check-0x11c--attempted-write-to-cm-protected-storage.md)                                   |
| 0x0000011D | [**イベント\_トレース\_FATAL\_エラー**](bug-check-0x11d---event-tracing-fatal-error.md)                                                                |
| 0x0000011E | [**すぎる\_多く\_再帰\_エラー**](bug-check-0x11e--too-many-recursive-faults.md)                                                                |
| 0x0000011F | [**無効な\_ドライバー\_処理**](bug-check-0x11f--invalid-driver-handle.md)                                                                         |
| 0x00000120 | [**BITLOCKER\_FATAL\_エラー**](bug-check-0x120--bitlocker-fatal-error-.md)                                                                        |
| 0x00000121 | [**ドライバー\_違反**](bug-check-0x121---driver-violation.md)                                                                                    |
| 0x00000122 | [**WHEA\_内部\_エラー**](bug-check-0x122---whea-internal-error.md)                                                                             |
| 0x00000123 | [**CRYPTO\_セルフ\_テスト\_エラー**](bug-check-0x123--crypto-self-test-failure-.md)                                                                 |
| 0x00000124 | [**WHEA\_修正不可能な\_エラー**](bug-check-0x124---whea-uncorrectable-error.md)                                                                   |
| 0x00000125 | [**NMR\_無効な\_状態**](bug-check-0x125--nmr-invalid-state.md)                                                                                 |
| 0x00000126 | [**NETIO\_無効な\_プール\_呼び出し元**](bug-check-0x126--netio-invalid-pool-caller.md)                                                                |
| 0x00000127 | [**ページ\_いない\_0**](bug-check-0x127---page-not-zero.md)                                                                                         |
| 0x00000128 | [**ワーカー\_スレッド\_から返された\_WITH\_不良\_IO\_優先順位**](bug-check-0x128--worker-thread-returned-with-bad-io-priority.md)                          |
| 0x00000129 | [**ワーカー\_スレッド\_から返された\_WITH\_不良\_ページング\_IO\_優先順位**](bug-check-0x129--worker-thread-returned-with-bad-paging-io-priority.md)           |
| 0x0000012A | [**MUI\_いいえ\_有効\_システム\_言語**](bug-check-0x12a--mui-no-valid-system-language.md)                                                          |
| 0x0000012B | [**障害のある\_ハードウェア\_破損した\_ページ**](bug-check-0x12b---faulty-hardware-corrupted-page.md)                                                      |
| は 0x0000012C | [**EXFAT\_ファイル\_システム**](bug-check-0x12c---exfat-file-system.md)                                                                                 |
| 0x0000012D | [**VOLSNAP\_OVERLAPPED\_テーブル\_アクセス**](bug-check-0x12d--volsnap-overlapped-table-access.md)                                                     |
| 0x0000012E | [**無効な\_MDL\_範囲**](bug-check-0x12e--invalid-mdl-range.md)                                                                                  |
| 0x0000012F | [**VHD\_ブート\_初期化\_失敗**](bug-check-0x12f--vhd-boot-initialization-failed.md)                                                       |
| 0x00000130 | [**動的\_追加\_プロセッサ\_が一致しません**](bug-check-0x130--dynamic-add-processor-mismatch.md)                                                       |
| 0x00000131 | [**無効な\_拡張\_プロセッサ\_状態**](bug-check-0x131--invalid-extended-processor-state.md)                                                   |
| 0x00000132 | [**リソース\_所有者\_ポインター\_が無効です**](bug-check-0x132--resource-owner-pointer-invalid.md)                                                       |
| 0x00000133 | [**DPC\_ウォッチドッグ\_違反**](bug-check-0x133-dpc-watchdog-violation.md)                                                                         |
| 0x00000134 | [**ドライブ\_エクステンダー**](bug-check-0x134--drive-extender.md)                                                                                         |
| 0x00000135 | [**レジストリ\_フィルター\_ドライバー\_例外**](bug-check-0x135--registry-filter-driver-exception.md)                                                   |
| 0x00000136 | [**VHD\_ブート\_ホスト\_ボリューム\_いない\_ENOUGH\_領域**](bug-check-0x136--vhd-boot-host-volume-not-enough-space.md)                                      |
| 0x00000137 | [**WIN32K\_処理\_マネージャー**](bug-check-0x137--win32k-handle-manager.md)                                                                          |
| 0x00000138 | [**GPIO\_コント ローラー\_ドライバー\_エラー**](bug-check-0x138-gpio-controller-driver-error.md)                                                            |
| 0x00000139 | [**カーネル\_セキュリティ\_確認\_エラー**](bug-check-0x139--kernel-security-check-failure.md)                                              |
| 0x0000013A | [**カーネル\_モード\_ヒープ\_破損**](bug-check-0x13a--kernel-mode-heap-corruption.md)                                                             |
| 0x0000013B | [**パッシブ\_INTERRUPT\_エラー**](bug-check-0x13b--passive-interrupt-error.md)                                                                      |
| 0x0000013C | [**無効な\_IO\_BOOST\_状態**](bug-check-0x13c--invalid-io-boost-state.md)                                                                       |
| 0x0000013D | [**重要な\_初期化\_エラー**](bug-check-0x13d--critical-initialization-failure.md)                                                      |
| 0x00000140 | [**記憶域\_デバイス\_異常\_検出**](bug-check-0x140--storage-device-abnormality-detected.md)                                             |
| 0x00000141 | [**ビデオ\_エンジン\_タイムアウト\_検出**](bug-check-0x141---video-engine-timeout-detected.md)                                                        |
| 0x00000142 | [**ビデオ\_TDR\_アプリケーション\_ブロック**](bug-check-0x142--video-tdr-application-blocked.md)                                                         |
| 0x00000143 | [**プロセッサ\_ドライバー\_内部**](bug-check-0x143--processor-driver-internal.md)                                                                  |
| 0x00000144 | [**BUGCODE\_USB3\_ドライバー**](bug-check-0x144--bugcode-usb3-driver.md)                                                                              |
| 0x00000145 | [**セキュリティで保護された\_ブート\_違反**](bug-check-0x145--secure-boot-violation-.md)                                                                         |
| 0x00000147 | [**ABNORMAL\_RESET\_DETECTED**](bug-check-0x147--abnormal-reset-detected.md)                                                                      |
| 0x00000149 | [**REFS\_ファイル\_システム**](bug-check-0x149--refs-file-system.md)                                                                                    |
| 0x0000014A | [**カーネル\_WMI\_内部**](bug-check-0x14a--kernel-wmi-internal.md)                                                                              |
| 0x0000014B | [**SOC\_サブシステム\_エラー**](bug-check-0x14b--soc-subsystem-failure.md)                                                                          |
| 0x0000014C | [**FATAL\_ABNORMAL\_RESET\_ERROR**](bug-check-0x14c--fatal-abnormal-reset-error.md)                                                               |
| 0x0000014D | [**例外\_スコープ\_が無効です**](bug-check-0x14d--exception-scope-invalid.md)                                                                      |
| 0x0000014E | [**SOC\_重大\_デバイス\_削除しました**](bug-check-0x14e--soc-critical-device-removed.md)                                                             |
| 0x0000014F | [**PDC\_ウォッチドッグ\_タイムアウト**](bug-check-0x14f--pdc-watchdog-timeout.md)                                                                            |
| 0x00000150 | [**TCPIP\_AOAC\_NIC\_ACTIVE\_REFERENCE\_LEAK**](bug-check-0x150--tcpip-aoac-nic-active-reference-leak.md)                                         |
| 0x00000151 | [**サポートされていない\_命令\_モード**](bug-check-0x151--unsupported-instruction-mode.md)                                                            |
| 0x00000152 | [**無効な\_プッシュ\_ロック\_フラグ**](bug-check-0x152--invalid-push-lock-flags.md)                                                                     |
| 0x00000153 | [**カーネル\_ロック\_エントリ\_漏洩した\_ON\_スレッド\_終了**](bug-check-0x153--kernel-lock-entry-leaked-on-thread-termination.md)                    |
| 0x00000154 | [**予期しない\_ストア\_例外**](bug-check-0x154--unexpected-store-exception.md)                                                                |
| 0x00000155 | [**OS\_データ\_改ざん**](bug-check-0x155--os-data-tampering.md)                                                                                  |
| 0x00000156 | [**WINSOCK\_検出\_ハング\_CLOSESOCKET\_LIVEDUMP**](bug-check-0x156--winsock-detected-hung-closesocket-livedump.md)                              |
| 0x00000157 | [**カーネル\_スレッド\_優先度\_FLOOR\_違反**](bug-check-0x157--kernel-thread-priority-floor-violation.md)                                      |
| 0x00000158 | [**無効な\_IOMMU\_ページ\_エラー**](bug-check-0x158--illegal-iommu-page-fault.md)                                                                   |
| 0x00000159 | [**HAL\_不正な\_IOMMU\_ページ\_エラー**](bug-check-0x159--hal-illegal-iommu-page-fault.md)                                                          |
| 0x0000015A | [**SDBUS\_内部\_エラー**](bug-check-0x15a--sdbus-internal-error.md)                                                                            |
| 0x0000015B | [**ワーカー\_スレッド\_から返された\_WITH\_システム\_ページ\_優先度\_ACTIVE**](bug-check-0x15b--worker-thread-returned-with-system-page-priority-active.md) |
| 0x0000015C | [**PDC\_ウォッチドッグ\_タイムアウト\_LIVEDUMP**](bug-check-0x15c--pdc-watchdog-timeout-livedump.md)              
| 0x0000015D | [**SOC\_サブシステム\_エラー\_LIVEDUMP**](bug-check-0x15d-soc-subsystem-failure-livedump.md)              
| 0x0000015E | [**BUGCODE\_NDIS\_ドライバー\_LIVE\_ダンプ**](bug-check-0x15e-bugcode-ndis-driver-live-dump.md)                                                         |
| 0x0000015F | [**接続されている\_スタンバイ\_ウォッチドッグ\_タイムアウト\_LIVEDUMP**](bug-check-0x15f--connected-standby-watchdog-timeout-livedump.md)                            |
| 0x00000160 | [**WIN32K\_アトミック\_確認\_エラー**](bug-check-0x160--win32k-atomic-check-failure.md)                                                             |
| 0x00000161 | [**LIVE\_システム\_ダンプ**](bug-check-0x161--live-system-dump.md)                                                                                    |
| 0x00000162 | [**カーネル\_自動\_BOOST\_無効な\_ロック\_リリース**](bug-check-0x162--kernel-auto-boost-invalid-lock-release.md)                                     |
| 0x00000163 | [**ワーカー\_スレッド\_テスト\_条件**](bug-check-0x162--worker-thread-test-condition.md)                                                           |
| 0x00000164 | [**WIN32K\_重大\_エラー**](bug-check-0x164--win32k-critical-failure.md)                                                                      |
| 0x00000165 | [**クラスター\_CSV\_状態\_IO\_タイムアウト\_LIVEDUMP**](bug-check-0x165--cluster-csv-staus-io-timeout-livedump.md)                                      | 
| 0x00000166 | [**クラスター\_リソース\_呼び出す\_タイムアウト\_LIVEDUMP**](bug-check-0x166--cluster-resource-call-timeout-livedump.md)                                      |
| 0x00000167 | [**クラスター\_CSV\_スナップショット\_デバイス\_情報\_タイムアウト\_LIVEDUMP**](bug-check-0x167--cluster-csv-snapshot-device-info-timeout-livedump.md)              |    
| 0x00000168 | [**クラスター\_CSV\_状態\_遷移\_タイムアウト\_LIVEDUMP**](bug-check-0x168--cluster-csv-state-transition-timeout-livedump.md)                       |   
| 0x00000169 | [**クラスター\_CSV\_ボリューム\_到着\_LIVEDUMP**](bug-check-0x169--cluster-csv-volume-arival-livedump.md)                                             |      
| 0x0000016A | [**クラスター\_CSV\_ボリューム\_削除\_LIVEDUMP**](bug-check-0x16a--cluster-csv-volume-removal-livedump.md)                                            |    
| 0x0000016B | [**CLUSTER\_CSV_\_CLUSTER\_WATCHDOG_\LIVEDUMP**](bug-check-0x16b--cluster-csv-cluster-watchdog-livedump.md)                                       |   
| 0x0000016C | [**無効な\_ランダウン\_保護\_フラグ**](bug-check-0x16c--invalid-rundown-protection-flags.md)                                                   |
| 0x0000016D | [**無効な\_スロット\_アロケーター\_フラグ**](bug-check-0x16d--invalid-slot-allocator-flags.md)                                                           |
| 0x0000016E | [**スケジュール作成\_無効な\_リリース**](bug-check-0x16e--eresource-invalid-release.md)                                                                  |
| 0x0000016F | [**CLUSTER\_CSV_\STATE\_TRANSITION\_INTERVAL\_TIMEOUT\_LIVEDUMP**](bug-check-0x16f--cluster-csv-state-transistion-interval-livedump.md)           |
| 0x00000170 | [**CRYPTO\_ライブラリ\_内部\_エラー**](bug-check-0x170--crypto-library-internal-error.md)                                                         |
| 0x00000171 | [**クラスター\_CSV\_CLUSSVC\_切断\_ウォッチドッグ**](bug-check-0x171--cluster-csv-clussvc-disconnect-watchdog.md)                                    |
| 0x00000173 | [**COREMSGCALL\_内部\_エラー**](bug-check-0x173--coremsgcall-internal-error.md)                                                                |
| 0x00000174 | [**COREMSG\_内部\_エラー**](bug-check-0x174--coremsg-internal-error.md)                                                                        |
| 0x00000175 | [**以前\_FATAL\_異常\_リセット\_エラー**](bug-check-0x175--previous-fatal-abnormal-reset-error.md)                                            |
| 0x00000178 | [**ELAM\_ドライバー\_検出\_FATAL\_エラー**](bug-check-0x175--elam-driver-detected-fatal-error.md)                                                  |
| 0x00000179 | [**クラスター\_CLUSPORT\_状態\_IO\_タイムアウト\_LIVEDUMP**](bug-check-0x179--cluster-clusport-status-io-timeout-livedump.md)                           |
| 0x0000017B | [**プロファイラー\_構成\_が無効です**](bug-check-0x17b--profiler-configuration-illegal.md)                                                        | 
| 0x0000017C | [**PDC\_ロック\_ウォッチドッグ\_LIVEDUMP**](bug-check-0x17c--pdc-lock-watchdog-livedump.md)                                                               | 
| 0x0000017D | [**PDC\_予期しない\_失効\_LIVEDUMP**](bug-check-0x17d-unexpected-revocation-livedump.md)                                                    | 
| 0x0000017E | [**マイクロ コード\_リビジョン\_が一致しません**](bug-check-0x17e--microcode-revision-mismatch.md)                                                              | 
| 0x00000187 | [**ビデオ\_DWMINIT\_タイムアウト\_フォールバック\_BDD**](bug-check-0x187--video-dwminit-timeout-fallback-bdd.md)                                              |
| 0x00000188 | [**クラスター\_CSVFS\_LIVEDUMP**](bug-check-0x188--cluster-csvfs-livedump.md)                                                                        |
| 0x00000189 | [**不適切な\_オブジェクト\_ヘッダー**](bug-check-0x189--bad-object-header.md)                                                                                  |
| 0x0000018B | [**セキュリティで保護された\_カーネル\_エラー**](bug-check-0x18b--secure-kernel-error.md)                                                                              |
| 0x0000018C | [**HYPERGUARD\_違反**](bug-check-0x18c--hyperguard-violation.md)                                                                              |   
| 0x0000018D | [**セキュリティで保護された\_フォールト\_未処理**](bug-check-0x18d--secure-fault-unhandled.md)                                                                        | 
| 0x0000018E | [**カーネル\_パーティション\_参照\_違反**](bug-check-0x18e--kernel-partition-reference-violation.md)                                           |
| 0x00000190 | [**WIN32K\_重大\_エラー\_LIVEDUMP**](bug-check-0x190--win32k-critical-failure-livedump.md)                                                   |
| 0x00000191 | [**PF\_検出\_破損**](bug-check-0x191--pf-detected-corruption.md)                                                                        |
| 0x00000192 | [**カーネル\_自動\_BOOST\_ロック\_買収\_WITH\_発生\_IRQL**](bug-check-0x192--kernel-auto-boost-lock-acquisition-with-raised-irql.md)         |
| 0x00000193 | [**ビデオ\_DXGKRNL\_LIVEDUMP**](bug-check-0x192--video-dxgkrnl-livedump.md)                                                                        |
| 0x00000195 | [**SMB\_SERVER\_LIVEDUMP**](bug-check-0x195--smb-server-livedump.md)                                                                              |
| 0x00000196 | [**ローダー\_ロールバック\_検出**](bug-check-0x196--loader-rollback-detected.md)                                                                    |
| 0x00000197 | [**WIN32K\_セキュリティ\_エラー**](bug-check-0x197--win32k-security-failure.md)                                                                      |
| 0x00000198 | [**UFX\_LIVEDUMP**](bug-check-0x198--ufx-livedump.md)                                                                                             |
| 0x00000199 | [**カーネル\_ストレージ\_スロット\_IN\_使用**](bug-check-0x199--kernel-storage-slot-in-use.md)                                                              |
| 0x0000019A | [**ワーカー\_スレッド\_から返された\_中\_ATTACHED\_TO\_サイロ**](bug-check-0x19a--worker-thread-returned-while-attached-to-silo.md)                      |
| 0x0000019B | [**TTM\_FATAL\_ERROR**](bug-check-0x19b--ttm-fatal-error.md)                                                                                      |
| 0x0000019C | [**WIN32K\_POWER\_ウォッチドッグ\_タイムアウト**](bug-check-0x19c--win32k-power-watchdog-timeout.md)                                                         |
| 0x0000019D | [**クラスター\_SVHDX\_LIVEDUMP**](bug-check-0x19d--cluster-svhdx-livedump.md)                                                                        |
| 0x000001A0 | [**TTM\_WATCHDOG\_TIMEOUT**](bug-check-0x1a0--ttm-watchdog-timeout.md)                                                                            |
| 0x000001A3 | [**呼び出す\_HAS\_いない\_から返された\_ウォッチドッグ\_タイムアウト\_LIVEDUMP**](bug-check-0x1a3--call-has-not-returned-watchdog-timeout-livedump.md)                  |
| 0x000001A4 | [**DRIPS\_SW\_HW\_相違\_LIVEDUMP**](bug-check-0x1a4--drips-sw-hw-divergence-livedump.md)                                                    |
| 0x000001A5 | [**USB\_DRIPS\_BLOCKER\_突然\_削除\_LIVEDUMP**](bug-check-0x1a5--usb-drips-blocker-surprise-removal-livedump.md)                           |
| 0x000001A6 | [**BLUETOOTH\_エラー\_RECOVERY\_LIVEDUMP**](bug-check-0x1a6--bluetooth-error-recovery-livedump.md)                                                 |
| 0x000001A7 | [**SMB\_リダイレクター\_LIVEDUMP**] bug-check-0x1A7--smb-redirector-livedump.md)                                                                       |
| 0x000001A8 | [**ビデオ\_DXGKRNL\_黒い\_画面\_LIVEDUMP**](bug-check-0x1a8--video-dxgkrnl-black-screen-livedump.md)                                            |
| 0x000001B0 | [**VIDEO_MINIPORT_FAILED_LIVEDUMP**](bug-check-0x1b0--video-miniport-failed-livedump.md)                                                          |
| 0x000001C4 | [**ドライバー\_VERIFIER\_検出\_違反\_LIVEDUMP**](bug-check-0x1c4--driver-verifier-detected-violation-livedump.md)                            |
| 0x000001C5 | [**IO\_THREADPOOL\_デッドロック\_LIVEDUMP**](bug-check-0x1c5--io-threadpool-deadlock-livedump.md)                                                     |
| 0x000001C6 | [**高速\_÷ リソース\_PRECONDITION\_違反**](bug-check-0x1c6--fast-eresource-precondition-violation.md)                                         |
| 0x000001C7 | [**ストア\_データ\_構造\_破損**](bug-check-0x1c7--store-data-structure-corruption.md)                                                     |
| 0x000001C8 | [**手動で\_INITIATED\_POWER\_ボタン\_保持**](bug-check-0x1c8--manually-initiated-power-button-hold.md)                                          |
| 0x000001C9 | [**ユーザー\_モード\_ヘルス\_モニター\_LIVEDUMP**](bug-check-0x1c9--user-mode-health-monitor-livedump.md)                                                |
| 0x000001CA | [**代理\_ウォッチドッグ\_タイムアウト**](bug-check-0x1ca--synthetic-watchdog-timeout.md)                                                                |
| 0x000001CB | [**無効な\_サイロ\_デタッチ**](bug-check-0x1cb--invalid-silo-detach.md)                                                                              |
| 0x000001CC | [**EXRESOURCE_TIMEOUT_LIVEDUMP**](bug-check-0x1cc--exresource-timeout-livedump.md)                                                                |
| 0x000001CD | [**INVALID\_CALLBACK\_STACK_ADDRESS**](bug-check-0x1cd--invalid-callback-stack-address.md)                                                        |
| 0x000001CE | [**無効な\_カーネル\_スタック\_アドレス**](bug-check-0x1ce--invalid-kernel-stack-address.md)                                                           |
| 0x000001CF | [**ハードウェア\_ウォッチドッグ\_タイムアウト**](bug-check-0x1cf--hardware-watchdog-timeout.md)                                                                  |  
| 0x000001D0 | [**CPI\_ファームウェア\_ウォッチドッグ\_タイムアウト**](bug-check-0x1d0--acpi-firmware-watchdog-timeout.md)                                                        |
| 0x000001D1 | [**テレメトリ\_アサート\_LIVEDUMP**](bug-check-0x1d1--telemetry-asserts-livedump.md)                                                                |
| 0x000001D2 | [**ワーカー\_スレッド\_無効な\_状態**](bug-check-0x1d2--worker-thread-invalid-state.md)                                                             |
| 0x000001D3 | [**WFP\_INVALID\_OPERATION**](bug-check-0x1d3--wfp-invalid-operation.md)                                                                          |
| 0x000001D4 | [**UCMUCSI\_LIVEDUMP**](bug-check-0x1d4--ucmusci-livedump.md)                                                                                     |
| 0x000001D5 | [**DRIVER_PNP_WATCHDOG**](bug-check-0x1d5--driver-pnp-watchdog.md)                                                                                |
| 0x000001D6 | [**WORKER\_THREAD\_RETURNED\_WITH\_NON\_DEFAULT\_WORKLOAD\_CLASS**](bug-check-0x1d6--worker-thread-returned-with-non-default-workload-class.md)   |
| 0x000001D7 | [**EFS\_FATAL\_エラー**](bug-check-0x1d7--efs-fatal-error.md)                                                                                      |
| 0x000001D8 | [**UCMUCSI\_エラー**](bug-check-0x1d8--ucmucsi-failure.md)                                                                                       |
| 0x000001D9 | [**HAL\_IOMMU\_INTERNAL\_ERROR**](bug-check-0x1d8--ucmucsi-failure.md)                                                                            |
| 0x000001DB | [**IPI\_ウォッチドッグ\_タイムアウト**](bug-check-0x1db--ipi-watchdog-timeout.md)                                                                            |
| 0x000001DC | [**DMA_COMMON_BUFFER_VECTOR_ERROR**](bug-check-0x1dc--dma-common-buffer-vector-error.md)                                                          |
| 0x00000356 | [**XBOX\_ERACTRL\_CS\_タイムアウト**](bug-check-0x356--xbox-eractrl-cs-timeout.md)                                                                     |
| 0x00000BFE | [**BC\_BLUETOOTH\_VERIFIER\_エラー**](bug-check-0xbfe--bc-bluetooth-verifier-fault.md)                                                             |
| 0x00000BFF | [**BC\_BTHMINI\_VERIFIER\_エラー**](bug-check-0xbff--bc-bthmini-verifier-fault.md)                                                                 |
| 0x00020001 | [**ハイパーバイザー\_エラー**](bug-check-0x20001--hypervisor-error.md)                                                                                   |
| 0x1000007E | [**システム\_スレッド\_例外\_いない\_HANDLED\_M**](bug-check-0x1000007e--system-thread-exception-not-handled-m.md)                                  |
| 0x1000007F | [**予期しない\_カーネル\_モード\_トラップ\_M**](bug-check-0x1000007f--unexpected-kernel-mode-trap-m.md)                                                   |
| 0x1000008E | [**カーネル\_モード\_例外\_いない\_HANDLED\_M**](bug-check-0x1000008e--kernel-mode-exception-not-handled-m.md)                                      |
| 0x100000EA | [**スレッド\_STUCK\_IN\_デバイス\_ドライバー\_M**](bug-check-0x100000ea--thread-stuck-in-device-driver-m.md)                                              |
| 0x4000008A | [**スレッド\_TERMINATE\_保持\_ミュー テックス**](bug-check-0x4000008a--thread-terminate-held-mutex.md)                                                        |
| 0xC0000218 | [**ステータス\_できない\_ロード\_レジストリ\_ファイル**](bug-check-0xc0000218--status-cannot-load-registry-file.md)                                             |
| 0xC000021A | [**ステータス\_システム\_プロセス\_終了**](bug-check-0xc000021a--status-system-process-terminated.md)                                              |
| 0xC0000221 | [**ステータス\_イメージ\_チェックサム\_が一致しません**](bug-check-0xc0000221--status-image-checksum-mismatch.md)                                                  |
| 0 xdeaddead | [**手動で\_INITIATED\_CRASH1**](bug-check-0xdeaddead--manually-initiated-crash1.md)                                                             |

 

 

 





