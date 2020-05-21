---
title: StorNVMe SCSI 変換のサポート
description: StorNVMe SCSI 変換のサポート
ms.assetid: cd903ef8-9528-46a5-a276-06cf2fff2b88
ms.date: 05/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: ab729f36428b9db85798ffbb65ae02e3435cc552
ms.sourcegitcommit: d395d4b36f39d3557adda53735a4fdc8745a6408
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83642596"
---
# <a name="stornvme-scsi-translation-support"></a>StorNVMe SCSI 変換のサポート

次の表に、SCSI コマンドと、変換された NVMe コマンド (該当する場合) を示します。 Windows 10 バージョン1903以降のバージョンの**Stornvme**は、SCSI Translation Reference Rev 1.5 に準拠しています。

詳細については、「 [NVMe ドライブの操作](https://docs.microsoft.com/windows/win32/fileio/working-with-nvme-devices#protocol-specific-queries)」を参照してください。

| SCSI コマンド | NVMe コマンド |
| ------------ | ------------ |
| 単位/サニタイズの書式設定    | NVM のフォーマット                  |
| 照会                 | 識別                    |
| ログの意味               | 機能の取得、ログの取得ページ  |
| モードの選択 (10)        | -                           |
| モードの意味 (10)         | 特定、機能の取得      |
| 読み取り (10)               | 読み取り                        |
| 読み取り (16)               | 読み取り                        |
| 読み取り容量 (10)      | 識別                    |
| 読み取り容量 (16)      | 識別                    |
| データバッファー16の読み取り     | [ログの取得] ページ                |
| レポート Lun             | 識別                    |
| のセキュリティプロトコル    | セキュリティの受信            |
| セキュリティプロトコルの送信   | セキュリティ送信               |
| 診断の送信         | 該当なし                         |
| 停止単位の開始         | 機能の設定、機能の取得  |
| キャッシュの同期 (10)  | フラッシュ                       |
| テスト単位の準備完了         | -                           |
| Unmap                   | データセットの管理          |
| 検証10               | 確認事項                      |
| 検証16               | 確認事項                      |
| 書き込み10                | Write                       |
| 書き込み16                | Write                       |
| バッファーの書き込み            | ファームウェアのダウンロード、アクティブ化 |
