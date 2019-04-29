---
title: 使用できないブート エントリ バックアップ ファイルの認識
description: 使用できないブート エントリ バックアップ ファイルの認識
ms.assetid: ff61c8e9-ad6b-4f3f-9c4b-72c24c27eda6
keywords:
- NVRAM ブート オプション WDK、
- EFI NVRAM ブート オプション WDK、
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: e84f7deda6ff41901cbae59ef00ec3872886f77c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339748"
---
# <a name="recognizing-unusable-boot-entry-backup-files"></a>使用できないブート エントリ バックアップ ファイルの認識

残念ながら、ブート エントリのバックアップ コピーは常に使用できません。

EFI 環境では、アプリケーションとドライバーは、パーティション GUID によってディスク パーティションを識別します。 何らかの理由で、ディスク パーティションの GUID が変更された場合は、ブート エントリのバックアップ コピーでは、パーティション GUID は無効になりましたし、EFI ブート ローダーは、バックアップのコピーを使用して、システムを起動することはできません。

次の Bootcfg は、無効なパーティションの Guid を持つインポートされたブート エントリを示しています。

```
Boot entry ID:    4
OS Friendly Name: Windows Server 2003 - mydebug
OsLoadOptions:    /debug /debugport=com1 /baudrate=115200
BootFilePath:     (null)
OsFilePath:       (null)
```

ここでは、オペレーティング システムのインストールから別のブート エントリをコピーして、パラメーターを変更するブート エントリを再作成する必要があります。
