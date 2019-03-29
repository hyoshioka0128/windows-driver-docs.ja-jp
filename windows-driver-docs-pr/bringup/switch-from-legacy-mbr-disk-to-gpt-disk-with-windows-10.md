---
title: レガシ MBR ディスクから Windows 10 では GPT ディスクに切り替える
description: シームレスなアップグレードを有効にして、Windows 10 の新機能と更新のセキュリティ機能を活用するユーザーを有効にするためのガイダンスを提供します。
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 98df70836d05e6f36c8dd8bac56d1e8e44b5c1f2
ms.sourcegitcommit: 3cdabbe0af52459e484e093a9e11da8f5312daf6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2019
ms.locfileid: "58441927"
---
# <a name="switch-from-legacy-mbr-disk-to-gpt-disk-with-windows-10"></a>レガシ MBR ディスクから Windows 10 では GPT ディスクに切り替える

Windows 7 などのダウンレベルのオペレーティング システムからのアップグレードや強化されたセキュリティ機能の UEFI ブートする BIOS ブートからの移行を容易になります。 Microsoft は、次の情報を提供しています。 次のセクションの手順は Windows 10 へのシームレスなアップグレードを有効にして、ユーザーの Windows 10 の新機能と更新のセキュリティ機能を活用する機能を有効にします。 目的で、以下の手順では、GPT として GUID パーティション テーブルと従来の MBR ブート ディスクとして従来のマスター ブート レコードに言及されます。

これら 4 つの構成が使用されます。

- Config\#互換性サポート モジュール (CSM) または CSM がファームウェアで無効にせずに 1 - UEFI ブートします。 GPT のハード ディスク ドライブ (HDD) が必要です。
- Config \# GPT HDD からのブートが有効な CSM と 2 での UEFI ブート
- Config\#レガシ MBR HDD からのブートが有効な CSM 3 - 従来の BIOS ブート
- Config\#レガシ MBR HDD からのブートが有効な CSM と 4 での UEFI ブート

## <a name="upgrade-paths"></a>アップグレード パス

| 既存の OS + Config | ターゲット OS + Config | 結果 | セキュリティ オプション |
| ---  |--- | --- | --- |
| Windows 7 **x64** CSM は UEFI ファームウェアでシステムにインストールされている、GPT の HDD で有効になって (Config \# 2) | Windows 10 **x64** CSM GPT HDD で有効になっている UEFI ファームウェアにインストールされている (Config \# 2)        | 起動し、Windows 10 の OS を実行               | OS は MS を使用することが CSM が無効になるとは、ファームウェアでサポートされているセキュリティ機能 |
| Windows 7 **x64** NTFS HDD のアクティブなパーティションを BIOS にインストールされている (Config \# 3)               | Windows 10 **x64** NTFS HDD のアクティブなパーティションを BIOS にインストールされている (Config \# 3)         | 起動し、Windows 10 の OS を実行               | Bitlocker を活用することのみ                                                           | このドキュメントで扱わない内容                                                                  |
| Windows 7 **x86** NTFS HDD のアクティブなパーティションを BIOS にインストールされている (Config \# 3)               | Windows 10 **x86** NTFS HDD のアクティブなパーティションを BIOS にインストールされている動作を = (Config \# 3) | 起動し、Windows 10 の OS を実行               | Bitlocker を活用することのみ                                                           | このドキュメントで扱わない内容                                                                  |
| Windows 7 **x86**アクティブ パーティションを NTFS で BIOS にインストールされている (Config \# 3)                   | Windows 10 **x64** NTFS HDD のアクティブなパーティションを BIOS にインストールされている (Config \# 3)         | インストール メディアが必要ですし、クリーン インストールします。 | Bitlocker (その他のセキュリティ機能には、UEFI ブートが必要です) を活用することのみ               |
| Windows 7 **x64**アクティブ パーティションを NTFS で BIOS にインストールされている (Config \# 3)                   | Windows 10 **x64** CSM GPT HDD で無効になっている UEFI ファームウェアにインストールされている (Config \# 1)        | 次の特別な手順                      | OS は MS を使用することがファームウェアでサポートされているセキュリティ機能

## <a name="definition-of-terms"></a>用語の定義

**互換性サポート モジュール (CSM)** 通常を有効にしたり、ファームウェアで無効になっています。 このモジュールは、容易にするが、従来のマスター ブート レコード (MBR) のアクティブなパーティションにブートは指定しません。 /の BIOS ファームウェア ブートのオプションによっては、CSM を有効にして、ブートする GPT ディスクを使用して、UEFI ブート モードまたはレガシ MBR ブート モードを選択することができます。 CSM を有効になっており、メモリに読み込まれることは、ブート UEFI Windows 7 の必要があります。
*UEFI ブート*CSM が有効にする必要はありません。 無効になっている CSM、ハード ディスク Drive(HDD) の起動がアクティブなパーティションを使用しない、認識されるファイル システムをブート ファイルを FAT、FAT32 などの見た目 EFI システム パーティション (ESP) を使用すること。 ブート ファイルは、a) NVRAM (boot000n) または b のいずれかで定義できます) を使用して UEFI 仕様には、フォールバックの起動方法を探してが定義されている\\EFI\\ブート\\ブート (arch) .efi (例: bootx64.efi) このブートの方法では動作しません、従来の MBR には、NTFS ブート ディスクが構成されています。

**従来の MBR ブート**は GUID パーティション テーブル (GPT) ディスクを認識できません。 アクティブなパーティションおよびディスクへのアクセスを容易に BIOS のサポートが必要です。 古いと HDD のサイズとパーティションの数に制限されています。 UEFI ファームウェアのシステムでは、CSM が有効になっており、アクティブなパーティションの起動を簡単にメモリに読み込まれることが必要です。

## <a name="in-this-section"></a>このセクションの内容

[新しいメソッド - Windows 10 バージョン 1703 以降](new-method--windows-10--version-1703-and-later.md)

[MBR2GPT ツール テスト ガイダンス](mbr2gpt-tool-test-guidance.md)

[古いメソッド - Windows 10 バージョン 1607 およびそれ以前](old-method--windows-10--version-1607-and-earlier.md)

[インストールされている x64 に変換する方法 システムの Windows 7](how-to-convert-an-installed-x64-windows-7.md)

## <a name="related-resources"></a>関連リソース

[Windows 10 の仕様](https://www.microsoft.com/windows/Windows-10-specifications)
