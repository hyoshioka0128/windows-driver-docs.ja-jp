---
title: StorNVMe でサポートされている NVMe 機能
description: StorNVMe でサポートされている NVMe 機能
ms.assetid: 96b62fbb-bcf3-402d-ba29-0a61dc95c92c
ms.date: 01/13/2020
ms.localizationpriority: medium
ms.openlocfilehash: 15374cbab57e3b87abfb933f165ab50ab88a979e
ms.sourcegitcommit: bc6ee54ecf053edf144aab7eeb811e0d233296d3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80435020"
---
# <a name="nvme-features-supported-by-stornvme"></a>StorNVMe でサポートされている NVMe 機能

次の表は、NVME の機能の一覧です。また、Windows 10 バージョン1903以降のバージョンで**Stornvme**が提供するサポートを示しています。

| 機能  | サポート対象 | コメント |
| :------- | :-------: | :------- |
| ファームウェアの更新プロセス                                        | X |  スロット1読み取り専用、複数スロットのコミット/ダウンロードをサポートします。 コントローラーに対して、FW 更新の粒度を報告します。 |
| リセットせずにファームウェアをアクティブ化する                              | X | |
| メタデータの処理                                              |   | |
| エンドツーエンドのデータ保護                                     |   | |
| 電源管理                                               | X | 操作不可能な電源状態をサポートします。 自律電源状態の移行は、既定では無効になっています。 最新のスタンドアロンで選択されたプラットフォームでは、ランタイム D3 の移行が既定で有効になっています。 ホスト制御された thermal 管理 IOCTL_STORAGE_QUERY_PROPERTY と IOCTL_STORAGE_SET_PROPERTY によってサポートされる機能を取得および設定します。 |
| 仮想化の機能強化                                    |   | |
| ソフトウェアエミュレーションの Doorbell Stride                         |   | |
| 標準ベンダー固有のコマンド形式                        |   | |
| 予約                                                   |   | |
| ホストのメモリバッファー                                             | X | |
| 保護されたメモリブロックの再生                                  |   | |
| デバイスの自己テスト操作                                    | X | ネイティブサポートはありません。機能は IOCTL_STORAGE_PROTOCOL_COMMAND から利用できます。|
| 名前空間の管理                                           | X | ネイティブサポートはありません。機能は、WinPE モードの IOCTL_STORAGE_PROTOCOL_COMMAND を通じて利用できます。 |
| ブートパーティション                                                |   | |
| 製品利用統計情報                                                      | X | READ_BUFFER_MODE_ERROR_HISTORY としてのバッファーモードでのコマンド SCSIOP_READ_DATA_BUFF16 IOCTL_SCSI_PASS_THROUGH 使用してサポートされます。 IOCTL_STORAGE_QUERY_PROPERTY の Storageadapterprotocol固有のプロパティ/Storagedeviceprotocol固有のプロパティを介して使用することもできます。 ホストテレメトリの場合は、IOCTL_STORAGE_GET_DEVICE_INTERNAL_LOG でも使用できます。 |
| サニタイズ操作                                            | X | WinPE モードの IOCTL_STORAGE_PROTOCOL_COMMAND でサポートされます。 |
| 復旧レベルの読み取り                                            |   | |
| 耐久性のあるグループ                                               | X | 情報は、を使用して取得でき IOCTL_STORAGE_QUERY_PROPERTY |
| 予測可能な待機時間モード                                       |   | |
| 名前空間の書き込み保護                                     |   | |
| 非対称名前空間のアクセスレポート                          |   | |
| LBA 状態の取得                                                 |   | |
| SQ の関連付け                                                |   | |
| ベンダ固有の情報の Uuid                          |   | |
| I/o サイズとアラインメントの準拠によるパフォーマンスの向上 | X | 名前空間の最適な IO 境界 (NOIOB) をサポートします。 現在、NPWG、NPWA、NPDG、NPWA、および NOWS はサポートされていません。 |

<!---  Everything commented out was provided by Vishal but is not in NVME Spec Section 8

| Directives                                                     | X | Supports Stream and Identify directive |
|                                                                |   | |
| Version Compliance                                             | X | Compliance of version <= 1.4 |
| Recommended Arbitration Burst                                  | X | User could set any value apart from controller reported value through registry key ArbitrationBurst |
| Controller Multi-path IO                                       |   | |
| Namespace sharing capabilities                                 |   | |
| Maximum Data Transfer Size Support                             | X | |
| Runtime D3 latency                                             | X | |
| Namespace Attribute Notices event                              | X | Log the event and trigger namespace reenumeration based on change log |
| Firmware Activation Notices event                              | X | Log the event and read the log page |
| Endurance Group Event Aggregate Log Page notices event         |   | |
| Controller Attributes                                          | X | Non-operational Power State Permissive Mode and NVM Sets are checked and used |
| NVM Sets                                                       | X | |
| FRU Globally Unique Identifier                                 |   | |
| Security Send/Security Receive Support                         | X | |
| Format NVM Support                                             | X | Supported through SCSI sanitize |
| NVMe-MI Send and NVMe-MI Receive                               | X | Supported through IOCTL_STORAGE_PROTOCOL_COMMAND in WinPE mode |
| Doorbell Buffer Config Support                                 |   | |
| Abort Command Support with Specified Limits                    |   | |
| Asynchronous Event Request Support                             | X | Supports limited to event count of 4 |
| SMART Log Page Support                                         | X | Supports log page per Namespace |
| Command Supported and Effects Log Page Support                 | X | Checked for vendor specific command execution |
| Extended Data for Log Page                                     | X | Supported through IOCTL_STORAGE_QUERY_PROPERTY |
| Persistent Event Log Support                                   |   | |
| Firmware Activation maximum time support                       |   | Currently not supported even though firmware activation without reset is supported |
| Firmware Update Granularity                                    | X | |
| Keep Alive Support                                             |   | |
| Temperature Report                                             | X | WCTEMP and CCTEMP. Accessible though IOCTL_STORAGE_QUERY_PROPERTY |
| Multiple Namespaces                                            | X | Supports runtime enumeration of namespaces |
| Compare Command                                                | X | Supported through IOCTL_STORAGE_PROTOCOL_COMMAND in WinPE mode |
| Write Uncorrectable Command                                    |   | |
| Dataset Management Command                                     | X | |
| Write Zeroes                                                   |   | |
| Set Features Save Option                                       | X | Currently only used for VWC persistent setting |
| Timestamp                                                      | X | |
| Verify Command                                                 |   | |
| Fused Operations (Compare and Write)                           |   | |
| Volatile Write Cache                                           | X | |
| Atomic Write Unit Normal                                       |   | |
| NVMe Qualified Names                                           |   | |
| Namespace Thinprovisioning                                     | X | |
| NVMe Boot                                                      | X | |
| Controller Fatal Status Condition                              | X | Log the event and continue with controller re-initialization |
--->

## <a name="reference-links"></a>参照リンク
- [NVMe デバイスの操作](https://docs.microsoft.com/windows/win32/fileio/working-with-nvme-devices)
- [NVMe ストレージ廃棄データ型](https://docs.microsoft.com/windows/win32/api/winioctl/ne-winioctl-storage_protocol_nvme_data_type)
