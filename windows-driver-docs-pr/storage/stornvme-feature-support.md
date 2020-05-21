---
title: StorNVMe でサポートされている NVMe 機能
description: StorNVMe でサポートされている NVMe 機能
ms.assetid: 96b62fbb-bcf3-402d-ba29-0a61dc95c92c
ms.date: 05/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: 54b7529f57bcab5c970ee0d4c4ca08df431bb3e3
ms.sourcegitcommit: d395d4b36f39d3557adda53735a4fdc8745a6408
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83642591"
---
# <a name="nvme-features-supported-by-stornvme"></a>StorNVMe でサポートされている NVMe 機能

次の表は、NVME の機能の一覧です。また、Windows 10 バージョン1903以降のバージョンで**Stornvme**が提供するサポートを示しています。

詳細については、「 [NVMe ドライブの操作](https://docs.microsoft.com/windows/win32/fileio/working-with-nvme-devices#protocol-specific-queries)」を参照してください。

| 機能  | サポートされています | 説明 |
| :------- | :-------: | :------- |
| ファームウェアの更新プロセス                                        | x |  スロット1読み取り専用、複数スロットのコミット/ダウンロードをサポートします。 コントローラーに対して、FW 更新の粒度を報告します。 |
| リセットせずにファームウェアをアクティブ化する                              | x | |
| メタデータの処理                                              |   | |
| エンドツーエンドのデータ保護                                     |   | |
| 電源管理                                               | x | 操作不可能な電源状態をサポートします。 自律電源状態の移行は、既定では無効になっています。 最新のスタンドアロンで選択されたプラットフォームでは、ランタイム D3 の移行が既定で有効になっています。 ホスト制御された thermal 管理 IOCTL_STORAGE_QUERY_PROPERTY と IOCTL_STORAGE_SET_PROPERTY によってサポートされる機能を取得および設定します。 |
| 仮想化の機能強化                                    |   | |
| ソフトウェアエミュレーションの Doorbell Stride                         |   | |
| 標準ベンダー固有のコマンド形式                        |   | |
| Reservations                                                   |   | |
| ホストのメモリバッファー                                             | x | |
| 保護されたメモリブロックの再生                                  |   | |
| デバイスの自己テスト操作                                    | x | ネイティブサポートはありません。機能は IOCTL_STORAGE_PROTOCOL_COMMAND から利用できます。|
| 名前空間の管理                                           | x | ネイティブサポートはありません。機能は、WinPE モードの IOCTL_STORAGE_PROTOCOL_COMMAND を通じて利用できます。 |
| ブートパーティション                                                |   | |
| テレメトリ                                                      | x | READ_BUFFER_MODE_ERROR_HISTORY としてのバッファーモードでのコマンド SCSIOP_READ_DATA_BUFF16 IOCTL_SCSI_PASS_THROUGH 使用してサポートされます。 IOCTL_STORAGE_QUERY_PROPERTY の Storageadapterprotocol固有のプロパティ/Storagedeviceprotocol固有のプロパティを介して使用することもできます。 ホストテレメトリの場合は、Windows 10 バージョン2004以降の IOCTL_STORAGE_GET_DEVICE_INTERNAL_LOG からも利用できます。 |
| サニタイズ操作                                            | x | WinPE モードの IOCTL_STORAGE_PROTOCOL_COMMAND でサポートされます。 |
| 復旧レベルの読み取り                                            |   | |
| 耐久性のあるグループ                                               | x | 情報は、を使用して取得でき IOCTL_STORAGE_QUERY_PROPERTY |
| 予測可能な待機時間モード                                       |   | |
| 名前空間の書き込み保護                                     |   | |
| 非対称名前空間のアクセスレポート                          |   | |
| LBA 状態の取得                                                 |   | |
| SQ の関連付け                                                |   | |
| ベンダ固有の情報の Uuid                          |   | |
| I/o サイズとアラインメントの準拠によるパフォーマンスの向上 | x | 名前空間の最適な IO 境界 (NOIOB) をサポートします。 現在、NPWG、NPWA、NPDG、NPWA、および NOWS はサポートされていません。 |

## <a name="reference-links"></a>参照リンク

- [NVMe デバイスの操作](https://docs.microsoft.com/windows/win32/fileio/working-with-nvme-devices)
- [NVMe ストレージプロトコルデータ型](https://docs.microsoft.com/windows/win32/api/winioctl/ne-winioctl-storage_protocol_nvme_data_type)
