---
title: StorNVMe SCSI 変換のサポート
description: StorNVMe SCSI 変換のサポート
ms.assetid: cd903ef8-9528-46a5-a276-06cf2fff2b88
ms.date: 01/13/2020
ms.localizationpriority: medium
ms.openlocfilehash: 3ba918b2dc76b2a99c8d095f194f36b6f91c08cb
ms.sourcegitcommit: ee70846334ab6710ec0f9143e9f3a3754bc69f98
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2020
ms.locfileid: "76706929"
---
# <a name="stornvme-scsi-translation-support"></a>StorNVMe SCSI 変換のサポート

次の表に、SCSI コマンドと、変換された NVMe コマンド (該当する場合) を示します。 Windows 10 バージョン1903以降のバージョンの**Stornvme**は、SCSI Translation Reference Rev 1.5 に準拠しています。

| SCSI コマンド | NVMe Command |
| ------------ | ------------ |
| 単位/サニタイズの書式設定    | Format NVM                  |
| 照会                 | 特定                    |
| ログの意味               | 機能の取得、ログの取得ページ  |
| モードの選択 (10)        | -                           |
| モードの意味 (10)         | 特定、機能の取得      |
| 読み取り (10)               | 読み取り                        |
| 読み取り (16)               | 読み取り                        |
| 読み取り容量 (10)      | 特定                    |
| 読み取り容量 (16)      | 特定                    |
| データバッファー16の読み取り     | Get Log Page                |
| レポート Lun             | 特定                    |
| のセキュリティプロトコル    | Security Receive            |
| セキュリティプロトコルの送信   | Security Send               |
| 診断の送信         | なし                         |
| 停止単位の開始         | 機能の設定、機能の取得  |
| キャッシュの同期 (10)  | フラッシュ                       |
| テスト単位の準備完了         | -                           |
| Unmap                   | Dataset Management          |
| 検証10               | 検証                      |
| 検証16               | 検証                      |
| 書き込み10                | 書き込み                       |
| 書き込み16                | 書き込み                       |
| バッファーの書き込み            | ファームウェアのダウンロード、アクティブ化 |
