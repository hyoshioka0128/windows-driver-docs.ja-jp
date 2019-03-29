---
title: 既存のブート エントリに対するバックアップ ファイルの識別
description: 既存のブート エントリに対するバックアップ ファイルの識別
ms.assetid: 8f7e13b4-32f9-4b54-a8ab-db8148434ae8
keywords:
- NVRAM ブート オプション WDK、バックアップ ファイルの検索
- EFI NVRAM ブート オプション WDK、バックアップ ファイルの検索
- WDK のブート オプションを検索します。
- ブート エントリ バックアップ WDK を検索します。
- 既存のブート エントリは、WDK を検索します。
- ブート エントリ バックアップ WDK
- ブート エントリのバックアップ ファイルを識別します。
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8777a62ce485103921a1c7bc93ce160be870d580
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573645"
---
# <a name="identifying-backup-files-for-existing-boot-entries"></a>既存のブート エントリに対するバックアップ ファイルの識別

ブート エントリのバックアップ コピーのファイル名で検索するには、エントリの EFI ブート エントリ ID が必要です。 ただし、Bootcfg も Nvrboot はこの ID を表示します。

代わりに、ブートでブート エントリのバックアップ コピーを検索できます*xxxx* EFI パーティションのインストール ディレクトリのファイル。 インストール ディレクトリを検索するには、オペレーティング システムのインストールのブート ローダーのファイルへのパスを見つけます。 インストールのブート エントリのバックアップ ファイルは、同じディレクトリに格納されます。

使用して、 **nvrboot d** (表示) コマンドまたは**bootcfg**または**bootcfg クエリ**オペレーティング システムのブート ローダーのディレクトリへのパスを表示するコマンド格納されています。

EFI パーティションで次の例では、ブート ローダーのブート エントリが格納されている、 \\Microsoft\\WINNT50 サブディレクトリ。 このインストールのブート エントリのバックアップ コピーがブートという名前のファイル*xxxx*同じサブディレクトリにします。

> [!NOTE]
> **ブート エントリ ID** Bootcfg 内のフィールドと Nvrboot でブート エントリの数で EFI ブート エントリ ID が表示されません。 Bootcfg と Nvrboot Id は、行番号のブート エントリの順序を表す、**ブート エントリ**セクションおよびエントリの順序は変更時に変更します。

Bootcfg サンプルを次に示すようにブート ローダーのファイルへのパスが表示されます、 **BootFilePath**フィールド。

Bootcfg としてファイルの場所が表示されます、 [NT デバイス名](https://docs.microsoft.com/windows-hardware/drivers/kernel/nt-device-names)ブート ローダーのファイルへのファイル システム パスを続けて、パーティションの。

```
Boot Entries
------------
Boot entry ID:    1
OS Friendly Name: Windows Server 2003, Enterprise
OsLoadOptions:     /debug /debugport=COM1 /baudrate=115200
BootFilePath:     \Device\HarddiskVolume1\EFI\Microsoft\WINNT50\ia64ldr.efi
OsFilePath:       \Device\HarddiskVolume3\WINDOWS
```

Nvrboot ディスプレイの次のサンプルでは、オペレーティング システムのインストールのブート ローダーのファイルへのパスが表示されます、 **EFIOSLoaderFilePath**フィールド。

Nvrboot パーティション GUID ブート ローダーのファイルへのパスを続けて、ファイルの場所を表示します。

```
1. Load identifier = Windows Server 2003, Enterprise
2. OsLoadOptions = /debug /debugport=COM1 /baudrate=115209
3. EFIOSLoaderFilePath = 006F0073-0066-0074-5C00-570049004E00  ::  \EFI\Microsoft\WINNT50\ia64ldr.efi
4. OSLoaderFilePath = 04000004-5D18-3F27-0000-0000205C273F  :: \Windows
```

どちらの場合も、ブート ローダーのファイル (および、ブート*xxxx*ブート エントリのバックアップ ファイル)、オペレーティング システムが、EFI システム パーティションのディレクトリに WINNT50 (EFI\\Microsoft\\WINNT50)。
