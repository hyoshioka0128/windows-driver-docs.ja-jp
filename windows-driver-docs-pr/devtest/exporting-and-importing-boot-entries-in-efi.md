---
title: EFI でのブート エントリのエクスポートとインポート
description: EFI でのブート エントリのエクスポートとインポート
ms.assetid: bd019064-cb8c-434c-b471-192168564540
keywords:
- NVRAM ブート オプション、WDK をエクスポートします。
- EFI NVRAM ブート オプション、WDK をエクスポートします。
- NVRAM ブート オプション、WDK をインポートします。
- EFI NVRAM ブート オプション、WDK をインポートします。
- WDK のブート エントリのエクスポート
- ブート エントリのインポート
- ブート エントリ Id WDK
- EFI ブート エントリ Id WDK
- WDK のブート オプションの識別子
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: d0f19d6219aa1c1fdf057ad2884b71f75ef3f508
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378812"
---
# <a name="exporting-and-importing-boot-entries-in-efi"></a>EFI でのブート エントリのエクスポートとインポート

使用して、 **nvrboot x**ブート エントリのバックアップ コピーを作成する (エクスポート) コマンド。 簡単に必要なときに、バックアップ コピーのファイルを検索する規則に名前付けとストレージを設計します。

使用して、 **nvrboot は**(インポート) コマンドをエクスポートしたバックアップ コピーから、または起動時のブート エントリをインポートする*xxxx*セットアップが作成されたエントリのバックアップ ファイルを起動します。

インポートされたブート エントリには、常に新しい EFI ブート エントリ Id が表示されます。 たとえば、Boot0003 のコピーをエクスポートし、NVRAM にコピーをインポートする場合、インポートされたブート エントリは Boot000A などの新しいブート エントリ ID を受け取ります。
