---
title: ファームウェアに関する Windows エンジニアリング ガイド (WEG)
description: ファームウェアに関する Windows エンジニアリング ガイド (WEG) は、システム ファームウェアに関連するベスト プラクティスの実装時に従うロードマップを提供します。
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: fc5fd86aa82665f574d42dde95d2a998a4cd2a02
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337621"
---
# <a name="firmware-windows-engineering-guide-weg"></a>ファームウェアに関する Windows エンジニアリング ガイド (WEG)

ファームウェアに関する Windows エンジニアリング ガイド (WEG) は、システム ファームウェアに関連するベスト プラクティスの実装時に従うロードマップを提供します。


## <a name="in-this-section"></a>このセクションの内容

[UEFI のセキュリティ](uefi-security.md)

[ファームウェアの更新](firmware-update.md)

[SMBIOS](smbios.md)

[HTTPS](https-boot.md)

[ファームウェアでの Wi-fi のサポート](wi-fi-support-in-firmware.md)

[従来の MBR ディスクから Windows 10 では GPT ディスクに切り替える](switch-from-legacy-mbr-disk-to-gpt-disk-with-windows-10.md)

[ファームウェア WEG よく寄せられる質問](frequently-asked-questions.md)

[Windows 7 および Windows 10 以降の更新プログラムのシステム ファームウェアを構成します。](configure-system-firmware-for-windows-7-and-later-update-for-windows-10.md)

[ローカルで SMBIOS をクエリするサンプル PowerShell スクリプト](sample-powershell-script-to-query-smbios-locally.md)

                                           





## <a name="firmware-weg-terminology"></a>ファームウェア WEG 用語集

ファームウェア WEG 全体で、次の用語が使用されます。

- ACPI - Advanced Configuration and Power Interface

- BCD のブート構成データ

- BIOS の基本入出力システム

- CSM - 互換性サポート モジュール

- eMMC - マルチ メディアのコント ローラーの埋め込み

- ESRT – EFI システム リソースのテーブル

- GPT – GUID パーティション テーブル

- GUID: グローバルに一意の Id

- HDD のハード ディスク ドライブ

- HSTI/HSTS – ハードウェア セキュリティ テストの容易性インターフェイス/仕様

- HVCI ハイパーバイザー コードの整合性

- IOMMU - – 入出力メモリ管理ユニット

- [INT10](https://en.wikipedia.org/wiki/INT_10H) -BIOS の基本的なビデオの表示に使用する呼び出しを中断します。

- マット/MADT – メモリ A

- MBR - マスター ブート レコード

- されます – メモリ上書きの要求

- OEM - Original Equipment Manufacturer/製造

- RPMC – 再生モノトニックなカウンターを保護します。

- SMBIOS – システム管理の基本入出力システム

- SPI - シリアル周辺インターフェイス

- TCG - Trusted Computing Group

- TPM-トラステッド プラットフォーム モジュール

- UEFI の Unified Extensible Firmware インターフェイス

- WEG – Windows エンジニア リングのガイド

- WinPE の Windows プレインストール環境

- WinRE - Windows 回復環境

- WSMT - Windows SMM セキュリティ緩和策テーブル



