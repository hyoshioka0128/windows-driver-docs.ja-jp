---
title: StorNVMe コマンドセットのサポート
description: StorNVMe コマンドセットのサポート
ms.assetid: c0bcee11-ea66-4726-99a2-ad18256cf616
ms.date: 12/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: ff9ffed8c39469bfc086ebee85b1be55722fd248
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252079"
---
# <a name="stornvme-command-set-support"></a>StorNVMe コマンドセットのサポート

次の表は、NVMe *Admin*と*nvm*コマンドセットおよび関連するオペコードを一覧表示し、 **stornvme**が各コマンドに提供するサポートを示しています。  

## <a name="admin-command-set-support"></a>管理コマンドセットのサポート

| オペコード  | NVMe コマンド                | StorNVMe のサポート      | コメント |
| ------  | --------------------------  | --------------------- | -------- |
| 0       | I/o 送信キューの削除 | 内部ドライバーの使用 |    |
| 1       | I/o 送信キューの作成 | 内部ドライバーの使用 |    |
| 2       | [ログの取得] ページ                | 内部ドライバーの使用IOCTL_STORAGE_QUERY_PROPERTY |   |
| ホーム フォルダーが置かれているコンピューターにアクセスできない       | I/o 完了キューの削除 | 内部ドライバーの使用 |   |
| 5       | I/o 完了キューの作成 | 内部ドライバーの使用 |
| 6       | ため                    | 内部ドライバーの使用IOCTL_STORAGE_QUERY_PROPERTY、IOCTL_STORAGE_FIRMWARE_GET_INFO |   |
| 8       | 中止                       |   | 現在サポートされていません |
| 9       | 機能の設定                | 内部ドライバーの使用IOCTL_STORAGE_SET_PROPERTY | IOCTL_STORAGE_SET_PROPERTY 用のホスト制御の温度管理セット機能に対してのみ有効です |
| Ah      | 機能の取得                | 内部ドライバーの使用IOCTL_STORAGE_QUERY_PROPERTY |   |
| ハーフ      | 非同期イベント要求  | 内部ドライバーの使用 |   |   |
| Dh      | 名前空間の管理        | IOCTL_STORAGE_PROTOCOL_COMMAND | IOCTL_STORAGE_PROTOCOL_COMMAND の Win PE モードでのみ有効です |
| 10h     | ファームウェアのコミット             | IOCTL_STORAGE_FIRMWARE_ACTIVATE | |
| 11h     | ファームウェアイメージのダウンロード     | IOCTL_STORAGE_FIRMWARE_DOWNLOAD | |
| 14h     | デバイスのセルフテスト            | IOCTL_STORAGE_PROTOCOL_COMMAND  | |
| 15h     | 名前空間の添付ファイル        | IOCTL_STORAGE_PROTOCOL_COMMAND | IOCTL_STORAGE_PROTOCOL_COMMAND の Win PE モードでのみ有効です |
| 19h     | ディレクティブの送信              | 内部ドライバーの使用 |   |
| 1Ah     | ディレクティブの受信           | 内部ドライバーの使用 |   |
| 1Ch     | 仮想化管理   |   | 現在サポートされていません |
| 1 Dh     | NVMe-MI 送信                | IOCTL_STORAGE_PROTOCOL_COMMAND | IOCTL_STORAGE_PROTOCOL_COMMAND の Win PE モードでのみ有効です |
| 1 Eh     | NVMe-MI 受信             | IOCTL_STORAGE_PROTOCOL_COMMAND | IOCTL_STORAGE_PROTOCOL_COMMAND の Win PE モードでのみ有効です |
| 7Ch     | Doorbell バッファー構成      |   | 現在サポートされていません |
| 80h     | NVM のフォーマット                  | IOCTL_SCSI_PASS_THROUGH、IOCTL_STORAGE_PROTOCOL_COMMAND、IOCTL_STORAGE_REINITIALIZE_MEDIA | IOCTL_STORAGE_PROTOCOL_COMMAND の Win PE モードでのみ有効です。 IOCTL_SCSI_PASS_THROUGH の SCSIOP_SANITIZE。 IOCTL_STORAGE_REINITIALIZE_MEDIA は、暗号化消去だけをサポートします。 |
| 81h     | セキュリティ送信               | IOCTL_SCSI_PASS_THROUGH | IOCTL_SCSI_PASS_THROUGH の SCSIOP_SECURITY_PROTOCOL_OUT |
| 82h     | セキュリティの受信            | IOCTL_SCSI_PASS_THROUGH | IOCTL_SCSI_PASS_THROUGH の SCSIOP_SECURITY_PROTOCOL_IN |
| 84 h     | 不要部分                    | IOCTL_STORAGE_PROTOCOL_COMMAND | IOCTL_STORAGE_PROTOCOL_COMMAND の Win PE モードでのみ有効です |
| 86h     | LBA 状態の取得              |   | 現在サポートされていません |
| C0h-FFh | ベンダー固有             | IOCTL_STORAGE_PROTOCOL_COMMAND | ベンダー固有のパススルーコマンド。 コマンド効果ログをサポートするためにコントローラーが必要です。また、ベンダコマンドのコマンド効果データはサポートされているものとして報告する必要があります。 |

## <a name="nvm-command-set-support"></a>NVM コマンドセットのサポート

| オペコード  | NVMe コマンド                | StorNVMe のサポート      | コメント |
| ------  | --------------------------  | --------------------- | -------- |
| 0       | Flush                       | 内部ドライバーの使用状況、IOCTL_SCSI_PASS_THROUGH | IOCTL_SCSI_PASS_THROUGH の SCSIOP_SYNCHRONIZE_CACHE |
| 1       | 書き込み                       | 内部ドライバーの使用状況、IOCTL_SCSI_PASS_THROUGH | IOCTL_SCSI_PASS_THROUGH の SCSIOP_WRITE/SCSIOP_WRITE16 |
| 2       | Read                        | 内部ドライバーの使用状況、IOCTL_SCSI_PASS_THROUGH | IOCTL_SCSI_PASS_THROUGH の SCSIOP_READ/SCSIOP_READ16 |
| ホーム フォルダーが置かれているコンピューターにアクセスできない       | 修正不可能に書き込み         |   | 現在サポートされていません |
| 5       | 時差]                     | IOCTL_STORAGE_PROTOCOL_COMMAND | IOCTL_STORAGE_PROTOCOL_COMMAND の Win PE モードでのみ有効です |
| 8       | ゼロの書き込み                |   | 現在サポートされていません |
| 9       | データセットの管理          | IOCTL_SCSI_PASS_THROUGH | トリムのみ (割り当て解除);IOCTL_SCSI_PASS_THROUGH の SCSIOP_UNMAP |
| ハーフ      | 検証                      |   | 現在サポートされていません |
| Dh      | 予約レジスタ        |   | 現在サポートされていません |
| Eh      | 予約レポート          |   | 現在サポートされていません |
| 11h     | 予約の取得         |   | 現在サポートされていません |
| 15h     | 予約リリース         |   | 現在サポートされていません |
| 80h-FFh | ベンダー固有             | IOCTL_STORAGE_PROTOCOL_COMMAND | ベンダー固有のパススルーコマンド。 コマンド効果ログをサポートするためにコントローラーが必要です。また、ベンダコマンドのコマンド効果データはサポートされているものとして報告する必要があります。 |
