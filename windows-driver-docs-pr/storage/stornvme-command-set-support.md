---
title: StorNVMe コマンド セットのサポート
description: StorNVMe コマンド セットのサポート
ms.assetid: c0bcee11-ea66-4726-99a2-ad18256cf616
ms.date: 01/13/2020
ms.localizationpriority: medium
ms.openlocfilehash: 68a7e099f13f2e0da3f93accd314d227cc69c45a
ms.sourcegitcommit: ee70846334ab6710ec0f9143e9f3a3754bc69f98
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2020
ms.locfileid: "76706937"
---
# <a name="stornvme-command-set-support"></a>StorNVMe コマンド セットのサポート

The matrices below list the NVMe *Admin* and *NVM* command sets and associated opcodes, and indicate the support provided by **StorNVMe** on Windows 10 version 1903 and later.  

## <a name="admin-command-set-support"></a>Admin Command Set Support

| オペコード  | NVMe Command                | StorNVMe Support      | 備考 |
| ------  | --------------------------  | --------------------- | -------- |
| 0       | Delete I/O Submission Queue | Internal Driver Usage |    |
| 1 で保護されたプロセスとして起動されました       | Create I/O Submission Queue | Internal Driver Usage |    |
| 2 で保護されたプロセスとして起動されました       | Get Log Page                | Internal Driver Usage; IOCTL_STORAGE_QUERY_PROPERTY |   |
| ホーム フォルダーが置かれているコンピューターにアクセスできない       | Delete I/O Completion Queue | Internal Driver Usage |   |
| 5       | Create I/O Completion Queue | Internal Driver Usage |
| 6       | 特定                    | Internal Driver Usage; IOCTL_STORAGE_QUERY_PROPERTY, IOCTL_STORAGE_FIRMWARE_GET_INFO |   |
| 8       | 中止                       |   | 以下は現在サポートされていません |
| 9       | Set Features                | Internal Driver Usage; IOCTL_STORAGE_SET_PROPERTY | Only enabled for Host Controlled Thermal Management Set Features for IOCTL_STORAGE_SET_PROPERTY |
| Ah      | Get Features                | Internal Driver Usage; IOCTL_STORAGE_QUERY_PROPERTY |   |
| Ch      | Asynchronous Event Request  | Internal Driver Usage |   |   |
| Dh      | 名前空間の管理        | IOCTL_STORAGE_PROTOCOL_COMMAND | Only enabled in Win PE mode for IOCTL_STORAGE_PROTOCOL_COMMAND |
| 10h     | Firmware Commit             | IOCTL_STORAGE_FIRMWARE_ACTIVATE | |
| 11h     | Firmware Image Download     | IOCTL_STORAGE_FIRMWARE_DOWNLOAD | |
| 14h     | Device Self-Test            | IOCTL_STORAGE_PROTOCOL_COMMAND  | |
| 15h     | Namespace Attachment        | IOCTL_STORAGE_PROTOCOL_COMMAND | Only enabled in Win PE mode for IOCTL_STORAGE_PROTOCOL_COMMAND |
| 19h     | Directive Send              | Internal Driver Usage |   |
| 1Ah     | Directive Receive           | Internal Driver Usage |   |
| 1Ch     | 仮想化管理   |   | 以下は現在サポートされていません |
| 1Dh     | NVMe-MI Send                | IOCTL_STORAGE_PROTOCOL_COMMAND | Only enabled in Win PE mode for IOCTL_STORAGE_PROTOCOL_COMMAND |
| 1Eh     | NVMe-MI Receive             | IOCTL_STORAGE_PROTOCOL_COMMAND | Only enabled in Win PE mode for IOCTL_STORAGE_PROTOCOL_COMMAND |
| 7Ch     | Doorbell Buffer Config      |   | 以下は現在サポートされていません |
| 80h     | Format NVM                  | IOCTL_SCSI_PASS_THROUGH, IOCTL_STORAGE_PROTOCOL_COMMAND, IOCTL_STORAGE_REINITIALIZE_MEDIA | Only enabled in Win PE mode for IOCTL_STORAGE_PROTOCOL_COMMAND. SCSIOP_SANITIZE for IOCTL_SCSI_PASS_THROUGH. IOCTL_STORAGE_REINITIALIZE_MEDIA only supports crypto erase. |
| 81h     | Security Send               | IOCTL_SCSI_PASS_THROUGH | SCSIOP_SECURITY_PROTOCOL_OUT for IOCTL_SCSI_PASS_THROUGH |
| 82h     | Security Receive            | IOCTL_SCSI_PASS_THROUGH | SCSIOP_SECURITY_PROTOCOL_IN for IOCTL_SCSI_PASS_THROUGH |
| 84h     | Sanitize                    | IOCTL_STORAGE_PROTOCOL_COMMAND | Only enabled in Win PE mode for IOCTL_STORAGE_PROTOCOL_COMMAND |
| 86h     | Get LBA Status              |   | 以下は現在サポートされていません |
| C0h-FFh | Vendor Specific             | IOCTL_STORAGE_PROTOCOL_COMMAND | Vendor-specific pass-through commands. Requires controller to support command effects log and command effect data of vendor command should report as supported. |

## <a name="nvm-command-set-support"></a>NVM Command Set Support

| オペコード  | NVMe Command                | StorNVMe Support      | 備考 |
| ------  | --------------------------  | --------------------- | -------- |
| 0       | フラッシュ                       | Internal Driver Usage, IOCTL_SCSI_PASS_THROUGH | SCSIOP_SYNCHRONIZE_CACHE for IOCTL_SCSI_PASS_THROUGH |
| 1 で保護されたプロセスとして起動されました       | 書き込み                       | Internal Driver Usage, IOCTL_SCSI_PASS_THROUGH | SCSIOP_WRITE/SCSIOP_WRITE16 for  IOCTL_SCSI_PASS_THROUGH |
| 2 で保護されたプロセスとして起動されました       | 読み取り                        | Internal Driver Usage, IOCTL_SCSI_PASS_THROUGH | SCSIOP_READ/SCSIOP_READ16 for IOCTL_SCSI_PASS_THROUGH |
| ホーム フォルダーが置かれているコンピューターにアクセスできない       | Write Uncorrectable         |   | 以下は現在サポートされていません |
| 5       | 時差                     | IOCTL_STORAGE_PROTOCOL_COMMAND | Only enabled in Win PE mode for IOCTL_STORAGE_PROTOCOL_COMMAND |
| 8       | Write Zeroes                |   | 以下は現在サポートされていません |
| 9       | Dataset Management          | IOCTL_SCSI_PASS_THROUGH | Only TRIM (Deallocate); SCSIOP_UNMAP for IOCTL_SCSI_PASS_THROUGH |
| Ch      | 検証                      |   | 以下は現在サポートされていません |
| Dh      | Reservation Register        |   | 以下は現在サポートされていません |
| Eh      | Reservation Report          |   | 以下は現在サポートされていません |
| 11h     | Reservation Acquire         |   | 以下は現在サポートされていません |
| 15h     | Reservation Release         |   | 以下は現在サポートされていません |
| 80h-FFh | Vendor Specific             | IOCTL_STORAGE_PROTOCOL_COMMAND | Vendor-specific pass-through commands. Requires controller to support command effects log and command effect data of vendor command should report as supported. |
