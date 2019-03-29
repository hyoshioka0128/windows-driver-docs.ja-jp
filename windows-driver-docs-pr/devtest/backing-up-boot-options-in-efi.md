---
title: EFI でのブート オプションのバックアップ
description: EFI でのブート オプションのバックアップ
ms.assetid: a9c7052c-c554-460c-a8ba-12b79126e67f
keywords:
- 戻る ups の EFI、WDK のブート オプション
- NVRAM ブート オプション WDK、バックアップします。
- EFI NVRAM ブート オプション WDK、バックアップします。
- コピーのブート オプション
- ブート オプションを保存しています
- ブート オプション WDK、バックアップします。
- Nvrboot ツール
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: a72f7b449c7bc42ec938077c76467070d90737ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581106"
---
# <a name="backing-up-boot-options-in-efi"></a>EFI でのブート オプションのバックアップ


セットアップが自動的にインストールのブート エントリを作成し、Boot という名前のバイナリ ファイルへのブート エントリのバックアップ コピーを保存します Windows の 64 ビット バージョンをインストールするときに*xxxx*、起動、*xxxx*が、。ブート エントリの NVRAM ID。 セットアップでは、新規インストール用の EFI ブート ローダーと共に、EFI パーティション上の新しいディレクトリでブート エントリのバックアップ コピーを格納します。既定では、インストール ディレクトリはでは、 \\EFI\\Microsoft\\サブディレクトリ。

ただし、システムが作成したブート エントリのバックアップ コピーを保存できませんし、それらを編集した後、ブート エントリのバックアップ コピーは更新しません。

作成および編集するには、ブート エントリのバックアップ コピーを保存し、セットアップによって作成されるエントリの追加のバックアップ コピーを保存するには、Nvrboot (nvrboot.efi) を使用します。 Nvrboot では、セットアップと EFI コンポーネントを使用するバイナリ形式でエントリを保存します。 次に、インストール用のブート エントリが紛失または破損している場合は、import コマンドを使用できます (**nvrboot は**) で Nvrboot NVRAM にブート エントリのバックアップ コピーをインポートします。

このセクションの内容:

- [エクスポートとインポートの efi ブート エントリ](exporting-and-importing-boot-entries-in-efi.md)
- [既存のブート エントリのバックアップ ファイルを識別します。](identifying-backup-files-for-existing-boot-entries.md)
- [削除されたブート エントリのバックアップ ファイルを識別します。](identifying-backup-files-for-deleted-boot-entries.md)
- [使用不可のブート エントリのバックアップ ファイルを認識します。](recognizing-unusable-boot-entry-backup-files.md)
 





